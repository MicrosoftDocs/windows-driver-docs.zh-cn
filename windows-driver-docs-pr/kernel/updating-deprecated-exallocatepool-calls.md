---
title: 将对已弃用的 ExAllocatePool 调用更新为 ExAllocatePool2 和 ExAllocatePool3
description: 了解如何更新对 ExAllocatePool2 和 ExAllocatePool3 的不推荐使用的 ExAllocatePool 调用
keywords:
- 内存管理 WDK 内核，系统分配的空间
- 系统分配的空间 WDK 内核
- 分配系统空间内存
- 分配 i/o 缓冲区内存
- ExAllocatePool3
- ExAllocatePool2
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: f76e7a35e94613469cbc18694270077739ad1e52
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648126"
---
# <a name="updating-deprecated-exallocatepool-calls-to-exallocatepool2-and-exallocatepool3"></a>将对已弃用的 ExAllocatePool 调用更新为 ExAllocatePool2 和 ExAllocatePool3

从 Windows 10 版本2004开始，不推荐使用以下 DDIs，因此应将其替换为本主题中所述。

[ExAllocatePool](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)

[ExAllocatePoolWithTag](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[ExAllocatePoolWithQuota](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)

[ExAllocatePoolWithQuotaTag](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[ExAllocatePoolWithTagPriority](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)

## <a name="driver-updates-for-versions-of-windows-10-version-2004-and-later"></a>Windows 10 版本2004及更高版本的驱动程序更新

如果要构建面向 Windows 10 版本2004及更高版本的驱动程序，请改用替代 Api [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) 和 [ExAllocatePool3](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool3) 。

| 旧 API                       | 新的 API                                                                     |
|-------------------------------|-----------------------------------------------------------------------------|
| ExAllocatePool                | [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) |
| ExAllocatePoolWithTag         | [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) |
| ExAllocatePoolWithQuota       | [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) |
| ExAllocatePoolWithQuotaTag    | [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) |
| ExAllocatePoolWithTagPriority | [ExAllocatePool3](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool3) |

默认情况下，新 Api 将为零个池分配，以帮助避免可能的内存泄漏错误。  

### <a name="exallocatepoolexallocatepoolwithtag"></a>ExAllocatePool/ExAllocatePoolWithTag

```cpp
// Old code
PVOID Allocation = ExAllocatePoolWithTag(PagedPool, 100, 'abcd');
RtlZeroMemory(Allocation, 100);

// New code
PVOID Allocation = ExAllocatePool2(POOL_FLAG_PAGED, 100, 'abcd');
```

旧的池分配 Api 接受 [POOL_TYPE](/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type) 参数，但新的分配 api 接受 [POOL_FLAGS](./pool_flags.md) 参数。 更新任何关联的代码以使用新的 [POOL_FLAGS](./pool_flags.md) 参数。

### <a name="exallocatepoolwithquotaexallocatepoolwithquotatag"></a>ExAllocatePoolWithQuota/ExAllocatePoolWithQuotaTag

默认情况下，新函数将在分配失败时返回 NULL。 为了使分配器引发失败时引发异常，必须按 [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2)中所述传递 POOL_FLAG_RAISE_ON_FAILURE 标志。

```cpp
// Old code
PVOID Allocation = ExAllocatePoolWithQuotaTag(PagedPool | POOL_QUOTA_FAIL_INSTEAD_OF_RAISE, 100, 'abcd');
RtlZeroMemory(Allocation, 100);

// New code
PVOID Allocation = ExAllocatePool2(POOL_FLAG_PAGED | POOL_FLAG_USE_QUOTA, 100, 'abcd');
```

### <a name="exallocatepoolwithtagpriority"></a>ExAllocatePoolWithTagPriority

```cpp
// Old code
PVOID Allocation = ExAllocatePoolWithTagPriority(PagedPool, 100, 'abcd', HighPoolPriority);
RtlZeroMemory(Allocation, 100);

// New code
POOL_EXTENDED_PARAMETER params = {0};
params.Type = PoolExtendedParameterPriority;
params.Priority = HighPoolPriority;
PVOID Allocation = ExAllocatePool3(POOL_FLAG_PAGED, 100, 'abcd', &params, 1);
```

## <a name="driver-updates-for-versions-of-windows-earlier-than-windows-10-version-2004"></a>早于 Windows 10 版本2004的 Windows 版本的驱动程序更新

如果要在 Windows 10 版本2004之前构建面向 Windows 版本的驱动程序，则必须使用以下强制内联包装函数。

在调用池分配函数之前，还必须 #define POOL_ZERO_DOWN_LEVEL_SUPPORT 并在驱动程序初始化期间调用 [ExInitializeDriverRuntime](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializedriverruntime) 。

### <a name="locally-defined-inline-functions"></a>本地定义的内联函数

```cpp
PVOID
NTAPI
ExAllocatePoolZero (
    _In_ __drv_strictTypeMatch(__drv_typeExpr) POOL_TYPE PoolType,
    _In_ SIZE_T NumberOfBytes,
    _In_ ULONG Tag
    )

PVOID
NTAPI
ExAllocatePoolQuotaZero (
    _In_ __drv_strictTypeMatch(__drv_typeExpr) POOL_TYPE PoolType,
    _In_ SIZE_T NumberOfBytes,
    _In_ ULONG Tag
    )

PVOID
NTAPI
ExAllocatePoolPriorityZero (
    _In_ __drv_strictTypeMatch(__drv_typeExpr) POOL_TYPE PoolType,
    _In_ SIZE_T NumberOfBytes,
    _In_ ULONG Tag,
    _In_ EX_POOL_PRIORITY Priority
    )
```

有关这些代码包装的实现代码，请参阅最新的 wdm 标头。 例如，这是 ExAllocatePoolPriorityZero 的实现，显示使用 [RtlZeroMemory](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)。

```cpp
{
    PVOID Allocation;

    Allocation = ExAllocatePoolWithTagPriority((POOL_TYPE) (PoolType | POOL_ZERO_ALLOCATION),
                                               NumberOfBytes,
                                               Tag,
                                               Priority);

#if defined(POOL_ZERO_DOWN_LEVEL_SUPPORT)

    if ((!ExPoolZeroingNativelySupported) && (Allocation != NULL)) {
        RtlZeroMemory(Allocation, NumberOfBytes);
    }

#endif

    return Allocation;
}
```

### <a name="mapping-of-old-apis-to-new-apis"></a>将旧 Api 映射到新 Api

| 旧 API                       | 新的 API                    |
|-------------------------------|----------------------------|
| ExAllocatePool                | ExAllocatePoolZero         |
| ExAllocatePoolWithTag         | ExAllocatePoolZero         |
| ExAllocatePoolWithQuota       | ExAllocatePoolQuotaZero    |
| ExAllocatePoolWithQuotaTag    | ExAllocatePoolQuotaZero    |
| ExAllocatePoolWithTagPriority | ExAllocatePoolPriorityZero |

### <a name="example"></a>示例

```cpp
// Old code
PVOID Allocation = ExAllocatePoolWithTag(PagedPool, 100, 'abcd');
RtlZeroMemory(Allocation, 100);

// New code

// Before headers are pulled in (or compiler defined)
#define POOL_ZERO_DOWN_LEVEL_SUPPORT

// Once during driver initialization
// Argument can be any value
ExInitializeDriverRuntime(0);

// Replacement for each pool allocation
PVOID Allocation = ExAllocatePoolZero(PagedPool, 100, 'abcd');
```

## <a name="driver-verifier-unsafeallocatepool-rules"></a>驱动程序验证程序 UnSafeAllocatePool 规则

Driver verifier [UnSafeAllocatePool](../devtest/kmdf-unsafeallocatepool.md) 规则是一个重要的安全规则，用于检查驱动程序是否未使用不推荐使用的 DDIs 来分配内存。 预览版 WDK 版本20236及更高版本中提供了此规则。

## <a name="see-also"></a>另请参阅

[ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) 

[ExAllocatePool3](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool3)

[ExAllocatePool](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)

[ExAllocatePoolWithTag](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[ExAllocatePoolWithQuota](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)

[ExAllocatePoolWithQuotaTag](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[ExAllocatePoolWithTagPriority](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)