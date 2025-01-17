---
title: _CorExeMain — Funkcja
ms.date: 03/30/2017
api_name:
- _CorExeMain
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- _CorExeMain
helpviewer_keywords:
- _CorExeMain function [.NET Framework hosting]
ms.assetid: 898f76e2-16f4-4a63-b7d9-dad2d3824d8a
topic_type:
- apiref
ms.openlocfilehash: 8541e7761e2f8e1839d028fdaea3eb71307ba615
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73131199"
---
# <a name="_corexemain-function"></a>_CorExeMain — Funkcja
Inicjuje środowisko uruchomieniowe języka wspólnego (CLR), lokalizuje zarządzany punkt wejścia w nagłówku CLR zestawu wykonywalnego i rozpoczyna wykonywanie.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
__int32 STDMETHODCALLTYPE _CorExeMain ();  
```  
  
## <a name="remarks"></a>Uwagi  
 Ta funkcja jest wywoływana przez moduł ładujący w ramach procesów utworzonych z zarządzanych zestawów plików wykonywalnych. W przypadku zestawów bibliotek DLL moduł ładujący wywołuje funkcję [_CorDllMain](../../../../docs/framework/unmanaged-api/hosting/cordllmain-function.md) .  
  
 Moduł ładujący systemu operacyjnego wywołuje tę metodę niezależnie od punktu wejścia określonego w pliku obrazu.  
  
 W systemach Windows 98, Windows ME, Windows NT i Windows 2000 funkcja `_CorExeMain` jest wywoływana pośrednio przez korektę w module ładującym systemu operacyjnego. We wszystkich innych wersjach systemu Windows jest on wywoływany bezpośrednio przez program ładujący systemu operacyjnego.  
  
 Aby uzyskać dodatkowe informacje, zobacz sekcję Uwagi w temacie [_CorValidateImage](../../../../docs/framework/unmanaged-api/hosting/corvalidateimage-function.md) .  
  
## <a name="requirements"></a>Wymagania  
 **Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Uwzględnione jako zasób w bibliotece MsCorEE. dll  
  
 **Wersje .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Statyczne funkcje globalne metadanych](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
