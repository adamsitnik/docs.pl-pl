---
ms.openlocfilehash: 384f8c7fa08b69c13d05edb3404787d428dad837
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61640052"
---
### <a name="stack-traces-obtained-when-using-portable-pdbs-now-include-source-file-and-line-information-if-requested"></a>Ślady stosu uzyskane podczas przy użyciu przenośnych plików PDB teraz obejmować informacje o pliku i wiersza źródłowego, jeśli jest to wymagane

|   |   |
|---|---|
|Szczegóły|Począwszy od .NET Framework 4.7.2 ślady stosu, uzyskanych przy użyciu przenośnych plików PDB obejmują źródło pliku i wierszu informacji żądanie. W wersjach wcześniejszych niż .NET Framework 4.7.2, plik źródłowy i wiersza informacji będzie niedostępne podczas przy użyciu przenośnych plików PDB, nawet wtedy, gdy wyraźnie wymagane.|
|Sugestia|W przypadku aplikacji przeznaczonych dla platformy .NET Framework 4.7.2 można zrezygnować z informacje o pliku i wierszu źródła przy użyciu przenośnych plików PDB, jeśli nie jest pożądane, dodając następujące polecenie, aby <code>&lt;runtime&gt;</code> części Twojej <code>app.config</code> pliku:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Diagnostics.IgnorePortablePDBsInStackTraces=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Dla aplikacji przeznaczonych dla wcześniejszych wersji programu .NET Framework jednak uruchomić w środowisku .NET Framework 4.7.2 lub później, można włączyć do informacji o pliku i wierszu źródła przy użyciu przenośnych plików PDB, dodając następujące polecenie, aby <code>&lt;runtime&gt;</code> części Twojej <code>app.config</code>pliku:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Diagnostics.IgnorePortablePDBsInStackTraces=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Zakres|Krawędź|
|Wersja|4.7.2|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.Diagnostics.StackTrace.%23ctor(System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.StackTrace.%23ctor(System.Exception,System.Boolean)?displayProperty=nameWithType><li><xref:System.Diagnostics.StackTrace.%23ctor(System.Exception,System.Int32,System.Boolean)?displayProperty=nameWithType></li></ul>|
