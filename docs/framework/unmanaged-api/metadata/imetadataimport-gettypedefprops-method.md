---
title: IMetaDataImport::GetTypeDefProps — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetTypeDefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetTypeDefProps
helpviewer_keywords:
- GetTypeDefProps method [.NET Framework metadata]
- IMetaDataImport::GetTypeDefProps method [.NET Framework metadata]
ms.assetid: 00061a25-ba05-47a7-b984-fd916b06b149
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 77f72fb7eb7b0542dc9a3179811a78b189d6b3b0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778837"
---
# <a name="imetadataimportgettypedefprops-method"></a>IMetaDataImport::GetTypeDefProps — Metoda
Zwraca informacje o metadanych <xref:System.Type> reprezentowany przez określony token TypeDef.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetTypeDefProps (  
   [in]  mdTypeDef   td,  
   [out] LPWSTR      szTypeDef,  
   [in]  ULONG       cchTypeDef,  
   [out] ULONG       *pchTypeDef,  
   [out] DWORD       *pdwTypeDefFlags,  
   [out] mdToken     *ptkExtends  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `td`  
 [in] TypeDef token, który reprezentuje typ, można zwrócić metadanych dla.  
  
 `szTypeDef`  
 [out] Bufor zawierający nazwę typu.  
  
 `cchTypeDef`  
 [in] Rozmiar w znaków `szTypeDef`.  
  
 `pchTypeDef`  
 [out] Liczba znaków dwubajtowych zwracane w `szTypeDef`.  
  
 `pdwTypeDefFlags`  
 [out] Wskaźnik do flag, które modyfikują definicji typu. Ta wartość jest z [cortypeattr —](../../../../docs/framework/unmanaged-api/metadata/cortypeattr-enumeration.md) wyliczenia.  
  
 `ptkExtends`  
 [out] Element TypeDef lub TypeRef metadanych token, który reprezentuje typ podstawowy elementu żądanego typu.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** COR.h  
  
 **Biblioteka:** Dołączony jako zasób w MsCorEE.dll  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
