---
title: ICorProfilerCallback::JITCachedFunctionSearchFinished — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchFinished
helpviewer_keywords:
- JITCachedFunctionSearchFinished method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchFinished method [.NET Framework profiling]
ms.assetid: 3c325c82-cddd-4b00-b3da-e450c36abf62
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 882d3b3c359724688c0fb8fe5e2b567f1d575e76
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782872"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchfinished-method"></a>ICorProfilerCallback::JITCachedFunctionSearchFinished — Metoda
Powiadamia program profilujący, że wyszukiwanie zakończył się dla funkcji, która została skompilowana wcześniej przy użyciu Native Image Generator (NGen.exe).  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT JITCachedFunctionSearchFinished(  
    [in] FunctionID        functionId,  
    [in] COR_PRF_JIT_CACHE result);  
```  
  
## <a name="parameters"></a>Parametry  
 `functionId`  
 [in] Identyfikator funkcji, dla której zostało wykonane wyszukiwanie.  
  
 `result`  
 [in] Wartość [cor_prf_jit_cache —](../../../../docs/framework/unmanaged-api/profiling/cor-prf-jit-cache-enumeration.md) wyliczenia, która wskazuje wynik wyszukiwania.  
  
## <a name="remarks"></a>Uwagi  
 W .NET Framework w wersji 2.0 [icorprofilercallback::jitcachedfunctionsearchstarted —](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcachedfunctionsearchstarted-method.md) i `JITCachedFunctionSearchFinished` wywołania zwrotne nie zostaną wprowadzone dla wszystkich funkcji w zwykłych obrazów NGen. Tylko obrazów NGen zoptymalizowane pod kątem program profilujący wygeneruje wywołania zwrotne dla wszystkich funkcji w obrazie. Jednak ze względu na dodatkowe obciążenie, program profilujący powinien zażądać profiler zoptymalizowane pod kątem obrazów NGen tylko wtedy, gdy zamierza korzystać z tych wywołań zwrotnych do wymuszenia funkcję, która ma być skompilowany just-in-time (JIT). W przeciwnym razie do zbierania informacji o funkcji strategii z opóźnieniem należy używać programu profilującego.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
