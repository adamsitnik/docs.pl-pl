---
title: IMetaDataImport::GetMethodProps — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMethodProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMethodProps
helpviewer_keywords:
- GetMethodProps method [.NET Framework metadata]
- IMetaDataImport::GetMethodProps method [.NET Framework metadata]
ms.assetid: e0667ef7-1d31-4c89-a2d3-d426f023f8d2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 27b2867019085bf5b44f2ee364c07af66144d4b5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782327"
---
# <a name="imetadataimportgetmethodprops-method"></a>IMetaDataImport::GetMethodProps — Metoda
Pobiera metadane skojarzone z metody odwołuje się określona MethodDef token.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetMethodProps (  
    [in]  mdMethodDef         mb,  
    [out] mdTypeDef           *pClass,  
    [out] LPWSTR              szMethod,  
    [in]  ULONG               cchMethod,  
    [out] ULONG               *pchMethod,  
    [out] DWORD               *pdwAttr,  
    [out] PCCOR_SIGNATURE     *ppvSigBlob,  
    [out] ULONG               *pcbSigBlob,  
    [out] ULONG               *pulCodeRVA,  
    [out] DWORD               *pdwImplFlags  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `mb`  
 [in] Token MethodDef, który reprezentuje metodę, można zwrócić metadanych dla.  
  
 `pClass`  
 [out] Wskaźnik do TypeDef token, który reprezentuje typ, który implementuje metodę.  
  
 `szMethod`  
 [out] Wskaźnik do buforu, który ma nazwę metody.  
  
 `cchMethod`  
 [in] Żądany rozmiar `szMethod`.  
  
 `pchMethod`  
 [out] Wskaźnik do rozmiaru znaków `szMethod`, lub w przypadku obcinania, rzeczywista liczba znaków dwubajtowych w polu Nazwa metody.  
  
 `pdwAttr`  
 [out] Wskaźnik flagi, powiązany z metodą.  
  
 `ppvSigBlob`  
 [out] Wskaźnik do binarnych metadanych podpis metody.  
  
 `pcbSigBlob`  
 [out] Wskaźnik do rozmiar w bajtach `ppvSigBlob`.  
  
 `pulCodeRVA`  
 [out] Wskaźnik do wirtualnej adres względny metody.  
  
 `pdwImplFlags`  
 [out] Wskaźnik do flag implementacji metody.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** COR.h  
  
 **Biblioteka:** Dołączony jako zasób w MsCorEE.dll  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
