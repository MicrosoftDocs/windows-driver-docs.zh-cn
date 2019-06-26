---
title: Bug 检查 0x1D2 WORKER_THREAD_INVALID_STATE
description: WORKER_THREAD_INVALID_STATE bug 检查具有 0x000001D2 值。
keywords:
- Bug 检查 0x1D2 WORKER_THREAD_INVALID_STATE
- WORKER_THREAD_INVALID_STATE
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WORKER_THREAD_INVALID_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 89416fb269fc99c3843cf45d963136baca8d437e
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239409"
---
# <a name="bug-check-bug-check-0x1d2-workerthreadinvalidstate"></a>Bug 检查 Bug 检查 0x1D2:辅助角色\_线程\_无效\_状态 

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


辅助角色\_线程\_无效\_状态 bug 检查的值为 0x000001D2。 

此错误表示 executive 工作线程处于无效状态。

## <a name="workerthreadinvalidstate-parameters"></a>辅助角色\_线程\_无效\_状态参数

参数 | 描述 
|---------|--------------|
1 | 失败的类型
2 | 工作线程地址
3 | 保留
4 | 保留



**参数 1 的值**

  0x0:工作线程终止的过程中具有未完成 I/O
  
  2-的工作线程地址
  
  3-保留
  
  4-保留