---
title: DispatchSetInformation Routines
description: DispatchSetInformation Routines
ms.assetid: 9fb56504-32a7-47b0-b731-df1dc74ce861
keywords:
- 调度例程 WDK 内核，DispatchSetInformation 例程
- DispatchSetInformation 例程
- 设置信息的调度例程 WDK 内核
- IRP_MJ_SET_INFORMATION I/O 函数代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f259e0b3bf2e743bcaa3b87115d436e4e00e2a22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543548"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation Routines





驱动程序的[ *DispatchSetInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_设置\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff550799) I/O 函数代码。 此 I/O 函数代码的驱动程序支持是可选的并通常显示在更高级别的或文件系统驱动程序。 此请求发送的 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序。 例如，发送时在用户模式应用程序调用[ **SetEndOfFile**](https://msdn.microsoft.com/library/windows/desktop/aa365531)，并在调用内核模式组件[ **ZwSetInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567096).

 

 



