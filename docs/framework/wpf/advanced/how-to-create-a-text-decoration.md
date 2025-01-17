---
title: 'Instrukcje: Tworzenie dekoracji tekstu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- fonts [WPF], baseline
- text [WPF], decorations
- fonts [WPF], underline
- fonts [WPF], overline
- strikethrough type [WPF]
- fonts [WPF], strikethrough
- overline type [WPF]
- underline type [WPF]
- typography [WPF], text decorations
- baseline type [WPF]
ms.assetid: cf3cb4e7-782a-4be7-b2d4-e0935e21e4e0
ms.openlocfilehash: d586eef8d1308070da38a0a54c63c3ba64d30c8b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776636"
---
# <a name="how-to-create-a-text-decoration"></a>Instrukcje: Tworzenie dekoracji tekstu
A <xref:System.Windows.TextDecoration> obiekt jest ornamentacji visual, można dodać do tekstu. Istnieją cztery typy dekoracje tekstu: podkreślenie, linii bazowej, przekreślenia i nadkreślenia. Poniższy przykład przedstawia lokalizacje dekoracje tekstu względem tekstu.  
  
 ![Diagram przedstawiający typów dekoracji tekstu](./media/how-to-create-a-text-decoration/text-decoration-types.gif)  
  
 Aby dodać dekoracji tekstu do tekstu, należy utworzyć <xref:System.Windows.TextDecoration> obiektów i modyfikowania jego właściwości. Użyj <xref:System.Windows.TextDecoration.Location%2A> właściwości w celu określenia, gdzie dekoracji tekstu pojawi się, takie jak podkreślenie. Użyj <xref:System.Windows.TextDecoration.Pen%2A> właściwości w celu określenia wyglądu dekoracji tekstu, takiego jak wypełnienia kryjącego lub kolor gradientu. Jeśli nie określisz wartości <xref:System.Windows.TextDecoration.Pen%2A> właściwości wartość domyślna dekoracje, to ten sam kolor jak tekst. Po zdefiniowaniu <xref:System.Windows.TextDecoration> obiektu, dodaj ją do <xref:System.Windows.TextDecorations> kolekcji obiektu odpowiedni tekst.  
  
 Dekorację tekstu, który został wstawiony w pędzel gradientów liniowych i Pióro przerywaną, co można znaleźć w poniższym przykładzie.  
  
 ![Dekoracja tekstu z podkreślenie gradientu liniowego](./media/how-to-create-a-text-decoration/text-decoration-gradient.png)  
  
 <xref:System.Windows.Documents.Hyperlink> Obiekt jest element zawartości śródwierszowy przepływ, który pozwala na hosta hiperlinki w dowolnej zawartości. Domyślnie <xref:System.Windows.Documents.Hyperlink> używa <xref:System.Windows.TextDecoration> obiektu, aby wyświetlić podkreślenie. <xref:System.Windows.TextDecoration> obiekty mogą być intensywnie do utworzenia wystąpienia, wydajność, zwłaszcza, jeśli dostępnych jest wiele <xref:System.Windows.Documents.Hyperlink> obiektów. Jeśli wprowadzisz zwiększone użycie <xref:System.Windows.Documents.Hyperlink> elementów, warto wziąć pod uwagę przedstawiający podkreślenie, tylko wtedy, gdy wyzwalanie zdarzenia, takie jak <xref:System.Windows.ContentElement.MouseEnter> zdarzeń.  
  
 W poniższym przykładzie jest dynamiczny podkreślenie dla linku "Mój MSN" — pojawia się tylko, gdy <xref:System.Windows.ContentElement.MouseEnter> zdarzenie jest wyzwalane.  
  
 ![Wyświetlanie właściwości TextDecorations hiperłącza](./media/how-to-create-a-text-decoration/text-decorations-hyperlinks.png)  
   
 Aby uzyskać więcej informacji, zobacz [określ czy hiperłącze jest podkreślone](how-to-specify-whether-a-hyperlink-is-underlined.md).  
  
## <a name="example"></a>Przykład  
 W poniższym przykładzie kodu podkreślenia dekoracji tekstu używa wartość domyślna czcionka.  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets1)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets1)]
 [!code-xaml[TextDecorationSnippets#TextDecorationSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets1)]  
  
 W poniższym przykładzie kodu podkreślenia Dekoracja tekstu jest tworzony z pędzel pełnego koloru pióra.  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets2)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets2)]
 [!code-xaml[TextDecorationSnippets#TextDecorationSnippets2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets2)]  
  
 W poniższym przykładzie kodu dekoracyjną podkreślenie jest tworzony z pędzel gradientów liniowych kreskowane pióra.  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets3](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets3)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets3)]
 [!code-xaml[TextDecorationSnippets#TextDecorationSnippets3](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets3)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.TextDecoration>
- <xref:System.Windows.Documents.Hyperlink>
- [Określanie, czy hiperlink jest podkreślony](how-to-specify-whether-a-hyperlink-is-underlined.md)
