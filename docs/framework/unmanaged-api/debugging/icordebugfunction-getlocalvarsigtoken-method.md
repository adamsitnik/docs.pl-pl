---
title: ICorDebugFunction::GetLocalVarSigToken — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetLocalVarSigToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetLocalVarSigToken
helpviewer_keywords:
- ICorDebugFunction::GetLocalVarSigToken method [.NET Framework debugging]
- GetLocalVarSigToken method [.NET Framework debugging]
ms.assetid: 31e53494-bcc9-4981-91a4-f7e0f02cad48
topic_type:
- apiref
ms.openlocfilehash: c159a175ddd380015cc2dc21637c8b63fd3caea6
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73137898"
---
# <a name="icordebugfunctiongetlocalvarsigtoken-method"></a>ICorDebugFunction::GetLocalVarSigToken — Metoda
Pobiera token metadanych dla zmiennej lokalnej sygnatury funkcji reprezentowanej przez to wystąpienie ICorDebugFunction.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetLocalVarSigToken (  
    [out] mdSignature *pmdSig  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `pmdSig`  
 określoną Wskaźnik do `mdSignature` token dla zmiennej lokalnej tej funkcji lub `mdSignatureNil`, jeśli ta funkcja nie ma zmiennych lokalnych.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
