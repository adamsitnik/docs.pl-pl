---
title: ICorProfilerCallback::RemotingServerSendingReply — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RemotingServerSendingReply
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RemotingServerSendingReply
helpviewer_keywords:
- RemotingServerSendingReply method [.NET Framework profiling]
- ICorProfilerCallback::RemotingServerSendingReply method [.NET Framework profiling]
ms.assetid: dfe84a19-2e03-4be2-8b25-f02bad38e4a9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c73889a6daaa50d1694e786c78f50d0e87644967
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750430"
---
# <a name="icorprofilercallbackremotingserversendingreply-method"></a>ICorProfilerCallback::RemotingServerSendingReply — Metoda
Powiadamia program profilujący, że proces zakończył przetwarzanie żądania wywołania zdalnej metody i ma przesłanie odpowiedzi za pośrednictwem kanału.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT RemotingServerSendingReply(  
    [in] GUID *pCookie,  
    [in] BOOL fIsAsync);  
```  
  
## <a name="parameters"></a>Parametry  
 `pCookie`  
 [in] Wskaźnik do identyfikatora GUID, które będą odpowiadać wartość podana w [icorprofilercallback::remotingclientreceivingreply —](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientreceivingreply-method.md) w tych warunkach:  
  
- Pliki cookie identyfikatora GUID komunikacji zdalnej są aktywne.  
  
- Kanał powiedzie się podczas przesyłania wiadomości.  
  
- Identyfikator GUID pliki cookie są aktywne na proces po stronie klienta.  
  
 Dzięki temu można łatwo parowanie wywołaniem funkcji zdalnych wywołań i Tworzenie stosu wywołań logicznych.  
  
 `fIsAsync`  
 [in] Wartość, która jest `true` Jeśli wywołanie jest asynchroniczne; w przeciwnym razie `false`.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
