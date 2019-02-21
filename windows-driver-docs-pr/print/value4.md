---
title: 值 (TCP/IP)
description: TCP/IP 值构造可以双向通信使用扩展架构从特定的 MIB 对象检索数据的查询。
ms.assetid: 46b24830-10a1-405b-9c12-b5804f76d668
keywords:
- 值构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f48c5e71e3f3779efee4c1641841ff04009acae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525078"
---
# <a name="value-tcpip"></a>值 (TCP/IP)


TCP/IP`Value`构造可以扩展从特定的 MIB 对象检索数据的查询的双向通信架构。 `Value` Tcpbidi.xsd 中定义构造。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>deviceIndex</strong></p></td>
<td><p>一个标志，当<strong>，则返回 TRUE</strong>，表示关联的算法，必须在指定的 OID; 包含设备索引时<strong>FALSE</strong>，尾随零追加到该 OID。 默认值是<strong>FALSE</strong>。 有关详细信息，请参阅此表后面的说明。</p></td>
</tr>
<tr class="even">
<td><p><strong>drvPrinterEvent</strong></p></td>
<td><p>（可选）一个布尔值，该值指示端口监视器是否将通知发送到该驱动程序。 一个<strong>，则返回 TRUE</strong>值指示端口监视器将通知发送到驱动程序;<strong>FALSE</strong>指示端口监视器不向驱动程序发送通知。</p></td>
</tr>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>oid</strong></p></td>
<td><p>形式的对象 ID (OID) 的 MIB 对象的地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>refreshInterval</strong></p></td>
<td><p>（可选）轮询间隔 （秒） 的值。 默认值为 600 秒。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>中的数据类型<code> Value</code>构造中的值<a href="https://msdn.microsoft.com/library/windows/hardware/ff545211" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545211)"> <strong>BIDI_TYPE</strong> </a>枚举。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  支持 SNMP 协议的网络设备可以是不同的子设备，如处理器、 网络、 打印机和磁盘存储的主机。 在网络打印机中实现的 MIB 表中具有由设备索引编制索引的条目。 若要从 MIB 表 （如送纸器的名称） 检索数据，查询必须具有正确地标识子设备索引。 标准 TCP/IP 端口监视器允许通过端口配置 UI 来手动配置的设备索引。 使用扩展名为 bidi **deviceIndex**="true"与从端口配置 UI 中获取相应的设备索引生成 OID。 此外，如果`Value`构造包含属性实例中，OID 会追加到其最终的零的索引。

 

### <a href="" id="code-example"></a> 代码示例

下面的代码示例通过添加新属性扩展 bidi 通信架构**系统**给**打印机**属性。 **系统**属性具有`Value`构造，具有**名称**，**类型**，并且**oid**属性。

```cpp
<Property name="Printer">
  <Property name="System">
    <Value name="Name" type="BIDI_STRING" oid="1.3.6.1.2.1.1.5"/>
  </Property>
</Property>
```

前面的示例生成以下查询：

```cpp
\Printer.System:Name
```

请注意，由于`Value`构造包含了属性实例而不是 IndexedProperty 实例中，尾随零自动追加到该 OID。

 

 



