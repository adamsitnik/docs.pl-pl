---
ms.openlocfilehash: b5f12e648a82ebaba7d09b546e8aa2fc7cd82a37
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803206"
---
### <a name="calling-datagridcommitedit-from-a-celleditending-handler-drops-focus"></a>Wywoływanie DataGrid.CommitEdit z obsługi CellEditEnding spada koncentracji uwagi

|   |   |
|---|---|
|Szczegóły|Wywoływanie <xref:System.Windows.Controls.DataGrid.CommitEdit> z jednego z <xref:System.Windows.Controls.DataGrid?displayProperty=name>firmy <xref:System.Windows.Controls.DataGrid.CellEditEnding?displayProperty=name> powoduje, że procedury obsługi zdarzeń <xref:System.Windows.Controls.DataGrid?displayProperty=name> utratę fokus.|
|Sugestia|Ten błąd został naprawiony w programie .NET Framework 4.5.2, dzięki czemu można uniknąć przez uaktualnienie programu .NET Framework. Alternatywnie można należy unikać ponownie, wybierając jawnie <xref:System.Windows.Controls.DataGrid?displayProperty=name> po wywołaniu <xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=name>.|
|Scope|Krawędź|
|Wersja|4.5|
|Typ|Środowisko uruchomieniowe|
|Dotyczy interfejsów API|<ul><li><xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.DataGrid.CommitEdit(System.Windows.Controls.DataGridEditingUnit,System.Boolean)?displayProperty=nameWithType></li></ul>|

