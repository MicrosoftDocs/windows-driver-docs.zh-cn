---
title: OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: 为查询，基础驱动程序使用 OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES OID 获取 PCI 设备的自定义属性。
ms.assetid: fe94884b-f5e3-4c60-8f52-e61d0df81a2a
ms.date: 08/08/2017
keywords: -OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 792e7ea9d146f741762dc4fc025644af5c470146
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544767"
---
# <a name="oidgenpcidevicecustomproperties"></a>OID\_GEN\_PCI\_设备\_自定义\_属性


为查询，基础驱动程序使用 OID\_GEN\_PCI\_设备\_自定义\_属性 OID，若要获取设备的 PCI 自定义属性。

<a name="remarks"></a>备注
-------

NDIS 处理 OID\_GEN\_PCI\_设备\_自定义\_属性和微型端口驱动程序不会收到一个 OID 查询。

此查询是可选的其他 NDIS 驱动程序。

返回 NDIS [ **NDIS\_PCI\_设备\_自定义\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff566745)结构，其中包含 PCI 的自定义属性。

对于非 PCI 微型端口适配器，NDIS 失败 OID\_GEN\_PCI\_设备\_自定义\_属性与的 NDIS\_状态\_无效\_设备\_请求状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PCI\_设备\_自定义\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff566745)

 

 



