---
title: ICLRStrongName::StrongNameTokenFromAssembly — Metoda
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameTokenFromAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly
helpviewer_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly method [.NET Framework hosting]
- StrongNameTokenFromAssembly method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: fc725afb-b66b-4015-aa44-1c0d1304197f
topic_type:
- apiref
ms.openlocfilehash: 0e7e49fae24ff7e12c5a8d9cac5e814f7a7ae813
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73092593"
---
# <a name="iclrstrongnamestrongnametokenfromassembly-method"></a>ICLRStrongName::StrongNameTokenFromAssembly — Metoda
Tworzy token silnej nazwy z określonego pliku zestawu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT StrongNameTokenFromAssembly (  
    [in]  LPCWSTR   wszFilePath,  
    [out] BYTE      **ppbStrongNameToken,  
    [out] ULONG     *pcbStrongNameToken  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `wszFilePath`  
 podczas Ścieżka do przenośnego pliku wykonywalnego (PE) dla zestawu.  
  
 `ppbStrongNameToken`  
 określoną Zwrócony token silnej nazwy.  
  
 `pcbStrongNameToken`  
 określoną Rozmiar (w bajtach) tokenu silnej nazwy.  
  
## <a name="return-value"></a>Wartość zwracana  
 `S_OK`, jeśli metoda została ukończona pomyślnie; w przeciwnym razie wartość HRESULT wskazująca niepowodzenie (zobacz [typowe wartości HRESULT](https://go.microsoft.com/fwlink/?LinkId=213878) dla listy).  
  
## <a name="remarks"></a>Uwagi  
 Token silnej nazwy to skrócona postać klucza publicznego. Token jest 64-bitowym skrótem, który jest tworzony na podstawie klucza publicznego używanego do podpisywania zestawu. Token jest częścią silnej nazwy zestawu i można go odczytać z metadanych zestawu.  
  
 Po utworzeniu tokenu należy wywołać metodę [ICLRStrongName:: StrongNameFreeBuffer —](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) , aby zwolnić przydzieloną pamięć.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** Obiekt ServiceHost. h  
  
 **Biblioteka:** Uwzględnione jako zasób w bibliotece MSCorEE. dll  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [StrongNameTokenFromAssemblyEx, metoda](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfromassemblyex-method.md)
- [ICLRStrongName, interfejs](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
