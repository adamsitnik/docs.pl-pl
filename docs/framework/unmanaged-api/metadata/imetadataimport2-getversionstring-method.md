---
title: IMetaDataImport2::GetVersionString — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetVersionString
helpviewer_keywords:
- GetVersionString method, IMetaDataImport2 interface [.NET Framework metadata]
- IMetaDataImport2::GetVersionString method [.NET Framework metadata]
ms.assetid: 308183ee-fd44-4432-9d86-ef00d181b49b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d500584afd608f79e41e932be259d29ae51db2db
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781585"
---
# <a name="imetadataimport2getversionstring-method"></a>IMetaDataImport2::GetVersionString — Metoda
Pobiera numer wersji środowiska uruchomieniowego, który został użyty do tworzenia zestawu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetVersionString (  
   [out] LPWSTR      pwzBuf,  
   [in]  DWORD       ccBufSize,  
   [out] DWORD       *pccBufSize  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `pwzBuf`  
 [out] Tablica do przechowywania ciąg, który określa numer wersji.  
  
 `ccBufSize`  
 [in] Rozmiar w szerokich znaków z `pwzBuf` tablicy.  
  
 `pccBufSize`  
 [out] Liczba znaków dwubajtowych, łącznie z terminatorem null, jest zwracany w `pwzBuf` tablicy.  
  
## <a name="remarks"></a>Uwagi  
 `GetVersionString` Metoda pobiera wersję utworzone dla bieżącego zakresu metadanych. Jeśli nigdy nie został zapisany zakresu, nie zostaną utworzone dla wersji i zostanie zwrócony pusty ciąg.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** COR.h  
  
 **Biblioteka:** Używany jako zasób w MsCorEE.dll  
  
 **Wersje programu .NET framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport2, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
- [IMetaDataImport, interfejs](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
