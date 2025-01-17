---
title: 'Model obiektów pisma odręcznego: Windows Forms i COM a WPF'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling ink [WPF]
- InkCanvas control [WPF]
- ink object model [WPF]
- tablet pen [WPF], events [WPF]
- ink [WPF], enabling
- events [WPF], tablet pen
ms.assetid: 577835be-b145-4226-8570-1d309e9b3901
ms.openlocfilehash: 68003943041fe0ba405eff1236c43a8e7e9c2b71
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051679"
---
# <a name="the-ink-object-model-windows-forms-and-com-versus-wpf"></a>Model obiektów pisma odręcznego: Windows Forms i COM a WPF

Istnieją zasadniczo trzech platformach, które obsługują cyfrowy atrament: platforma typu Tablet PC Windows Forms, platformy Tablet PC COM i platformy Windows Presentation Foundation (WPF).  Udział platformy Windows Forms i COM, model obiektów programu podobne, ale obiekt model na potrzeby [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] platformy różni się znacznie.  W tym temacie omówiono różnice w ogólne, tak aby deweloperów, które działały w jeden obiekt modelu mogą lepiej zrozumieć innych.  
  
## <a name="enabling-ink-in-an-application"></a>Włączanie pisma odręcznego w aplikacji  
 Wszystkich trzech platformach dostarczane obiekty oraz kontrolki, które umożliwiają aplikacji na odbieranie danych wejściowych z pióra.  Windows Forms i COM platformy są dostarczane z [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)), [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90)), [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) i [ Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) klasy.  [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) i [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90)) kontrolek, które można dodać do aplikacji w celu zbierania pisma odręcznego.  [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) i [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) można dołączyć do istniejącego okna pisma odręcznego z obsługą systemu windows i kontrolki niestandardowe.  
  
 Platforma WPF obejmuje <xref:System.Windows.Controls.InkCanvas> kontroli.  Możesz dodać <xref:System.Windows.Controls.InkCanvas> do aplikacji i rozpocząć zbieranie atramentu natychmiast. Za pomocą <xref:System.Windows.Controls.InkCanvas>, użytkownik może skopiować, wybierz i zmienianie rozmiaru pisma odręcznego.  Możesz dodać inne formanty do <xref:System.Windows.Controls.InkCanvas>, a użytkownik umożliwia pisanie ręczne nad te kontrolki za.  Można utworzyć niestandardowego formantu włączone pisma odręcznego, dodając <xref:System.Windows.Controls.InkPresenter> i zbieranie punktów pióra.  
  
 W poniższej tabeli wymieniono, gdzie można dowiedzieć się więcej na temat włączania pisma odręcznego w aplikacji:  
  
|Aby to zrobić...|Na platformie WPF...|Na platformach Windows Forms/COM...|  
|-----------------|--------------------------|------------------------------------------|  
|Dodaj kontrolkę, która jest włączona pisma odręcznego do aplikacji|Zobacz [wprowadzenie do użycia atramentu](getting-started-with-ink.md).|Zobacz [oświadczeń automatycznego utworzenia próbki](/windows/desktop/tablet/auto-claims-form-sample)|  
|Włączanie pisma odręcznego na niestandardowej kontrolce|Zobacz [tworzenia pisma odręcznego kontrolka wprowadzania](creating-an-ink-input-control.md).|Zobacz [pisma odręcznego przykładowe Schowka](/windows/desktop/tablet/ink-clipboard-sample).|  
  
## <a name="ink-data"></a>Dane pisma odręcznego  
 Na Windows Forms i COM platformach [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)), [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)), [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90)), i [ Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) każdego udostępniają [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiektu. [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiekt zawiera dane dla jednego lub kilku [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) obiektów i udostępnia typowe metody i właściwości do zarządzania i manipulowania tymi pociągnięć.  [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiektu zarządza czasem istnienia pociągnięć zawiera; [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiektu tworzy i usuwa pociągnięć, które jest właścicielem.  Każdy [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) ma identyfikator, który jest unikatowy w obrębie nadrzędnego [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiektu.  
  
 Na platformie WPF <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> klasy jest właścicielem i zarządza swój własny okres istnienia. Grupa <xref:System.Windows.Ink.Stroke> obiekty mogą być zbierane ze sobą w <xref:System.Windows.Ink.StrokeCollection>, która zapewnia metody do wspólnego pisma odręcznego operacji zarządzania danymi takich jak trafień, testowania, usuwania, przekształcanie i serializacji pisma odręcznego. A <xref:System.Windows.Ink.Stroke> mogą należeć do zera, co najmniej jeden <xref:System.Windows.Ink.StrokeCollection> obiektów w dowolnym dać czas.  Zamiast [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiektu <xref:System.Windows.Controls.InkCanvas> i <xref:System.Windows.Controls.InkPresenter> zawierają <xref:System.Windows.Ink.StrokeCollection?displayProperty=nameWithType>.  
  
 Następujące pary ilustracje porównuje modele obiektów danych pisma odręcznego.  Na Windows Forms i COM platformach [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) obiektu ogranicza okres istnienia [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) obiektów i pakietów pióra, należą do poszczególnych pociągnięć.  Co najmniej dwóch pociągnięć może odwoływać się takie same [Microsoft.Ink.DrawingAttributes](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583636(v=vs.90)) obiektu, jak pokazano na poniższej ilustracji.  
  
 ![Diagram modelu obiektów pisma odręcznego dla modelu COM&#47;Winforms. ](./media/ink-inkownsstrokes.png "Ink_InkOwnsStrokes")  
  
 Na [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], każdy <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> jest wspólne obiekt środowiska uruchomieniowego języka, który istnieje tak długo, jak coś, co ma odwołanie do niej.  Każdy <xref:System.Windows.Ink.Stroke> odwołania <xref:System.Windows.Input.StylusPointCollection> i <xref:System.Windows.Ink.DrawingAttributes?displayProperty=nameWithType> obiektu, które są również obiekty środowiska uruchomieniowego języka wspólnego.  
  
 ![Diagram modelu obiektów pisma odręcznego dla WPF. ](./media/ink-wpfinkobjectmodel.png "Ink_WPFInkObjectModel")  
  
 W poniższej tabeli porównano jak wykonywać niektóre typowe zadania na [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] platformy i platformy Windows Forms i COM.  
  
|Zadanie|Windows Presentation Foundation|Windows Forms i COM|  
|----------|-------------------------------------|---------------------------|  
|Zapisz pisma odręcznego|<xref:System.Windows.Ink.StrokeCollection.Save%2A>|[Microsoft.Ink.Ink.Save](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571335(v=vs.90))|  
|Ładowanie pisma odręcznego|Tworzenie <xref:System.Windows.Ink.StrokeCollection> z <xref:System.Windows.Ink.StrokeCollection.%23ctor%2A> konstruktora.|[Microsoft.Ink.Ink.Load](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms569609(v=vs.90))|  
|Przeprowadzanie testu trafienia|<xref:System.Windows.Ink.StrokeCollection.HitTest%2A>|[Microsoft.Ink.Ink.HitTest](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571330(v=vs.90))|  
|Skopiuj pisma odręcznego|<xref:System.Windows.Controls.InkCanvas.CopySelection%2A>|[Microsoft.Ink.Ink.ClipboardCopy](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571316(v=vs.90))|  
|Wklejanie pisma odręcznego|<xref:System.Windows.Controls.InkCanvas.Paste%2A>|[Microsoft.Ink.Ink.ClipboardPaste](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571318(v=vs.90))|  
|Dostęp do właściwości niestandardowe zbieranie pociągnięć|<xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A> (właściwości są przechowywane wewnętrznie i dostępne za pośrednictwem <xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A>, <xref:System.Windows.Ink.StrokeCollection.RemovePropertyData%2A>, i <xref:System.Windows.Ink.StrokeCollection.ContainsPropertyData%2A>)|Use [Microsoft.Ink.Ink.ExtendedProperties](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms582214(v=vs.90))|  
  
### <a name="sharing-ink-between-platforms"></a>Udostępnianie pisma odręcznego między platformami  
 Mimo że platformy mają różne modele obiektów dla danych pisma odręcznego, udostępnianie danych między platformami jest bardzo proste. Poniższe przykłady Zapisz pisma odręcznego z aplikacji Windows Forms i załadować pisma odręcznego w aplikacji Windows Presentation Foundation.  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#SaveWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewinforms)]
[!code-vb[WinFormWPFInk#SaveWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewinforms)]  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#LoadWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwpf)]
[!code-vb[WinFormWPFInk#LoadWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwpf)]  
  
 Poniższe przykłady pisma odręcznego z aplikacji Windows Presentation Foundation i załadować pisma odręcznego w aplikacji Windows Forms.  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#SaveWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewpf)]
[!code-vb[WinFormWPFInk#SaveWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewpf)]  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#LoadWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwinforms)]
[!code-vb[WinFormWPFInk#LoadWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwinforms)]
## <a name="events-from-the-tablet-pen"></a>Zdarzenia z pióra  

 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)), [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)), i [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) na Windows Forms i COM odebrane zdarzenia z platformami po użytkownik dane wejściowe piórem danych. [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) lub [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) dołączonego do okna lub kontrolki i może subskrybować zdarzenia wygenerowane przez usługę danych wejściowych typu tablet. Wątek, w których odbywa się te zdarzenia zależy od tego, czy zdarzenia są wywoływane za pomocą pióra, źródłem jest mysz lub programowo. Aby uzyskać więcej informacji dotyczących wielowątkowości w odniesieniu do tych zdarzeń, zobacz [Ogólne zagadnienia wielowątkowości](/windows/desktop/tablet/general-threading-considerations) i [wątki w może wyzwalać zdarzenia](/windows/desktop/tablet/threads-on-which-an-event-can-fire).  
  
 Na platformie Windows Presentation Foundation <xref:System.Windows.UIElement> klasa zawiera zdarzenia dla piórem. Oznacza to, że każdy formant uwidacznia pełny zestaw zdarzeń pióra.  Zdarzenia pióra mają tunelowania Propagacja zdarzeń pary i zawsze wykonywane dla wątku aplikacji.  Aby uzyskać więcej informacji, zobacz [Przegląd zdarzeń kierowane](routed-events-overview.md).  
  
 Na poniższym diagramie przedstawiono porównanie modeli obiektów dla klas, które wywoływanie zdarzeń pióra. Model obiektów programu Windows Presentation Foundation zawiera tylko zdarzenia propagacji, a nie tunelowania odpowiedniki zdarzeń.  
  
 ![Diagram z porównaniem zdarzeń w WPF i Winforms. ](./media/ink-stylusevents.png "Ink_StylusEvents")  
  
## <a name="pen-data"></a>Dane pióra  
 Wszystkich trzech platformach zapewniają sposoby przechwytywania i manipulowanie danymi, które pochodzą z pióra.  Na Windows Forms i COM, jest to osiągane przez utworzenie [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90)), dołączanie do niego okna lub kontroli i tworzenie implementujące klasy [ Microsoft.StylusInput.IStylusSyncPlugin](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms575201(v=vs.90)) lub [Microsoft.StylusInput.IStylusAsyncPlugin](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms575194(v=vs.90)) interfejsu. Niestandardowa wtyczka jest dodawane do kolekcji wtyczki [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90)). Aby uzyskać więcej informacji na temat modelu obiektowego zobacz [Architektura interfejsów API StylusInput](/windows/desktop/tablet/architecture-of-the-stylusinput-apis).  
  
 Na [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] platformy <xref:System.Windows.UIElement> klasa udostępnia kolekcję dodatków plug-in, podobne w projekcie, która ma [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90)).  Do przechwycenia pióra danych, należy utworzyć klasę, która dziedziczy po elemencie <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> i dodać obiekt do <xref:System.Windows.UIElement.StylusPlugIns%2A> zbiór <xref:System.Windows.UIElement>. Aby uzyskać więcej informacji na temat interakcji, zobacz [przechwytywanie danych wejściowych z pisaka](intercepting-input-from-the-stylus.md).  
  
 Na wszystkich platformach z puli wątków odbiera dane pisma odręcznego za pomocą pióra, zdarzeń i wysyła je do wątku aplikacji.  Aby uzyskać więcej informacji dotyczących wielowątkowości w modelu COM i na platformach Windows, zobacz [wielowątkowości dotyczące interfejsów API StylusInput](/windows/desktop/tablet/threading-considerations-for-the-stylusinput-apis).  Aby uzyskać więcej informacji na temat wątkowości na oprogramowanie do prezentacji Windows zobacz [Model wątkowości typu atrament](the-ink-threading-model.md).  
  
 Na poniższej ilustracji przedstawiono porównanie modeli obiektów dla klas, które odbiera pióra danych w puli wątków pióra.  
  
 ![Diagram StylusPlugin — model WPF i Winforms. ](./media/ink-stylusplugins.png "Ink_StylusPlugins")
