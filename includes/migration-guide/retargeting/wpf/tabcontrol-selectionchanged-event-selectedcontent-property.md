---
ms.openlocfilehash: e80748c183a10cac4ef66c96ab48458cd9baa806
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858963"
---
### <a name="tabcontrol-selectionchanged-event-and-selectedcontent-property"></a>TabControl SelectionChanged zdarzeń i właściwości SelectedContent

|   |   |
|---|---|
|Szczegóły|Począwszy od programu .NET Framework 4.7.1, <xref:System.Windows.Controls.TabControl> aktualizuje wartość jego <xref:System.Windows.Controls.TabControl.SelectedContent> właściwości przed zgłoszeniem <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> zdarzenie, gdy zmieni się jego zaznaczenie. W .NET Framework 4.7 i wcześniejszych wersjach aktualizacja SelectedContent wystąpiło po zdarzeniu.|
|Sugestia|Aplikacje, które obsługują program .NET Framework 4.7.1 lub nowszej można zrezygnować z tego zmienić i użyć starsze zachowanie, dodając następujące polecenie, aby <code>&lt;runtime&gt;</code> sekcję pliku konfiguracji aplikacji:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Aplikacje przeznaczone dla .NET Framework 4.7 lub wcześniej, ale są uruchomione w środowisku .NET Framework 4.7.1 lub później włączyć nowe zachowanie, dodając następujący wiersz do <code>&lt;runtime&gt;</code> części pliku .configuration aplikacji:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Scope|Mały|
|Wersja|4.7.1|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.Windows.Controls.TabControl.SelectedContent?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.Primitives.Selector.SelectionChanged?displayProperty=nameWithType></li></ul>|

