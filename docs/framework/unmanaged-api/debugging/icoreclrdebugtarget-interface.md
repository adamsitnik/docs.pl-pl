---
title: ICoreClrDebugTarget — Interfejs
ms.date: 03/30/2017
api_name:
- ICoreClrDebugTarget
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget
helpviewer_keywords:
- remote debugging API [Silverlight]
- ICorClrDebugTarget interface
- Silverlight, remote debugging
ms.assetid: 7cfaee76-e284-4a66-a431-8e33f0f60038
topic_type:
- apiref
ms.openlocfilehash: 83afe121b6bf0de3c5542695e38b6605db7a8b6d
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73121814"
---
# <a name="icoreclrdebugtarget-interface"></a>ICoreClrDebugTarget — Interfejs
Zapewnia metody, które kontrolują liczby odwołań, wyliczają procesy i zwalniają pamięć skojarzoną z debugerem, który jest dołączony do zdalnego obiektu docelowego Silverlight platformy Macintosh.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
class ICoreClrDebugTarget {  
      HRESULT EnumProcesses (  
          [out] DWORD*                    pcProcs,  
          [out] CoreClrDebugProcInfo**    ppProcs  
      );  
  
      HRESULT EnumRuntimes (  
      [in]  DWORD                      dwInternalProcessID,  
      [out] DWORD*                     pcRuntimes,  
      [out] CoreClrDebugRuntimeInfo**  ppRuntimes  
      );  
  
      void FreeMemory (  
      [in] void*      pMemory  
    );  
};  
```  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[ICoreClrDebugTarget::EnumProcesses, metoda](../../../../docs/framework/unmanaged-api/debugging/icoreclrdebugtarget-enumprocesses-method.md)|Wylicza procesy, które są uruchomione na komputerze zdalnym.|  
|[ICoreClrDebugTarget::EnumRuntimes, metoda](../../../../docs/framework/unmanaged-api/debugging/icoreclrdebugtarget-enumruntimes-method.md)|Wylicza środowisko uruchomieniowe języka wspólnego (CLRs) w określonym procesie na komputerze zdalnym.|  
|[ICoreClrDebugTarget::FreeMemory, metoda](../../../../docs/framework/unmanaged-api/debugging/icoreclrdebugtarget-freememory-method.md)|Zwalnia pamięć przydzieloną przez metody wyliczenia w tej klasie.|  
  
## <a name="remarks"></a>Uwagi  
 Obecnie ta funkcja jest obsługiwana tylko w przypadku debugowania obiektu docelowego aplikacji opartego na technologii Silverlight, który jest uruchomiony na komputerze zdalnym Macintosh.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CoreClrRemoteDebuggingInterfaces. h  
  
 **Biblioteka:** mscordbi_macx86. dll  
  
 **.NET Framework wersje:** 3,5 SP1  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugRemoteTarget, interfejs](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)
- [ICorDebug, interfejs](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)

- [Debugowanie, interfejsy](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
