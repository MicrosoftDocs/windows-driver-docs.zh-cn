---
title: WDI_TLV_CIPHER_KEY_TKIP_MIC
description: WDI_TLV_CIPHER_KEY_TKIP_MIC 是包含 TKIP MIC 材料 TLV。
ms.assetid: 5F1AE81C-6AB4-468C-9DEE-D1BB16A2EC4D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TKIP_MIC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cace5ddd168aa7799677bfe59e3a474e8ebe382d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568242"
---
# <a name="wditlvcipherkeytkipmic"></a>WDI\_TLV\_CIPHER\_KEY\_TKIP\_MIC


WDI\_TLV\_密码\_密钥\_TKIP\_MIC 是包含 TKIP MIC 材料 TLV。

## <a name="tlv-type"></a>TLV 类型


0x4A

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                      |
|-----------|------------------------------------------------------------------|
| UINT8\[\] | 指定 TKIP MIC 材料 UINT8 元素的数组。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 



