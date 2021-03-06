---
title: OID_SWITCH_PROPERTY_ENUM
description: Hyper-v 可扩展交换机扩展发出对象标识符 (OID) 方法请求 OID_SWITCH_PROPERTY_ENUM 获取数组。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_ENUM 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 336f1e22082c62cebc14db6e527b2b138dcfc062
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248148"
---
# <a name="oid_switch_property_enum"></a>OID \_ 开关 \_ 属性 \_ 枚举


Hyper-v 可扩展交换机扩展会发出对象标识符 (OID) 方法请求， \_ \_ \_ 以获取数组。 此数组包含与指定条件匹配的预配交换机策略。 数组中的每个元素指定可扩展交换机策略的属性。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   用于指定可扩展交换机策略枚举参数的 [**NDIS \_ 交换机 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters) 结构。

-   [**NDIS \_ 开关 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构的数组。 其中每个结构都包含有关可扩展交换机策略的信息。

    **注意** 如果尚未为扩展预配指定的可扩展交换机策略的实例，扩展会将 [**ndis \_ 交换机 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构的 **NumProperties** 成员设置为零，且不会返回 [**ndis \_ 交换机 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。

     

<a name="remarks"></a>备注
-------

\_ \_ \_ 仅当 hyper-v 可扩展交换机完成激活时才必须发出 oid 开关属性 ENUM。 有关更多详细信息，请参阅 [查询 Hyper-v 可扩展交换机配置](./querying-the-hyper-v-extensible-switch-configuration.md) 。

与 oid [ \_ 交换机 \_ 端口 \_ 属性 \_ 枚举](oid-switch-port-property-enum.md)的 oid 查询请求不同，扩展在向下发出 oid 开关  \_ \_ 属性枚举请求时，无需调用任何 ReferenceSwitchXxx 或 DereferenceSwitchXxx 函数 \_ 。

**注意**  如果扩展插件收到 oid \_ 开关属性枚举的 oid 方法 \_ 请求 \_ ，则它不能完成 oid 请求。 相反，它必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将 OID 请求向下转发到可扩展交换机驱动程序堆栈。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID switch 属性枚举的 OID 查询 \_ 请求 \_ \_ ，并返回以下状态代码之一。

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
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法返回 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)"><strong>NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS</strong></a> 结构及其 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)"><strong>NDIS_SWITCH_PROPERTY_ENUM_INFO</strong></a> 元素数组。 可扩展交换机的基础微型端口边缘设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>由于其他原因，请求失败。</p></td>
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

[**NDIS \_ 交换机 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)

[**NDIS \_ 交换机 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)

[查询 Hyper-V 可扩展交换机配置](./querying-the-hyper-v-extensible-switch-configuration.md)

