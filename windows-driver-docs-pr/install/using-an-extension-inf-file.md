---
title: 使用扩展 INF 文件
description: 从 Windows 10 开始，可以通过提供名为扩展 INF 的其他 INF 文件来扩展驱动程序包 INF 文件的功能。
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dcbf99d79860a24f0e777b7f1c6fedca0cdc723
ms.sourcegitcommit: 011e8218c9e9a253558d27e2b4de75e46011d814
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/11/2021
ms.locfileid: "103087134"
---
# <a name="using-an-extension-inf-file"></a>使用扩展 INF 文件

在 Windows 10 之前，Windows 选择了要为给定设备安装的单个驱动程序包。  这会生成大量复杂的驱动程序包，其中包括所有方案和配置的代码，每次更新需要更新整个驱动程序包。  从 Windows 10 开始，你可以将 INF 功能拆分为多个组件，每个组件都可以单独进行维护。

若要扩展驱动程序包 INF 文件的功能，请在单独的驱动程序包中提供扩展 INF。  扩展 INF：

* 可由不同的公司提供，并独立于基本 INF 进行更新。
* 看起来与基本 INF 相同，但可以扩展用于自定义或专用化的基本 INF。
* 增强设备的值，但基本驱动程序无法正常运行。
* 必须是 [通用 INF 文件](../install/using-a-universal-inf-file.md)。

每个设备都必须有一个基本 INF，还可以选择将一个或多个扩展 Inf 与其关联。

可以使用扩展 INF 的典型方案包括：

* 修改基本 INF 中提供的设置，例如自定义设备友好名称或修改硬件配置设置。
* 通过指定 [INF AddComponent 指令](inf-addcomponent-directive.md) 并提供 [组件 INF 文件](using-a-component-inf-file.md)来创建一个或多个软件组件。

可以在下面的示例中查找这些方案的示例代码。  另请参阅 [DCH 兼容驱动程序包示例](../develop/dch-example.md)，其中介绍了 [DCHU 通用驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU) 如何使用 extension inf。

在下图中，两个不同的公司为同一设备创建了单独的驱动程序包，它们显示在点线中。  第一个仅包含扩展 INF，第二个包含组件 INF 和旧软件模块。  该图还显示了扩展 INF 如何引用组件 INF，后者又可以引用要安装的软件模块。

![扩展和组件 INF 层次结构](images/extension-component-inf-hierarchy.png)

## <a name="how-extension-inf-and-base-inf-work-together"></a>扩展 INF 和基本 INF 如何协同工作

扩展 INF 中的设置在基础 INF 中的设置后应用。 因此，如果扩展 INF 和基本 INF 指定了相同的设置，则会应用扩展 INF 中的版本。 同样，如果基本 INF 发生更改，扩展 INF 仍保留，并应用于新的基本 INF。

在描述哪些项可以重写，以及适用的参数值范围和约束的基本 INF 中包含注释很有用。

## <a name="specifying-extensionid"></a>指定 ExtensionId

编写扩展 INF 时，会生成一个名为 " **ExtensionId**" 的特殊 GUID，它是 INF 的 " **\[ 版本 \]** " 部分中的条目。

系统通过将设备的硬件 ID 和兼容 Id 与适用于该系统的 " [**模型**](inf-models-section.md) " 部分的扩展 INF 中指定的 id 相匹配，来标识特定设备可能的扩展 inf。

在指定相同 **ExtensionId** 值的所有可能的扩展 inf 中，系统仅选择一个安装，并将其设置应用于基本 INF 的设置。  按照该顺序使用在 INF 中指定的驱动程序日期和驱动程序版本来选择具有相同 **ExtensionId** 的多个扩展 inf 之间的单个 INF。

为了说明这一点，请考虑以下方案，其中包含一个假设设备，其中有三个扩展 Inf：

![显示如何选择基本 INF 和扩展 Inf 的关系图](images/extension-base-inf-example.png)

**ExtensionId** 值 `{A}` 、 `{B}` 和 `{C}` 显示在大括号中，每个驱动程序的 [排名](how-setup-ranks-drivers--windows-vista-and-later-.md)显示在横幅功能区中。

首先，系统选择具有最新版本和最高级别的驱动程序。

接下来，系统处理可用的扩展 Inf。  两个具有 **ExtensionId** 值 `{B}` ，一个具有 **ExtensionId** 值 `{A}` 。  在前两个中，假设驱动程序日期相同。  下一个 tiebreaker 是驱动程序版本，因此系统将选择带有 v2.0 的扩展 INF。

同时选择具有唯一 **ExtensionId** 值的扩展 INF。  系统会应用设备的基本 INF，然后应用该设备的两个扩展 Inf。

请注意，在基本 INF 之后始终应用扩展 INF 文件，但不会确定扩展 inf 的应用顺序。

## <a name="creating-an-extension-inf"></a>创建扩展 INF

以下是将 INF 定义为扩展 INF 所需的项。

1.  在 "[**版本**](inf-version-section.md)" 部分中指定 **类** 和 **ClassGuid** 的这些值。 有关安装程序类的详细信息，请参阅 [供应商可用的系统定义的设备安装程序类](./system-defined-device-setup-classes-available-to-vendors.md)。

    ```cpp
    [Version]
    ...
    Class       = Extension
    ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
    ```

2.  提供 " [**\[ \] 版本**](inf-version-section.md)" 部分中的 **ExtensionId** 条目。 为扩展 INF 的初始版本生成新的 GUID，或重复使用最后一个 GUID 对初始扩展 INF 进行后续更新。

    ```cpp
    ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
    ```

请注意，组织可能仅使用其拥有的 **ExtensionID** 。  有关注册扩展 ID 的信息，请参阅 [Windows 硬件开发人员中心仪表板中的管理硬件提交](../dashboard/manage-your-hardware-submissions.md)。     

3.  如果要更新扩展 INF，请将 **ExtensionId** 保留不变，并递增 (或 [**) 的版本**](inf-driverver-directive.md) 或日期，或同时指定这两个。 对于给定的 **ExtensionId** 值，PnP 选择具有最高 **DriverVer** 的 INF。

>[!NOTE]
> 如果扩展 INF 面向 Windows 10 S，请参阅 [S 模式下的 windows 10 驱动程序要求](./windows10sdriverrequirements.md) ，了解有关该版本 Windows 的驱动程序安装的信息。

4.  在 " [**INF 模型" 部分**](inf-models-section.md)中，指定与目标设备的一个或多个硬件和兼容 id。  请注意，这些硬件和兼容的 Id 不需要与基本 INF 的 Id 匹配。  通常，扩展 INF 会列出比基本 INF 更具体的硬件 ID，目的是进一步专用化特定的驱动程序配置。  例如，基本 INF 可能使用由两部分组成的 PCI 硬件 ID，而扩展 INF 指定由四个部分组成的 PCI 硬件 ID，如下所示：
    
    ```cpp
    [DeviceExtensions.NTamd64]
    %Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX
    ```

    或者，扩展 INF 可能会列出与基本 INF 相同的硬件 ID，例如，如果设备的目标非常窄，或者基本 INF 已列出最具体的硬件 ID。
    
    在某些情况下，扩展 INF 可能提供不太具体的设备 ID （例如兼容的 ID），以便在更广泛的设备集中自定义设置。

    如果由四个部分组成的硬件 ID 是不可能的，或者没有足够的限制，则可以使用[子目标](../bringup/target-a-system-using-chid.md)。

5.  不要使用定义服务 `SPSVCINST_ASSOCSERVICE` 。  但是，扩展 INF 可以定义其他服务，例如设备的筛选器驱动程序。  有关指定服务的详细信息，请参阅 [**INF AddService 指令**](inf-addservice-directive.md)。

在大多数情况下，你将扩展 INF 包分别从基础驱动程序包提交到硬件开发人员中心。  有关如何打包 extension Inf 以及指向示例代码的链接的示例，请参阅 [DCH 兼容驱动程序包示例](../develop/dch-example.md)。

对于常规 Inf，对于扩展 Inf，驱动程序验证和提交过程是相同的。 有关详细信息，请参阅 [WINDOWS HLK 入门](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

## <a name="uninstalling-an-extension-driver"></a>卸载扩展驱动程序

若要卸载扩展驱动程序，请使用 `delete-driver` 带有标志的 PnPUtil 命令 `uninstall` 。 这允许在不删除基础驱动程序的情况下卸载扩展驱动程序。

查找要卸载和使用的驱动程序包的 oem< # > `pnputil /delete-driver oem<#>.inf /uninstall` 名称。 

`pnputil /enum-drivers` 可用于帮助识别相应的 oem< # > .inf 名称。

## <a name="example-1-using-an-extension-inf-to-set-the-device-friendly-name"></a>示例1：使用扩展 INF 设置设备友好名称

在常见方案中，设备制造商 (IHV) 提供基础驱动程序和基本 INF，然后系统构建商 (OEM) 提供一个扩展 INF，在某些情况下会替代基本 INF 的配置和设置。  以下代码片段是一个完整的扩展 INF，演示如何设置设备友好名称。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = %CONTOSO%
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
DriverVer   = 05/28/2013,1.0.0.0
CatalogFile = delta.cat

[Manufacturer]
%CONTOSO% = DeviceExtensions,NTamd64

[DeviceExtensions.NTamd64]
%Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX

[DeviceExtension_Install]
; No changes

[DeviceExtension_Install.HW]
AddReg = FriendlyName_AddReg

[FriendlyName_AddReg]
HKR,,FriendlyName,, "New Device Friendly Name"

[Strings]
CONTOSO              = "Contoso"
Device.ExtensionDesc = "Sample Device Extension"
```

## <a name="example-2-using-an-extension-inf-to-install-additional-software"></a>示例2：使用扩展 INF 安装其他软件

以下代码片段是 [适用于通用驱动程序的驱动程序包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)中包含的完整扩展 INF。  此示例使用 [INF AddComponent 指令](inf-addcomponent-directive.md) 创建用于安装服务和可执行文件的组件。  有关组件 INF 中可执行的操作的详细信息，请参阅 [使用组件 Inf 文件](using-a-component-inf-file.md)。

若要联机访问此文件，请参阅 [`osrfx2_DCHU_extension.inx`](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx) 。

```cpp
;/*++
;
;Copyright (c) Microsoft Corporation.  All rights reserved.
;
;   THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY
;   KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
;   IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR
;   PURPOSE.
;
;Module Name:
;
;    osrfx2_DCHU_extension.INF
;
;Abstract:
;
;    Extension inf for the OSR FX2 Learning Kit
;
;--*/

[Version]
Signature = "$WINDOWS NT$"
Class = Extension
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider = %ManufacturerName%
ExtensionId = {3846ad8c-dd27-433d-ab89-453654cd542a}
CatalogFile = osrfx2_DCHU_extension.cat
DriverVer = 05/16/2017,15.14.36.721

[Manufacturer]
%ManufacturerName% = OsrFx2Extension, NT$ARCH$

[OsrFx2Extension.NT$ARCH$]
%OsrFx2.ExtensionDesc% = OsrFx2Extension_Install, USB\Vid_045e&Pid_94aa&mi_00
%OsrFx2.ExtensionDesc% = OsrFx2Extension_Install, USB\Vid_0547&PID_1002

[OsrFx2Extension_Install.NT]
CopyInf=osrfx2_DCHU_usersvc.inf

[OsrFx2Extension_Install.NT.HW]
AddReg = OsrFx2Extension_AddReg
AddReg = OsrFx2Extension_COMAddReg

[OsrFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86"

; Add all registry keys to successfully register the
; In-Process ATL COM Server MSFT Sample.
[OsrFx2Extension_COMAddReg]
HKCR,AppID\ATLDllCOMServer.DLL,AppID,,"{9DD18FED-55F6-4741-AF25-798B90C4AED5}"
HKCR,AppID\{9DD18FED-55F6-4741-AF25-798B90C4AED5},,,"ATLDllCOMServer"
HKCR,ATLDllCOMServer.SimpleObject,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,ATLDllCOMServer.SimpleObject\CurVer,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,ATLDllCOMServer.SimpleObject.1,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject.1\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084},,,"SimpleObject Class"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,,%REG_EXPAND_SZ%,"%%SystemRoot%%\System32\ATLDllCOMServer.dll"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,ThreadingModel,,"Apartment"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\ProgID,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\Programmable,,%FLG_ADDREG_KEYONLY%
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\TypeLib,,,"{9B23EFED-A0C1-46B6-A903-218206447F3E}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\VersionIndependentProgID,,,"ATLDllCOMServer.SimpleObject"

[OsrFx2Extension_Install.NT.Components]
AddComponent = osrfx2_DCHU_component,,OsrFx2Extension_ComponentInstall
AddComponent = osrfx2_DCHU_usersvc,,OsrFx2Extension_ComponentInstall_UserSvc

[OsrFx2Extension_ComponentInstall]
ComponentIds=VID_045e&PID_94ab

[OsrFx2Extension_ComponentInstall_UserSvc]
ComponentIds=VID_045e&PID_94ac

[Strings]
ManufacturerName = "Contoso"
OsrFx2.ExtensionDesc = "OsrFx2 DCHU Device Extension"
REG_EXPAND_SZ = 0x00020000
FLG_ADDREG_KEYONLY = 0x00000010
```
有关如何使用扩展 INF 安装筛选器驱动程序的信息，请参阅 [设备筛选器驱动程序顺序](../develop/device-filter-driver-ordering.md)。

若要改善扩展性，建议使用 IHV 将可选功能置于 [扩展 INF 模板](using-an-extension-inf-file-template.md)中。

## <a name="backward-compatibility"></a>向后兼容性

对基本 INF 所做的任何更改都必须经过全面测试，以确保它不会中断现有扩展 Inf 的向后兼容性。

管理基本 INF 时，请遵循以下最佳做法：

* 文档参数值范围和约束都在代码注释和设计文档中。 将来的更改必须符合指定的范围。
* 若要支持新范围，请添加一个可选参数， () 没有默认值。

如果 IHV 将所有功能放在基本 INF 中，则可以通过以下方法确保现有扩展 Inf 继续工作：

1. IHV 提供一个助理应用，用于设置一个注册表标志，默认情况下禁用可选功能。
2. 基本驱动程序在使用可选功能之前检查是否已启用标志。
3. OEM 提供的扩展 INF 可通过将标志设置为启用来选择加入。

##  <a name="submitting-an-extension-inf-for-certification"></a>提交用于认证的扩展 INF

有关如何在硬件开发人员中心使用扩展 Inf 的详细信息，请参阅 [Windows 硬件开发人员中心仪表板中的使用扩展 inf](../dashboard/submit-dashboard-extension-inf-files.md)。

## <a name="related-topics"></a>相关主题

* [在合作伙伴中心使用扩展 INF](../dashboard/submit-dashboard-extension-inf-files.md)
* [符合 DCH 的驱动程序包示例](../develop/dch-example.md)
* [Using a Universal INF File](using-a-universal-inf-file.md)（使用通用 INF 文件）
* [Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)
* [适用于通用驱动程序的驱动程序包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)
