---
title: ICorProfilerModuleEnum::Skip — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum.Skip Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum::Skip
helpviewer_keywords:
- Skip method, ICorProfilerModuleEnum interface [.NET Framework profiling]
- ICorProfilerModuleEnum::Skip method [.NET Framework profiling]
ms.assetid: 8dc29c6a-e2ba-41d8-a1e0-0fdd21421e0b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: eecb2a5da9dddaccbab7fcc6d74af6e4c6bfb72c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67775126"
---
# <a name="icorprofilermoduleenumskip-method"></a>ICorProfilerModuleEnum::Skip — Metoda
Przesuwa kursor modułu wyliczającego z jego bieżącej pozycji, tak, aby określoną liczbę elementów są pomijane.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT Skip([in] ULONG celt);  
```  
  
## <a name="parameters"></a>Parametry  
 `celt`  
 [in] Liczba elementów, które mają zostać pominięte.  
  
## <a name="return-value"></a>Wartość zwracana  
 Ta metoda zwraca następujące specyficzne wyniki HRESULT, a także HRESULT błędów wskazujących Niepowodzenie metody.  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|S_OK|`celt` elementy zostały pominięte.|  
|S_FALSE|Mniej niż `celt` elementy zostały pominięte, co oznacza, że nie istnieją żadne więcej elementów.|  
  
## <a name="remarks"></a>Uwagi  
 Nowe położenie kursora ten moduł wyliczający jest (bieżącej pozycji) + `celt`.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerModuleEnum, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilermoduleenum-interface.md)
- [Interfejsy profilowania](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
