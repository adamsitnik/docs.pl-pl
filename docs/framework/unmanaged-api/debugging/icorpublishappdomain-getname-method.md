---
title: ICorPublishAppDomain::GetName — Metoda
ms.date: 03/30/2017
api_name:
- ICorPublishAppDomain.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishAppDomain::GetName
helpviewer_keywords:
- GetName method, ICorPublishAppDomain interface [.NET Framework debugging]
- ICorPublishAppDomain::GetName method [.NET Framework debugging]
ms.assetid: 6ef8ac9b-9803-4b65-8b13-25f3e0b1bc6b
topic_type:
- apiref
ms.openlocfilehash: 2f91891164f1f80617cab10347eb4a7a08762c10
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140351"
---
# <a name="icorpublishappdomaingetname-method"></a>ICorPublishAppDomain::GetName — Metoda
Pobiera nazwę domeny aplikacji reprezentowanej przez ten [ICorPublishAppDomain](../../../../docs/framework/unmanaged-api/debugging/icorpublishappdomain-interface.md).  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetName (  
    [in]  ULONG32   cchName,   
    [out] ULONG32   *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]   
        WCHAR       *szName  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `cchName`  
 podczas Rozmiar tablicy `szName`.  
  
 `pcchName`  
 określoną Wskaźnik do liczby znaków dwubajtowych, w tym znak null, zwracany w tablicy `szName`.  
  
 `szName`  
 określoną Tablica, w której ma zostać przechowana nazwa.  
  
## <a name="remarks"></a>Uwagi  
 Jeśli `szName` ma wartość różną od null, Metoda `GetName` kopiuje do `szName`znaki `cchName` (w tym terminator wartości null). Jeśli w `pcchName`jest zwracana wartość inna niż null, rzeczywista liczba znaków w nazwie (łącznie z terminatorem wartości null) jest przechowywana w tablicy `szName`.  
  
 Metoda `GetName` zwraca wartość HRESULT S_OK, niezależnie od liczby skopiowanych znaków.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorPub. idl, CorPub. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorPublishAppDomain, interfejs](../../../../docs/framework/unmanaged-api/debugging/icorpublishappdomain-interface.md)
