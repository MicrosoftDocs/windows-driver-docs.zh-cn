---
title: 拆分 IPv4 帧
description: 拆分 IPv4 帧
keywords:
- 网络帧拆分 WDK 网络，IPv4 帧
- IPv4 帧 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e03c95f78ec8edbe7865c7b73cda0cf7e0a5f8
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248728"
---
# <a name="splitting-ipv4-frames"></a>拆分 IPv4 帧





若要支持标头数据拆分，NIC 必须支持拆分没有 IPv4 选项的 IPv4 以太网帧。 NIC 必须能够在 [上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)拆分此类帧。

支持 ipv4 以太网帧与 IPv4 选项是可选的。 NIC 可支持某些 IPv4 选项，而不支持其他 IPv4 选项。 NIC 不得拆分包含它无法识别的 IPv4 选项的 IPv4 帧。 拆分框架的标头部分必须包含整个 IPv4 标头以及所有存在的 IPv4 选项。

NIC 还可以支持分段 IPv4 帧的标头数据拆分。 有关分段 IPv4 帧的详细信息，请参阅 [拆分分段的 IP 帧](splitting-fragmented-ip-frames.md)。

**注意**  出于标头数据要求的目的，支持 IPv4 选项、IPv6 扩展标头或 TCP 选项，这意味着 NIC 识别元素的能力，确定元素的长度，将其包含在标头 MDL 中，并找到其端和帧中下一个元素的开头。

 

如果标头-数据拆分提供程序拆分 IPv4 帧，则指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构必须将 NDIS \_ NBL \_ 标志 \_ \_ 设置为 **NblFlags** 成员中的 IPv4 标志。 有关在 NET buffer 列表结构中设置标头数据拆分标志的完整信息 \_ \_ ，请参阅 [设置网络 \_ 缓冲区 \_ 列表信息](setting-net-buffer-list-information.md)。

其他以太网帧特征确定如何拆分 IPv4 帧。 如果 IP 帧有碎片，请参阅 [拆分分段的 IP 帧](splitting-fragmented-ip-frames.md)。 如果帧包含 TCP 信息，请参阅 [在 TCP 负载处拆分帧](splitting-frames-at-the-tcp-payload.md)。 如果帧包含 UDP 信息，请参阅 [在 UDP 负载处拆分帧](splitting-frames-at-the-udp-payload.md)。 对于所有其他情况，请参阅 [拆分除 TCP 和 UDP 以外的帧](splitting-icmp-frames-and-other-upper-layer-protocol-frames.md)。

 

