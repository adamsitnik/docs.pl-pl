---
title: ICorDebugController::HasQueuedCallbacks — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugController.HasQueuedCallbacks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::HasQueuedCallbacks
helpviewer_keywords:
- HasQueuedCallbacks method [.NET Framework debugging]
- ICorDebugController::HasQueuedCallbacks method [.NET Framework debugging]
ms.assetid: 0d6a1cd9-370b-4462-adbf-e3980e897ea7
topic_type:
- apiref
ms.openlocfilehash: 51ee8b3631bffe9fd7fef4351e0aa67d1cbbe2c9
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73125398"
---
# <a name="icordebugcontrollerhasqueuedcallbacks-method"></a>ICorDebugController::HasQueuedCallbacks — Metoda
Pobiera wartość wskazującą, czy wszystkie zarządzane wywołania zwrotne są obecnie umieszczane w kolejce dla określonego wątku.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT HasQueuedCallbacks (  
    [in] ICorDebugThread *pThread,  
    [out] BOOL           *pbQueued  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `pThread`  
 podczas Wskaźnik do obiektu "ICorDebugThread", który reprezentuje wątek.  
  
 `pbQueued`  
 określoną Wskaźnik do wartości, która jest `true`, jeśli wszystkie zarządzane wywołania zwrotne są obecnie umieszczane w kolejce dla określonego wątku; w przeciwnym razie `false`.  
  
 Jeśli określono wartość null dla parametru `pThread`, `HasQueuedCallbacks` zwróci `true`, jeśli w dowolnym wątku istnieją obecnie zarządzane wywołania zwrotne.  
  
## <a name="remarks"></a>Uwagi  
 Wywołania zwrotne będą wysyłane pojedynczo, za każdym razem, gdy [ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) jest wywoływana. Debuger może zaznaczyć tę flagę, jeśli chce zgłosić wiele zdarzeń debugowania, które wystąpiły jednocześnie.  
  
 Gdy zdarzenia debugowania są umieszczane w kolejce, są już wystąpiły, więc debuger musi opróżnić całą kolejkę, aby upewnić się, że stan debugowanego obiektu. (Wywołaj `ICorDebugController::Continue`, aby opróżnić kolejkę.) Na przykład, jeśli kolejka zawiera dwa zdarzenia debugowania w wątku *x*, a Debuger zawiesza wątek *x* po pierwszym zdarzeniu debugowania, a następnie wywołuje `ICorDebugController::Continue`, drugie zdarzenie debugowania dla wątku *X* zostanie wysłane, mimo że wątek został zawieszony.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także
