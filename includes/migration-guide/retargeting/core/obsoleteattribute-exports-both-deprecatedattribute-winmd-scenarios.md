---
ms.openlocfilehash: e8c48c4b1031813ce62f576e5bf1f94c082dfe4b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62091696"
---
### <a name="obsoleteattribute-exports-as-both-obsoleteattribute-and-deprecatedattribute-in-winmd-scenarios"></a>ObsoleteAttribute eksportuje zarówno jako ObsoleteAttribute i DeprecatedAttribute w scenariuszach WinMD

|   |   |
|---|---|
|Szczegóły|Podczas tworzenia biblioteki metadanych Windows (plik winmd), <xref:System.ObsoleteAttribute?displayProperty=name> atrybutu są eksportowane jako <xref:System.ObsoleteAttribute?displayProperty=name> i [Windows.Foundation.DeprecatedAttribute](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.deprecatedattribute).|
|Sugestia|Ponowna kompilacja elementu istniejący kod źródłowy, który używa <xref:System.ObsoleteAttribute?displayProperty=name> atrybut może generować ostrzeżenia podczas korzystania z tego kodu z C++/CX lub JavaScript.We nie zaleca się stosowanie zarówno <xref:System.ObsoleteAttribute?displayProperty=name> i [ Windows.Foundation.DeprecatedAttribute](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.deprecatedattribute) kodem w zarządzanych zestawów; może to spowodować ostrzeżenia kompilacji.|
|Zakres|Krawędź|
|Wersja|4.5.1|
|Typ|Przekierowanie|
