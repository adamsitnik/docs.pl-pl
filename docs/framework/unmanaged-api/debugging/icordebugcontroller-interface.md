---
title: ICorDebugController — Interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugController
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController
helpviewer_keywords:
- ICorDebugController interface [.NET Framework debugging]
ms.assetid: dbb1c4dc-269a-459b-ab1d-6c70788782ce
topic_type:
- apiref
ms.openlocfilehash: 27f991c12ea7786d6146b5731848ca5ad3a37e21
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73125371"
---
# <a name="icordebugcontroller-interface"></a>ICorDebugController — Interfejs

Reprezentuje zakres, <xref:System.Diagnostics.Process> lub <xref:System.AppDomain>, w którym można kontrolować kontekst wykonywania kodu.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|`ICorDebugController::CanCommitChanges`|Ta metoda jest przestarzała.|  
|`ICorDebugController::CommitChanges`|Ta metoda jest przestarzała.|  
|[Continue, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)|Wznawia wykonywanie zarządzanych wątków po wywołaniu [ICorDebugController:: Stop](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md).|  
|[Detach, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-detach-method.md)|Odłącza debuger od domeny procesu lub aplikacji.|  
|[EnumerateThreads, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-enumeratethreads-method.md)|Pobiera moduł wyliczający dla aktywnych wątków zarządzanych w procesie.|  
|[HasQueuedCallbacks, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-hasqueuedcallbacks-method.md)|Pobiera wartość wskazującą, czy wszystkie zarządzane wywołania zwrotne są obecnie umieszczane w kolejce dla określonego wątku.|  
|[IsRunning, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-isrunning-method.md)|Pobiera wartość wskazującą, czy wątki w procesie są obecnie uruchomione swobodnie.|  
|[SetAllThreadsDebugState, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-setallthreadsdebugstate-method.md)|Ustawia stan debugowania wszystkich zarządzanych wątków w procesie.|  
|[Stop, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md)|Wykonuje przerwanie w ramach wszystkich wątków, które uruchamiają kod zarządzany w procesie.|  
|[Terminate, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-terminate-method.md)|Kończy proces z określonym kodem zakończenia.|  
  
## <a name="remarks"></a>Uwagi  
 Jeśli `ICorDebugController` kontroluje proces, zakres obejmuje wszystkie wątki procesu. Jeśli `ICorDebugController` kontroluje domenę aplikacji, zakres obejmuje tylko wątki tej konkretnej domeny aplikacji.  
  
> [!NOTE]
> Ten interfejs nie obsługuje wywoływania zdalnego na wielu maszynach ani wielu procesów.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie, interfejsy](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
