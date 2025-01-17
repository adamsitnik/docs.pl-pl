---
title: ICorDebugModule2::ApplyChanges — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ApplyChanges
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ApplyChanges
helpviewer_keywords:
- ApplyChanges method [.NET Framework debugging]
- ICorDebugModule2::ApplyChanges method [.NET Framework debugging]
ms.assetid: 96fa3406-6a6f-41a1-88c6-d9bc5d1a16d1
topic_type:
- apiref
ms.openlocfilehash: c324019e1e62701f4f2aaba1c00948b292ba6847
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73127911"
---
# <a name="icordebugmodule2applychanges-method"></a>ICorDebugModule2::ApplyChanges — Metoda
Stosuje zmiany w metadanych i zmiany w kodzie języka pośredniego firmy Microsoft (MSIL) do uruchomionego procesu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT ApplyChanges (  
    [in] ULONG                       cbMetadata,  
    [in, size_is(cbMetadata)] BYTE   pbMetadata[],  
    [in] ULONG                       cbIL,  
    [in, size_is(cbIL)] BYTE         pbIL[]  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `cbMetadata`  
 podczas Rozmiar metadanych różnicowych w bajtach.  
  
 `pbMetadata`  
 podczas Bufor zawierający metadane różnicowe. Adres buforu jest zwracany z metody [IMetaDataEmit2:: SaveDeltaToMemory —](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md) .  
  
 Względne adresy wirtualne (RVA) w metadanych powinny być względne względem początku kodu MSIL.  
  
 `cbIL`  
 podczas Rozmiar (w bajtach) różnicowego kodu MSIL.  
  
 `pbIL`  
 podczas Bufor zawierający zaktualizowany kod MSIL.  
  
## <a name="remarks"></a>Uwagi  
 Parametr `pbMetadata` jest w specjalnym formacie metadanych różnicowych (jako dane wyjściowe przez [IMetaDataEmit2:: SaveDeltaToMemory —](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md)). `pbMetadata` pobiera poprzednie metadane jako podstawowe i opisuje indywidualne zmiany, które mają zastosowanie do tej bazy.  
  
 Z kolei parametr `pbIL[`] zawiera nowe MSIL dla zaktualizowanej metody i ma na celu całkowite zamienienie poprzedniej MSIL dla tej metody  
  
 Po utworzeniu różnicowego MSIL i metadanych w pamięci debugera debuger wywołuje `ApplyChanges`, aby wysłać zmiany do środowiska uruchomieniowego języka wspólnego (CLR). Środowisko uruchomieniowe aktualizuje swoje tabele metadanych, umieszcza nowe MSIL w procesie i konfiguruje kompilację just-in-Time (JIT) nowej MSIL. Po zastosowaniu zmian debuger powinien wywołać [IMetaDataEmit2:: ResetENCLog —](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-resetenclog-method.md) , aby przygotować się do następnej sesji edytowania. Debuger może następnie kontynuować proces.  
  
 Za każdym razem, gdy debuger wywołuje `ApplyChanges` w module, który ma metadane różnicowe, powinien również wywołać [IMetaDataEmit:: ApplyEditAndContinue —](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-applyeditandcontinue-method.md) z tymi samymi metadanymi Delta we wszystkich kopiach metadanych tego modułu, z wyjątkiem kopii użytej do emisji zmian. Jeśli kopia metadanych w jakiś sposób stanie się niezsynchronizowana z rzeczywistymi metadanymi, debuger zawsze może zgłosić tę kopię i uzyskać nową kopię.  
  
 Jeśli metoda `ApplyChanges` nie powiedzie się, sesja debugowania jest w nieprawidłowym stanie i należy ją ponownie uruchomić.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
