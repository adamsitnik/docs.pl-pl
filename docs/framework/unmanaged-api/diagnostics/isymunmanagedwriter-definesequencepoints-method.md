---
title: ISymUnmanagedWriter::DefineSequencePoints — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineSequencePoints
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineSequencePoints
helpviewer_keywords:
- DefineSequencePoints method [.NET Framework debugging]
- ISymUnmanagedWriter::DefineSequencePoints method [.NET Framework debugging]
ms.assetid: 64202baf-be6b-40ba-8162-8cc6c0c9b8e1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f07685351425a4685ac4a0c8e1b8e3c198b14187
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777300"
---
# <a name="isymunmanagedwriterdefinesequencepoints-method"></a>ISymUnmanagedWriter::DefineSequencePoints — Metoda
Definiuje grupę punktów sekwencji w bieżącej metodzie. Każda linia początkowa i kolumnę początkową definiują rozpoczęcia instrukcji wewnątrz metody. Zakończenie każdego wiersza i zakończenie kolumnę zdefiniuj końca instrukcji wewnątrz metody. Tablice powinny być sortowane rosnąco przesunięcia. Przesunięcie zawsze jest mierzony od początku metody, w bajtach.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT DefineSequencePoints(  
    [in] ISymUnmanagedDocumentWriter*  document,  
    [in] ULONG32 spCount,  
    [in, size_is(spCount)] ULONG32     offsets[],  
    [in, size_is(spCount)] ULONG32     lines[],  
    [in, size_is(spCount)] ULONG32     columns[],  
    [in, size_is(spCount)] ULONG32     endLines[],  
    [in, size_is(spCount)] ULONG32     endColumns[]);  
```  
  
## <a name="parameters"></a>Parametry  
 `document`  
 [in] Obiekt dokumentu, dla której są zdefiniowane punktów sekwencji.  
  
 `spCount`  
 [in] A `ULONG32` oznacza to rozmiar wszystkich `offsets`, `lines`, `columns`, `endLines`, i `endColumns` buforów.  
  
 `offsets`  
 [in] Przesunięcie punktów sekwencji jest mierzony od początku metody.  
  
 `lines`  
 [in] Linia początkowa liczby punktów sekwencji.  
  
 `columns`  
 [in] Począwszy od liczby kolumn punktów sekwencji.  
  
 `endLines`  
 [in] Końcowy numery wierszy punktów sekwencji. Ten parametr jest opcjonalny.  
  
 `endColumns`  
 [in] Końcowej kolumny liczby punktów sekwencji. Ten parametr jest opcjonalny.  
  
## <a name="return-value"></a>Wartość zwracana  
 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub innego kodu błędu.  
  
## <a name="requirements"></a>Wymagania  
 **Nagłówek:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Zobacz także

- [ISymUnmanagedWriter, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)
