---
title: pcm
description: Pcm 扩展显示指定的专用缓存映射。 此扩展仅在 Windows 2000 中提供。
keywords:
- 专用缓存映射
- 缓存管理器
- pcm Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9bc958b2ee28d81535f1fa92bf90257db3f8c0b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792011"
---
# <a name="pcm"></a>!pcm


**！ Pcm** 扩展显示指定的专用缓存映射。 此扩展仅在 Windows 2000 中提供。

```dbgcmd
!pcm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定专用缓存映射的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p> (，请参阅 "备注" 部分) </p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关缓存管理的信息，Microsoft Windows SDK 请参阅 Russinovich 文档和 *Microsoft Windows 内部机制* ，并标记和 David 所罗门群岛。

有关其他缓存管理扩展的信息，请参阅 [**！ cchelp**](-cchelp.md) extension reference。

<a name="remarks"></a>备注
-------

只有 Windows 2000 支持此扩展。 在 Windows XP 和更高版本的 Windows 中，使用 [**dt nt！ \_专用 \_ 缓存 \_ 映射地址**](dt--display-type-.md) 命令。

 

 





