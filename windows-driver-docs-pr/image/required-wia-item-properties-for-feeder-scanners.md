---
title: 送纸器扫描仪的必需 WIA 项属性
description: 送纸器扫描仪的必需 WIA 项属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d757935d58b34b2184174b889658a1f6bf3b6a6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814442"
---
# <a name="required-wia-item-properties-for-feeder-scanners"></a>送纸器扫描仪的必需 WIA 项属性





支持以下 WIA 属性需要 WIA 进纸器扫描器项：

[**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](./wia-dps-document-handling-select.md)

[**WIA \_ DPS \_ 页面 \_ 大小**](./wia-dps-page-size.md)

[**WIA \_ IPA \_ 访问 \_ 权限**](./wia-ipa-access-rights.md)

[**WIA \_ \_ \_ 每通道 IPA 位数 \_**](./wia-ipa-bits-per-channel.md)

[**WIA \_ IPA \_ 项 \_ 类别**](./wia-ipa-item-category.md)

[**WIA \_ IPA \_ \_ 每像素通道数 \_**](./wia-ipa-channels-per-pixel.md)

[**WIA \_ IPA \_ 压缩**](./wia-ipa-compression.md)

[**WIA \_ IPA \_ 数据类型**](./wia-ipa-datatype.md)

[**WIA \_ IPA \_ 深度**](./wia-ipa-depth.md)

[**WIA \_ IPA \_ 格式**](./wia-ipa-format.md)

[**WIA \_ IPA \_ 完整 \_ 项 \_ 名称**](./wia-ipa-full-item-name.md)

[**WIA \_ IPA \_ 项 \_ 名称**](./wia-ipa-item-name.md)

[**WIA \_ IPA \_ 项 \_ 大小**](./wia-ipa-item-size.md)

[**WIA \_ IPA \_ 首选 \_ 格式**](./wia-ipa-preferred-format.md)

[**WIA \_ IPA \_ TYMED**](./wia-ipa-tymed.md)

[**WIA \_ IPS \_ 亮度**](./wia-ips-brightness.md)

[**WIA \_ IP \_ 对比**](./wia-ips-contrast.md)

[**WIA \_ IP \_ 当前 \_ 意向**](./wia-ips-cur-intent.md)

[**WIA \_ IPS \_ 最大 \_ 水平 \_ 大小**](./wia-ips-max-horizontal-size.md)

[**WIA \_ IPS \_ 最大 \_ 垂直 \_ 大小**](./wia-ips-max-vertical-size.md)

[**WIA \_ IPS \_ 最小 \_ 水平 \_ 大小**](./wia-ips-min-horizontal-size.md)

[**WIA \_ IPS \_ 最小 \_ 垂直 \_ 大小**](./wia-ips-min-vertical-size.md)

[**WIA \_ IP \_ 光纤 \_ XRES**](./wia-ips-optical-xres.md)

[**WIA \_ IP \_ 光纤 \_ YRES**](./wia-ips-optical-yres.md)

[**WIA \_ IP \_ 页面**](./wia-ips-pages.md)

[**WIA \_ IP \_ 页面 \_ 高度**](./wia-ips-page-height.md)

[**WIA \_ IP \_ 页面 \_ 宽度**](./wia-ips-page-width.md)

[**WIA \_ IP \_ PHOTOMETRIC \_ INTERP**](./wia-ips-photometric-interp.md)

[**WIA \_ IP \_ XEXTENT**](./wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](./wia-ips-xpos.md)

[**WIA \_ IP \_ XRES**](./wia-ips-xres.md)

[**WIA \_ IP \_ YEXTENT**](./wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](./wia-ips-ypos.md)

[**WIA \_ IP \_ YRES**](./wia-ips-yres.md)

**注意**   如果支持 WiaImgFmt raw 格式，则需要 " [**WIA \_ IPA \_ raw \_ BITS \_ PER \_ 通道**](./wia-ipa-raw-bits-per-channel.md) " 属性 \_ 。 [**WIA \_ IPA \_ format**](./wia-ipa-format.md)属性必须支持 WiaImgFmt \_ BMP 格式。 如果 [**wia \_ IPA \_ DEPTH**](./wia-ipa-depth.md)属性设置为1位/像素 (BPP) 或 [**wia \_ IPA \_ DATATYPE**](./wia-ipa-datatype.md)属性设置为 wia 数据阈值，则需要 [**wia \_ ip \_ 阈值**](./wia-ips-threshold.md)属性 \_ \_ 。

 

 

