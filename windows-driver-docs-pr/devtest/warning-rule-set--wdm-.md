---
title: 警告规则集 (WDM)
description: 使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。
ms.assetid: 29374BBE-D1DF-48C0-80A9-96CBAC6D8A22
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: cafc618b0bc94497f96267a22e46636b088ae932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380467"
---
# <a name="warning-rule-set-wdm"></a>警告规则集 (WDM)


使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-checkdeviceobjectflags.md" data-raw-source="[&lt;strong&gt;CheckDeviceObjectFlags&lt;/strong&gt;](wdm-checkdeviceobjectflags.md)"><strong>CheckDeviceObjectFlags</strong></a></p></td>
<td align="left"><p><a href="wdm-checkdeviceobjectflags.md" data-raw-source="[&lt;strong&gt;CheckDeviceObjectFlags&lt;/strong&gt;](wdm-checkdeviceobjectflags.md)"> <strong>CheckDeviceObjectFlags</strong> </a>规则指定总线驱动程序必须检查设备对象标志 DO_POWER_PAGABLE 和 DO_POWER_INRUSH 设置保持一致 FDO 和子 PDOs。 此规则仅适用于总线驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completioneventchecking.md" data-raw-source="[&lt;strong&gt;CompletionEventChecking&lt;/strong&gt;](wdm-completioneventchecking.md)"><strong>CompletionEventChecking</strong></a></p></td>
<td align="left"><p><a href="wdm-completioneventchecking.md" data-raw-source="[&lt;strong&gt;CompletionEventChecking&lt;/strong&gt;](wdm-completioneventchecking.md)"> <strong>CompletionEventChecking</strong> </a>规则指定一个驱动程序不会调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549422" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549422)"> <strong>IoMarkIrpPending</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>中相同的 IRP 完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-deletedevice.md" data-raw-source="[&lt;strong&gt;DeleteDevice&lt;/strong&gt;](wdm-deletedevice.md)"><strong>DeleteDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-deletedevice.md" data-raw-source="[&lt;strong&gt;DeleteDevice&lt;/strong&gt;](wdm-deletedevice.md)"> <strong>DeleteDevice</strong> </a>规则指定驱动程序不应依赖于 I/O 管理器或 PnP 管理器是在调用后保留 DeviceObject 保持活动状态<a href="https://msdn.microsoft.com/library/windows/hardware/ff549083" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549083)"> <strong>IoDeleteDevice</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-multremovelock.md" data-raw-source="[&lt;strong&gt;MultRemoveLock&lt;/strong&gt;](wdm-multremovelock.md)"><strong>MultRemoveLock</strong></a></p></td>
<td align="left"><p><a href="wdm-multremovelock.md" data-raw-source="[&lt;strong&gt;MultRemoveLock&lt;/strong&gt;](wdm-multremovelock.md)"> <strong>MultRemoveLock</strong> </a>规则验证<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong> </a>调用使用只有一个唯一的删除锁定。 这是警告规则。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](wdm-pagedcode.md)"><strong>PagedCode</strong></a></p></td>
<td align="left"><p><a href="wdm-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](wdm-pagedcode.md)"> <strong>PagedCode</strong> </a>规则指定驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff558773" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558773)"> <strong>PAGED_CODE</strong> </a>宏仅当它在执行时<strong>IRQL &lt;= APC_LEVEL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pagedcodeatpowertrans.md" data-raw-source="[&lt;strong&gt;PagedCodeAtPowerTrans&lt;/strong&gt;](wdm-pagedcodeatpowertrans.md)"><strong>PagedCodeAtPowerTrans</strong></a></p></td>
<td align="left"><p><a href="wdm-pagedcodeatpowertrans.md" data-raw-source="[&lt;strong&gt;PagedCodeAtPowerTrans&lt;/strong&gt;](wdm-pagedcodeatpowertrans.md)"> <strong>PagedCodeAtPowerTrans</strong> </a>规则指定一个驱动程序不应调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff558773" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558773)"> <strong>PAGED_CODE</strong> </a>时响应系统 IRP_MJ_POWER Irp (IRP_MN_SET_POWER) 到设备 IRP_MJ_POWER Irp (IRP_MN_SET_POWER)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-reservedddis.md" data-raw-source="[&lt;strong&gt;ReservedDDIs&lt;/strong&gt;](wdm-reservedddis.md)"><strong>ReservedDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-reservedddis.md" data-raw-source="[&lt;strong&gt;ReservedDDIs&lt;/strong&gt;](wdm-reservedddis.md)"> <strong>ReservedDDIs</strong> </a>规则验证驱动程序不会调用任何保留的函数。</p></td>
</tr>
</tbody>
</table>

 

**若要选择警告规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**警告**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Warning.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 




