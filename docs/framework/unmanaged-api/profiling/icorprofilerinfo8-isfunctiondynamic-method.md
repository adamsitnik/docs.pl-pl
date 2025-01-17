---
title: ICorProfilerInfo8::IsFunctionDynamic
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo8.IsFunctionDynamic
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 01aa1df27dccf41060083333588e04bc5ea88520
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855929"
---
# <a name="icorprofilerinfo8isfunctiondynamic-method"></a>ICorProfilerInfo8:: IsFunctionDynamic, Metoda

Określa, czy funkcja nie ma skojarzonych metadanych.

## <a name="syntax"></a>Składnia

```cpp
HRESULT IsFunctionDynamic( [in]  FunctionID  functionId,
                           [out] BOOL        *isDynamic);
```

#### <a name="parameters"></a>Parametry

`functionId` \
podczas  `FunctionID` Identyfikuje daną funkcję.

`isDynamic` \
określoną Wskaźnik do elementu `BOOL` , który będzie zawierał wartość wskazującą, czy funkcja nie ma metadanych.

## <a name="remarks"></a>Uwagi

Funkcja jest uznawana za dynamiczną, jeśli nie ma metadanych. Niektóre metody, takie jak elementy zastępcze IL lub metody LCG, nie mają skojarzonych metadanych, które można pobrać za pomocą interfejsów API IMetaDataImport. Te metody mogą być napotkane przez program do przechodzenia za pomocą wskaźników instrukcji lub przez nasłuchiwanie [ICorProfilerCallback::D ynamicmethodjitcompilationstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md).

## <a name="requirements"></a>Wymagania

**Poszczególnych** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).

**Nagłówki** CorProf. idl, CorProf. h

**Biblioteki** CorGuids.lib

**.NET Framework wersje:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo8, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo8-interface.md)
