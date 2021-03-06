---
title: 点击和执行方案
description: 点击和执行方案
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: a8510f7e12d45743a690e6195fadc96bcd1c3974
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090948"
---
# <a name="tap-and-do-scenarios"></a>点击和执行方案

*点击和 Do* 是在靠近的人员之间进行自然交互的笔势，用于触发在其所持有的设备之间进行操作。

从 Windows 8 开始，为现实世界交互引入了一个新的手势，称为 *点击和操作*。 在窄的物理卷中 *点击并执行操作* (按厘米) ，因此它非常故意。 编程模型将此 intentionality 映射到物理环境内的设备之间的操作触发。 近处 (NFP) 的基础系统主要是在使用电磁辐射的技术（如 NFC）上建模，但平台很灵活，并且支持其他满足 NFP 要求的创新系统。 Windows 提供了基于 NFP 的用户模型，该模型易于理解、轻型和直观。 Windows 附带了许多利用 NFP 的内置体验。 该 API 可用于第三方开发。

在 Windows 中 *，点击和操作* 都支持两个用户方案区。

## <a name="peripheral-wireless-device-setup"></a>外设无线设备设置

在用户可以将外围设备用于 Windows 之前，必须在计算机上以逻辑方式连接、配对和设置设备。 它们可以通过电缆或无线网络来实现此目的。

虽然使用电缆是直观而有效的，但这通常会导致用户体验不佳，因为用户通常不会使用电缆来保持连接。 同时，将外设无线设备与 Windows 配对可能需要执行设备发现和身份验证。

通过点击，用户只需将外围无线设备点击到计算机即可。 此单一操作可用于触发设备的自动无线设置，而无需执行任何其他步骤。 此体验的简单性消除了与设备设置相关的常见用户困难。

## <a name="ad-hoc-interaction-in-the-real-world"></a>现实世界中的即席交互

Windows 不能为用户提供通过其设备与其他用户或物理环境交互的常用方法。 若要让一个用户直接发现附近的其他用户，并与他们进行的操作进行交互，这两个用户通常都必须通过 Internet 通过具有专有汇集机制的应用进行连接。 这种方法通常需要与应用或服务相关的每个用户都具有预先存在的关系，并且通常还要求用户彼此交换某些标识符，以便支持集合。

通过 *点击和执行* 操作，用户只需将计算机组合在一起即可创建关系，并触发与用户正在执行的操作上下文相对应的其他操作。 这一简单的操作可以启动计算机之间的复杂交互。 它可用于交换简单信息，如 URL。 它可用于触发有关备用无线传输的更复杂信息的共享。 一个例子就是 exchange 图片或 Wi-fi 上的文档。 此外，应用程序还可以使用它来交换应用程序特定的信息，例如，在运行在这两台计算机上的应用程序和 Internet 上的服务之间触发活动所需的标识和地址信息。

用户还可以使用此手势与他们自己的环境中的其他设备进行通信。 例如，在海报上读取标记，或将信息从其计算机传递到手机，反之亦然。

请参阅 [点击和执行用例](tap-and-do-use-cases.md) ，并使用 *分流和 do* 手势解释各种设备交互。

## <a name="related-topics"></a>相关主题

[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  

[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/_nfpdrivers)
