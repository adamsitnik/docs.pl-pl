---
title: ICorDebugEval — Interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugEval
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval
helpviewer_keywords:
- ICorDebugEval interface [.NET Framework debugging]
ms.assetid: 3a5c9815-832d-47e1-b7f7-bbba135d7cf1
topic_type:
- apiref
ms.openlocfilehash: 33b1afca0b7b662cb7f922e20ba0d6d614c319f2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73085035"
---
# <a name="icordebugeval-interface"></a>ICorDebugEval — Interfejs

Dostarcza metody umożliwiające debugerowi wykonywanie kodu w kontekście debugowanego kodu.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Abort, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-abort-method.md)|Przerywa obliczenia wykonywane przez ten obiekt `ICorDebugEval`.|  
|[CallFunction, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-callfunction-method.md)|Konfiguruje wywołanie do określonej funkcji. (Przestarzałe w .NET Framework w wersji 2,0; Użyj zamiast tego [ICorDebugEval2:: CallParameterizedFunction —](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-callparameterizedfunction-method.md) ).|  
|[CreateValue, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-createvalue-method.md)|Pobiera wskaźnik interfejsu do obiektu "ICorDebugValue" określonego typu z początkową wartością zero lub null. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: CreateValueForType —](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-createvaluefortype-method.md) ).|  
|[GetResult, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-getresult-method.md)|Pobiera wskaźnik interfejsu do `ICorDebugValue`, który zawiera wyniki obliczania.|  
|[GetThread, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-getthread-method.md)|Pobiera wskaźnik interfejsu do elementu "ICorDebugThread", w którym ta Ocena wykonuje lub zostanie wykonana.|  
|[IsActive, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-isactive-method.md)|Pobiera wartość wskazującą, czy ten obiekt `ICorDebugEval` jest aktualnie wykonywany.|  
|[NewArray, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newarray-method.md)|Przypisuje nową tablicę określonego typu elementu i wymiarów. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: NewParameterizedArray —](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedarray-method.md) ).|  
|[NewObject, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newobject-method.md)|Przydziela nowe wystąpienie obiektu i wywołuje określoną metodę konstruktora. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: NewParameterizedObject —](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedobject-method.md) ).|  
|[NewObjectNoConstructor, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newobjectnoconstructor-method.md)|Przydziela nowe wystąpienie obiektu określonego typu, bez próby wywołania metody konstruktora. (Przestarzałe w .NET Framework 2,0; Użyj zamiast tego [ICorDebugEval2:: NewParameterizedObjectNoConstructor —](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedobjectnoconstructor-method.md) ).|  
|[NewString, metoda](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newstring-method.md)|Przypisuje nowy obiekt ciągu z określoną zawartością.|  
  
## <a name="remarks"></a>Uwagi  
 Obiekt `ICorDebugEval` jest tworzony w kontekście określonego wątku, który jest używany do wykonywania obliczeń. Wszystkie obiekty i typy używane w danej ocenie muszą znajdować się w tej samej domenie aplikacji. Ta domena aplikacji nie musi być taka sama, jak bieżąca domena aplikacji wątku. Obliczenia mogą być zagnieżdżane.  
  
 Operacje oceny nie zostaną ukończone, dopóki debuger nie wywoła [ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md), a następnie odbiera wywołanie zwrotne [ICorDebugManagedCallback:: EvalComplete —](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-evalcomplete-method.md) . Jeśli musisz użyć funkcji oceny bez zezwalania na uruchamianie innych wątków, Zawieś wątki przy użyciu jednej z [ICorDebugController:: SetAllThreadsDebugState —](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-setallthreadsdebugstate-method.md) lub [ICorDebugController:: Stop](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md) przed wywołaniem [ ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md).  
  
 Ponieważ kod użytkownika jest uruchamiany, gdy trwa szacowanie, mogą wystąpić wszystkie zdarzenia debugowania, w tym obciążenia klas i punkty przerwania. Debuger otrzyma wywołania zwrotne, tak jak normalne, dla tych zdarzeń. Stan oceny będzie widoczny jako część inspekcji normalnego stanu programu. Łańcuch stosu będzie łańcuchem `CHAIN_FUNC_EVAL` (zobacz Wyliczenie "CorDebugStepReason —" i [ICorDebugChain:: getprzyczyna](../../../../docs/framework/unmanaged-api/debugging/icordebugchain-getreason-method.md) ). Interfejs API pełnego debugera będzie kontynuował normalne działanie.  
  
 Jeśli wystąpi zakleszczenie lub nieskończone sytuacje pętli, kod użytkownika może nigdy nie zostać ukończony. W takim przypadku należy wywołać [ICorDebugEval:: Abort](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-abort-method.md) przed wznowieniem działania programu.  
  
> [!NOTE]
> Ten interfejs nie obsługuje wywoływania zdalnego na wielu maszynach ani wielu procesów.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie, interfejsy](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
