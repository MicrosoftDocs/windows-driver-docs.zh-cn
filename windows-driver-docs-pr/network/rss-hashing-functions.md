---
title: RSS 哈希函数
description: RSS 哈希函数
keywords:
- 接收方缩放 WDK 网络，哈希
- RSS WDK 网络，哈希
- 哈希 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1faebb9ffa56fcbef1e8832528deeeee27b9c248
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248462"
---
# <a name="rss-hashing-functions"></a>RSS 哈希函数


## <a name="overview"></a>概述

NIC 或其微型端口驱动程序使用 RSS 哈希函数来计算 RSS 哈希值。

过量驱动程序设置哈希类型、函数和表以将连接分配给 Cpu。 有关详细信息，请参阅 [RSS 配置](rss-configuration.md)。

哈希函数可以是下列项之一：

- **NdisHashFunctionToeplitz**
- **NdisHashFunctionReserved1**
- **NdisHashFunctionReserved2**
- **NdisHashFunctionReserved3**

>[!NOTE]
> 目前， **NdisHashFunctionToeplitz** 是可用于微型端口驱动程序的唯一哈希函数。 其他哈希函数是为 NDIS 预留的。 

微型端口驱动程序应标识在驱动程序指示接收的数据之前，它在每个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构中所使用的哈希函数和值。 有关详细信息，请参阅 [指示 RSS 接收数据](indicating-rss-receive-data.md)。

## <a name="examples"></a>示例

以下四个伪代码示例显示了如何计算 **NdisHashFunctionToeplitz** 哈希值。 这些示例表示可用于 **NdisHashFunctionToeplitz** 的四种可能的哈希类型。 有关哈希类型的详细信息，请参阅 [RSS 哈希类型](rss-hashing-types.md)。

若要简化示例，需要一个用于处理输入字节流的通用算法。 在后面的四个示例中定义字节流的特定格式。

过量驱动程序提供 (K) 到微型端口驱动程序的密钥，以便在哈希计算中使用。 密钥为40字节 (320 位) 长。 有关密钥的详细信息，请参阅 [RSS 配置](rss-configuration.md)。

给定包含 *n* 个字节的输入数组，字节流定义如下：

```c++
input[0] input[1] input[2] ... input[n-1]
```

最左侧的字节为输入 \[ 0 \] ，输入0的最高有效位是最左侧的位 \[ \] 。 最右侧的字节是输入 \[ n-1 \] ，输入 n-1 的最小有效位 \[ \] 是最右端。

给定前面的定义，用于处理常规输入字节流的伪代码定义如下：

```c++
ComputeHash(input[], n)

result = 0
For each bit b in input[] from left to right
{
if (b == 1) result ^= (left-most 32 bits of K)
shift K left 1 bit position
}

return result
```

伪代码包含窗体的条目 @n-m 。 这些条目标识 TCP 数据包中每个元素的字节范围。

### <a name="example-hash-calculation-for-ipv4-with-the-tcp-header"></a>带有 TCP 标头的 IPv4 的示例哈希计算

将包的 SourceAddress、DestinationAddress、SourcePort 和 DestinationPort 字段连接到字节数组，并保留它们在数据包中的出现顺序：

```c++
Input[12] = @12-15, @16-19, @20-21, @22-23
Result = ComputeHash(Input, 12)
```

### <a name="example-hash-calculation-for-ipv4-only"></a>仅 IPv4 的示例哈希计算

将数据包的 SourceAddress 和 DestinationAddress 字段连接到字节数组。

```c++
Input[8] = @12-15, @16-19
Result = ComputeHash(Input, 8) 
```

### <a name="example-hash-calculation-for-ipv6-with-the-tcp-header"></a>带有 TCP 标头的 IPv6 的示例哈希计算

将包的 SourceAddress、DestinationAddress、SourcePort 和 DestinationPort 字段连接到字节数组，并保留它们在数据包中出现的顺序。

```c++
Input[36] = @8-23, @24-39, @40-41, @42-43
Result = ComputeHash(Input, 36)
```

### <a name="example-hash-calculation-for-ipv6-only"></a>仅适用于 IPv6 的示例哈希计算

将数据包的 SourceAddress 和 DestinationAddress 字段连接到字节数组。

```c++
Input[32] = @8-23, @24-39
Result = ComputeHash(Input, 32)
```

 

