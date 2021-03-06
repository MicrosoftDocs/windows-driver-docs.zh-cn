---
title: OID_RECEIVE_FILTER_MOVE_FILTER
description: 过量驱动程序会 (OID 发出对象标识符) 设置 OID_RECEIVE_FILTER_MOVE_FILTER 移动先前配置的接收筛选器。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_MOVE_FILTER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7aaa91949f217e69eeef7498090688853cf48181
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248839"
---
# <a name="oid_receive_filter_move_filter"></a>OID \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器


过量驱动程序发出对象标识符 (OID) 设置 OID \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器，以移动以前配置的接收筛选器。 接收筛选器将从一个虚拟端口 (VPort) 移动到不同的 VPort。

过量驱动程序将此 OID 集请求颁发给网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 集请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)结构的指针。

<a name="remarks"></a>备注
-------

在将 OID 集请求转发到 PF 微型端口驱动程序之前，NDIS 验证 [**ndis \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters) 结构的成员。

PF 微型端口驱动程序必须以原子方式处理此 OID 集请求。 驱动程序必须能够将网络适配器配置为同时从接收队列和 VPort 中删除筛选器，并将其设置在不同的接收队列和 VPort 中。

有关详细信息，请参阅将 [接收筛选器移动到虚拟端口](./moving-a-receive-filter-to-a-virtual-port.md)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器，PF 小型端口驱动程序返回以下状态代码之一。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF 微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)"><strong>NDIS_RECEIVE_FILTER_MOVE_FILTER_PARAMETERS</strong></a>) 。 PF 微型端口驱动程序必须设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

[**NDIS \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)

