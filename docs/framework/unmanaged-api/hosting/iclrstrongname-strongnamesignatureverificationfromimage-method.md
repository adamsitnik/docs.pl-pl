---
title: ICLRStrongName::StrongNameSignatureVerificationFromImage — Metoda
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerificationFromImage
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerificationFromImage
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureVerificationFromImage method [.NET Framework hosting]
- StrongNameSignatureVerificationFromImage method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: da91c138-ee30-4fd4-a040-464d97d7e41a
topic_type:
- apiref
ms.openlocfilehash: adb3b4e33edafe6d25c8259e316a9b62e339f896
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73092668"
---
# <a name="iclrstrongnamestrongnamesignatureverificationfromimage-method"></a>ICLRStrongName::StrongNameSignatureVerificationFromImage — Metoda
Sprawdza, czy zestaw, który został już zamapowany na pamięć, jest prawidłowy dla skojarzonego klucza publicznego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT StrongNameSignatureVerificationFromImage (  
    [in]  BYTE    *pbBase,  
    [in]  DWORD   dwLength,  
    [in]  DWORD   dwInFlags,  
    [out] DWORD   *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `pbBase`  
 podczas Względny adres wirtualny zamapowanego manifestu zestawu.  
  
 `dwLength`  
 podczas Rozmiar zamapowanego obrazu w bajtach.  
  
 `dwInFlags`  
 podczas Flagi wpływające na zachowanie weryfikacji. Obsługiwane są następujące wartości:  
  
- `SN_INFLAG_FORCE_VER` (0x00000001) — wymusza weryfikację, nawet jeśli jest konieczna przesłonięcie ustawień rejestru.  
  
- `SN_INFLAG_INSTALL` (0x00000002) — określa, że jest to pierwsza weryfikacja wykonywana na tym obrazie.  
  
- `SN_INFLAG_ADMIN_ACCESS` (0x00000004) — określa, że pamięć podręczna będzie zezwalać na dostęp tylko użytkownikom z uprawnieniami administracyjnymi.  
  
- `SN_INFLAG_USER_ACCESS` (0x00000008) — określa, że zestaw będzie dostępny tylko dla bieżącego użytkownika.  
  
- `SN_INFLAG_ALL_ACCESS` (0x00000010) — określa, że pamięć podręczna nie będzie zapewniać żadnych gwarancji ograniczenia dostępu.  
  
- `SN_INFLAG_RUNTIME` (0x80000000) — zarezerwowane na potrzeby debugowania wewnętrznego.  
  
 `pdwOutFlags`  
 określoną Flaga dodatkowych informacji wyjściowych. Obsługiwana jest następująca wartość:  
  
- `SN_OUTFLAG_WAS_VERIFIED` (0x00000001) — ta wartość jest ustawiona na `false`, aby określić, że weryfikacja powiodła się z powodu ustawień rejestru.  
  
## <a name="return-value"></a>Wartość zwracana  
 `S_OK`, jeśli metoda została ukończona pomyślnie; w przeciwnym razie wartość HRESULT wskazująca niepowodzenie (zobacz [typowe wartości HRESULT](https://go.microsoft.com/fwlink/?LinkId=213878) dla listy).  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** Obiekt ServiceHost. h  
  
 **Biblioteka:** Uwzględnione jako zasób w bibliotece MSCorEE. dll  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRStrongName, interfejs](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
