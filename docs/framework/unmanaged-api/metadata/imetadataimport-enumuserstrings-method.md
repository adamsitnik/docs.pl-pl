---
title: IMetaDataImport::EnumUserStrings — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumUserStrings
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumUserStrings
helpviewer_keywords:
- IMetaDataImport::EnumUserStrings method [.NET Framework metadata]
- EnumUserStrings method [.NET Framework metadata]
ms.assetid: 2b1f1418-4be8-4cdb-b418-b3abccc527a7
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ea144784f82c192f41f68394eb2ccdf443db54c2
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782553"
---
# <a name="imetadataimportenumuserstrings-method"></a>IMetaDataImport::EnumUserStrings — Metoda
Wylicza tokenów ciąg reprezentujący zakodowane sprzętowo ciągi w bieżącym zakresie metadanych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT EnumUserStrings (  
   [in, out]  HCORENUM    *phEnum,  
   [out]  mdString        rStrings[],  
   [in]   ULONG           cMax,  
   [out]  ULONG           *pcStrings  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `phEnum`  
 [out w] Wskaźnik do modułu wyliczającego. Musi to być wartość NULL dla pierwszego wywołania tej metody.  
  
 `rStrings`  
 [out] Tablica do przechowywania tokenów ciąg.  
  
 `cMax`  
 [in] Maksymalny rozmiar `rStrings` tablicy.  
  
 `pcStrings`  
 [out] Liczba tokenów ciąg zwracany w `rStrings`.  
  
## <a name="return-value"></a>Wartość zwracana  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|`S_OK`|`EnumUserStrings` pomyślnie zwrócił.|  
|`S_FALSE`|Nie ma żadnych tokeny do wyliczenia. W takim przypadku `pcStrings` wynosi zero.|  
  
## <a name="remarks"></a>Uwagi  
 Tokeny ciągu są tworzone przez [IMetaDataEmit::DefineUserString](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineuserstring-method.md) metody. Ta metoda jest przeznaczona do użycia przez przeglądarkę metadanych, a nie przez kompilator.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** COR.h  
  
 **Biblioteka:** Dołączony jako zasób w MsCorEE.dll  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
