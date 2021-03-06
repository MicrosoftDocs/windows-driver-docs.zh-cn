---
title: SO_REUSEADDR
description: SO_REUSEADDR
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_REUSEADDR 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 90f6eebf57ce7af48e17e2372d677f33f6763c35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824985"
---
# <a name="so_reuseaddr"></a>\_REUSEADDR


\_REUSEADDR 套接字选项的状态确定套接字将绑定到的本地传输地址是否始终与其他套接字共享。 此套接字选项仅适用于侦听套接字、数据报套接字和面向连接的套接字。

如果 WSK 应用程序设置此套接字选项，则必须在将套接字绑定到本地传输地址之前执行此操作。

若要设置此套接字选项的状态，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_REUSEADDR</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量包含套接字选项的新状态值：</p>
<ul>
<li><p>0：禁用始终共享本地传输地址</p></li>
<li><p>1：允许始终共享本地传输地址</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

若要检索此 socket 选项的状态，WSK 应用程序需要使用以下参数调用 **WskControlSocket** 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_REUSEADDR</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收 socket 选项的状态值：</p>
<ul>
<li><p>0：始终共享本地传输地址已禁用</p></li>
<li><p>1：始终共享本地传输地址已启用</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

WSK 应用程序在调用 **WskControlSocket** 函数时，必须指定一个指向 IRP 的指针，以便设置或检索 to \_ REUSEADDR socket 选项的状态。

此套接字选项的默认状态是 "始终共享本地传输地址" 处于禁用状态。

若要详细了解如何使用 \_ REUSEADDR 套接字选项及其对套接字间本地传输地址的影响，请参阅 [共享传输地址](./sharing-transport-addresses.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ws2def (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

