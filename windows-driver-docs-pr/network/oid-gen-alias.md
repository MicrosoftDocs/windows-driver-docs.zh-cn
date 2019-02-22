---
title: OID_GEN_ALIAS
description: 为查询，使用 OID_GEN_ALIAS OID 获取的接口 (RFC 2863 从 ifAlias) 的别名字符串。 版本信息 Windows Vista 和 laterSupported。 NDIS 6.0 和更高版本的微型端口 driversNot 请求。 NDIS 接口提供程序仅。
ms.assetid: ff5e6494-aa4e-4a0a-b773-64b612236c8c
ms.date: 08/08/2017
keywords: -OID_GEN_ALIAS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 19c096ca75c596f7066f090bcb9f42ac177313d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542915"
---
# <a name="oidgenalias"></a>OID\_常规\_别名


为查询，使用 OID\_GEN\_别名 OID 获取接口的别名字符串 (*ifAlias*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054))。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序可以将分配为它的接口的唯一别名字符串。 如果名称应保持相同的接口与相关联，该提供程序可以使计算机重新启动后持久的字符串和需重新初始化。

仅 NDIS 网络接口提供程序，并因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果接口提供程序返回 NDIS\_状态\_成功后，查询的结果是在 NDIS 中返回的别名字符串\_IF\_盘点\_字符串结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 



