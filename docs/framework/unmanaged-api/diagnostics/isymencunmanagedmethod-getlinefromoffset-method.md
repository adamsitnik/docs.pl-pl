---
title: ISymENCUnmanagedMethod::GetLineFromOffset — Metoda
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetLineFromOffset
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetLineFromOffset
helpviewer_keywords:
- GetLineFromOffset method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetLineFromOffset method [.NET Framework debugging]
ms.assetid: cc09bad2-fb34-4d13-a521-6ec7b1a1d915
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b669921bf8d27283ba99f4ca1d97b6abc00e15db
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776887"
---
# <a name="isymencunmanagedmethodgetlinefromoffset-method"></a>ISymENCUnmanagedMethod::GetLineFromOffset — Metoda
Pobiera informacje o wiersz skojarzony z przesunięcia. Jeśli parametr offset (`dwOffset`) nie jest punktem sekwencji, ta metoda pobiera informacje o wiersz skojarzony z poprzednim przesunięcie.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetLineFromOffset(  
     [in]  ULONG32   dwOffset,  
     [out] ULONG32*  pline,  
     [out] ULONG32*  pcolumn,  
     [out] ULONG32*  pendLine,  
     [out] ULONG32*  pendColumn,  
     [out] ULONG32*  pdwStartOffset);  
```  
  
## <a name="parameters"></a>Parametry  
 `dwOffset`  
 [in] Element `ULONG32` zawiera przesunięcie.  
  
 `pline`  
 [out] Wskaźnik do `ULONG32` odbierająca wiersza.  
  
 `pcolumn`  
 [out] Wskaźnik do `ULONG32` kolumny, która otrzymuje.  
  
 `pendLine`  
 [out] Wskaźnik do `ULONG32` odbierająca zakończyć wiersza.  
  
 `pendColumn`  
 [out] Wskaźnik do `ULONG32` końcowa kolumny, która otrzymuje.  
  
 `pdwStartOffset`  
 [out] Wskaźnik do `ULONG32` odbierająca punktu sekwencji skojarzone.  
  
## <a name="return-value"></a>Wartość zwracana  
 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub innego kodu błędu.  
  
## <a name="requirements"></a>Wymagania  
 **Nagłówek:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Zobacz także

- [ISymENCUnmanagedMethod, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-interface.md)
