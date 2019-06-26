---
title: DEVPKEY_NAME（设备安装程序类）
description: DEVPKEY_NAME（设备安装程序类）
ms.assetid: cc953918-f11a-464c-95cc-ee2a9aa68b7a
keywords:
- DEVPKEY_NAME （设备安装程序类） 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Setup Class)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3939d28abf4ae90921e48c724f29200e739b1d3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327498"
---
# <a name="devpkeyname-device-setup-class"></a>DEVPKEY_NAME（设备安装程序类）


DEVPKEY_NAME 设备属性表示的名称[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_NAME</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以使用 DEVPKEY_NAME 的值来标识设备安装程序类中，以便在用户界面项中的最终用户。

如果设置 DEVPKEY_DeviceClass_Name，DEVPKEY_NAME 的值是相同的值[ **DEVPKEY_DeviceClass_Name** ](devpkey-deviceclass-name.md)设备属性。 否则，DEVPKEY_NAME 值是相同的值[ **DEVPKEY_DeviceClass_ClassName** ](devpkey-deviceclass-classname.md)设备属性。

您可以调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)或[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)检索设备 DEVPKEY_NAME 的值安装程序类。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持相应的 name 属性。 但是，这些早期版本的 Windows 支持与 DEVPKEY_DeviceClass_Name 和 DEVPKEY_DeviceClass_ClassName 相对应的属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPKEY_DeviceClass_ClassName**](devpkey-deviceclass-classname.md)

[**DEVPKEY_DeviceClass_Name**](devpkey-deviceclass-name.md)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiGetClassDescription**](https://msdn.microsoft.com/library/windows/hardware/ff551053)

[**SetupDiClassNameFromGuid**](https://msdn.microsoft.com/library/windows/hardware/ff550947)

 

 





