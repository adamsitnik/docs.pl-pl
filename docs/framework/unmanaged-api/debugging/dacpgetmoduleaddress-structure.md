---
title: DacpGetModuleAddress Structure
ms.date: 01/16/2019
api.name:
- DacpGetModuleAddress Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpGetModuleAddress Structure
helpviewer.keywords:
- DacpGetModuleAddress Structure [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 145b06f89b45b165b9d6329a4c16ac5739406113
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739182"
---
# <a name="dacpgetmoduleaddress-structure"></a>DacpGetModuleAddress Structure

Definiuje kontener dla żądania adres modułu.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Składnia

```cpp
struct DacpGetModuleAddress
{
    CLRDATA_ADDRESS ModulePtr;
};
```

## <a name="members"></a>Elementy członkowskie

| Element członkowski      | Opis                |
| ----------- | -------------------------- |
| `ModulePtr` | Wskaźnik do modułu. |

## <a name="methods"></a>Metody

| Metoda                                                                                               | Opis                                                                    |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [Żądanie](../../../../docs/framework/unmanaged-api/debugging/dacpgetmoduleaddress-request-method.md) | Wykonuje żądanie, aby wypełnić struktury ze struktury danego środowiska uruchomieniowego. |

## <a name="remarks"></a>Uwagi

Ta struktura znajduje się wewnątrz środowiska uruchomieniowego i nie jest dostępna za pośrednictwem wszystkich nagłówków lub pliki biblioteki. Aby go użyć, definiują strukturę zgodnie z powyższym opisem gdzie `CLRDATA_ADDRESS` jest 64-bitowej nieoznaczonej liczby całkowitej.

## <a name="requirements"></a>Wymagania
**Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
**Nagłówek:** Brak  
**Biblioteka:** Brak  
**Wersje programu .NET framework:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Zobacz także

- [Debugowanie](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [Struktury debugowania](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
