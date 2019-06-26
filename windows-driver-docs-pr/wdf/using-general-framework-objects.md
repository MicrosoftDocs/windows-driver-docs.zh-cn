---
title: 使用常规框架对象
description: 使用常规框架对象
ms.assetid: d3356d3f-8110-44dd-b4a2-36265f5a1714
keywords:
- framework 对象 WDK KMDF，常规
- 通用框架对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfb13887725bd1288796c03d4fd258e13855fd38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327019"
---
# <a name="using-general-framework-objects"></a>使用常规框架对象


*常规框架对象*是所有其他类型的框架对象都派生的 framework 对象。

类似于其他框架对象，一般的对象支持引用计数、 上下文空间、 删除回调函数和父对象，如中所述[Framework 对象简介](introduction-to-framework-objects.md)。

驱动程序可以创建和使用通用框架对象。 如果您的驱动程序调用[ **WdfObjectCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548730)若要创建一般的对象，该驱动程序可以：

-   创建每个常规对象的一个或多个上下文空间。

    可以使用对象上下文空间来存储有关你想要将与常规对象相关联的系统资源的信息。

    有关上下文空间的详细信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

-   分配给常规对象的父级。

    删除父对象时，将删除常规对象。 例如，如果您的驱动程序指定 framework 设备对象作为其常规对象之一的父对象，该框架将删除常规对象时它将删除的设备对象。

    驱动程序通过设置指定对象的父对象**ParentObject**的对象的成员[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构。

-   提供了删除回调函数。

    该驱动程序可以提供[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)并[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)函数，可以释放系统资源它创建常规对象时，分配给该驱动程序。 例如，如果该驱动程序调用[ **ExAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544501)创建了一个常规对象，清理或销毁回调函数时可以调用[ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590).

使用一般的对象可以是一种方便的方法来管理驱动程序分配资源。 例如，更高级别的驱动程序可能需要多个内存分配，以处理接收的 I/O 请求，如果驱动程序将请求发送到多个设备，或为多个较小的中断请求。 该驱动程序可以创建一个或多个一般的对象的子级的已接收的 I/O 请求，并且它可以在一般的对象的上下文空间中存储有关内存分配的信息。

 

 




