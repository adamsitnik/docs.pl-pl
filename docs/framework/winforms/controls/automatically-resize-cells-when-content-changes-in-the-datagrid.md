---
title: 'Instrukcje: automatyczne zmienianie rozmiaru komórek przy zmianie zawartości w kontrolce DataGridView formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data grids [Windows Forms], resizing cells automatically
- cells [Windows Forms], resizing automatically
- DataGridView control [Windows Forms], resizing cells
ms.assetid: 1d68934d-a04c-4b12-9e66-c856c6828131
ms.openlocfilehash: 3411b68b4dcc64dba86cd9fa8804e0a487cec76d
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586631"
---
# <a name="how-to-automatically-resize-cells-when-content-changes-in-the-windows-forms-datagridview-control"></a>Instrukcje: automatyczne zmienianie rozmiaru komórek przy zmianie zawartości w kontrolce DataGridView formularzy systemu Windows
Można skonfigurować <xref:System.Windows.Forms.DataGridView> kontrolować zmiany rozmiaru jego wiersze, kolumny i nagłówki automatycznie zawsze, gdy zmian zawartości, tak aby komórek są zawsze wystarczająco duży, aby wyświetlić ich wartości bez przycinania.  
  
 Masz wiele opcji, aby ograniczyć komórki, które są używane do określania nowe rozmiary. Na przykład można skonfigurować formant Aby automatycznie zmieniać rozmiar szerokość kolumn tylko na podstawie wartości w wierszach, które są obecnie wyświetlane. Dzięki temu można uniknąć dotyczące nieefektywności podczas pracy z dużą liczbę wierszy, mimo że w tym przypadku warto użyć metod zmiany rozmiaru, takich jak <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> dostosowania rozmiarów czasami wybrane.  
  
 Aby uzyskać więcej informacji na temat automatycznej zmiany rozmiaru, zobacz [opcje ustalania rozmiaru w formancie DataGridView formularzy Windows](sizing-options-in-the-windows-forms-datagridview-control.md).  
  
 Poniższy przykład kodu demonstruje opcjami dostępnymi na potrzeby automatycznej zmiany rozmiaru.  
  
## <a name="example"></a>Przykład  
 [!code-cpp[System.Windows.Forms.DataGridView.AutoSizing#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.AutoSizing/CPP/autosizing.cpp#0)]
 [!code-csharp[System.Windows.Forms.DataGridView.AutoSizing#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.AutoSizing/CS/autosizing.cs#0)]
 [!code-vb[System.Windows.Forms.DataGridView.AutoSizing#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.AutoSizing/VB/autosizing.vb#0)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Ten przykład wymaga:  
  
- Odwołania do zestawów systemu, System.Drawing i przestrzeń nazw System.Windows.Forms.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>
- <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>
- <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>
- [Zmiana rozmiaru wierszy i kolumn w kontrolce DataGridView formularzy Windows Forms](resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)
- [Opcje ustalania rozmiaru w kontrolce DataGridView formularzy Windows Forms](sizing-options-in-the-windows-forms-datagridview-control.md)
- [Instrukcje: Programowe zmienianie rozmiaru komórek w celu dopasowania do zawartości w kontrolce DataGridView formularzy Windows Forms](programmatically-resize-cells-to-fit-content-in-the-datagrid.md)
