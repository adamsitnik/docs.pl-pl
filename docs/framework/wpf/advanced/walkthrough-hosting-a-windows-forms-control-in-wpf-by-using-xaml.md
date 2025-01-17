---
title: 'Wskazówki: Hosting formantu Windows Form w WPF z wykorzystaniem XAML'
ms.date: 03/30/2017
helpviewer_keywords:
- hosting Windows Forms control in WPF [WPF]
ms.assetid: 1aef42cb-4cfb-44b4-9a7a-c02632d3d9c7
ms.openlocfilehash: 10596f3ec89a5dc8bb7c20274b697d2592ad93d5
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73197878"
---
# <a name="walkthrough-hosting-a-windows-forms-control-in-wpf-by-using-xaml"></a>Wskazówki: Hosting formantu Windows Form w WPF z wykorzystaniem XAML
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] udostępnia wiele kontrolek z bogatym zestawem funkcji. Czasami jednak może być konieczne użycie formantów [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] na stronach [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Na przykład możesz mieć znaczną inwestycję w istniejące kontrolki [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] lub mieć kontrolkę [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], która zapewnia unikalne funkcje.  
  
 W tym instruktażu pokazano, jak hostować Windows Forms kontrolę <xref:System.Windows.Forms.MaskedTextBox?displayProperty=nameWithType> na stronie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] za pomocą [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 Aby zapoznać się z pełną listą zadań przedstawionych w tym instruktażu, zobacz [hostowanie kontrolki Windows Forms w WPF przy użyciu języka XAML](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/HostingWfInWpfWithXaml).
  
## <a name="prerequisites"></a>Wymagania wstępne  

Aby ukończyć ten przewodnik, potrzebujesz programu Visual Studio.  
  
## <a name="hosting-the-windows-forms-control"></a>Hostowanie kontrolki Windows Forms  
  
#### <a name="to-host-the-maskedtextbox-control"></a>Aby hostować formant formantem MaskedTextBox  
  
1. Utwórz projekt aplikacji WPF o nazwie `HostingWfInWpfWithXaml`.  
  
2. Dodaj odwołania do następujących zestawów.  
  
    - WindowsFormsIntegration  
  
    - System. Windows. Forms  
  
3. Otwórz MainWindow. XAML w [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
4. W <xref:System.Windows.Window> elementu Dodaj następujące mapowanie przestrzeni nazw. Mapowanie przestrzeni nazw `wf` ustanawia odwołanie do zestawu, który zawiera kontrolkę Windows Forms.  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5. W <xref:System.Windows.Controls.Grid> element Dodaj następujący kod XAML.  
  
     Formant <xref:System.Windows.Forms.MaskedTextBox> jest tworzony jako element podrzędny kontrolki <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
     [!code-xaml[HostingWfInWpfWithXaml#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWpfWithXaml/CSharp/HostingWfInWpf/Window1.xaml#3)]  
  
6. Naciśnij klawisz F5, aby skompilować i uruchomić aplikację.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Projektowanie XAML w programie Visual Studio](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [Przewodnik: hosting kontrolki Windows Forms w WPF](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
- [Przewodnik: hosting złożonej kontrolki Windows Forms w WPF](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [Przewodnik: hosting złożonej kontrolki WPF w Windows Forms](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [Kontrolki formularzy Windows Forms i równoważne kontrolki WPF](windows-forms-controls-and-equivalent-wpf-controls.md)
- [Hostowanie formantu Windows Forms w WPF przy użyciu przykładu XAML](https://go.microsoft.com/fwlink/?LinkID=160000)
