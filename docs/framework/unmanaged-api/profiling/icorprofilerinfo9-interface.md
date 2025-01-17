---
title: ICorProfilerInfo9, interfejs
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: af6bd02c6d4e88c72dca20d2520d1ecc8cf1c421
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928786"
---
# <a name="icorprofilerinfo9-interface"></a>ICorProfilerInfo9, interfejs

Podklasa elementu [ICorProfilerInfo8](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo8-interface.md) , która dostarcza metody do wykonywania zapytań o informacje o funkcjach z wieloma natywnymi wersjami kodu.  

## <a name="methods"></a>Metody  

| Metoda|Opis|  
| ------------|-----------------|  
|[GetNativeCodeStartAddresses, Metoda](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-getnativecodestartaddresses-method.md)| Mając functionId i rejitId, wylicza natywny adres początkowy kodu dla wszystkich wersji trybie JIT tego kodu, który już istnieje. |
|[GetILToNativeMapping3, Metoda](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-getiltonativemapping3-method.md)| Przy podanym adresie początkowym kodu natywnego program zwraca informacje mapowania natywnego do IL dla tej trybie JIT wersji kodu. |
|[GetCodeInfo4, Metoda](icorprofilerinfo9-getcodeinfo4-method.md)| Przy podanym adresie początkowym kodu natywnego program zwraca bloki pamięci wirtualnej, która przechowuje ten kod. |

## <a name="requirements"></a>Wymagania  
**Poszczególnych** Zobacz [obsługiwane systemy operacyjne .NET Core](../../../core/windows-prerequisites.md#net-core-supported-operating-systems).  
**Nagłówki** CorProf. idl, CorProf. h  
**Wersje .NET:** [!INCLUDE[net_core](../../../../includes/net-core-22-md.md)]  

## <a name="see-also"></a>Zobacz także

- [Interfejsy profilowania](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
