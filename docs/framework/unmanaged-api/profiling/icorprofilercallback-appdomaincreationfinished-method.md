---
title: ICorProfilerCallback::AppDomainCreationFinished — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainCreationFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainCreationFinished
helpviewer_keywords:
- AppDomainCreationFinished method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainCreationFinished method [.NET Framework profiling]
ms.assetid: dbab7d90-d515-4dc9-8195-294d5d04bab6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 910f8b7f78b6348ace9036d35c0844f2a64cf433
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67763143"
---
# <a name="icorprofilercallbackappdomaincreationfinished-method"></a>ICorProfilerCallback::AppDomainCreationFinished — Metoda
Powiadamia program profilujący, że utworzono domeny aplikacji.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT AppDomainCreationFinished(  
    [in] AppDomainID appDomainId,  
    [in] HRESULT     hrStatus);   
```  
  
## <a name="parameters"></a>Parametry  
 `appDomainId`  
 [in] Identyfikuje domeny, który został utworzony.  
  
 `hrStatus`  
 [in] Wartość HRESULT, która wskazuje, czy Tworzenie domeny aplikacji została ukończona pomyślnie.  
  
## <a name="remarks"></a>Uwagi  
 Identyfikator aplikacji jest nieprawidłowa dla każdego żądania informacje do momentu `AppDomainCreationFinished` metoda jest wywoływana.  
  
 Niektóre części podczas ładowania domeny aplikacji może kontynuować po `AppDomainCreationFinished` wywołania zwrotnego. Błąd HRESULT w `hrStatus` wskazuje błąd. Jednak sukcesów wartość HRESULT w `hrStatus` wskazuje tylko, że pierwsza część tworzenia domeny aplikacji zakończyła się pomyślnie.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
