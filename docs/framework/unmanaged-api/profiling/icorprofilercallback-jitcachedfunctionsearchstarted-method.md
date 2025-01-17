---
title: ICorProfilerCallback::JITCachedFunctionSearchStarted — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchStarted
helpviewer_keywords:
- JITCachedFunctionSearchStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchStarted method [.NET Framework profiling]
ms.assetid: 5cba642c-0d80-48ee-889d-198c5044d821
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f4d35179b8ae35c03370cc3798609d6ed430cde3
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782851"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchstarted-method"></a>ICorProfilerCallback::JITCachedFunctionSearchStarted — Metoda
Powiadamia program profilujący, że wyszukiwania została uruchomiona dla funkcji, która została skompilowana wcześniej przy użyciu Native Image Generator (NGen.exe).  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT JITCachedFunctionSearchStarted(  
    [in]  FunctionID functionId,  
    [out] BOOL *pbUseCachedFunction);  
```  
  
## <a name="parameters"></a>Parametry  
 `functionId`  
 [in] Identyfikator funkcji, dla którego wyszukiwanie jest wykonywane.  
  
 `pbUseCachedFunction`  
 [out] `true` Jeśli silnik wykonywania powinien używać zbuforowaną wersję funkcji (jeśli dostępne); w przeciwnym razie `false`. Jeśli wartość jest `false`, wykonywanie aparatu JIT kompiluje funkcję zamiast wersji, który nie jest kompilowany dokładnie na czas.  
  
## <a name="remarks"></a>Uwagi  
 W .NET Framework w wersji 2.0 `JITCachedFunctionSearchStarted` i [icorprofilercallback::jitcachedfunctionsearchfinished — metoda](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcachedfunctionsearchfinished-method.md) wywołania zwrotne nie zostaną wprowadzone dla wszystkich funkcji w zwykłych obrazów NGen. Tylko obrazów NGen zoptymalizowane pod kątem profilu wygeneruje wywołania zwrotne dla wszystkich funkcji w obrazie. Jednak ze względu na dodatkowe obciążenie, program profilujący powinien zażądać profiler zoptymalizowane pod kątem obrazów NGen tylko wtedy, gdy zamierza korzystać z tych wywołań zwrotnych do wymuszenia funkcję, która ma być skompilowany just-in-time (JIT). W przeciwnym razie do zbierania informacji o funkcji strategii z opóźnieniem należy używać programu profilującego.  
  
 Profilery muszą obsługiwać przypadki, gdy wiele wątków profilowana aplikacja wywołania dotyczą tej samej metody jednocześnie. Na przykład, wywołania wątku A `JITCachedFunctionSearchStarted` , a program profilujący, ustawiając *pbUseCachedFunction*na wartość FALSE, aby wymusić kompilacja JIT. Wątek, następnie wywołuje [icorprofilercallback::jitcompilationstarted —](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md) i [icorprofilercallback::jitcompilationfinished —](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md).  
  
 Teraz wątek jest wywołany B `JITCachedFunctionSearchStarted` dla tej samej funkcji. Mimo że program profilujący ma stwierdziła swój zamiar funkcji skompilować wg JIT, profiler otrzymuje drugi wywołania zwrotnego, ponieważ wątek B wysyła wywołania zwrotnego, zanim program profilujący odpowiedział na wywołania wątku, A `JITCachedFunctionSearchStarted`. Kolejność, w którym wątki wykonywanie wywołań zależy od tego, jak wątki są zaplanowane.  
  
 Gdy profiler otrzymuje zduplikowane wywołań zwrotnych, należy ustawić w niej wartość przywołana przez `pbUseCachedFunction` taką samą wartość dla wszystkich duplikatów wywołań zwrotnych. Oznacza to, kiedy `JITCachedFunctionSearchStarted` jest wywoływana wiele razy z takimi samymi `functionId` wartości, program profilujący musi odpowiadać takie same każdorazowo.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
