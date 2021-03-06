---
title: PKEY \_ FX \_ ModeEffectClsid
description: 在 Windows 8.1 和更高版本中，PKEY \_ FX \_ ModeEffectClsid 属性键标识驱动程序支持的模式效果 (MFX) 。 驱动程序开发人员应指定其驱动程序支持的处理模式的列表。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 906457703bcf943a3160fe64daebc0f4abe72784
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800875"
---
# <a name="pkey_fx_modeeffectclsid"></a>PKEY \_ FX \_ ModeEffectClsid


在 Windows 8.1 和更高版本中， **PKEY \_ FX \_ ModeEffectClsid** 属性键标识驱动程序支持的模式效果 (MFX) 。 驱动程序开发人员应指定其驱动程序支持的处理模式的列表。

INF 文件属性键指示音频终结点生成器将终结点的 Clsid 设置到效果属性存储中。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定该设备的 "添加注册表" 部分中音频模式效果的设置。 以下 INF 示例显示了用于将模式效果的 APO 加载到注册表中的字符串和添加注册表部分。

```inf
[Strings]
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






