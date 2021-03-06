---
title: 确定网络适配器的 VMQ 功能
description: 确定网络适配器的 VMQ 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4320b78d5a0c1be68d333ee990febd9fd0a163d3
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248361"
---
# <a name="determining-the-vmq-capabilities-of-a-network-adapter"></a>确定网络适配器的 VMQ 功能





NDIS 提供接口来确定网络适配器的 VMQ 功能，如：

-   网络适配器的一般筛选功能。

-   支持的 VM 队列功能。

-   预测先行支持允许将网络数据内存拆分为两个不同的缓冲区。

    **注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。

     

小型端口驱动程序在网络适配器初始化期间为 NDIS 提供以下信息：

-   网络适配器可支持的 VMQ 硬件功能。

-   当前启用的 VMQ 功能。

-   在网络适配器上启用或禁用的全局接收筛选功能。

过量驱动程序和应用程序可以使用以下 OID 查询请求来获取网络适配器功能。

[OID \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md)

[OID \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md)

[OID \_ 接收 \_ 筛选器 \_ 全局 \_ 参数](./oid-receive-filter-global-parameters.md)

NDIS 处理微型端口驱动程序的这些 OID 查询请求。 因此，没有为微型端口驱动程序请求查询。 NDIS 在初始化期间报告网络适配器的当前启用的接收 VMQ 功能。 因此，过量驱动程序不必查询这些 Oid。

[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构指定网络适配器的筛选功能。 此结构的使用方式如下：

-   当 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，微型端口驱动程序通过初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构来注册其筛选功能。 然后，该驱动程序将 [**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的 **HardwareReceiveFilterCapabilities** 成员设置为指向 **ndis \_ 接收 \_ 筛选器 \_ 功能** 结构。 接下来，驱动程序将调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，然后将 *MiniportAttributes* 参数设置为指向 **NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性** 结构的指针。

-   当 NDIS 调用驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，过量协议驱动程序在 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中接收 [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

-   当 NDIS 调用驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数时，过量筛选器驱动程序在 [**ndis \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构中接收 [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

-   过量驱动程序通过发出 oid 查询请求（ [oid \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md)或 [oid \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md)）来接收 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。 **HardwareReceiveFilterCapabilities** 和 **CurrentReceiveFilterCapabilities** 成员指向 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构包含以下信息：

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
支持的接收筛选器的类型。 NDIS \_ 接收 \_ 筛选 \_ VMQ \_ 筛选器 \_ 已启用标志指定虚拟机队列 (VMQ) 筛选器已启用。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
支持的接收队列的类型。 "NDIS \_ 接收 \_ 筛选器 \_ VM \_ 队列 \_ 已启用" 标志指定启用虚拟机 (VM) 队列。

<a href="" id="numqueues"></a>**NumQueues**  
网络适配器支持的接收队列的数量。 若要支持 VMQ，此数字必须等于或小于 NIC 支持的单播 MAC 地址数。 此数字不能包含默认队列。

**注意**  网络适配器支持的单播 MAC 地址或 VM 队列的数目不包括相关 NIC 的 MAC 地址。

 

<a href="" id="supportedqueueproperties"></a>**SupportedQueueProperties**  
网络适配器支持的队列属性。 "NDIS \_ 接收 \_ 筛选器 \_ VM \_ 队列支持" \_ 标志指定网络适配器提供支持 VMQ 筛选的最低要求。 支持 VMQ 的 NIC 必须为每个接收队列提供一个 MSI-X 表条目。 因此，VMQ 微型端口驱动程序必须设置 NDIS \_ 接收 \_ 筛选器 \_ MSI \_ X 支持的 \_ 标志。

<a href="" id="supportedfiltertests"></a>**SupportedFilterTests**  
小型端口驱动程序支持的筛选器测试操作。 例如，网络适配器支持测试选定的标头字段，以确定它是否等于给定的值。 VMQ 微型端口驱动程序必须将 NDIS \_ 接收 \_ 筛选器 \_ 测试 \_ 标头字段设置为 \_ \_ 等于 \_ 受支持的标志。

<a href="" id="supportedheaders"></a>**SupportedHeaders**  
微型端口驱动程序可以检查的网络数据包标头的类型。 例如，网络适配器可以检查网络数据包的 MAC 标头。 MAC 标头包括数据包类型、目标和源 MAC 地址、VLAN 标识符和优先级标记字段。 VMQ 微型端口驱动程序必须设置 NDIS \_ 接收 \_ 筛选器 \_ MAC \_ 标头 \_ 支持的标志。

<a href="" id="supportedmacheaderfields"></a>**SupportedMacHeaderFields**  
微型端口驱动程序可以检查的 MAC 标头字段的类型。 VMQ 微型端口驱动程序必须设置 NDIS \_ 接收 \_ 筛选器 \_ MAC \_ 标头 \_ 目标 \_ 地址 \_ 支持的标志。

<a href="" id="maxmacheaderfilters"></a>**MaxMacHeaderFilters**  
微型端口驱动程序支持的 MAC 标头筛选器的最大数目。 标头筛选器应该至少与 VM 队列一样多。

<a href="" id="maxqueuegroups"></a>**MaxQueueGroups**  
此成员是为 NDIS 保留的。

<a href="" id="maxqueuesperqueuegroup"></a>**MaxQueuesPerQueueGroup**  
此成员是为 NDIS 保留的。

<a href="" id="minlookaheadsplitsize"></a>**MinLookaheadSplitSize**  
网络适配器为预测先行数据包段支持的最小大小（以字节为单位）。

**注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 支持 NDIS 6.30 或更高版本的微型端口驱动程序必须将此成员设置为零。

 

<a href="" id="maxlookaheadsplitsize"></a>**MaxLookaheadSplitSize**  
网络适配器为预测先行数据包段支持的最大大小（以字节为单位）。

**注意**  从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 支持 NDIS 6.30 或更高版本的微型端口驱动程序必须将此成员设置为零。

 

成功从 [oid \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md)OID 查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 ndis \_ 接收 \_ 筛选器 \_ 功能结构的指针。 这些功能可能包括由 INF 文件设置或通过 " **高级** 属性" 页当前禁用的 VMQ 硬件功能。 有关 VMQ INF 文件设置的详细信息，请参阅 [Vmq 标准 INF 条目](./standardized-inf-keywords-for-vmq.md)。

NDIS 微型端口驱动程序在初始化期间，在 [**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的 **HardwareReceiveFilterCapabilities** 成员中提供接收筛选硬件功能。

成功从 [oid \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md)OID 查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的指针。 这些功能包括当前启用的 VMQ 功能。

NDIS 微型端口驱动程序在初始化期间提供当前启用的接收筛选功能，在 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的 **CurrentReceiveFilterCapabilities** 成员中。

在绑定操作期间，NDIS 会将基础网络适配器的当前启用的接收筛选功能报告给 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **ReceiveFilterCapabilities** 成员中的过量协议驱动程序。

在 [OID 接收筛选器 \_ \_ \_ 全局 \_](./oid-receive-filter-global-parameters.md)参数结构中使用了 [**NDIS \_ 接收 \_ 筛选 \_ \_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)器全局参数结构，以获取当前的全局接收筛选器设置。

NDIS \_ 接收 \_ 筛选器 \_ 全局 \_ 参数包含以下信息：

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
已启用的接收筛选器的类型。 NDIS \_ 接收 \_ 筛选 \_ VMQ \_ 筛选器 \_ 已启用标志指定虚拟机队列 (VMQ) 筛选器已启用。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
已启用的接收队列的类型。 "NDIS \_ 接收 \_ 筛选器 \_ VM \_ 队列 \_ 已启用" 标志指定启用虚拟机 (VM) 队列。

成功从 [oid \_ 接收 \_ 筛选器 \_ 全局 \_ 参数](./oid-receive-filter-global-parameters.md)OID 查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 全局 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)结构的指针。 NDIS \_ 接收 \_ 筛选器 \_ 全局 \_ 参数结构指定在网络适配器上启用或禁用的接收筛选功能。

NDIS 协议驱动程序使用 OID \_ 接收 \_ 筛选器 \_ 全局 \_ 参数在网络适配器上查询接收筛选的当前全局配置参数。 例如，协议驱动程序可以使用此 OID 来确定是启用还是禁用接收队列的类型。

 

