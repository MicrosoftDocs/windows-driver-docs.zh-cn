---
title: Bug 检查 0x168 CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP bug 检查具有 0x00000168 值。 这表示群集共享卷状态转换时间太长。
keywords:
- Bug 检查 0x168 CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 557e4069b7eb94971257813e770270a0d52c57e2
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519958"
---
# <a name="bug-check-0x168-clustercsvstatetransitiontimeoutlivedump"></a>Bug 检查 0x168：群集\_CSV\_状态\_过渡\_超时\_LIVEDUMP

群集\_CSV\_状态\_过渡\_超时\_LIVEDUMP bug 检查的值为 0x00000168。 这表示群集共享卷状态转换时间太长。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。



## <a name="clustercsvstatetransitiontimeoutlivedump-parameters"></a>群集\_CSV\_状态\_过渡\_超时\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 群集服务 PID。|
|2| CSV 目标状态 Id-下面列出。 |
|3| 保留 |
|4| 保留 |


**CSV 目标状态 Id**

卷转换为 Init 状态等待 0。 

1 等待卷转换为已暂停状态。 

卷转换为排出状态等待 2。 

3 个等待转换为组低级别状态的卷。 

4 个等待卷转换为活动状态。


## <a name="cause"></a>原因
-----

群集共享卷状态转换时间太长。 系统生成的转储实时的分析的延迟。

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[Bug 检查代码参考](bug-check-code-reference2.md)




