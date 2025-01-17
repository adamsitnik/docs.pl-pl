---
title: ContextMenu — Przegląd
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ContextMenu
- ContextMenu controls [WPF], about ContextMenu controls
ms.assetid: 16909c42-799a-4561-91e0-7d69dcfeea91
ms.openlocfilehash: 1818718d3ca9e8f56da99d6e504b41b217bfd980
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053265"
---
# <a name="contextmenu-overview"></a>ContextMenu — Przegląd
<xref:System.Windows.Controls.ContextMenu> Klasa reprezentuje element, który udostępnia funkcje przy użyciu określonego kontekstu <xref:System.Windows.Controls.Menu>. Zazwyczaj użytkownik udostępnia <xref:System.Windows.Controls.ContextMenu> w [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] klikając prawym przyciskiem myszy przycisk myszy. W tym temacie przedstawiono <xref:System.Windows.Controls.ContextMenu> elementu oraz przykłady sposobu używania go w [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] i kod.  

<a name="contextmenu_control"></a>   
## <a name="contextmenu-control"></a>ContextMenu — formant  
 Element <xref:System.Windows.Controls.ContextMenu> jest dołączony do określonej kontrolki. <xref:System.Windows.Controls.ContextMenu> Element umożliwia prezentowanie użytkowników z listą elementów, które określają poleceń lub opcje, które są skojarzone z określonego formantu, na przykład <xref:System.Windows.Controls.Button>. Użytkownicy kliknij prawym przyciskiem myszy formant Aby utworzyć menu są wyświetlane. Zazwyczaj kliknięcie <xref:System.Windows.Controls.MenuItem> spowoduje otwarcie podmenu lub powoduje, że aplikacja do wykonania polecenia.  
  
<a name="creating_contextmenus"></a>   
## <a name="creating-contextmenus"></a>Tworzenie ContextMenu  
 W poniższych przykładach pokazano sposób tworzenia <xref:System.Windows.Controls.ContextMenu> z podmenu. <xref:System.Windows.Controls.ContextMenu> Formanty są dołączone do kontrolek przycisku.  
  
 [!code-xaml[ContextMenu#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml#1)]  
  
 [!code-csharp[ContextMenu#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ContextMenu#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ContextMenu/VisualBasic/Pane1.xaml.vb#2)]  
  
<a name="applying_styles_to_contextmenu"></a>   
## <a name="applying-styles-to-a-contextmenu"></a>Stosowanie stylów do element ContextMenu  
 Za pomocą formantu <xref:System.Windows.Style>, możesz radykalnie zmienić wygląd i zachowanie <xref:System.Windows.Controls.ContextMenu> bez konieczności pisania niestandardowego formantu. Poza ustawieniem właściwości wizualnego, można również zastosować style do części kontrolki. Na przykład można zmienić zachowanie części kontrolki za pomocą właściwości, lub można dodać części do lub zmieniać układ, <xref:System.Windows.Controls.ContextMenu>. W poniższych przykładach pokazano kilka sposobów dodawania stylów <xref:System.Windows.Controls.ContextMenu> kontrolki.  
  
 Pierwszy przykład definiuje styl o nazwie `SimpleSysResources`, który ilustruje sposób używania ustawień systemu swojego stylu. Przykład przypisuje <xref:System.Windows.SystemColors.MenuHighlightBrushKey%2A> jako <xref:System.Windows.Controls.Control.Background%2A> kolorów i <xref:System.Windows.SystemColors.MenuTextBrushKey%2A> jako <xref:System.Windows.Controls.Control.Foreground%2A> kolor <xref:System.Windows.Controls.ContextMenu>.  
  
```xaml  
<Style x:Key="SimpleSysResources" TargetType="{x:Type MenuItem}">  
  <Setter Property = "Background" Value=   
    "{DynamicResource {x:Static SystemColors.MenuHighlightBrushKey}}"/>  
  <Setter Property = "Foreground" Value=   
    "{DynamicResource {x:Static SystemColors.MenuTextBrushKey}}"/>  
</Style>  
```  
  
 W poniższym przykładzie użyto <xref:System.Windows.Trigger> elementu, aby zmienić wygląd <xref:System.Windows.Controls.Menu> w odpowiedzi na zdarzenia, które są wywoływane na <xref:System.Windows.Controls.ContextMenu>. Gdy użytkownik przesuwa mysz nad menu wygląd <xref:System.Windows.Controls.ContextMenu> elementy zmiany.  
  
```xaml  
<Style x:Key="Triggers" TargetType="{x:Type MenuItem}">  
  <Style.Triggers>  
    <Trigger Property="MenuItem.IsMouseOver" Value="true">  
      <Setter Property = "FontSize" Value="16"/>  
      <Setter Property = "FontStyle" Value="Italic"/>  
      <Setter Property = "Foreground" Value="Red"/>  
    </Trigger>  
  </Style.Triggers>  
</Style>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.Style>
- <xref:System.Windows.Controls.Menu>
- <xref:System.Windows.Controls.MenuItem>
- [ContextMenu](contextmenu.md)
- [ContextMenu — style i szablony](contextmenu-styles-and-templates.md)
- [Przykładu z galerii kontrolki WPF](https://go.microsoft.com/fwlink/?LinkID=160053)
