---
title: ImportFile — Metoda
ms.date: 03/30/2017
api_name:
- IALink.ImportFile
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportFile
helpviewer_keywords:
- ImportFile method
ms.assetid: bcbe321f-b83a-4e9a-9f10-8d913e244dc9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f7fee7a91de99e2db69609cbc7c73e22d85d045f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70777063"
---
# <a name="importfile-method"></a>ImportFile — Metoda
Importuje zestawy i niepowiązane moduły.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT ImportFile(  
    LPCWSTR pszFilename,  
    LPCWSTR pszTargetName,  
    BOOL fSmartImport,  
    mdToken* pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD* pdwCountOfScopes  
) PURE;  
```  
  
## <a name="parameters"></a>Parametry  
 `pszFilename`  
 W pełni kwalifikowana nazwa pliku do zaimportowania.  
  
 `pszTargetName`  
 Opcjonalna nazwa pliku wyjściowego, która może zostać użyta do zmiany nazwy pliku, ponieważ jest on połączony z zestawem.  
  
 `fSmartImport`  
 Jeśli wartość jest równa TRUE, używane są wartości, w przeciwnym razie importowanie należy wykonać ręcznie.  
  
 `pImportToken`  
 Wskaźnik do tokenu, w którym będzie przechowywany unikatowy identyfikator pliku. Plik może być zestawem lub plikiem.  
  
 `ppAssemblyScope`  
 Odbiera wskaźnik do [interfejsu IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md). Może mieć wartość NULL, jeśli plik nie jest zestawem.  
  
 `pdwCountOfScopes`  
 Wskaźnik do liczby zaimportowanych plików i/lub zakresów.  
  
## <a name="return-value"></a>Wartość zwracana  
 Zwraca S_OK, jeśli metoda zakończy się pomyślnie.  
  
## <a name="requirements"></a>Wymagania  
 Wymaga Alink. h  
  
## <a name="see-also"></a>Zobacz także

- [IALink, interfejs](ialink-interface.md)
- [IALink2, interfejs](ialink2-interface.md)
- [ALink, interfejs API](index.md)
