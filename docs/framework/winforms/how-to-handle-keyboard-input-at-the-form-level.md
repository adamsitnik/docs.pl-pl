---
title: 'Instrukcje: Obsługa wprowadzania z klawiatury na poziomie formularza'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboard input [Windows Forms], at form level
- Windows Forms, handling keyboard input
- keyboards [Windows Forms], form-level input
ms.assetid: d7f8b390-dc91-42d2-ae0f-2ffa388127ad
ms.openlocfilehash: c10852273eeb3caea01f448e4cbef571f20769bd
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592047"
---
# <a name="how-to-handle-keyboard-input-at-the-form-level"></a>Instrukcje: Obsługa wprowadzania z klawiatury na poziomie formularza
Windows Forms zapewnia możliwość obsłużyć komunikaty klawiatury na poziomie formularza, zanim komunikaty do formantu. W tym temacie przedstawiono sposób wykonania tego zadania.  
  
### <a name="to-handle-a-keyboard-message-at-the-form-level"></a>Do obsługi komunikatu z klawiatury na poziomie formularza  
  
- Obsługa <xref:System.Windows.Forms.Control.KeyPress> lub <xref:System.Windows.Forms.Control.KeyDown> zdarzenia, formularz początkowy i zestaw <xref:System.Windows.Forms.Form.KeyPreview%2A> właściwości formularza w celu `true` tak, aby komunikaty klawiatury są odbierane przez formularz, zanim osiągną one wszystkie formanty w formularzu. Poniższy kod obsługuje przykład <xref:System.Windows.Forms.Control.KeyPress> zdarzeń, wykrywając, wszystkie klawisze numeryczne i wykorzystywanie '1', '4' i '7'.  
  
     [!code-cpp[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/cpp/form1.cpp#10)]
     [!code-csharp[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/CS/form1.cs#10)]
     [!code-vb[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/VB/form1.vb#10)]  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kodu jest całej aplikacji, na przykład powyżej. Aplikacja zawiera <xref:System.Windows.Forms.TextBox> wraz z innych kontrolek, które pozwalają przenieść fokus z <xref:System.Windows.Forms.TextBox>. <xref:System.Windows.Forms.Control.KeyPress> Zdarzeń głównego <xref:System.Windows.Forms.Form> zużywa '1', '4' i '7' i <xref:System.Windows.Forms.Control.KeyPress> zdarzenia <xref:System.Windows.Forms.TextBox> zużywa "2", "5" i "8" podczas wyświetlania pozostałe klucze. Porównaj <xref:System.Windows.Forms.MessageBox> dane wyjściowe po naciśnięciu klawisza chwilę liczba kluczy <xref:System.Windows.Forms.TextBox> ma fokus z <xref:System.Windows.Forms.MessageBox> dane wyjściowe, gdy ponownie naciśniesz klawisz liczby podczas, gdy fokus jest ustawiony na jedną z innych kontrolek.  
  
 [!code-cpp[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/cpp/form1.cpp#0)]
 [!code-csharp[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Ten przykład wymaga:  
  
- Odwołania do zestawów systemu, System.Drawing i przestrzeń nazw System.Windows.Forms.  
  
## <a name="see-also"></a>Zobacz także

- [Wprowadzanie z klawiatury w aplikacjach Windows Forms](keyboard-input-in-a-windows-forms-application.md)
