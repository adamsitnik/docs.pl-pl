---
title: ICLRStrongName::StrongNameKeyGenEx — Metoda
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameKeyGenEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameKeyGenEx
helpviewer_keywords:
- ICLRStrongName::StrongNameKeyGenEx method [.NET Framework hosting]
- StrongNameKeyGenEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 1f8b59d0-5b72-45b8-ab74-c2b43ffc806e
topic_type:
- apiref
ms.openlocfilehash: 1a5bcfb7a272af694126025f28ca3efe5a881c15
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73135018"
---
# <a name="iclrstrongnamestrongnamekeygenex-method"></a>ICLRStrongName::StrongNameKeyGenEx — Metoda
Generuje nową parę kluczy publicznych/prywatnych z określonym rozmiarem klucza w celu użycia silnej nazwy.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT StrongNameKeyGenEx (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  DWORD     dwFlags,  
    [in]  DWORD     dwKeySize,  
    [out] BYTE      **ppbKeyBlob,  
    [out] ULONG     *pcbKeyBlob  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `wszKeyContainer`  
 podczas Nazwa żądanego kontenera kluczy. `wszKeyContainer` musi być niepustym ciągiem lub wartością null w celu wygenerowania nazwy tymczasowej.  
  
 `dwFlags`  
 podczas Wartość określająca, czy klucz ma pozostać zarejestrowany. Obsługiwane są następujące wartości:  
  
- 0x00000000 — używany, gdy `wszKeyContainer` ma wartość null w celu wygenerowania nazwy kontenera kluczy tymczasowych.  
  
- 0x00000001 (`SN_LEAVE_KEY`) — określa, że klucz powinien pozostać zarejestrowany.  
  
 `dwKeySize`  
 podczas Żądany rozmiar klucza w bitach.  
  
 `ppbKeyBlob`  
 określoną Zwracana para kluczy publiczny/prywatny.  
  
 `pcbKeyBlob`  
 określoną Rozmiar w bajtach `ppbKeyBlob`.  
  
## <a name="return-value"></a>Wartość zwracana  
 `S_OK`, jeśli metoda została ukończona pomyślnie; w przeciwnym razie wartość HRESULT wskazująca niepowodzenie (zobacz [typowe wartości HRESULT](https://go.microsoft.com/fwlink/?LinkId=213878) dla listy).  
  
## <a name="remarks"></a>Uwagi  
 .NET Framework wersje 1,0 i 1,1 wymagają `dwKeySize` 1024 BITS do podpisania zestawu silną nazwą; w wersji 2,0 dodano obsługę kluczy 2048-bitowych.  
  
 Po pobraniu klucza należy wywołać metodę [ICLRStrongName:: StrongNameFreeBuffer —](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) , aby zwolnić przydzieloną pamięć.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** Obiekt ServiceHost. h  
  
 **Biblioteka:** Uwzględnione jako zasób w bibliotece MSCorEE. dll  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [StrongNameKeyGen, metoda](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeygen-method.md)
- [ICLRStrongName, interfejs](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
