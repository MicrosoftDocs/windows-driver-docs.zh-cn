---
title: Member 模板指令
description: Member 模板指令
keywords:
- 成员指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8c8d665577d7a3e472424556b3cc89127d583b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807891"
---
# <a name="member-template-directive"></a>Member 模板指令


\* `Member` 指令也是构造。 此构造的值是一个模板名称。 此模板名称必须出现在 \* 主机模板的 "成员" 列表中 (也就是说，生产所在的模板) 或 \* 主机模板从 (直接或间接) 继承的成员列表。 \* `Member` 构造可以包含被调用的可选子属性 \* **Occurs**。

\**_发生_* 次数指定绑定到成员生产指定的模板的实例数 \* ，该模板可能出现在主机模板的实例中。 绑定到模板的实例从成员指定的模板派生， \* 将作为该模板实例的实例计数。 如果此类出现次数在 \* **出现** 指令定义的范围内，则 \* `Member` 指令的计算结果将为 **TRUE**; 否则，指令将评估为 **FALSE**。 特性或构造模板 (\* 类型：构造或 \* 类型：特性) 可以在构造中引用 \* `Member` 。 \* `Member` 出现在生产指令内的构造与作为 \* \* 模板指令的子元素出现的成员指令不同 \* 。 \*`Member` 是构造，并且是单数形式， \* 成员是一个属性， (以字母 "s" ) 结尾。

\***出现** ：指定绑定到成员生产指定的模板的实例数 \* 。 可以指定一个特定的值，也可以通过使用一对使用连字符分隔 ( ) 来指定一定范围内的值。 如果指定了范围，则第一个数字必须小于第二个数字。 不允许使用负数。 允许的范围包括指定的终结点。 允许值0。 允许使用 GPD 通配符 (\*) ，并匹配范围为0到无限大的任何值。 如果 () 通配符 \* 显示为范围的上部点，则没有上限。 如果通配符显示为范围的下限，则忽略上限。 可以将数字或数字对括在方括号中， (\[ \]) 用于视觉强调。

如果在构造中省略了 " \* **发生**" 属性，则将 \* `Member` 假定范围为0到无限大 (也就是说， \[ 0- \* \]) ， \* `Member` 生产的计算结果将始终为 **TRUE**。

当 \* `Member` 生产为构造模板命名时， \* **出现** 的计数不区分构造的不同实例。 因此绑定到同一模板的构造的三个不同实例将与同一构造的三个相同实例具有相同的匹配项计数。

例如，如果将 **PaperSize** 和 **InputSlot** 绑定到同一个模板，并且如果 \* *_特征： PaperSize_* 定义了两次，则出现计数为2。 如果 \* *_功能： PaperSize_* 定义了一次并且 \* *_功能： InputSlot_* 定义了两次，则出现计数为三。

指令内不允许其他特性或构造 \* `Member` 。

当 \* members 指令与模板绑定过程结合使用时， \* members 指令尝试将模板与在构造内显示的每个子元素相关联。 但它不指定子元素可出现的次数或指定子元素之间或之间的任何依赖项。 \*生产指令负责指定这些要求。 请注意， \* 即使使用了生产指令，成员指令仍是必需的 \* 。

 

 




