---
title: 检索设备实例的状态和问题代码
description: 检索设备实例的状态和问题代码
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7fee118e982dda809522bf3bb898e9e1cf1b4d6c
ms.sourcegitcommit: b17e8a4c9ed6503e844416b4ca3f8c38199c1b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2021
ms.locfileid: "103193335"
---
# <a name="retrieving-the-status-and-problem-code-for-a-device-instance"></a>检索设备实例的状态和问题代码


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括设备状态属性和问题代码属性。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 不支持统一属性模型的属性键，也不支持表示这些属性的相应注册表项值。 但是，可以通过调用 [**CM_Get_DevNode_Status**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status) 函数来检索相应的信息。 为了保持与早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持 **CM_Get_DevNode_Status**。 但是，你应该使用统一设备属性模型的属性键来访问设备驱动程序属性。

此外，在 Windows 8 及更高版本的 Windows 中，还有一个问题状态属性。  此属性包含一个 [NTSTATUS](../kernel/using-ntstatus-values.md) 值，该值可能包含与设备上的问题代码集相关的其他信息。  如果 STATUS_SUCCESS 的问题状态值为，则在设备上设置了问题代码时，没有与问题代码相关的其他信息。

设备驱动程序属性由用于访问 Windows Vista 和更高版本中的属性的属性键标识符列出。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备驱动程序属性的信息，请参阅 [ (Windows vista 和更高版本) 访问设备实例属性 ](accessing-device-instance-properties--windows-vista-and-later-.md)。

若要访问 Windows Server 2003、Windows XP 和 Windows 2000 上的设备实例的状态和问题代码，请调用 **CM_Get_DevNode_Status** 并提供以下参数：

-   将 *pulStatus* 设置为指向 ULONG 类型值的指针，该类型的值接收为设备实例设置的状态位标志。 Status 值可以是在 *Cfg* 中定义前缀为 "DN_" 的任何位标志的组合。

-   将 *pulProblemNumber* 设置为指向 ULONG 类型值的指针，该类型的值接收为设备实例设置的问题号。 问题编号是在 *Cfg* 中定义的前缀为 "CM_PROB_" 的常量之一。 仅当在 *pulStatus* 中设置 DN_HAS_PROBLEM 时， **CM_Get_DevNode_Status** 才设置问题号。

-   将 *dnDevInst* 设置为要为其检索状态和问题代码的设备的设备实例句柄。

-   将 *ulFlags* 设置为零。

如果对 **CM_Get_DevNode_Status** 的调用成功，则 **CM_Get_DevNode_Status** 会检索设备实例的请求状态和问题代码，并返回 CR_SUCCESS。 如果函数调用失败， **CM_Get_DevNode_Status** 将返回一个错误代码，其中包含 *Cfgmgr32* 中定义的前缀 "CR_"。

## <a name="using-device-manager-to-find-problem-code-and-problem-status-for-a-device"></a>使用 Device Manager 查找设备的问题代码和问题状态

当设备出现问题时，设备管理器将在树状视图中覆盖该设备的图标，其中包含一个带感叹号的黄色三角形。  右键单击该设备，然后选择 "属性"，会显示一个对话框，其中包含有关设备的详细信息。 问题代码将出现在 "**设备状态**" 字段中的 "**常规**" 选项卡上。

在 Device Manager 中设备的 "**详细信息**" 选项卡上的 **属性** 下拉列表中，"[**问题状态**](devpkey-device-problemstatus.md)" 属性出现。

## <a name="using-the-debugger-to-find-problem-code-and-problem-status-for-a-device"></a>使用调试器查找设备的问题代码和问题状态

若要查看内核调试器中有问题代码的所有设备，请使用 [**！ devnode 0 21**](../debugger/-devnode.md) 扩展。 这也会显示设备上的 ProblemStatus。 例如：

```
0: kd> !devnode 0 21
Dumping IopRootDeviceNode (= 0x85d37e30)
DevNode 0x8ad6ab78 for PDO 0x81635c30
  InstancePath is "ROOT\DIINSTALLDRIVER\0003"
  ServiceName is "isolated"
  State = DeviceNodeRemoved (0x312)
  Previous State = DeviceNodeInitialized (0x302)
  Problem = CM_PROB_FAILED_ADD
  Problem Status = 0xc00000bb
```

你还可以通过发出 [**！ devnode**] ( 来查看问题代码和问题状态。DEVICE_NODE 地址上的/debugger/-devnode.md) ：

```
0: kd> !devnode 0x8ad6ab78 
DevNode 0x8ad6ab78 for PDO 0x81635c30
  Parent 0x85d37e30   Sibling 0x8adee670   Child 0000000000   
  ...
  Problem = CM_PROB_FAILED_ADD
  Problem Status = 0xc00000bb
```

## <a name="see-also"></a>另请参阅
 
* [**DEVPKEY_Device_ProblemCode**](devpkey-device-problemcode.md)
* [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)
