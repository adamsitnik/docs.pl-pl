---
ms.openlocfilehash: f1a1eab471d46f018a8e0d0cf787d487cf67c11e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61762667"
---
### <a name="contextmenustripsourcecontrol-property-contains-a-valid-control-in-the-case-of-nested-toolstripmenuitems"></a>Właściwość ContextMenuStrip.SourceControl zawiera nieprawidłowy kontroli w przypadku zagnieżdżonych kontrolki ToolStripMenuItems

|   |   |
|---|---|
|Szczegóły|.NET Framework 4.7.1 i poprzednich wersjach <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> właściwość niepoprawnie zwraca wartość null, gdy użytkownik otwiera menu w zagnieżdżonych <xref:System.Windows.Forms.ToolStripMenuItem> kontrolki. W programie .NET Framework 4.7.2 i nowszych <xref:System.Windows.Forms.ContextMenuStrip.SourceControl> właściwość ma zawsze wartość do kontroli rzeczywiste źródło.|
|Sugestia|<strong>Sposób korzystania z opcji na lub poza te zmiany</strong>w kolejności dla aplikacji, aby korzystać z tych zmian, należy uruchomić w środowisku .NET Framework 4.7.2 lub nowszej. Aplikacji mogą korzystać z tych zmian w jednej z następujących sposobów:<ul><li>Jest ono przeznaczone dla .NET Framework 4.7.2. Ta zmiana jest włączona domyślnie w aplikacji Windows Forms, przeznaczonych dla środowiska .NET Framework 4.7.2 lub nowszej.</li><li>Jest przeznaczony dla platformy .NET Framework 4.7.1 lub starszej wersji, a zdecyduje poza zachowania starszych ułatwień dostępu przez dodanie poniższego [przełącznika AppContext](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) do <code>&lt;runtime&gt;</code> sekcji w pliku app.config i ustawieniem dla niego <code>false</code>, jak pokazano w poniższym przykładzie.</li></ul><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Aplikacji przeznaczonych dla środowiska .NET Framework 4.7.2 lub nowszy i chcesz zachować starsze zachowanie zgodzić się na wartości kontroli źródła w starszej wersji przez jawne ustawienie tego parametru AppContext <code>true</code>.|
|Zakres|Krawędź|
|Wersja|4.7.2|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType></li></ul>|
