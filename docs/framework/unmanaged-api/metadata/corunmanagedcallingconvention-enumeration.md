---
title: CorUnmanagedCallingConvention — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorUnmanagedCallingConvention
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorUnmanagedCallingConvention
helpviewer_keywords:
- CorUnmanagedCallingConvention enumeration [.NET Framework metadata]
ms.assetid: 83058790-160b-4703-a5eb-74b66acbdfa9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9206fbde13f457d4b2e2941ee744d645c6df9774
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781998"
---
# <a name="corunmanagedcallingconvention-enumeration"></a>CorUnmanagedCallingConvention — Wyliczenie
Określa konwencji wywoływania niezarządzanego kodu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorUnmanagedCallingConvention {  
  
    IMAGE_CEE_UNMANAGED_CALLCONV_C         = 0x1,  
    IMAGE_CEE_UNMANAGED_CALLCONV_STDCALL   = 0x2,  
    IMAGE_CEE_UNMANAGED_CALLCONV_THISCALL  = 0x3,  
    IMAGE_CEE_UNMANAGED_CALLCONV_FASTCALL  = 0x4,  
  
    IMAGE_CEE_CS_CALLCONV_C                = 0x1,  
    IMAGE_CEE_CS_CALLCONV_STDCALL          = 0x2,  
    IMAGE_CEE_CS_CALLCONV_THISCALL         = 0x3,  
    IMAGE_CEE_CS_CALLCONV_FASTCALL         = 0x4  
  
} CorUnmanagedCallingConvention;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Element członkowski|Opis|  
|------------|-----------------|  
|`IMAGE_CEE_UNMANAGED_CALLCONV_C`|Konwencja wywoływania języka C.|  
|`IMAGE_CEE_UNMANAGED_CALLCONV_STDCALL`|Standardowej konwencji wywoływania.|  
|`IMAGE_CEE_UNMANAGED_CALLCONV_THISCALL`|"To" Konwencji wywołania.|  
|`IMAGE_CEE_UNMANAGED_CALLCONV_FASTCALL`|Konwencja wywoływania "fast".|  
|`IMAGE_CEE_CS_CALLCONV_C`|Nie używany.|  
|`IMAGE_CEE_CS_CALLCONV_STDCALL`|Nie używany.|  
|`IMAGE_CEE_CS_CALLCONV_THISCALL`|Nie używany.|  
|`IMAGE_CEE_CS_CALLCONV_FASTCALL`|Nie używany.|  
  
## <a name="remarks"></a>Uwagi  
 Środowisko CLR nie obsługuje "fast" Konwencja wywoływania w .NET Framework w wersji 1.0.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorHdr.h  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Wyliczenia metadanych](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
