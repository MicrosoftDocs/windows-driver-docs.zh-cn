---
title: OID_PNP_WAKE_UP_PATTERN_LIST
description: OID_PNP_WAKE_UP_PATTERN_LIST
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_PATTERN_LIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1c77859f530e3ee03555544a9f017c2e602ab419
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247941"
---
# <a name="oid_pnp_wake_up_pattern_list"></a>OID \_ PNP \_ 唤醒 \_ \_ 模式 \_ 列表





\_ \_ 协议使用 oid PNP \_ 唤醒 \_ 模式 \_ 列表 oid 来查询当前为微型端口驱动程序网络适配器设置的唤醒模式的列表。 协议指定具有 [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](oid-pnp-add-wake-up-pattern.md)的唤醒模式。

OID \_ PNP \_ 唤醒 \_ \_ 模式 \_ 列表由 NDIS 而不是微型端口驱动程序处理。

NDIS 返回到协议，其中包含微型端口驱动程序中每个唤醒模式集的说明。 每个唤醒模式连同其掩码，都由 [**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern) 结构描述。

对于每个唤醒模式， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含以下内容：

-   提供有关模式及其掩码的信息的 [**NDIS \_ PM \_ 包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern) 结构。

-   一个掩码，用于指示应将传入数据包的哪些字节与模式中的相应字节进行比较。 掩码以数据包的第一个字节开始。 掩码紧跟 **InformationBuffer** 中的 [**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构。

-   唤醒模式，从 **InformationBuffer** 的开头开始 **PatternOffset** 字节。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用 Ndis (Co) 请求将请求传播到基础微型端口驱动程序。

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
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用 <a href="oid-pm-wol-pattern-list.md" data-raw-source="[OID_PM_WOL_PATTERN_LIST](oid-pm-wol-pattern-list.md)">OID_PM_WOL_PATTERN_LIST</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[OID \_ PM \_ WOL \_ 模式 \_ 列表](oid-pm-wol-pattern-list.md)

[OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](oid-pnp-add-wake-up-pattern.md)

[OID \_ PNP \_ 删除 \_ 唤醒 \_ \_ 模式](oid-pnp-remove-wake-up-pattern.md)

 

