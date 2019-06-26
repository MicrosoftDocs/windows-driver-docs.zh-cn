---
title: Member 模板指令
description: Member 模板指令
ms.assetid: 3f4bdf3c-30cb-4edc-bd9e-422c4bfbb5b7
keywords:
- 成员指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41bfee072481fea3e585fe2b61a1e60fc63a953a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358610"
---
# <a name="member-template-directive"></a>Member 模板指令


\* `Member`指令也是一种构造。 此构造的值是一个模板名称。 此模板名称必须出现在\*成员列表的主机模板 （在生产中驻留的模板） 中或在\*主机模板 （直接或间接） 继承的成员列表。 \* `Member`构造可包含一个名为的可选子属性\* **Occurs**。

\***发生**指定绑定到模板的实例数的\*生产指定，这可能会出现主机模板的实例中的成员。 通过名为模板绑定到模板派生的实例\*成员生产，则计为该模板的实例的匹配项。 如果发生这种数量处于范围内的\* **Occurs**指令定义， \* `Member`指令的计算结果将为**TRUE**; 否则为指令将被视为**FALSE**。 属性或构造模板 (\*类型：构造或\*类型：可以在引用属性） \* `Member`构造。 \* `Member`出现在构造\*生产指令不与相同\*显示为的子成员指令\*Template 指令。 \*`Member` 是一个构造，并为单数形式，和\*成员是一个特性，并且为复数形式 （结尾字母"s"）。

\***发生**指定绑定到模板的实例数的\*成员生产指定。 可以指定特定值或一系列值可以通过使用一对指定的数字以连字符 （-） 分隔。 如果指定一个范围，则第一个数字必须小于第二个。 不允许使用负数。 允许的范围内包含指定终结点。 允许的值为 0。 GPD 通配符 (\*) 允许并匹配任何值，范围从 0 到无穷大。 如果通配符 (\*) 显示为一个范围的上限终结点没有上限。 如果通配符显示为一个范围的下限，则忽略的上限。 数字对可以放在方括号中 (\[\]) 来可视化表示强调。

如果\* **Occurs**中省略属性\*`Member`构造，从 0 到无穷大范围 (即\[0-\*\]) 假定和\*`Member`生产将计算结果始终为**TRUE**。

当\*`Member`生产名称构造模板\***执行**计数不会区分构造的不同实例之间。 因此，三个不同实例构造绑定到同一个模板将具有相同的匹配项将计为三个相同的构造相同的实例。

例如，如果这两个**PaperSize**并**InputSlot**绑定到同一个模板，如果\***功能：PaperSize**定义的匹配项计数会两次，有两个。 如果\***功能：PaperSize**定义一次并\***功能：InputSlot**定义两次，以及发生计数将为三。

中不允许使用其他属性或构造\*`Member`指令。

当\*成员指令是与模板绑定过程中，结合\*成员指令会尝试将模板与构造中将显示每个子元素相关联。 但它不指定多少次的子元素可以显示或指定的任何之间或子元素之间的依赖关系。 \*生产指令负责指定这些要求。 请注意，\*成员指令时仍要求，即使您使用\*生产指令。

 

 



