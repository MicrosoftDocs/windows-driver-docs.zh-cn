---
title: 创建新硬件提交
description: 创建新硬件提交
ms.date: 04/20/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 43b15750ec9004ee294baf5913b4768b069af5ad
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682274"
---
# <a name="create-a-new-hardware-submission"></a>创建新硬件提交

若要为 Windows 10 的 Windows 硬件兼容性计划（或适用于以前操作系统的单独认证计划）准备硬件，必须创建并提交 **.hlkx** 文件（适用于 Windows 10）或 **.hckx** 文件（适用于以前操作系统）。 此文件使用 Windows HLK Studio（或适用于以前操作系统的 Windows HCK Studio）进行创建，它包含你的产品的所有测试结果、驱动程序和符号。 提交此文件后，将能够通过仪表板查看你的测试结果，评估测试的任何驱动程序并返回 Microsoft 进行数字签名的目录文件。

## <a name="to-create-a-submission-file"></a>创建提交文件

有关创建 **.hlkx** 文件并对其进行数字签名的信息，请参阅 [Windows HLK 入门指南](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

有关创建 **.hckx** 文件并对其进行数字签名的信息，请参阅 [Windows HCK 入门指南](/previous-versions/windows/hardware/hck/jj123537(v=vs.85))。

## <a name="to-submit-a-file"></a>提交文件

1. 登录到合作伙伴中心，然后选择“提交新硬件”  。 这将加载提交创建向导。

2. 在“程序包和签名属性”  部分，为你的驱动程序提交选择一个名称。 该名称可用于搜索和组织你的驱动程序提交。 注意：如果与其他公司共享你的驱动程序，他们会看到该名称。

3. 拖放或浏览到想要提交的 **.hlkx/.hckx** 文件。 将开始上传该文件。
   ![显示驱动程序名称字段的屏幕截图](images/drivers-name.png)

4. 此时，提交门户将确定要提交的产品类型。 然后，在“提交”页上，门户会显示为 Windows Server 认证提交的产品可能需要的任何调查表。 对于提交用于 Windows Server 认证或签名的所有产品，如果提交门户提供调查表，则必须完成调查表。 除非完成调查表，否则提交将不会完成。

5. 如果希望在发布之前测试驱动程序，可以选中标记为“对 Win10 及更高版本执行测试签名”或“对 Win10 以下版本（旧版）的 OS 执行测试签名”的复选框。 测试签名驱动程序类似于为公开版本签名的驱动程序，但不需要 HLK 测试。 它们还没有通过 Windows 更新分发，但可以从硬件提交站点下载。 可以仅在测试计算机上安装它们。 有关对驱动程序包进行测试签名的详细信息，请参阅 [WHQL 测试签名计划](../install/whql-test-signature-program.md)以及[如何对驱动程序包进行测试签名](../install/how-to-test-sign-a-driver-package.md)。

7. 选择“请求签名”（如果适用）。 此选项允许你指定驱动程序应包含哪些操作系统签名（包括允许的下层操作系统）。 可用认证会因驱动程序提交程序包而有所不同，因此可能不会列出任何认证。 **注意** 若要对单个体系结构的驱动程序包进行签名，请仅将该体系结构的日志包括在内。 例如，若仅对 x64 进行签名，请仅提交 x64 日志。

   ![显示了驱动程序提交的可能认证和“完成”按钮的屏幕截图](images/additionalcertifications.png)

8. 在“认证”  部分，填写以下信息：

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>字段</th>
   <th>说明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="even">
   <td><p>设备类型</p></td>
   <td><p>指示你的设备是否是：</p>
   <ul>
   <li><p>内部组件，如果你的设备属于系统的一部分并连接到电脑内。</p></li>
   <li><p>外部组件，如果你的设备是连接到电脑的外部设备（外设）。</p></li>
   <li><p>两者，如果你的设备同时可以内部（在电脑内）和外部（外设）连接。</p></li>
   </ul></td>
   </tr>
   <tr class="odd">
   <td><p>设备元数据类别</p></td>
   <td><p>基于设备类别从默认图标列表中为你的设备选择图标。 这确定哪个图标显示在“设备和打印机”中。 如果你的设备不应出现，请选择“内部设备”。</p>
   <p>有关使用 Windows Device Stage 提供丰富体验的信息，请参阅<a href="/windows-hardware/drivers/dashboard/" data-raw-source="[Device Metadata](./index.yml)">设备元数据</a>。</p></td>
   </tr>
   <tr class="even">
   <td><p>设备元数据型号 ID</p></td>
   <td><p>这些 GUID 用于向传统 Sysdev 仪表板验证设备元数据提交。 如果提供，它们必须匹配设备元数据包中的型号 ID。</p></td>
   </tr>
   <tr class="odd">
   <td><p>公布日期</p></td>
   <td><p>输入想要将你的产品包含在 Windows Server 目录、Windows 认证产品列表和通用驱动程序列表中的日期。</p></td>
   </tr>
   <tr class="even">
   <td><p>市场营销名称</p></td>
   <td><p>输入提交的市场营销名称。 市场营销名称允许你为产品提供别名。 你可以提供多个所需名称。</p></td>
   </tr>
   </tbody>
   </table>

   ![显示认证部分的屏幕截图](images/drivers-certification.png)

9. 选择“提交”。 

10. “分发”  部分用于将驱动程序发布到 Windows 更新。 有关如何使用 **分发** 部分的信息，请参阅 [使用发货标签管理驱动程序分发](manage-driver-distribution-by-submission.md)。

11. 可以通过页面顶部的进度跟踪器监视提交的进度。 所有步骤都显示绿色打勾标记后，表示提交已完成，你的组织会在仪表板标头中收到通知。

    ![显示进度跟踪器的屏幕截图](images/drivers-allgreen-new.png)

12. 查看结果。 如果提交失败，请进行任何必要的更改，然后重新提交。

## <a name="related-topics"></a>相关主题

* [在合作伙伴中心管理硬件提交](manage-your-hardware-submissions.md)
* [获取由 Microsoft 签名的适用于多个 Windows 版本的驱动程序](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
* [驱动程序外部测试](driver-flighting.md)
