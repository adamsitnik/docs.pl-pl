---
ms.openlocfilehash: 72f907c117748fb19ca0663f24445a8c978afd32
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2019
ms.locfileid: "68235531"
---
### <a name="cspparametersparentwindowhandle-now-expects-hwnd-value"></a>CspParameters.ParentWindowHandle teraz oczekuje wartości HWND

|   |   |
|---|---|
|Szczegóły|<xref:System.Security.Cryptography.CspParameters.ParentWindowHandle> Wartość wprowadzona w programie .NET Framework 2.0 umożliwia aplikacji do zarejestrowania wartość uchwyt okna nadrzędnego w taki sposób, że wszelkich elementów interfejsu użytkownika wymagane do uzyskania dostępu do klucza (takie jak numer PIN Monituj lub okna dialogowego zgody) otwiera się jako modalne podrzędne do określonego okna. Począwszy od aplikacji przeznaczonych dla programu .NET Framework 4.7 aplikacji Windows Forms można ustawić <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle> właściwości z kodem, podobnie do poniższego:<pre><code class="lang-csharp">cspParameters.ParentWindowHandle = form.Handle;&#13;&#10;</code></pre>W poprzednich wersjach programu .NET Framework, wartość Oczekiwano <xref:System.IntPtr?displayProperty=name> reprezentujący lokalizacja w pamięci, gdzie [HWND](https://docs.microsoft.com/windows/desktop/WinProg/windows-data-types#HWND) wartości znajdowały się. Ustawianie właściwości formularza. Obsługi w systemie Windows 7 i wcześniejsze wersje nie miało wpływu, ale w systemie Windows 8 i nowszych wersjach powoduje ona &quot; <xref:System.Security.Cryptography.CryptographicException?displayProperty=name>: Parametr jest nieprawidłowy.&quot;|
|Sugestia|Aplikacje przeznaczone dla .NET Framework 4.7 lub nowszej pragnący zarejestrować relacji okna nadrzędnego, zaleca się używać Uproszczona forma:<pre><code class="lang-csharp">cspParameters.ParentWindowHandle = form.Handle;&#13;&#10;</code></pre>Użytkownicy, którzy miał identyfikowane, że poprawną wartość do przekazania był adres lokalizacji pamięci, w której przechowywane wartości <code>form.Handle</code> można zrezygnować z Zmiana zachowania, ustawiając przełącznik AppContext <code>Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle</code> do <code>true</code>:<ol><li>Programowe ustawiając compat przełącza się na AppContext, zgodnie z objaśnieniem [tutaj](https://devblogs.microsoft.com/dotnet/net-announcements-at-build-2015/#dotnet46).</li><li>Dodając następujący wiersz do <code>&lt;runtime&gt;</code> sekcji w pliku app.config:</li></ol><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Z drugiej strony, użytkownicy, którzy chcą zgadzaj się na nowe zachowanie w środowisku uruchomieniowym .NET Framework 4.7, gdy obciążenie aplikacji w starszej wersji programu .NET Framework można ustawić AppContext przełączyć się do <code>false</code>.|
|Scope|Mały|
|Wersja|4.7|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.Security.Cryptography.CspParameters.ParentWindowHandle?displayProperty=nameWithType></li></ul>|
