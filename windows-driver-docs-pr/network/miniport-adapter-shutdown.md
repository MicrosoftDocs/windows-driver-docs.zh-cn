---
title: 微型端口适配器关闭
description: 微型端口适配器关闭
ms.assetid: 57d964f1-03c7-4b54-9d04-1d187c96e052
keywords:
- 微型端口适配器 WDK 网络、 关闭
- 适配器 WDK 网络、 关闭
- MiniportShutdownEx
- 微型端口驱动程序 WDK 网络，系统关闭
- NDIS 微型端口驱动程序 WDK，系统关闭
- 关闭 WDK 网络
- 系统关闭 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aefc5819670a99448f6eb1d5e125dad6b6b3492a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378375"
---
# <a name="miniport-adapter-shutdown"></a>微型端口适配器关闭





NDIS 微型端口驱动程序必须注册[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)微型端口驱动程序初始化期间的函数。

NDIS 调用 NDIS 微型端口驱动程序的[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)系统关闭时的功能。 *MiniportShutdownEx*将硬件恢复到已知状态。

*ShutdownAction* NDIS 传递给参数[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)通知关机的原因的微型端口驱动程序。

可以调用关闭处理程序由于用户操作，而在此情况下它运行在 IRQL = 被动\_级别。 它也可以调用作为不可恢复的系统错误结果，这种情况下它可以运行的任何 irql。

[*MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)应调用无**Ndis * Xxx*** 函数。 微型端口驱动程序可以读取和写入 I/O 端口或禁用要返回到已知状态的硬件的 DMA 引擎调用函数。

与不同[ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)， [ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)应释放任何已分配的资源。 *MiniportShutdownEx*应只是停止 nic。

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[正在停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)

 

 





