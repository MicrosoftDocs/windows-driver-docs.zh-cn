---
title: 排除将数据包传送到可扩展交换机目标端口
description: 排除将数据包传送到可扩展交换机目标端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc11aa6e245ceb0c85eee648865b35612444edd7
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248677"
---
# <a name="excluding-packet-delivery-to-extensible-switch-destination-ports"></a>排除将数据包传送到可扩展交换机目标端口


本主题介绍 Hyper-v 可扩展交换机扩展可以如何排除数据包到可扩展交换机端口的传输。 数据包的目标端口在带外 (OOB 中指定，) 转发上下文位于数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构内。 有关此上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

**注意**  本页假设你熟悉 [Hyper-v 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md) 和 [混合转发](hybrid-forwarding.md)概述中的信息和关系图。


**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。 有关扩展的详细信息，请参阅 [Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)。

筛选和转发扩展可以排除在可扩展交换机入口或传出数据路径上获取的数据包的传送。 可以通过以下方式排除数据包传递：

-   此扩展可以通过完成数据包请求或指示来丢弃数据包。 这不包括将数据包传递到任何可扩展交换机端口。 此方法可用于具有一个或多个目标端口的数据包。

    对于在可扩展交换机入口数据路径上获取的数据包，扩展通过调用 [**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)来完成数据包发送请求。

    对于在可扩展交换机传出数据路径上获取的数据包，扩展通过调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)来完成数据包接收指示。

-   对于在包含多个目标端口的出口数据路径上获取的数据包，扩展可以通过修改一个或多个目标端口的数据来排除数据包传递。 此扩展通过将目标端口的 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的 **IsExcluded** 成员设置为1的值来实现此目的。 此方法允许将数据包传递到其 **IsExcluded** 值设置为零的那些端口。

    **注意**  在入口数据路径上获取的数据包不包含目标端口。 此数据仅在可扩展交换机将数据包向上转发传出数据路径后才可用。

扩展修改了目标端口的 **IsExcluded** 值后，必须将传出数据路径中的数据包转发到过量扩展。 但是，如果将所有数据包的目标端口的 **IsExcluded** 数据设置为1，则扩展应通过完成数据包接收指示而不是转发数据包来丢弃数据包。

**注意**  在扩展将目标端口的 **IsExcluded** 值设置为1后，传出数据路径上的过量扩展不能将此值更改为零。

**注意**  捕获扩展不能排除数据包到可扩展交换机端口的传送。

筛选和转发扩展必须遵循以下准则，将数据包传递到可扩展交换机端口：

-   在可扩展交换机入口数据路径上，筛选和转发扩展可以根据数据包的源端口或数据的策略条件排除数据包传送。

    源端口信息存储在包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的 OOB 数据中 [**NDIS \_ 交换机 \_ 转发 \_ 详细 \_ \_ \_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)信息联合。 扩展通过使用 [**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail) 宏获取数据。

    如果扩展插件不能传递从入口数据路径获取的数据包，则必须通过完成数据包发送请求来删除该数据包。

-   在可扩展交换机入口数据路径上，转发扩展会确定数据包的目标端口，并将此信息添加到数据包的 OOB 数据中。 根据扩展强制执行的策略条件，它可以通过不将包的目标端口信息添加到 OOB 数据来排除到端口的数据包传送。

    有关此过程的详细信息，请参阅 [将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

-   在可扩展的交换机出口数据路径上，筛选和转发扩展可以根据策略标准排除数据包的传送。 例如，筛选扩展可以根据包的源端口或目标端口的策略条件排除数据包传送。

    通过执行以下步骤，扩展插件不会将数据包传递到目标端口：

    1.  扩展通过调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)来获取数据包的目标端口。 如果调用返回 NDIS \_ 状态 " \_ 成功"，则 " *目标* " 参数包含指向 [**ndis \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array) 结构的指针。 此结构指定数据包的可扩展交换机目标端口。 每个目标端口的格式为 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination) 结构。

        **注意** 如果 [**NDIS \_ 交换机 \_ 转发 \_ 目标 \_ 数组**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)结构的 **NumDestinations** 成员包含的值为零，则数据包没有目标端口数据。

2.  此扩展通过将目标端口的 [**NDIS \_ 交换机 \_ 端口 \_ 目标**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)结构的 **IsExcluded** 成员设置为1，将数据包传递排除为可扩展交换机端口。

    **注意**  如果扩展不包括将数据包传送到其所有目标端口，则扩展必须通过完成数据包的接收指示来丢弃数据包。

3.  如果扩展不包括传递到数据包中的一个或所有目标端口，则必须执行以下操作：

    -   扩展必须调用 [*UpdateNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations) ，以将这些更改提交到数据包的 OOB 数据。

    -   扩展必须调用 [*ReportFilteredNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。 调用此函数时，可扩展交换机接口将为排除的数据包递增计数器和日志事件。 扩展必须先进行此调用，然后才能将数据包转发到从中获取数据包的可扩展交换机数据路径中。

    同样，如果扩展完成了数据包发送请求，或指示要排除数据包的所有端口，它还必须调用 [*ReportFilteredNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)。

    **注意**  扩展可以为扩展不包括的数据包创建 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的链接列表。 当扩展调用 [*ReportFilteredNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)时，它会将 *NetBufferLists* 参数设置为指向链接列表的指针。

有关可扩展交换机入口和出口数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。
