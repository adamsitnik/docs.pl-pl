---
title: ICorDebugProcess::ClearCurrentException — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ClearCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ClearCurrentException
helpviewer_keywords:
- ClearCurrentException method, ICorDebugProcess interface [.NET Framework debugging]
- ICorDebugProcess::ClearCurrentException method [.NET Framework debugging]
ms.assetid: 9e02ee1a-e495-4578-bfb5-b946274bede7
topic_type:
- apiref
ms.openlocfilehash: 37a7d8fa4439d52db3cddfff22ac6580b19af58a
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73128915"
---
# <a name="icordebugprocessclearcurrentexception-method"></a>ICorDebugProcess::ClearCurrentException — Metoda
Czyści bieżący wyjątek niezarządzany w danym wątku.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT ClearCurrentException([in] DWORD threadID);  
```  
  
## <a name="parameters"></a>Parametry  
 `threadID`  
 podczas Identyfikator wątku, w którym zostanie wyczyszczony bieżący wyjątek niezarządzany.  
  
## <a name="remarks"></a>Uwagi  
 Wywołaj tę metodę przed wywołaniem [ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) , gdy wątek zgłosił wyjątek niezarządzany, który powinien zostać zignorowany przez debugowanego obiektu. Spowoduje to wyczyszczenie wszystkich oczekujących zdarzeń w paśmie (IB) i poza pasmem (OOB) w danym wątku. Wszystkie punkty przerwania OOB i wyjątki pojedynczego kroku są automatycznie wyczyszczone.  
  
 Użyj [ICorDebugThread2:: InterceptCurrentException —](../../../../docs/framework/unmanaged-api/debugging/icordebugthread2-interceptcurrentexception-method.md) , aby przechwycić bieżący wyjątek zarządzany wątku.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
