---
title: CorSymAddrKind — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorSymAddrKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSymAddrKind
helpviewer_keywords:
- CorSymAddrKind enumeration [.NET Framework debugging]
ms.assetid: 3ef841c2-cade-42ee-ba34-2ef91d6d0879
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ba24f5394ef8fb31d8bfa4e74ac59e7bd4af86d8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769861"
---
# <a name="corsymaddrkind-enumeration"></a>CorSymAddrKind — Wyliczenie
Wskazuje typ adresu pamięci.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorSymAddrKind  
{  
    ADDR_IL_OFFSET          = 1,  
    ADDR_NATIVE_RVA         = 2,  
    ADDR_NATIVE_REGISTER    = 3,  
    ADDR_NATIVE_REGREL      = 4,  
    ADDR_NATIVE_OFFSET      = 5,  
    ADDR_NATIVE_REGREG      = 6,  
    ADDR_NATIVE_REGSTK      = 7,  
    ADDR_NATIVE_STKREG      = 8,  
    ADDR_BITFIELD           = 9,  
    ADDR_NATIVE_ISECTOFFSET = 10  
} CorSymAddrKind;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Element członkowski|Opis|  
|------------|-----------------|  
|`ADDR_IL_OFFSET`|Wskazuje Microsoft intermediate language (MSIL) lokalnej zmiennej lub parametru indeksu.|  
|`ADDR_NATIVE_RVA`|Oznacza względny adres wirtualny do modułu.|  
|`ADDR_NATIVE_REGISTER`|Wskazuje rejestru procesora CPU.|  
|`ADDR_NATIVE_REGREL`|Wskazuje, czy pierwszy adres jest rejestru, a drugi adres jest przesunięcie.|  
|`ADDR_NATIVE_OFFSET`|Określa przesunięcie od adres podstawowy.|  
|`ADDR_NATIVE_REGREG`|Wskazuje, że pierwszy adres jest niski część rejestr i drugi adres jest wysokiej część.|  
|`ADDR_NATIVE_REGSTK`|Wskazuje, że pierwszy adres jest niski część rejestr, druga jest wysokiej część i trzeci to przesunięcie.|  
|`ADDR_NATIVE_STKREG`|Wskazuje, że pierwszy adres jest rejestr, drugą jest wartość przesunięcia i trzeci jest wysoka części rejestru.|  
|`ADDR_BITFIELD`|Wskazuje, czy pierwszy adres jest początku pola, a drugi adres jest długość pola.|  
|`ADDR_NATIVE_ISECTOFFSET`|Wskazuje, czy pierwszy adres jest sekcji, a drugi adres jest przesunięta.|  
  
## <a name="requirements"></a>Wymagania  
 **Nagłówek:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Zobacz także

- [Wyliczenia magazynu symboli diagnostycznych](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-enumerations.md)
