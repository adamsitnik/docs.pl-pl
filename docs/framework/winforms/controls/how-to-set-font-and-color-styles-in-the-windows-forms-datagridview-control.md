---
title: 'Instrukcje: ustawianie stylów czcionek i koloru w kontrolce DataGridView formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], cell customization
- data grids [Windows Forms], customizing cells
- data grids [Windows Forms], font styles
- data grids [Windows Forms], color styles
ms.assetid: 588f2c57-d963-41b1-9c1d-d02d71818113
ms.openlocfilehash: ad2426ed9643fd46927c4f8b6373fedbec372d38
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638092"
---
# <a name="how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control"></a>Instrukcje: ustawianie stylów czcionek i koloru w kontrolce DataGridView formularzy systemu Windows
Można określić wygląd komórki znajdujące się wewnątrz <xref:System.Windows.Forms.DataGridView> kontroli przez ustawienie właściwości <xref:System.Windows.Forms.DataGridViewCellStyle> klasy. Wystąpienia tej klasy można pobrać z różnych właściwości obiektu <xref:System.Windows.Forms.DataGridView> klasy i jej klasy pomocnika lub można utworzyć wystąpienie <xref:System.Windows.Forms.DataGridViewCellStyle> obiektów w celu przypisania do tych właściwości.  
  
 Poniższe procedury przedstawiają podstawowe Dostosowywanie za pomocą wygląd komórki <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> właściwości. Każdej komórki w formancie dziedziczy style określone przez tę właściwość, chyba że zostaną zastąpione poziomie kolumny, wiersza lub komórki. Na przykład dziedziczenie stylów zobacz [jak: Ustawianie domyślnych stylów komórki dla formantu DataGridView formularzy Windows](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md). Aby uzyskać informacje o dodatkowych zastosowań <xref:System.Windows.Forms.DataGridViewCellStyle> klasy, zobacz tematy wymienione w sekcji Zobacz też.  
  
 Brak zaawansowaną obsługę dla tego zadania w programie Visual Studio.  Zobacz też [jak: Ustawianie domyślnych stylów komórek i formatów danych dla formantu DataGridView, które przy użyciu narzędzia Projektant formularzy Windows](default-cell-styles-datagridview.md).  
  
### <a name="to-specify-the-font-used-by-datagridview-cells"></a>Aby określić Czcionka używana w komórkach kontrolki DataGridView  
  
- Ustaw <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A> właściwość <xref:System.Windows.Forms.DataGridViewCellStyle>. Poniższy przykład kodu wykorzystuje <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> właściwości ustaw czcionkę dla całego formantu.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#101](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#101)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#101](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#101)]  
  
### <a name="to-specify-the-foreground-and-background-colors-of-datagridview-cells"></a>Aby określić kolory pierwszego planu i tła komórek DataGridView  
  
- Ustaw <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> i <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> właściwości <xref:System.Windows.Forms.DataGridViewCellStyle>. Poniższy przykład kodu wykorzystuje <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> właściwość umożliwiająca ustawienie tych stylów dla całego formantu.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#102](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#102)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#102](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#102)]  
  
### <a name="to-specify-the-foreground-and-background-colors-of-selected-datagridview-cells"></a>Aby określić kolory pierwszego planu i tła zaznaczonych komórek DataGridView  
  
- Ustaw <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A> i <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> właściwości <xref:System.Windows.Forms.DataGridViewCellStyle>. Poniższy przykład kodu wykorzystuje <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> właściwość umożliwiająca ustawienie tych stylów dla całego formantu.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#103](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#103)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#103](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#103)]  
  
## <a name="example"></a>Przykład  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#100)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#100)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Ten przykład wymaga:  
  
- A <xref:System.Windows.Forms.DataGridView> formantu o nazwie `dataGridView1`.  
  
- Odwołuje się do <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType>, i <xref:System.Windows.Forms?displayProperty=nameWithType> zestawów.  
  
## <a name="robust-programming"></a>Niezawodne programowanie  
 W przypadku maksymalnej skalowalności powinny współużytkować <xref:System.Windows.Forms.DataGridViewCellStyle> obiektów między wiele wierszy, kolumny lub komórki, które używają tego samego style, zamiast oddzielnie ustawienie ponownego obliczenia właściwości stylu dla każdego elementu. Aby uzyskać więcej informacji, zobacz [najlepsze praktyki dotyczące skalowania formantu DataGridView formularzy Windows](best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [Podstawowe formatowanie i style w kontrolce DataGridView formularzy Windows Forms](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Style komórki w kontrolce DataGridView formularzy Windows Forms](cell-styles-in-the-windows-forms-datagridview-control.md)
