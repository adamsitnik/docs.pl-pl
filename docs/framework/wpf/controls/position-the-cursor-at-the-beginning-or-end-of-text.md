---
title: 'Instrukcje: Umieszczanie kursora na początku lub na końcu tekstu w kontrolce TextBox'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- positioning cursor [WPF]
- TextBox control [WPF], positioning cursor
- cursor [WPF], positioning
ms.assetid: c771a0b8-c6b4-4240-aecd-a21d0ba51a2e
ms.openlocfilehash: 3d7da5daf09e06938b8366e0f5f98a599cae4571
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770620"
---
# <a name="how-to-position-the-cursor-at-the-beginning-or-end-of-text-in-a-textbox-control"></a>Instrukcje: Umieszczanie kursora na początku lub na końcu tekstu w kontrolce TextBox
W tym przykładzie pokazano, jak umieścić kursor na początku lub końcu zawartość tekstową <xref:System.Windows.Controls.TextBox> kontroli.  
  
## <a name="example"></a>Przykład  
 Następujące [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] kod opisuje <xref:System.Windows.Controls.TextBox> kontroli i przypisuje mu nazwę.  
  
 [!code-xaml[TextBox_MiscCode#_MoveCursorXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_movecursorxaml)]  
  
## <a name="example"></a>Przykład  
 Aby umieść kursor na początku zawartość <xref:System.Windows.Controls.TextBox> sterowania, wywołaj <xref:System.Windows.Controls.TextBox.Select%2A> metody i określ wybór start pozycji 0, a wybór długość 0.  
  
 [!code-csharp[TextBox_MiscCode#_CursorToStart](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_cursortostart)]
 [!code-vb[TextBox_MiscCode#_CursorToStart](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_cursortostart)]  
  
## <a name="example"></a>Przykład  
 Aby umieść kursor na końcu zawartości <xref:System.Windows.Controls.TextBox> sterowania, wywołaj <xref:System.Windows.Controls.TextBox.Select%2A> metodę i określić pozycja początkowa wybranego równa długości tekstu, zawartości i wyboru długość 0.  
  
 [!code-csharp[TextBox_MiscCode#_CursorToEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_cursortoend)]
 [!code-vb[TextBox_MiscCode#_CursorToEnd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_cursortoend)]  
  
## <a name="see-also"></a>Zobacz także

- [TextBox — omówienie](textbox-overview.md)
- [RichTextBox — omówienie](richtextbox-overview.md)
