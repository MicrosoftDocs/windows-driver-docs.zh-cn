---
title: 获取由 Microsoft 签名的适用于多个 Windows 版本的驱动程序
description: 如何获取由 Microsoft 签名的适用于多个版本的 Windows 的驱动程序
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 638af0b32bf4c3199f434f552b59b5086afcccf3
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682282"
---
# <a name="get-drivers-signed-by-microsoft-for-multiple-windows-versions"></a>获取由 Microsoft 签名的适用于多个 Windows 版本的驱动程序

## <a name="how-to-submit-to-the-dashboard"></a>如何提交到仪表板

本主题介绍如何将驱动程序等提交到仪表板，以及将它应用到多个版本的 Windows。 本主题还介绍如何在 Microsoft 对其进行签名后检索提交，以及如何验证 Microsoft 签名。

有两种方法可以将仪表板提交应用到 Windows 10 和较早版本的 Windows：

1. 使用 Hardware Lab Kit (HLK) 针对 Windows 10 测试你的提交，而使用硬件认证工具包 (HCK) 针对较早版本的 Windows 测试提交。 然后，创建一个包含所有[合并 HLK 测试结果](/windows-hardware/test/hlk/user/merge-packages)的仪表板提交。 在提交过程中，可以选择加入以获取适用于 Windows Vista 和 Windows XP 的免费签名，如本主题的后面部分所示。 若要选择加入 Windows Server 2008，请提供来自 [Windows Hardware Lab Kit (HLK)](/windows-hardware/test/hlk/index/) 提交的提交 ID。 这是使提交适用于所有 Windows 版本的唯一方法。
2. 作为 HLK 和 HCK 测试的替代方法，可以将驱动程序提交到仪表板以进行[证明签名](attestation-signing-a-kernel-driver-for-public-release.md)，以便它还可以在 Windows 10 上运行。 这个方法更复杂，但仍是一个有效选项。 有关如何对驱动程序进行证明签名的详细信息，请参阅[对内核驱动程序进行证明签名以便公开发布](attestation-signing-a-kernel-driver-for-public-release.md)。

本主题会提供有关用于上下文的仪表板的一些背景信息，然后演练使用 HLK/HCK 的过程。

在仪表板中，有两个与签名提交有相关的选项 – 你可以使用任一方法获取 Microsoft 签名的驱动程序。 硬件兼容性选项意味着你已走了额外的距离，并满足 [Windows 硬件兼容性计划](/windows-hardware/design/compatibility/index)要求。 这将给予你 Microsoft SmartScreen 附带的信誉、经认证的产品列表的可见性和其他业务好处。

对于背景，存在两种需要考虑的代码签名操作：

- 一种是将组织标识为仪表板的代码签名操作。 这是对你计划提交的程序包的签名，并且它是仪表板强加于合作伙伴的一项要求，以便仪表板可以阻止你组织以外的恶意用户使用你的凭据进行提交 - 这可能有损你的信誉！
- 另一个是 Microsoft 实际上对你提交的个别文件进行签名（例如，你的驱动程序）。

必须具有绑定到公司的 EV 证书才能访问仪表板中的提交功能。

若要在合作伙伴中心确认用于标识组织的证书，请参阅[更新代码签名证书](./update-a-code-signing-certificate.md)。

登录到合作伙伴中心并准备好对你的提交签名后，可以使用标准代码签名证书或 EV 代码签名证书。这适用于所有操作系统版本，不只适用于 Windows 10。

这是[策略的最新更改](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)。 如果你有绑定到你组织帐户的 EV 证书，可以放心开始安装 - 即，当你提交你的程序包时，可以继续使用标准 SHA-2 证书。

## <a name="how-to-submit-hlk-test-results"></a>如何提交 HLK 测试结果

下面介绍了如何将 HLK 测试结果提交到仪表板。 有单独的选项卡可供你查看已运行的测试和测试结果。 针对仪表板目的，HLK 项目最感兴趣的部分是“程序包”  选项卡：

![HLK 提交中“包”选项卡的屏幕截图，其中显示了驱动程序文件夹、符号文件夹、Signability、补充文件夹、目标和 OS 平台等。](images/hlkpackage.png)

选择项目的文件路径以打开它。 在此情况下，提交为一个驱动程序。

![类型为 .cat、.inf、 .sys、.cpf 和 .spf 的八个文件的屏幕截图。](images/capture.png)

假设你想要从头开始创建提交程序包 在 HLK 中，选择“添加驱动程序文件夹”。

![HLK UI 中的“添加驱动程序文件夹”按钮的屏幕截图](images/adddriverfolder.png)

现在是你对你的提交所支持的操作系统版本进行声明的第一次机会。 在此情况下，该提交经测试适用于 Windows 10 x64 和较早版本的 Windows 。

![在“驱动程序属性”的“产品”选项卡上，显示所选 OS 的多个版本（Windows v10.0 x64、Windows 7 客户端 x64、Windows 7 客户端 x32 等）的屏幕截图](images/osqualifications.png)

还需要针对区域设置进行声明。 例如，视你驱动程序的设计和架构而定，可以选择以不同的区域设置显示不同的字符串。 在这种情况下，实际上你可能有适用于不同区域设置的不同已编译的二进制文件。 因此，对于一台设备，你可能准备了一百个不同的驱动程序；每个区域设置一个驱动程序。

![在“驱动程序属性”的“区域设置”选项卡上，选择了多种语言以及“区域设置”](images/locales.png)

若要添加符号，选择并按住（或右键单击）该驱动程序文件夹。

![从驱动程序文件夹启动一个菜单，其中包含添加驱动程序、删除驱动程序、替换驱动程序、添加符号、删除符号和 Signability 结果的命令。](images/addsymbols.png)

选择“添加补充文件夹”以提交对该提交非常重要的其他文件，但这些文件实际上并不是提交本身的组成部分。 你可以将任何所需的内容添加到程序包。 你可以使用此方法来将对提交非常重要的其他项目提交到仪表板，例如用于驱动程序提交的自述文件。

![屏幕截图的一部分，其中显示补充文件夹下的部分文件路径](images/addsupplementalfolder.png)

在你准备好后，选择“创建程序包”。

![屏幕截图显示在 HLK 提交中，屏幕右下方有一个“创建包”按钮](images/createpackage.png)

下一步是指定你将用于签名程序包的证书 - 这是本主题开头部分所介绍的两种代码签名操作中的第一个。 可以选择“使用证书文件”来指定存储在诸如 USB 驱动器等设备上的证书，或者选择“使用证书存储”来指定已导入本地计算机的证书存储的证书。

![包含三个选项的对话框：1) 不签名；2) 使用证书存储；3) 使用证书文件](images/usecertstore.png)

在选择“确定”后，命名该程序包即会创建它并进行签名（假定你在要用于提交的计算机上已安装了证书），然后你将收获友好的成功消息。

同时程序包在“Signability”  下标有绿色复选标记：

![在 HLK 的“包”选项卡的 Signability 列中显示绿色复选标记的 UI](images/signability.png)

接下来的步骤将在合作伙伴中心仪表板中进行。 登录并按照[创建新硬件提交](create-a-new-hardware-submission.md)中的说明上传 HLK 程序包。

## <a name="how-to-retrieve-a-submission-after-microsoft-signs-it"></a>如何检索 Microsoft 已签名的提交

对于已提交到合作伙伴中心的 HLK 或 HCK 提交，请执行以下操作：

- [查找硬件提交](manage-your-hardware-submissions.md)，该提交中包含要为其下载签名文件的驱动程序。 选择 ID 打开驱动程序详细信息。 在该页面上，展开包含要下载的驱动程序的程序包的“程序包”选项卡，然后选择“下载已签名文件”。

对于已提交到硬件开发人员中心 (Sysdev) 的 WLK 提交、系统提交或证明签名的驱动程序：

- 依次选择“硬件兼容性”  &gt;“管理提交”  &gt;。在“摘要和任务”  选项卡上，如果状态为“已批准”  ，则表示提交可供检索。 在屏幕右下角的“下载”下，选择“已签名的驱动程序包”。 Microsoft 将流式传输内存中包含已签名提交的 zip 文件。

提交文件夹内将是程序包文件。 这些文件都由 Microsoft 进行签名。 合作伙伴无需对返回的负载进行签名。 Microsoft 始终返回内含已批准提交的 .cat 文件。 如果合作伙伴包含自己的 .cat 文件。 Microsoft 将丢弃它，并返回自己已签名的 .cat 文件。

过去，Microsoft 仅签名 .cat 文件。 从 Windows 10 开始，Microsoft 现在对返回负载中的所有可移植可执行文件进行签名。 例如，.dll 文件同样由 Microsoft 进行签名：

![文件夹的视图，其中显示了十三个文件，其中几个文件的图标表明它们已签名](images/filessignedbymicrosoft.png)

## <a name="how-to-validate-the-microsoft-signature"></a>如何验证 Microsoft 签名

在两种情况下，你可能希望验证提交的 Microsoft 签名。

1. 不确定驱动程序是否已由 Microsoft 进行签名，并且你想要检查。
2. 有两个驱动程序，并且需要确定哪一个经由证明签名，哪一个是在向仪表板提交 HLK/HCK 结果后签名的。

可以通过检查 Microsoft 签名提交所用证书的增强型密钥用法 (EKU) 来验证 Microsoft 签名。 若要检查 EKU，选择并按住（或右键单击）.cat 文件并选择“属性”。 依次选择“数字签名”选项卡、该证书的名称，然后选择“详细信息”。

![已选中“详细信息”选项卡和“增强型密钥使用”的“证书”对话框的屏幕截图。 下面的窗格显示有关代码签名、Windows 硬件驱动程序验证和 Windows 硬件驱动程序证明验证的信息](images/ekudetails.png)

在证书“详细信息”选项卡上，选择“增强型密钥用法”。 你将在该处看到 EKU 和证书的相应 OID 值。 在此情况下，“Windows 硬件驱动程序验证 OID”  以 5 结尾，这意味着驱动程序未由证明进行签名：

![“证书”对话框的屏幕截图，其中“增强型密钥使用”显示值“Windows 硬件驱动程序验证(1.3.6.1.4.1.311.10.3.5)” ](images/certified.png)

如果驱动程序已由证明签名，那么 OID 将以 1 结尾：

![“证书”对话框的屏幕截图，其中“增强型密钥使用”显示值“Windows 硬件驱动程序验证(1.3.6.1.4.1.311.10.3.1)”](images/attested.png)

## <a name="related-topics"></a>相关主题

- [创建新的硬件提交](create-a-new-hardware-submission.md)

- [在合作伙伴中心内管理硬件提交](manage-your-hardware-submissions.md)

- [驱动程序外部测试](driver-flighting.md)
