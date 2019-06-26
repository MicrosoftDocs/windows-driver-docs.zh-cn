---
title: WAN 数据包分帧
description: WAN 数据包分帧
ms.assetid: 11a6fbf5-c7a9-474b-811e-c77a36e834f3
keywords:
- WAN 微型端口驱动程序 WDK 网络数据包
- WAN 的 CoNDIS 驱动程序 WDK 网络数据包
- 数据包分帧 WDK WAN
- NDISWAN WDK 网络
- WAN 数据包分帧 WDK 网络
- 数据包分帧 WDK WAN 有关 WAN 数据包分帧
- WAN 数据包分帧 WDK 网络，WAN 数据包分帧有关
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec833a021ffec7f8dba9e4d78a5889f19ccdd4f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380565"
---
# <a name="wan-packet-framing"></a>WAN 数据包分帧





本部分提供有关 WAN 数据包分帧的信息。

NDISWAN 中间驱动程序检索信息由从微型端口驱动程序的响应的 WAN 微型端口驱动程序执行 WAN 数据包分帧[OID\_WAN\_MEDIUM\_子类型](https://msdn.microsoft.com/library/windows/hardware/ff561216)查询的信息请求。

NDISWAN 将 LAN 从传出数据包转换为 PPP 格式。 NDISWAN 使用简单 HDLC 组帧。 必须由微型端口驱动程序完成大部分特定于媒体的帧。

将数据包发送到 WAN 的微型端口驱动程序的 send 函数之前, NDISWAN 执行简单的 PPP HDLC 组帧。 简单的 PPP HDLC 组帧是不含 FCS、 位或字节堆砌和任何开头或结尾标志的 PPP 的 HDLC 组帧。

以下主题提供有关 WAN 数据包分帧的其他信息：

[异步帧](asynchronous-framing.md)

[ISDN 和切换-56 K 摄影](isdn-and-switched-56k-framing.md)

 

 




