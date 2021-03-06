---
title: 支持在协议和筛选器驱动程序中的标头数据拆分
description: 支持 Header-Data 剥离协议驱动程序和筛选器驱动程序
keywords:
- 标头-数据拆分 WDK，协议驱动程序
- 标头-数据拆分 WDK，筛选器驱动程序
- 协议驱动程序 WDK 网络，标题-数据拆分
- 筛选器驱动程序 WDK 网络，标题-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04375d47b96f97170802f6fc1369b0db45dc3f8b
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248018"
---
# <a name="supporting-header-data-split-in-protocol-drivers-and-filter-drivers"></a>支持 Header-Data 剥离协议驱动程序和筛选器驱动程序





NDIS 6.0 和更高版本的协议驱动程序和筛选器驱动程序必须支持在非连续缓冲区中包含标头和数据的接收指示。

您不得假设 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构中只有一个 MDL。 协议驱动程序和筛选器驱动程序不需要执行任何特定于支持标头数据拆分注册的操作。 但是，驱动程序接收处理代码必须处理 MDL 链中的一个或多个 MDL，并且必须使用以下 NDIS MDL 宏来访问 MDL 链：

-   [**NET \_ BUFFER \_ 第一 \_ MDL**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_first_mdl)

-   [**网络 \_ 缓冲区 \_ 当前 \_ MDL**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_current_mdl)

-   [**NET \_ BUFFER \_ 当前 \_ MDL \_ 偏移量**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_current_mdl_offset)

对于拆分缓冲区，与网络缓冲区 \_ [**\_ \_ 数据**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_data)结构) 的 **DataLength** 成员中的网络缓冲区 (相关联的数据长度将跨多个 MDLs 拆分。 例如，如果某个协议驱动程序尝试访问第一个 MDL 中的整个数据缓冲区，则该驱动程序可以访问无效数据。

**注意**  接收指示调用返回到微型端口驱动程序后，微型端口驱动程序可以回收标头 MDLs。 在接收指示调用返回到微型端口驱动程序之后，过量驱动程序或其客户端不能访问标头 MDLs。 即使微型端口驱动程序未指示收到的数据的状态为 "NDIS \_ 接收标志资源"，此限制也适用 \_ \_ 。

 

 

