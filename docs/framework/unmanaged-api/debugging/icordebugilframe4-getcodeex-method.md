---
title: Metoda ICorDebugILFrame4::GetCodeEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetLocalVariableEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: aeda0e42-29ee-4ca8-9f21-ac4641677a62
topic_type:
- apiref
ms.openlocfilehash: 9a74fd64e046ab3a8943e9a975e4de808c662677
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73090957"
---
# <a name="icordebugilframe4getcodeex-method"></a>Metoda ICorDebugILFrame4::GetCodeEx
[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]  
  
 Pobiera wskaźnik do kodu, który jest wykonywany przez tę ramkę stosu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp
HRESULT GetCodeEx(  
   [in] ILCodeKind flags,   
   [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `flags`  
 podczas Element członkowski wyliczenia [ILCodeKind](../../../../docs/framework/unmanaged-api/debugging/ilcodekind-enumeration.md) , który określa, czy język pośredni (IL) zdefiniowany przez żądanie ReJIT profilera zostanie uwzględniony w ramce.  
  
 `ppCode`  
 określoną Wskaźnik do adresu obiektu "ICorDebugCode", który reprezentuje kod, który jest wykonywany przez tę ramkę stosu.  
  
## <a name="remarks"></a>Uwagi  
 Ta metoda jest podobna do metody [ICorDebugFrame:: GetCode](../../../../docs/framework/unmanaged-api/debugging/icordebugframe-getcode-method.md) , z tą różnicą, że opcjonalnie uzyskuje dostęp do kodu zdefiniowanego przez żądanie ReJIT profilera. Wywołanie tej metody z `flags` wartością `ILCODE_ORIGINAL_IL` jest równoważne wywołaniu metody [GetCode](../../../../docs/framework/unmanaged-api/debugging/icordebugframe-getcode-method.md); Jeśli metoda jest Instrumentacją, jej kod IL nie będzie dostępny. `ILCODE_REJIT_IL` zezwala debugerowi na dostęp do IL zdefiniowanego przez żądanie ReJIT profilera. Jeśli IL nie ma instrumentacji, `ppCode` ma **wartość null**, a metoda zwraca `S_OK`.  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugILFrame4, interfejs](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-interface.md)
- [Debugowanie, interfejsy](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [ReJIT: Przewodnik po poradniku](https://blogs.msdn.microsoft.com/davbr/2011/10/12/rejit-a-how-to-guide/)
