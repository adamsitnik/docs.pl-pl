---
title: COR_IL_MAP — Struktura
ms.date: 03/30/2017
api_name:
- COR_IL_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_IL_MAP
helpviewer_keywords:
- COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type:
- apiref
ms.openlocfilehash: c37f039d9636854c464e7981693c573bd60deab9
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73132345"
---
# <a name="cor_il_map-structure"></a>COR_IL_MAP — Struktura
Określa zmiany w względnym przesunięciu funkcji.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;   
    ULONG32 newOffset;   
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Element członkowski|Opis|  
|------------|-----------------|  
|`oldOffset`|Poprzednie przesunięcie języka pośredniego firmy Microsoft (MSIL) względem początku funkcji.|  
|`newOffset`|Nowe przesunięcie MSIL względem początku funkcji.|  
|`fAccurate`|`true`, jeśli mapowanie jest znane z dokładnością; w przeciwnym razie `false`.|  
  
## <a name="remarks"></a>Uwagi  
 Format mapy jest następujący: debuger przyjmie, że `oldOffset` odnosi się do przesunięcia MSIL w oryginalnym, niezmodyfikowanym kodzie MSIL. `newOffset` parametr odnosi się do odpowiedniego przesunięcia MSIL w nowym, Instrumentacji kodu.  
  
 Aby wykonać prawidłowe działanie, należy spełnić następujące wymagania:  
  
- Mapa powinna być posortowana w kolejności rosnącej.  
  
- Nie należy zmienić kolejności kodu MSIL z instrumentacją.  
  
- Nie należy usuwać oryginalnego kodu MSIL.  
  
- Mapa powinna zawierać wpisy umożliwiające zamapowanie wszystkich punktów sekwencji z pliku bazy danych programu (PDB).  
  
 Mapa nie wykonuje interpolacji brakujących wpisów. Poniższy przykład pokazuje mapę i jej wyniki.  
  
 Zmapować  
  
- 0 Stare przesunięcie, 0 nowe przesunięcie  
  
- 5 starych przesunięcia, 10 nowego przesunięcia  
  
- 9 Stare przesunięcie, 20 nowego przesunięcia  
  
 Uzyskane  
  
- Stare przesunięcie 0, 1, 2, 3 lub 4 zostanie zmapowane na nowe przesunięcie o wartości 0.  
  
- Stare przesunięcie o wartości 5, 6, 7 lub 8 zostanie zmapowane na nowe przesunięcie 10.  
  
- Stare przesunięcie w wysokości 9 lub wyższej zostanie zmapowane do nowego przesunięcia 20.  
  
- Nowe przesunięcie 0, 1, 2, 3, 4, 5, 6, 7, 8 lub 9 zostanie zmapowane do starego przesunięcia 0.  
  
- Nowe przesunięcie 10, 11, 12, 13, 14, 15, 16, 17, 18 lub 19 zostanie zmapowane do starego przesunięcia 5.  
  
- Nowe przesunięcie o wartości 20 lub wyższej zostanie zmapowane do starego przesunięcia 9.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorProf. idl  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Struktury debugowania](debugging-structures.md)
- [Debugowanie](index.md)
