---
ms.openlocfilehash: 88e00454894c8404fd48e92404e35ae27fa056f6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235422"
---
### <a name="wpf-treeviewitem-must-be-used-within-a-treeview"></a>Należy użyć WPF TreeViewItem w TreeView

|   |   |
|---|---|
|Szczegóły|Zmiana została wprowadzona w 4.5, który ogranicza użycie <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> elementy poza <xref:System.Windows.Controls.TreeView?displayProperty=name>. To manifesty w następujących warunkach:<ul><li><xref:System.Windows.Controls.TreeViewItem?displayProperty=name>w visual element nadrzędny nie jest panelu. (A <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> wygenerowany <xref:System.Windows.Controls.TreeView?displayProperty=name> będzie miał panelu co jego element nadrzędny)</li><li><xref:System.Windows.Controls.TreeViewItem?displayProperty=name> Jest obiektem potomnym <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> działający jako &quot;elementów hosta&quot; kontrolki listy (pole listy DataGrid, ListView, itp.). Wirtualizacja nie muszą być włączone.</li><li><xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> Jest przewijanie elementu (<code>ScrollUnit=&quot;Item&quot;</code>).</li><li>Dla osób chcących <code>VirtualizingStackPanel.MakeVisible(v)</code> aby przewinąć element <code>v</code> do widoku. To może odbywać się jawnie lub niejawnie wiele sposobów; Prawdopodobnie najczęściej sposób jest po prostu kliknij <code>v</code> Aby ustawić fokus klawiatury.</li><li>Łańcuch relacji nadrzędny wizualizacji z <code>v</code> do <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> przechodzi przez <xref:System.Windows.Controls.TreeViewItem?displayProperty=name>.</li></ul>Innymi słowy, jest to widoczne podczas <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> jest używany poza <xref:System.Windows.Controls.TreeView?displayProperty=name>, a użytkownik kliknie element podrzędny <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> Aby wprowadzić dane do widoku. Jeśli <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> nie ma focusable elementów podrzędnych, nigdy nie zobaczysz tego problemu. Jest przykładem sytuacji, w którym ten zostanie osiągnięty, gdy <xref:System.Windows.Controls.TreeViewItem?displayProperty=name> jest głównym DataTemplate. Po osiągnięciu tego problemu jest InvalidCastException, który występuje w ramach programu WPF.|
|Sugestia|Poprawka zostanie udostępniona w tym.|
|Zakres|Mały|
|Wersja|4.5|
|Typ|Środowisko uruchomieniowe|
