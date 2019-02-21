---
title: 网络 INF 文件中删除部分
description: 网络 INF 文件中删除部分
ms.assetid: c9be4e98-fa35-4966-895a-aebe29f16289
keywords:
- INF 文件 WDK 网络，删除部分
- 可使用网络 INF 文件 WDK，删除部分
- 删除部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e95cf8aecd7d411470c53ed8640c05b154316fdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543209"
---
# <a name="remove-section-in-a-network-inf-file"></a>网络 INF 文件中删除部分





**删除**支持部分**NetClient**， **NetTrans**，并且**NetService**组件而不是为**Net**组件 （适配器）。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

网络类安装程序不会不跟踪的适配器实例。 一个**删除**删除由其他适配器或适配器的多个实例共享的文件的部分可能导致这些适配器或适配器实例不起作用。
是否必须由驱动程序文件中删除**Net**组件，请使用一个跟踪的所有驱动程序的使用文件的共同安装程序。 此类共同安装程序还应跟踪的同一个设备，以及多个设备的驱动程序的多个实例。 有关共同安装程序的详细信息，请参阅[创建一个 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff549520)。

 

 




