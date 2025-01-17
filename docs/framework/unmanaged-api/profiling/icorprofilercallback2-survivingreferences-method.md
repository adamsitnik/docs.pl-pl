---
title: ICorProfilerCallback2::SurvivingReferences — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.SurvivingReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::SurvivingReferences
helpviewer_keywords:
- ICorProfilerCallback2::SurvivingReferences method [.NET Framework profiling]
- SurvivingReferences method [.NET Framework profiling]
ms.assetid: f165200e-3a91-47f7-88fc-13ff10c8babc
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fc3ec00f11582ede1dc4b3d481a4eb9dcc4dd1d9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963916"
---
# <a name="icorprofilercallback2survivingreferences-method"></a>ICorProfilerCallback2::SurvivingReferences — Metoda
Raportuje układ obiektów w stercie w wyniku niekompaktowego wyrzucania elementów bezużytecznych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SurvivingReferences(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] ULONG  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>Parametry  
 `cSurvivingObjectIDRanges`  
 podczas Liczba bloków ciągłych obiektów, które przeżyły jako wynik niekompaktowego wyrzucania elementów bezużytecznych. Oznacza to `cSurvivingObjectIDRanges` , że wartość jest rozmiarem `objectIDRangeStart` tablic i `cObjectIDRangeLength` , które przechowują `ObjectID` odpowiednio długość i dla każdego bloku obiektów.  
  
 Dwa następne argumenty `SurvivingReferences` są równoległymi tablicami. Innymi słowy `objectIDRangeStart` i `cObjectIDRangeLength` dotyczy tego samego bloku sąsiadujących obiektów.  
  
 `objectIDRangeStart`  
 podczas Tablica `ObjectID` wartości, z których każdy jest adresem początkowym bloku ciągłego, na żywo obiektów w pamięci.  
  
 `cObjectIDRangeLength`  
 podczas Tablica liczb całkowitych, z których każdy jest rozmiarem ciągłego bloku ciągłych obiektów w pamięci.  
  
 Dla każdego bloku, do którego odwołuje `objectIDRangeStart` się tablica, jest określony rozmiar.  
  
## <a name="remarks"></a>Uwagi  
  
> [!IMPORTANT]
> Ta metoda zgłasza rozmiary `MAX_ULONG` dla obiektów, które są większe niż 4 GB na platformach 64-bitowych. W przypadku obiektów, które są większe niż 4 GB, zamiast tego użyj metody [ICorProfilerCallback4:: SurvivingReferences2 —](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-survivingreferences2-method.md) .  
  
 Elementy `objectIDRangeStart` tablic i `cObjectIDRangeLength` powinny być interpretowane w następujący sposób, aby określić, czy obiekt przeżyje odzyskiwanie pamięci. Załóżmy, że `ObjectID` wartość (`ObjectID`) znajduje się w następującym zakresie:  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 Dla każdej wartości `i` , która znajduje się w następującym zakresie, obiekt przeżyły odzyskiwanie pamięci:  
  
 0 <= `i` < `cSurvivingObjectIDRanges`  
  
 Niekompaktowe wyrzucanie elementów bezużytecznych przejmuje pamięć zajmowaną przez obiekty "martwe", ale nie kompaktuje ilości wolnego miejsca. W efekcie do sterty jest zwracana pamięć, ale nie są przenoszone żadne obiekty "na żywo".  
  
 Wywołania `SurvivingReferences` środowiska uruchomieniowego języka wspólnego (CLR) dla niekompaktowych kolekcji elementów bezużytecznych. W przypadku kompaktowania kolekcji elementów bezużytecznych zamiast niej wywoływana jest [ICorProfilerCallback:: MovedReferences —](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md) . Pojedyncze wyrzucanie elementów bezużytecznych może być kompaktowania dla jednej generacji i niekompaktowania dla innych. W przypadku wyrzucania elementów bezużytecznych na określonej generacji Profiler otrzyma `SurvivingReferences` wywołanie zwrotne `MovedReferences` lub wywołanie zwrotne, ale nie oba.  
  
 Podczas `SurvivingReferences` konkretnego wyrzucania elementów bezużytecznych może zostać odebranych wiele wywołań zwrotnych z powodu ograniczonego wewnętrznego buforowania, wiele wątków zgłasza w przypadku wyrzucania elementów bezużytecznych serwera i z innych przyczyn. W przypadku wielu wywołań zwrotnych podczas wyrzucania elementów bezużytecznych informacje są kumulowane — wszystkie odwołania, które są `SurvivingReferences` zgłaszane w przypadku wywołania zwrotnego w czasie odzyskiwania pamięci.  
  
## <a name="requirements"></a>Wymagania  
 **Poszczególnych** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówki** CorProf. idl, CorProf. h  
  
 **Biblioteki** CorGuids.lib  
  
 **.NET Framework wersje:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [SurvivingReferences2, metoda](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-survivingreferences2-method.md)
