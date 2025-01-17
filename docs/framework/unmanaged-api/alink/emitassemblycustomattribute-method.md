---
title: EmitAssemblyCustomAttribute — Metoda
ms.date: 03/30/2017
api_name:
- IALink.EmitAssemblyCustomAttribute
- EmitAssemblyCustomAttribute
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EmitAssemblyCustomAttribute
helpviewer_keywords:
- EmitAssemblyCustomAttribute method
ms.assetid: b72f5409-79af-4fa7-90a7-7630eec170f1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 77d54f6c8f67dda5132518d1fbd579a91ce82071
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70777440"
---
# <a name="emitassemblycustomattribute-method"></a>EmitAssemblyCustomAttribute — Metoda
Wywołanie ustawiania atrybutów niestandardowych na poziomie zestawu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT EmitAssemblyCustomAttribute(  
    mdAssembly   AssemblyID,  
    mdToken      FileToken,  
    mdToken      tkType,  
    void const*  pCustomValue,  
    DWORD        cbCustomValue,  
    BOOL         bSecurity,  
    BOOL         bAllowMulti  
) PURE;  
```  
  
## <a name="parameters"></a>Parametry  
 `AssemblyID`  
 Identyfikator zestawu.  
  
 `FileToken`  
 Plik, który deplikuje atrybut. Może mieć wartość null `AssemblyID` , jeśli nie wskazuje niepowiązanego modułu.  
  
 `tkType`  
 Typ atrybutu niestandardowego.  
  
 `pCustomValue`  
 Dane wartości niestandardowej.  
  
 `cbCustomValue`  
 Długość danych wartości niestandardowych.  
  
 `bSecurity`  
 Ma wartość TRUE, jeśli atrybut niestandardowy jest powiązany z podpisywaniem zestawu.  
  
 `bAllowMulti`  
 Ma wartość TRUE, jeśli wiele atrybutów ma być emitowanych.  
  
## <a name="return-value"></a>Wartość zwracana  
 Zwraca S_OK, jeśli metoda zakończy się pomyślnie.  
  
## <a name="requirements"></a>Wymagania  
 Wymaga Alink. h  
  
## <a name="see-also"></a>Zobacz także

- [IALink, interfejs](ialink-interface.md)
- [IALink2, interfejs](ialink2-interface.md)
- [ALink, interfejs API](index.md)
