---
title: IMetaDataEmit::SetPinvokeMap — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetPinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetPinvokeMap
helpviewer_keywords:
- IMetaDataEmit::SetPinvokeMap method [.NET Framework metadata]
- SetPinvokeMap method [.NET Framework metadata]
ms.assetid: c6bfd574-1da3-4ba7-82f2-46ca5efcbaba
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5a6fd0a9ae798fa5071d9b4b9fac1f8b3c759a20
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750872"
---
# <a name="imetadataemitsetpinvokemap-method"></a>IMetaDataEmit::SetPinvokeMap — Metoda
Ustawia lub zmienia funkcji PInvoke sygnatury metody, zgodnie z wcześniejszym wywołaniu [IMetaDataEmit::DefinePinvokeMap](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definepinvokemap-method.md).  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetPinvokeMap (   
    [in]  mdToken      tk,   
    [in]  DWORD        dwMappingFlags,  
    [in]  LPCWSTR      szImportName,   
    [in]  mdModuleRef  mrImportDLL   
);  
```  
  
## <a name="parameters"></a>Parametry  
 `tk`  
 [in] `mdToken` Do mapowania, które informacje mają zastosowanie.  
  
 `dwMappingFlags`  
 [in] Flagi używane przez PInvoke do na potrzeby mapowania. Jest to z `CorPinvokeMap` wartości.  
  
 `szImportName`  
 [in] Nazwa elementu docelowego eksportu w natywnej biblioteki DLL.  
  
 `mrImportDLL`  
 [in] `mdModuleRef` Tokenu dla obiektu docelowego niezarządzanych bibliotek DLL.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** COR.h  
  
 **Biblioteka:** Używany jako zasób w MSCorEE.dll  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataEmit, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
