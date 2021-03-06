---
title: OID_SWITCH_PORT_PROPERTY_ADD
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PORT_PROPERTY_ADD 请求，通知有关为可扩展交换机端口添加策略属性的可扩展交换机扩展。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_ADD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 91286ac58e6cfdf117ddf689eb13b0805acdd394
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248985"
---
# <a name="oid_switch_port_property_add"></a>OID \_ 交换机 \_ 端口 \_ 属性 \_ 添加


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ 端口 \_ 属性 " \_ 添加"，以通知可扩展交换机扩展有关为可扩展交换机端口添加策略属性的信息。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)结构，指定端口策略的参数的标识和类型。

-   包含端口策略参数的属性缓冲区。 属性缓冲区包含一个结构，该结构基于 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)结构的 **PropertyType** 成员。 例如，如果 **PropertyType** 成员设置为 **NdisSwitchPortPropertyTypeVlan**，则属性缓冲区包含 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ VLAN**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan) 结构。

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID \_ 交换机 \_ 端口 \_ 属性添加的 oid 设置请求 \_ 。 所有其他类型的扩展都必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，将 OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

此扩展可以通过返回 \_ \_ \_ OID 请求未接受的 NDIS 状态数据来否决添加端口属性 \_ 。 例如，如果扩展无法分配资源来强制在端口上配置策略，则它应否决添加请求。

**注意** 如果扩展返回其他 NDIS \_ 状态 \_ *Xxx* 错误状态代码，则创建通知也被否决。 然而，为暂时性方案返回状态代码（例如返回 NDIS \_ 状态 \_ 资源）可能会导致创建通知重试。

 

如果扩展不否决 OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

有关如何处理 OID 交换机端口属性添加的 OID 集请求的指南 \_ \_ \_ \_ ，请参阅 [管理端口策略](./managing-port-policies.md)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展插件完成 oid \_ 交换机端口属性添加的 oid 设置请求 \_ \_ \_ ，它将返回以下状态代码之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法处理 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PROPERTY_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)"><strong>NDIS_SWITCH_PORT_PROPERTY_PARAMETERS</strong></a> 结构和结构的属性缓冲区中的数据。 扩展将设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>转发扩展已拒绝端口策略添加通知。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>转发扩展不支持端口策略。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，OID 请求失败。</p></td>
</tr>
</tbody>
</table>

 

如果扩展未完成 oid \_ 交换机端口属性添加的 oid 集请求 \_ \_ \_ ，则该请求将由可扩展交换机的基础微型端口边缘完成。 微型端口边缘返回以下状态代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_custom)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ VLAN**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

