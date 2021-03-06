---
title: str
description: Str 扩展显示 ANSI_STRING 或 OEM_STRING 结构。
keywords:
- 字符串
- ANSI_STRING 结构
- str Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- str
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6824426988f54467e060751143f93414589b1783
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817003"
---
# <a name="str"></a>!str


**！ Str** 扩展显示 ANSI \_ 字符串或 OEM \_ 字符串结构。

```dbgcmd
!str Address
```

## <a name="span-idddk__str_dbgspanspan-idddk__str_dbgspanparameters"></a><span id="ddk__str_dbg"></span><span id="DDK__STR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 ANSI \_ 字符串或 OEM 字符串结构的十六进制地址 \_ 。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 ANSI 字符串结构的详细信息 \_ ，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

ANSI 字符串按以下结构中的定义，按8位字符字符串计数：

```cpp
typedef struct _STRING {
    USHORT Length;
    USHORT MaximumLength;
    PCHAR Buffer;
} STRING;
typedef STRING ANSI_STRING;
typedef STRING OEM_STRING;
```

如果字符串以 null 结尾，则 **长度** 不包含尾随 null。

 

 





