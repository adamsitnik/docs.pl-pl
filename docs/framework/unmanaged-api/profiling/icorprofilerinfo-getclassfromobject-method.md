---
title: ICorProfilerInfo::GetClassFromObject — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetClassFromObject
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetClassFromObject
helpviewer_keywords:
- GetClassFromObject method [.NET Framework profiling]
- ICorProfilerInfo::GetClassFromObject method [.NET Framework profiling]
ms.assetid: b97493fb-713e-49d5-a73e-5688b2ad0700
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 57f57d67c4f7641495feca0b9c128e6ccf456cab
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780199"
---
# <a name="icorprofilerinfogetclassfromobject-method"></a>ICorProfilerInfo::GetClassFromObject — Metoda
Pobiera `ClassID` obiektu, biorąc pod uwagę jej `ObjectID`.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetClassFromObject(  
    [in]  ObjectID objectId,  
    [out] ClassID *pClassId);  
```  
  
## <a name="parameters"></a>Parametry  
 `objectId`  
 [in] Identyfikator obiektu, dla którego należy pobrać `ClassID`.  
  
 `pClassId`  
 [out] Wskaźnik do zwracanego `ClassID`.  
  
## <a name="remarks"></a>Uwagi  
 Wartość null `pClassId` wskazuje, że `objectId` ma typ, który jest zwolnienie.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf.idl, CorProf.h  
  
 **Biblioteka:** CorGuids.lib  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo, interfejs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
