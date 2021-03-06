---
title: OID_WWAN_DRIVER_CAPS
description: OID_WWAN_DRIVER_CAPS 返回微型端口驱动程序支持的 MB 驱动程序型号版本。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DRIVER_CAPS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb556aa1284cfdc645d7d4a440232dbff8c0cb82
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248305"
---
# <a name="oid_wwan_driver_caps"></a>OID \_ WWAN \_ 驱动程序 \_ CAP


OID \_ WWAN \_ 驱动程序 \_ cap 返回微型端口驱动程序支持的 MB 驱动程序型号版本。

不支持设置请求。

微型端口驱动程序 \_ \_ 以同步方式处理 OID WWAN 驱动程序 \_ cap，并应立即返回包含 [**NDIS \_ wwan \_ 驱动程序 \_ cap**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps) 结构的响应缓冲区，该结构描述了在完成查询请求时由微型端口驱动程序实现的 MB 驱动程序的版本。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [MB 微型端口驱动程序初始化](mb-device-readiness.md#mb-miniport-driver-initialization)。

处理查询操作时，微型端口驱动程序不应访问提供程序网络或订阅服务器标识模块 (SIM 卡) 。

MB 驱动程序型号版本的当前版本由 WWAN \_ 主要 \_ 版本和 wwan \_ 次要版本定义标记定义 \_ \# 。 如果微型端口驱动程序返回 MB 服务不支持的 MB 驱动程序型号版本，MB 服务将忽略此设备。

如果初始化或重新启动了 MB 服务，则可能已加载微型端口驱动程序。 在这种情况下，MB 服务会查询通过微型端口驱动程序实现的 MB 驱动程序模型的版本，然后再继续发出其他任何 Oid。 此操作发生在任何会话的开头。

\_ \_ \_ 如果出现任何初始化错误，微型端口驱动程序应返回 NDIS 状态。 如果微型端口驱动程序返回 \_ \_ 不受支持的 NDIS 状态 \_ ，MB 服务将忽略该设备，并且不会继续进行其他任何 oid。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[MB 微型端口驱动程序初始化](mb-device-readiness.md#mb-miniport-driver-initialization)

[**NDIS \_ WWAN \_ 驱动程序 \_ CAP**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_driver_caps)

 

