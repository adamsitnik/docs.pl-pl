---
title: _EFN_GetManagedObjectFieldInfo — Funkcja
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedObjectFieldInfo
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedObjectFieldInfo
helpviewer_keywords:
- _EFN_GetManagedObjectFieldInfo function [.NET Framework debugging]
ms.assetid: 3b93bcff-62a4-47b2-babc-6bcf4216119a
topic_type:
- apiref
ms.openlocfilehash: b68f24908a5b214d507da8e8a4636a7c55259604
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73123017"
---
# <a name="_efn_getmanagedobjectfieldinfo-function"></a>\_EFN\_funkcja GetManagedObjectFieldInfo
Pobiera przesunięcie od początku obiektu do pola i wartości pola przy użyciu podanego wskaźnika obiektu i nazwy pola.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT _EFN_GetManagedObjectFieldInfo(  
    [in]  PDEBUG_CLIENT Client,  
    [in]  ULONG64       objAddr,  
    [in]  __out_ecount (mdNameLen) PSTR szFieldName,  
    [out] PULONG64      pValue,  
    [out] PULONG        pOffset  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `Client`  
 podczas Wskaźnik do klienta debugowania.  
  
 `objAddr`  
 podczas Wskaźnik obiektu zarządzanego.  
  
 szFieldName  
 podczas Wskaźnik obiektu zarządzanego do nazwy pola.  
  
 `pValue`  
 określoną Wartość pola. Ten parametr może mieć wartość null.  
  
 `pOffset`  
 określoną Przesunięcie od `objAddr` do pola. Ten parametr może mieć wartość null.  
  
## <a name="remarks"></a>Uwagi  
 Jeśli przesunięcie ma wartość 0, przesunięcie nie jest zapisywane.  
  
 W przypadku braku kodu zarządzanego w wątku, który jest obecnie w kontekście, funkcja zwraca wartość HRESULT SOS_E_NOMANAGEDCODE z wartością instrumentu 0xa0 i kod błędu 0x1000.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** SOS_Stacktrace. h  
  
 **Wersja .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie statycznych funkcji globalnych](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)
