---
title: 用户拔出设备
description: 用户拔出设备
ms.assetid: 85e69401-0128-4641-aa0f-fd7c4f22f395
keywords:
- PnP WDK KMDF，拔出设备
- 插 WDK KMDF，拔出设备
- 有序设备删除 WDK KMDF
- 拔出设备 WDK KMDF
- 感到惊讶设备删除 WDK KMDF
- 意外的设备删除 WDK KMDF
- 删除设备 WDK KMDF
- 弹出设备 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98662294894f1bf190168b03715465a4561f2af1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342213"
---
# <a name="a-user-unplugs-a-device"></a>用户拔出设备


在运行时系统，用户可以通过两种方式之一删除设备： 通过*有序地删除*，这意味着用户通知系统设备是将要移除 （例如，通过使用拔出或弹出硬件程序）; 或通过*感到惊讶删除*，这意味着用户而不通知系统断开设备。 如果在总线支持在意外删除 (例如，USB)，设备的驱动程序必须能够处理设备的突然消失。

### <a href="" id="orderly-removal"></a> 有序地删除

用户请求删除通过使用系统的拔出或弹出硬件程序，通过禁用设备使用设备管理器，或通过将推送[无可退出](supporting-ejectable-devices.md)设备的弹出按钮。 该框架允许设备以删除或禁用，除非该驱动程序有：

-   名为[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)和特殊文件是在设备上打开。

-   名为[ **WdfDeviceSetStaticStopRemove**](https://msdn.microsoft.com/library/windows/hardware/ff546915)。

-   提供[ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)回调函数和回调函数已禁止删除。

对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，一个驱动程序时，开始驱动程序堆栈中最高的驱动程序：

1.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)回调函数。

2.  该框架将停止的所有驱动程序的电源管理的 I/O 队列。

3.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)， [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)，并[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)回调函数 （如果存在） 用于创建每个 DMA 通道。

4.  框架将调用的驱动程序[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)回调函数 （如果存在），然后调用的驱动程序[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)回调函数 （如果存在） 为每个中断，以便该驱动程序可以禁用设备中断。

5.  框架将调用的驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数 （如果存在）。

6.  框架将调用的驱动程序[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数 （如果存在），并向其传递的即插即用的管理员分配给设备的硬件资源的列表。

7.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff540901)回调函数。

8.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)回调函数。

总线驱动程序是最后调用堆栈中的驱动程序。 当框架将调用总线驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数，则回调函数会将设备 （在总线的子设备） 的电源状态设置为 D3。 总线驱动程序可以控制当框架将调用其[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)通过调用回调函数[ **WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)。

### <a href="" id="surprise-removal"></a> 意外删除

用户意外断开设备。 设备的总线的总线驱动程序发现设备缺少并调用[ **WdfChildListUpdateChildDescriptionAsMissing**](https://msdn.microsoft.com/library/windows/hardware/ff545674)。

对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，一个驱动程序时，开始驱动程序堆栈中最高的驱动程序：

1.  框架将调用的驱动程序[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)回调函数 （如果存在）。

2.  如果设备处于其工作 (D0) 状态时被拔出，框架将停止的所有驱动程序的电源管理的 I/O 队列。

3.  如果设备已在其工作 (D0) 状态时被拔出，并且如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)回调函数。

4.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)， [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)，并[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)回调函数 （如果存在） 用于创建每个 DMA 通道。

5.  框架将调用的驱动程序[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)并[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)回调函数 （如果存在），以便该驱动程序可以禁用设备中断。

6.  框架将调用的驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数 （如果存在）。

7.  框架将调用的驱动程序[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数 （如果存在），同时传入的即插即用的管理员分配给设备的硬件资源的列表。

8.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff540901)回调函数。

9.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)回调函数。

请注意，可以在任何时候意外删除设备。 因此，该框架可能调用的驱动程序[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)以外的上一步骤中所示的一次回调函数。 例如，如果用户意外断开时设备很[进入低功耗状态](a-device-enters-a-low-power-state.md)，可能会调用框架[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)回调函数后它会调用[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)回调函数。 您必须编写代码[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)假定按特定顺序调用它和其他回调函数的方式的回调函数。

此外，该框架不会同步的设备[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)该设备的上一步骤中列出的任何回调函数的回调函数。 因此， [ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)回调函数可能会运行前面列出的回调函数的另一个正在运行时。

 

 




