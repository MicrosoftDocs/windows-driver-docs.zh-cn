---
title: 筛选扩展
description: 筛选扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b4c655e43e35e7c1b3f3e45a2988dda862296f
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249295"
---
# <a name="filtering-extensions"></a>筛选扩展


Hyper-v 可扩展交换机筛选扩展可检查、修改和插入可扩展交换机数据路径中的数据包。 根据可扩展交换机端口和交换机策略设置，扩展可以删除数据包或排除其向一个或多个目标端口的传递。

筛选扩展在捕获传入数据路径中的扩展后和传出数据路径中的转发扩展后调用。 有关这些数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

筛选扩展可对在入口数据路径上获取的数据包执行以下操作：

-   筛选数据包流量，并强制使用自定义端口或交换机策略，通过可扩展交换机进行数据包传送。 当筛选扩展筛选入站数据路径中的数据包时，它只能基于源端口和数据包来源的网络适配器连接应用筛选规则。 此信息存储在带外 (OOB) 数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的数据中，可以通过使用 [**网络 \_ 缓冲区 \_ 列表 \_ 开关 \_ 转发 \_ 详细信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail) 宏获取。

    **注意**  在入口数据路径上获取的数据包不包含目标端口。 只能对在出口数据路径上获取的数据包筛选基于目标端口的数据包。

    自定义策略是由独立软件供应商 (ISV) 定义的。 此策略类型的属性设置通过 Hyper-v WMI 管理层进行管理。 筛选扩展通过对象标识符进行配置， () OID [ \_ 交换机 \_ 端口 \_ 属性 \_ 更新](./oid-switch-port-property-update.md) 和 [oid \_ 开关 \_ 属性 \_ 更新](./oid-switch-property-update.md)的对象标识符。

    有关自定义可扩展端口或交换机策略的详细信息，请参阅 [管理 Hyper-v 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

    **注意**  只有转发扩展可以通过可扩展交换机强制实施标准端口策略来传送数据包。

-   将新的、已修改或已克隆的数据包注入入入口数据路径。

    有关详细信息，请参阅 [Hyper-v 可扩展交换机发送和接收操作](hyper-v-extensible-switch-send-and-receive-operations.md)。

筛选扩展可对在出口数据路径上获取的数据包执行以下操作：

-   筛选数据包流量，并强制使用自定义端口或交换机策略，通过可扩展交换机进行数据包传送。 当筛选扩展筛选出出口数据路径中的数据包时，它可以根据数据包的源或目标端口应用筛选规则。 目标端口数据存储在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的 OOB 数据中。 扩展通过调用 [*GetNetBufferListDestinations*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations) 函数获取此信息。

-   排除将数据包传递到一个或多个可扩展交换机目标端口。 这允许筛选扩展排除数据包到可扩展交换机端口的传送。

    有关如何将数据包传递到可扩展交换机端口的详细信息，请参阅 [排除数据包传递到可扩展交换机目标端口](excluding-packet-delivery-to-extensible-switch-destination-ports.md)。

-   通过延迟传出数据路径上的数据包转发，管理流量流向一个或多个目标端口。

    例如，支持服务质量 (QoS) 功能的筛选扩展可能需要立即调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 来转发使用较高优先级值指定的数据包。 根据流量的不同，扩展可能需要在以后转发具有较低优先级值的数据包。

-   修改包数据。 如果筛选扩展需要修改数据包中的数据，则必须先克隆数据包，而不保留端口目标。 然后，该扩展插件必须将已修改的数据包注入入入口数据路径。 这允许基础扩展在已修改的数据包上强制实施策略，转发扩展可以添加端口目标。

    有关详细信息，请参阅 [克隆数据包通信](cloning-or-duplicating-packet-traffic.md)。

除了检查 OID 请求和 NDIS 状态指示，筛选扩展还可以执行以下操作：

-   通过返回 \_ \_ 适用的可扩展交换机 OID 的状态数据，否决创建可扩展交换机端口或网络适配器连接 \_ 。 例如， \_ \_ \_ 当驱动程序收到 [oid \_ 交换机 \_ 端口 \_ CREATE](./oid-switch-port-create.md)的 oid 设置请求时，筛选扩展可以通过返回不被接受的状态数据来拒绝端口创建请求。

    **注意**  筛选扩展不会创建或删除端口或网络适配器连接。 可扩展交换机的协议边缘会发出 Oid，通知底层筛选器驱动程序创建或删除端口或网络适配器连接的过程。 有关详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)。

-   通过返回 \_ \_ 适用的可扩展交换机 OID 的状态数据，拒绝添加或更新可扩展交换机或端口策略 \_ 。 例如， \_ \_ \_ 当扩展接收到 [oid 设置 oid \_ 交换机 \_ 端口 \_ 属性 " \_ 添加](./oid-switch-port-property-add.md)" 时，筛选扩展可以拒绝添加端口策略，方法是返回不被接受的状态数据。

    有关可扩展交换机策略的详细信息，请参阅 [管理 Hyper-v 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

筛选扩展具有以下要求：

-   筛选扩展必须开发为支持可扩展交换机接口的 NDIS 筛选器驱动程序。

    有关筛选器驱动程序的详细信息，请参阅 [NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md)。

    有关如何编写筛选扩展的详细信息，请参阅 [编写 Hyper-v 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)。

    **注意**  Windows 筛选平台 (WFP) 提供内置的可扩展交换机筛选扩展 (Wfplwfs.sys ) 。 此扩展允许 WFP 筛选器或标注驱动程序按照 Hyper-v 可扩展交换机数据路径截获数据包。 这允许筛选器或标注驱动程序使用 WFP 管理和系统函数执行数据包检查或修改。 有关 WFP 的概述，请参阅 [Windows 筛选平台](porting-packet-processing-drivers-and-apps-to-wfp.md)。

-   筛选扩展的 INF 文件必须安装驱动程序作为修改筛选器驱动程序。 NDIS 监视筛选器驱动程序不能安装在可扩展交换机驱动程序堆栈中。

    有关修改筛选器驱动程序的详细信息，请参阅 [筛选器驱动程序的类型](types-of-filter-drivers.md)。

    有关修改筛选器驱动程序的 INF 要求的详细信息，请参阅 [配置修改筛选器驱动程序的 Inf 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

-   筛选器驱动程序的 INF 文件中的 **FilterClass** 值必须设置为 **ms \_ switch \_ 筛选器**。 有关详细信息，请参阅 [Hyper-v 可扩展交换机扩展的 INF 要求](inf-requirements-for-hyper-v-extensions.md)。

-   对于可扩展交换机的每个实例，可以在驱动程序堆栈中绑定和启用任意数量的筛选扩展。 默认情况下，多个筛选扩展基于其安装时间进行排序。 例如，多个筛选扩展在可扩展交换机驱动程序堆栈中分层，其中最新安装的扩展位于堆栈中的其他筛选扩展之上。

    在可扩展交换机的实例中绑定和启用后，可对可扩展交换机驱动程序堆栈中筛选扩展的分层进行重新排序。 有关详细信息，请参阅对 [Hyper-v 可扩展交换机扩展重新排序](reordering-hyper-v-extensibility-switch-extensions.md)。
