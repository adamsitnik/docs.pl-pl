---
title: ICorProfilerInfo::SetEnterLeaveFunctionHooks — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetEnterLeaveFunctionHooks
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetEnterLeaveFunctionHooks
helpviewer_keywords:
- SetEnterLeaveFunctionHooks method [.NET Framework profiling]
- ICorProfilerInfo::SetEnterLeaveFunctionHooks method [.NET Framework profiling]
ms.assetid: 72399636-c219-4ffd-8ac8-39432c9d4641
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1b6f53d5747eca00b898b2cde66d75764ca490cf
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772108"
---
# <a name="icorprofilerinfosetenterleavefunctionhooks-method"></a>ICorProfilerInfo::SetEnterLeaveFunctionHooks — Metoda
Określa funkcje implementowane przez profiler ma być wywołane na "enter", "Opuść" i "rekurencja ogonowa" hooks zarządzanej funkcji.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetEnterLeaveFunctionHooks(  
    [in] FunctionEnter    *pFuncEnter,  
    [in] FunctionLeave    *pFuncLeave,  
    [in] FunctionTailcall *pFuncTailcall);  
```  
  
## <a name="parameters"></a>Parametry  
 `pFuncEnter`  
 [in] Wskaźnik do implementacji, które ma być używany jako [functionenter —](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md) wywołania zwrotnego.  
  
 `pFuncLeave`  
 [in] Wskaźnik do implementacji, które ma być używany jako [functionleave —](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md) wywołania zwrotnego.  
  
 `pFuncTailcall`  
 [in] Wskaźnik do implementacji, które ma być używany jako [functiontailcall —](../../../../docs/framework/unmanaged-api/profiling/functiontailcall-function.md) wywołania zwrotnego.  
  
## <a name="remarks"></a>Uwagi  
 W .NET Framework w wersji 1.0 każdy wskaźnik funkcji może być null powoduje wyłączenie odpowiedniego wywołania zwrotnego.  
  
 Tylko jeden zestaw wywołań zwrotnych, może być aktywne w danym momencie. W związku z tym jeśli program profilujący wywołuje zarówno `SetEnterLeaveFunctionHooks` i [icorprofilerinfo2::setenterleavefunctionhooks2 —](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md), następnie `SetEnterLeaveFunctionHooks2` ma pierwszeństwo.  
  
 `SetEnterLeaveFunctionHooks` Metoda może być wywołana tylko z poziomu programu profilującego [ICorProfilerCallback::Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md) wywołania zwrotnego.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
