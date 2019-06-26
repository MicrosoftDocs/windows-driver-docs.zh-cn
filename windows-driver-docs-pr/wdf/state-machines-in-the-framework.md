---
title: 框架中的状态计算机
description: 框架中的状态计算机
ms.assetid: 5ef307c6-0310-4a83-a63f-3a6d96782013
keywords:
- 即插即用 WDK KMDF，状态机
- 插 WDK KMDF，状态机
- 电源管理 WDK KMDF，状态机
- 状态机 WDK KMDF
- 指出 WDK KMDF
- 即插即用的状态机 WDK KMDF
- 电源状态 WDK KMDF
- 当前状态计算机状态 WDK KMDF
- WDK KMDF，状态机的状态信息
- 电源策略 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce09ece00bf70351ab95a528bb236209cc96849d
ms.sourcegitcommit: 39c0b7e84e5087447493507a478b870c7a834446
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/03/2019
ms.locfileid: "66458843"
---
# <a name="state-machines-in-the-framework"></a>框架中的状态计算机


若要跟踪的每个设备的状态，框架将使用即插即用的状态机、 电源状态机和电源策略状态机。 框架将创建每个设备都插入到系统每个状态机的实例。

>[!NOTE]
>此功能是仅供 Microsoft 内部使用。

对于确实需要了解此信息的驱动程序，framework 提供了两个集的接口：

-   一组驱动程序所提供事件回调函数。

    该驱动程序可以请求 framework 调用一个以下回调的函数的一个状态机将进入或退出某一特定状态时：

    -   [*EvtDevicePnpStateChange*](https://msdn.microsoft.com/library/windows/hardware/ff540874)，该驱动程序将通过调用其注册[ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546057)。
    -   [*EvtDevicePowerStateChange*](https://msdn.microsoft.com/library/windows/hardware/ff540878)，该驱动程序将通过调用其注册[ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546071)。
    -   [*EvtDevicePowerPolicyStateChange*](https://msdn.microsoft.com/library/windows/hardware/ff540876)，该驱动程序将通过调用其注册[ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)。
-   一组返回的状态机的当前状态的方法。

    该驱动程序可以调用以下方法之一来确定某个特定设备的状态机的当前状态：

    -   [**WdfDeviceGetDevicePnpState**](https://msdn.microsoft.com/library/windows/hardware/ff545969)
    -   [**WdfDeviceGetDevicePowerState**](https://msdn.microsoft.com/library/windows/hardware/ff545985)
    -   [**WdfDeviceGetDevicePowerPolicyState**](https://msdn.microsoft.com/library/windows/hardware/ff545974)

 

 




