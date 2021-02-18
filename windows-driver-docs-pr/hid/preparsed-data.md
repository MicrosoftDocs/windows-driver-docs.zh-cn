---
title: 预分析的数据
description: 预分析的数据
keywords:
- 分析的数据 WDK HID
- preparsed 数据 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de916ddb33927520fd334fa3caf590f9612d8ed6
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648150"
---
# <a name="preparsed-data"></a>预分析的数据





*Preparsed 数据* 是与 [顶级集合](top-level-collections.md)关联的报表描述符数据。 用户模式应用程序或内核模式驱动程序使用 preparsed 数据提取有关特定 HID 控件的信息，而无需获取和解释设备的整个报表描述符。 用户模式应用程序使用 [**HidD \_ GetPreparsedData**](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata) 获取集合的 preparsed 数据，并且内核模式驱动程序使用 [**IOCTL \_ HID \_ 获取 \_ 集合 \_ 描述符**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor) 请求。

以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid) 支持提取和设置按钮和值数据：

[**HidP \_ GetButtons**](/windows-hardware/drivers/ddi/hidpi/#functionsfunctions)

[**HidP \_ SetButtons**](/windows-hardware/drivers/ddi/hidpi/#functionsfunctions)

[**HidP \_ UnsetButtons**](/windows-hardware/drivers/ddi/hidpi/#functionsfunctions)

[**HidP \_ GetUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)

[**HidP \_ SetUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)

[**HidP \_ GetScaledUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)

[**HidP \_ SetScaledUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)

[**HidP \_ GetUsageValueArray**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)

[**HidP \_ SetUsageValueArray**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)

