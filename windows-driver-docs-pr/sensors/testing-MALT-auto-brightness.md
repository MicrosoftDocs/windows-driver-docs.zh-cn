---
title: 测试自动亮度
description: 本主题介绍如何使用 MALT (Microsoft 环境光线工具) 工具测试自动亮度。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: decafbfe0777bccf6b4133e0a6ef40b487a09c2f
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682292"
---
# <a name="testing-auto-brightness"></a>测试自动亮度

本主题介绍如何使用 MALT (Microsoft 环境光线工具) 工具测试自动亮度。 自动或自适应亮度是指系统自动设置的屏幕亮度，以响应环境光线传感器读数。

## <a name="set-up"></a>设置

通读 [ (MALT) 的构建轻型测试工具 ](testing-MALT-building-a-light-testing-tool.md) 主题，以确保满足测试的要求。

### <a name="configuring-the-sut-manually"></a>手动配置 SUT

我们强烈建议你使用 **MALT_SUT_Setup.bat** 来设置 MALT，以及 (SUT) 测试的系统。 以下有关手动设置 MALT 和 SUT 的说明仅用于透明度和传统用途。

1. 确保 SUT 的环境光线传感器 (ALS) 。 若要确定你的电脑是否有 ALS，请在 " **显示** 设置" 中的 " **亮度" 和 "颜色**" 下，查找 **"光线变化时自动更改亮度"** 复选框，然后选择它以使用此功能。
2. 请确保在测试过程中屏幕不会关闭。 若要在 Windows 10 中调整睡眠设置，请单击 "**开始**"，然后选择 "**设置**" "   >  **系统**  >  **电源 & 睡眠**"。 在 "**屏幕**" 下，更改 **电池电源，在接通电源后** 关闭，**并在****接通** 电源后关闭 **。**
3. 确保在测试过程中设备不会进入睡眠状态。 若要在 Windows 10 中调整睡眠设置，请单击 "**开始**"，然后选择 "**设置**" "   >  **系统**  >  **电源 & 睡眠**"。 在 **睡眠状态** 下 **，使用电池电量改变，pc 进入睡眠状态后进入睡眠状态** **，pc 进入睡眠状态后进入睡眠状态** **。** 
4. 若要减少测试可变性，请在测试之前将 SUT 的屏幕背景设置为纯白。 选择 " **设置" > 个性化 > "背景**"，然后将 "背景" 下拉列表更改为 **"纯色"**。 单击 " **自定义颜色 > 更多** "，并将 "十六进制值" 更改为 `FFFFFF` 。 这会将桌面背景更改为纯白。
5. 请确保在 SUT 上已打开该卷。 当长时间运行的测试完成时，应用程序将发出声音，通知您已完成。

## <a name="automatic-brightness-test-procedures"></a>自动亮度测试过程

### <a name="get-ambient-light-response-curve"></a>获取环境光线响应曲线

**(推荐使用 [SensorExplorer](testing-sensor-explorer.md) 应用)**

1. 打开 SensorExplorer，并单击左侧菜单栏中的 " **MALT** "。

    ![SensorExplorer MALT 页](images/SensorExplorerMALT.png)

2. 通过单击 "**传感器数据**  >  **获取环境亮度**" 来验证连接。 如果正确设置 MALT，则会显示正确的 lux 值;否则，请关闭应用程序，尝试重新上传 Arduino 程序并检查串行监视器。
3. 在 " **运行测试**" 下，单击 " **携带自动亮度曲线**"。
4. 选择保存 .csv 文件的位置。
5. 指定测试开始之前的等待时间。 这是为了让你有时间将传感器置于系统上。
6. 再. 此测试大约需要5-10 分钟。 测试将光源的亮度从0调整到其最大亮度，范围为大约0到2600的环境 lux。
7. 测试完成后，输出将自动保存到， `autoBrightness.csv` 然后播放一则声音，通知您测试已完成。

### <a name="using-maltutilexe"></a>使用 MALTUtil.exe

1. 通过从 cmd 运行来验证连接 `MALTUtil.exe /screenLux` 。 如果正确设置 MALT，则会显示正确的 lux 值，否则 cmd 将挂起或显示 `No Arduino devices connected to the system` 。
2. 在 SUT 上， `MALTUtil.exe /autoCurve 30` 在 cmd 中运行。 30是指在测试开始之前30秒的等待时间，这是为了让你有时间将传感器置于系统上。 如果需要更长的 (或更短的) ，以便在测试开始之前在安装中移动任何内容，请相应地调整此数字。
3. 再. 此测试大约需要5-10 分钟。 测试将光源的亮度从0调整到其最大亮度，范围为大约0到2600的环境 lux。
4. 测试完成后，输出将自动保存到， `autoBrightness.csv` 然后播放一则声音，通知您测试已完成。

### <a name="open-the-results-in-microsoft-excel"></a>在 Microsoft Excel 中打开结果

1. `autoBrightness.csv`在 Microsoft Excel 中打开。 本指南假定你使用的是 Microsoft Excel 2016。 如果你使用的是其他版本，则可能需要调整这些步骤。
2. 单击 "**文件**  >  **导出**  >  **更改文件类型**"。 将文件类型更改为 .xlsx。 这将允许您创建和保存数据的可视化效果。
3. 在文档中，将看到三列：

| 细级 | 环境 Lux  | 屏幕 Lux |
|-----|----|----|
| MALT 程序设置的最小光源级别 | MALT 环境光线传感器度量的最小环境 lux 值 | MALT 屏幕光线传感器度量的相应屏幕 lux 值 |
| MALT 程序设置的最大光源级别 | 由 MALT 环境光线传感器度量的最大环境 lux 值 | MALT 屏幕光线传感器度量的相应屏幕 lux 值 |

### <a name="visualize-the-results"></a>可视化结果

如果你使用的程序不是 Microsoft Excel 2016，这些步骤可能会有所不同。

1. 在 Microsoft Excel .xlsx 文件中，选择包含数据的两个列： "环境 Lux" 和 "Screen Lux"。
2. 单击 "**插入**  >  **(X、Y) 的插入散点图或气泡图**  >  **散点（带直线**）

![插入散点图](images/insertScatter1.png)

现在，您可以直观地表示由 MALT 度量的自动亮度响应曲线。

### <a name="interpret-the-results"></a>解释结果

您必须自行或您的工程团队负责自动亮度曲线手动检查结果。 以下是一些需要考虑的事项：

1. MALT 衡量的结果是否与 BIOS 中的环境光源响应曲线的预期定义匹配？
2. 环境光线响应曲线中是否有足够的步骤？ 当用户调整亮度时，具有几个点的曲线将对用户很明显。
3. 曲线的底部的步骤是否小于曲线的最低端？ 亮度变化更明显降低亮度。 请考虑在亮度百分比较低的情况下添加更频繁的曲线点。

请参阅 [此白皮书](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) ，了解有关如何集成光源传感器和环境光线响应曲线的 Microsoft 完整指导。
