---
title: 'NdisAllocateMdl 规则 (ndis) '
description: NdisAllocateMdl 规则指定按替代顺序调用 NdisAllocateMdl 和 NdisFreeMdl。 最终目标是确保在 MiniportHaltEx 结束时释放所有 MDLs。
ms.date: 05/21/2018
keywords:
- 'NdisAllocateMdl 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisAllocateMdl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 933bffa4a3896c142f292a024cdf678eef84d69e
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248534"
---
# <a name="ndisallocatemdl-rule-ndis"></a>NdisAllocateMdl 规则 (ndis) 


**NdisAllocateMdl** 规则指定按替代顺序调用 [**NdisAllocateMdl**](/windows-hardware/drivers/ddi/mdlapi/nf-mdlapi-ndisallocatemdl)和 [**NdisFreeMdl**](/windows-hardware/drivers/ddi/mdlapi/nf-mdlapi-ndisfreemdl) 。 最终目标是确保在 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 结束时释放所有 MDLs。

此规则使用三种不同的状态。 分配或释放 MDL 后，状态会更改。 如果在 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 退出时仍分配 MDL，规则将报告缺陷。

**驱动程序模型： NDIS**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>NdisAllocateMdl</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisAllocateMdl**](/windows-hardware/drivers/ddi/mdlapi/nf-mdlapi-ndisallocatemdl) 
[ **NdisFreeMdl**](/windows-hardware/drivers/ddi/mdlapi/nf-mdlapi-ndisfreemdl)
