---
title: 启用和禁用连接卸载服务
description: 启用和禁用连接卸载服务
keywords:
- 连接卸载 WDK TCP/IP 传输，启用服务
- 连接卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4434c1f3c688ac44112e1e6501b25604c725352e
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249124"
---
# <a name="enabling-and-disabling-connection-offload-services"></a>启用和禁用连接卸载服务





协议驱动程序使用对象标识符 (OID) 请求启用连接卸载服务。

**注意**  启用或禁用任务卸载服务不同于启用或禁用连接卸载服务。 小型端口驱动程序在协议驱动程序指定封装类型后激活所有可用的任务卸载服务。

 

TCP/IP 传输通过设置 [oid \_ TCP \_ 连接 \_ 卸载 \_ 参数](./oid-tcp-connection-offload-parameters.md) OID，启用或禁用网络接口卡的连接卸载功能 (NIC) 。 在此设置操作中，TCP/IP 传输传递 \_ \_ \_ \_ [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员中的 ndis TCP 连接卸载参数结构。  (有关 NDIS \_ TCP \_ 连接 \_ 卸载参数的信息 \_ ，请参阅 [ndis 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。 ) 

有关配置连接卸载服务的详细信息，请参阅 [NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)中的初始化卸载目标。

 

