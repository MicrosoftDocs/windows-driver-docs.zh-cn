---
title: WDI_TLV_ASSOCIATION_RESPONSE_FRAME
description: WDI_TLV_ASSOCIATION_RESPONSE_FRAME 是包含收到的关联响应的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESPONSE_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 874405ce69ac79d7fb92b3ad2028cea05fa9ea07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789611"
---
# <a name="wdi_tlv_association_response_frame"></a>WDI \_ TLV \_ 关联 \_ 响应 \_ 帧


WDI \_ tlv \_ 关联 \_ 响应 \_ 帧是包含收到的关联响应的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x2F

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                              |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 一个 UINT8 元素数组，其中包含收到的关联响应。 这不包括 802.11 MAC 标头。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




