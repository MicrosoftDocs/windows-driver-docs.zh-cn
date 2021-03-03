---
title: 通过传感器诊断工具测试传感器功能
description: 使用传感器诊断工具来测试驱动程序、固件和硬件功能。
keywords:
- 测试传感器
- 传感器，测试
- 传感器诊断工具
- 传感器驱动程序，测试
- 传感器固件，测试
- 传感器硬件，测试
- 传感器事件
- 传感器，报表间隔
- 传感器，更改敏感度
- 报表间隔
- 更改敏感度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12145a181c18de401d21f241934016e514c5c77c
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682246"
---
# <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>通过传感器诊断工具测试传感器功能

> [!IMPORTANT]
> 传感器诊断工具与以前版本的 Windows 一起使用。 Microsoft 建议使用 [SensorExplorer](testing-sensor-explorer.md) 来验证是否安装了支持的传感器。

使用传感器诊断工具来测试驱动程序、固件和硬件功能。

该工具调用要测试的传感器和位置 API：

- 数据检索
- 事件处理
- 报表间隔
- 更改敏感度
- 属性检索

您可以使用传感器诊断工具，该工具随 Windows 驱动程序工具包的一部分提供，而不是编写应用程序来执行这些测试，)  (。

例如，如果你的驱动程序开发计算机是基于 x64 的计算机，并且你将该 WDK 安装到了默认位置，则会在以下文件夹中找到传感器诊断工具：

*C： \\Program Files (x86) \\ Windows 工具包 \\ 10 \\ 工具 \\ x64 \\sensordiagnostictool.exe* 安装传感器或位置驱动程序并将硬件连接到 PC 后，该工具会立即在可用传感器列表中识别并记录你的设备。

下图显示了在多个传感器连接到 PC 时的传感器诊断工具启动屏幕。 计算机上的可用传感器显示在左窗格中。

![传感器诊断工具：启动](images/sdt-startup.png)

在这种情况下，传感器诊断工具检测到存在一个 HID 传感器集合，以及一个简单的设备方向传感器、Windows 位置提供程序和地理位置驱动程序示例支持的地理位置传感器。

## <a name="support-for-ambient-light-sensors"></a>支持环境光线传感器

传感器诊断工具包括对环境光线传感器 (ALS) 的支持。 当前显示亮度会在工具左上角的 SB% 框中报告。

但是，请务必注意，当工具检索 ALS 值时，它会将这些值作为 (LUX、Offset) 对返回。 此顺序不同于高级配置和电源接口 (ACPI) 标准 (Offset，LUX) 对。

## <a name="related-topics"></a>相关主题

[测试传感器功能](testing-sensor-functionality.md)  
[测试定位功能](testing-location-functionality.md)  
