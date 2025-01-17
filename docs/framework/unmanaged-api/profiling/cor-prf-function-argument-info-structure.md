---
title: COR_PRF_FUNCTION_ARGUMENT_INFO — Struktura
ms.date: 03/30/2017
api_name:
- COR_PRF_FUNCTION_ARGUMENT_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO
helpviewer_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO structure [.NET Framework profiling]
ms.assetid: 07cf3bab-e193-4991-8205-3f41cf2d67b3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 658b88349bedcbcefd0b97226c7bd1fa34f656c7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781921"
---
# <a name="corprffunctionargumentinfo-structure"></a>COR_PRF_FUNCTION_ARGUMENT_INFO — Struktura
Reprezentuje argumenty funkcji, w kolejności od lewej do prawej.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef struct _COR_PRF_FUNCTION_ARGUMENT_INFO {  
    ULONG numRanges;  
    ULONG totalArgumentSize;  
    COR_PRF_FUNCTION_ARGUMENT_RANGE ranges[1];  
} COR_PRF_FUNCTION_ARGUMENT_INFO;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Element członkowski|Opis|  
|------------|-----------------|  
|`numRanges`|Liczba bloków argumentów. Ta wartość jest liczbą [cor_prf_function_argument_range —](../../../../docs/framework/unmanaged-api/profiling/cor-prf-function-argument-range-structure.md) struktury w `ranges` tablicy.|  
|`totalArgumentSize`|Całkowity rozmiar wszystkich argumentów. Innymi słowy ta wartość jest sumy długości argumentu.|  
|`ranges`|Tablica `COR_PRF_FUNCTION_ARGUMENT_RANGE` struktur, z których każdy reprezentuje jeden blok argumentów funkcji.|  
  
## <a name="remarks"></a>Uwagi  
 Funkcja może mieć wiele argumentów. Tych argumentów nie może być ciągłym przechowywane w pamięci. Może być blokiem trzy argumenty w jednym miejscu, blok dwa argumenty w inne miejsce i blok końcowy jeden argument w innym miejscu. Te argumenty są dostępne dla tej samej funkcji; po prostu są one przechowywane w różnych miejscach.  
  
 `COR_PRF_FUNCTION_ARGUMENT_INFO` Struktury reprezentuje wszystkie argumenty funkcji pojedynczej. Używa tablicy, aby odwoływać się do wszystkich bloków argumentów funkcji. Dlatego dla jednej funkcji, masz jeden `COR_PRF_FUNCTION_ARGUMENT_INFO` struktury, która odwołuje się do wielu `COR_PRF_FUNCTION_ARGUMENT_RANGE` struktur, które wskazuje na jeden lub więcej argumentów funkcji.  
  
 Argumenty, które są przechowywane w rejestrach, są rozrzucone w pamięci, aby skompilować struktur.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Profiling — struktury](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
