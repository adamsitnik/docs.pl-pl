---
title: ICorProfilerInfo::SetILFunctionBody — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerInfo::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method [.NET Framework profiling]
ms.assetid: b159c712-00f4-4fc7-a990-40bf9f642e8f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: abe0a0fc177c9ec89f4621e7defb5330c911034b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778620"
---
# <a name="icorprofilerinfosetilfunctionbody-method"></a>ICorProfilerInfo::SetILFunctionBody — Metoda
Zastępuje treść określonej funkcji w określonym module.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetILFunctionBody(  
    [in] ModuleID    moduleId,  
    [in] mdMethodDef methodid,  
    [in] LPCBYTE     pbNewILMethodHeader);  
```  
  
## <a name="parameters"></a>Parametry  
 `moduleId`  
 [in] Identyfikator modułu, w której znajduje się funkcja.  
  
 `methodid`  
 [in] Token funkcji, do których chcesz zastąpić treści.  
  
 `pbNewILMethodHeader`  
 [in] Nowy nagłówek dla tej funkcji.  
  
## <a name="remarks"></a>Uwagi  
 `SetILFunctionBody` Metoda zastępuje wirtualny adres względny funkcji w metadanych, które wskazuje na nowych treści funkcji oraz dostosowuje wszelkich struktur danych wewnętrznych, zgodnie z potrzebami.  
  
 `SetILFunctionBody` Metodę można wywołać tylko funkcje, które nigdy nie zostały skompilowane przez kompilator just-in-time (JIT).  
  
 Użyj [icorprofilerinfo::getilfunctionbodyallocator —](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md) metodę, aby przydzielić miejsce dla nowej metody upewnić się, że rozmiar buforu jest zgodna.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
