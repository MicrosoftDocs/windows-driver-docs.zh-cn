---
title: 自定义的半色调
description: 自定义的半色调
ms.assetid: cc14ff92-743b-42ca-b70f-0df768762f01
keywords:
- Unidrv、 半色调
- 半色调 WDK Unidrv
- 自定义半色调 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffa9b44578ae34ecba3124c2af4232ab8d32497a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369827"
---
# <a name="customized-halftoning"></a>自定义的半色调





Unidrv 使您能够使用 GDI，打印机设备的半色调操作，或通过自定义驱动程序代码。 本部分介绍如何执行自定义驱动程序代码中的半色调操作。

提供了两种类型的自定义项：

-   自定义的半色调模式

-   自定义的半色调方法

### <a href="" id="ddk-customized-halftone-patterns-gg"></a>自定义的半色调模式

可以指定半色调模式中的资源 DLL，也可以生成这些插件的呈现实现[ **IPrintOemUni::HalftonePattern** ](https://msdn.microsoft.com/library/windows/hardware/ff554258)方法。 此方法的参考页提供了如何生成半色调模式的示例。

[**IPrintOemUni::HalftonePattern** ](https://msdn.microsoft.com/library/windows/hardware/ff554258)如果下列任一条件，则应实现：

-   中的资源 DLL，提供了自定义的模式和模式进行加密。

-   资源 DLL 中未提供自定义的模式。 相反，它们都由[ **IPrintOemUni::HalftonePattern**](https://msdn.microsoft.com/library/windows/hardware/ff554258)。

[ **IPrintOemUni::HalftonePattern** ](https://msdn.microsoft.com/library/windows/hardware/ff554258)方法的用途是返回到 Unidrv，又将其传递给 GDI 可用半色调模式。 该方法既可以解码存储以加密形式，资源 DLL 中的模式或可能在执行期间会生成一种模式。

如果你实现了**IPrintOemUni::HalftonePattern**文件必须包含\*HTCallbackID 属性中每个半色调\*选项指定为其自定义的模式是半色调方法的条目使用。

有关此属性的详细信息，请参阅[半色调功能的选项属性](option-attributes-for-the-halftone-feature.md)。

### <a href="" id="ddk-customized-halftoning-methods-gg"></a>自定义的半色调方法

对于使用 Unidrv 打印机，以提供实现代码自定义的半色调方法的步骤如下所示：

1.  提供用于实现的插件呈现[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)方法。

2.  包括半色调\*功能与每个包含的打印机的 GPD 文件中的条目\*选项表示半色调方法的条目。 （标准和自定义的半色调方法都可以是包含。）

[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)方法接收 GDI 位图作为输入。 该方法必须执行的操作半色调，基于当前所选的半色调方法，并返回到 Unidrv 的生成的位图。

如果呈现插件实现[ **IPrintOemUni::ImageProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff554261)，它可以实现[ **IPrintOemUni::MemoryUsage** ](https://msdn.microsoft.com/library/windows/hardware/ff554264).

有关半色调的详细信息，请参阅[Unidrv 与半色调](halftoning-with-unidrv.md)。

 

 



