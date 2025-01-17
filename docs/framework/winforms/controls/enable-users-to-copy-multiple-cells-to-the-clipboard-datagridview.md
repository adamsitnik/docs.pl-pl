---
title: 'Instrukcje: umożliwianie użytkownikom kopiowania wielu komórek do schowka z kontrolki DataGridView formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cells [Windows Forms], copying to Clipboard
- DataGridView control [Windows Forms], copying multiple cells
- data grids [Windows Forms], copying multiple cells
- Clipboard [Windows Forms], copying multiple cells
ms.assetid: fd0403b2-d0e3-4ae0-839c-0f737e1eb4a9
ms.openlocfilehash: b220603adcaeae6f3380a2e3c10ea524c9a61f24
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591922"
---
# <a name="how-to-enable-users-to-copy-multiple-cells-to-the-clipboard-from-the-windows-forms-datagridview-control"></a>Instrukcje: umożliwianie użytkownikom kopiowania wielu komórek do schowka z kontrolki DataGridView formularzy systemu Windows
Po włączeniu kopiowanie komórki wprowadzić dane w Twojej <xref:System.Windows.Forms.DataGridView> łatwo dostępne dla innych aplikacji za pomocą kontrolki <xref:System.Windows.Forms.Clipboard>. Wartości zaznaczonych komórek są konwertowane na ciągi i dodane do Schowka jako tekst rozdzielany tabulatorami wartości wklejania w aplikacji, takich jak Notatnik, a program Excel, a w formacie HTML tabeli wklejania w aplikacji, takich jak Word.  
  
 Można skonfigurować w komórce kopiowania do skopiowania tylko wartości komórek, zawierają tekst nagłówka wierszy i kolumn w danych ze Schowka lub zawierają tekst nagłówka, tylko wtedy, gdy użytkownicy wybierają całych wierszy lub kolumn.  
  
 W zależności od trybu zaznaczania użytkownicy mogą wybrać wiele grup odłączonego komórek. Gdy użytkownik kopiuje komórek do Schowka, wierszy i kolumn z nie zaznaczone komórki nie są kopiowane. Wszystkie pozostałe wiersze lub kolumny stają się wierszy i kolumn w tabeli dane skopiowane do Schowka. Niezaznaczone komórek w te wiersze lub kolumny są kopiowane jako elementy zastępcze pustego do Schowka.  
  
### <a name="to-enable-cell-copying"></a>Aby umożliwić kopiowanie komórki  
  
- Ustaw <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A?displayProperty=nameWithType> właściwości.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewClipboardDemo#15](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/CS/datagridviewclipboarddemo.cs#15)]
     [!code-vb[System.Windows.Forms.DataGridViewClipboardDemo#15](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/VB/datagridviewclipboarddemo.vb#15)]  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kompletny kod pokazuje, jak komórek są kopiowane do Schowka. W tym przykładzie zawiera przycisk, który kopiuje zaznaczonych komórek do Schowka z użyciem <xref:System.Windows.Forms.DataGridView.GetClipboardContent%2A?displayProperty=nameWithType> metody i wyświetla zawartość Schowka, w polu tekstowym.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewClipboardDemo#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/CS/datagridviewclipboarddemo.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewClipboardDemo#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/VB/datagridviewclipboarddemo.vb#00)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Ten kod wymaga:  
  
- Odwołania do zestawów N:System i N:System.Windows.Forms.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A>
- <xref:System.Windows.Forms.DataGridView.GetClipboardContent%2A>
- [Wybór i używanie schowka za pomocą kontrolki DataGridView formularzy Windows Forms](selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)
