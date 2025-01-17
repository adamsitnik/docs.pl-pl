---
title: 'Porady: implementowanie ICommandSource'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ICommandSource interfaces [WPF], implementing
ms.assetid: 7452dd39-6e11-44bf-806a-31d87f3772ac
ms.openlocfilehash: 974b145a125a158bcafff93f8e9bc11001e00bf1
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73453580"
---
# <a name="how-to-implement-icommandsource"></a>Porady: implementowanie ICommandSource
Ten przykład przedstawia sposób tworzenia źródła poleceń przez implementację <xref:System.Windows.Input.ICommandSource>.  Źródło polecenia jest obiektem, który wie, jak wywołać polecenie.  Interfejs <xref:System.Windows.Input.ICommandSource> uwidacznia trzy elementy członkowskie: <xref:System.Windows.Input.ICommandSource.Command%2A>, <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>i <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>.  <xref:System.Windows.Input.ICommandSource.Command%2A> to polecenie, które zostanie wywołane. <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> jest typem danych zdefiniowanym przez użytkownika, który jest przesyłany ze źródła polecenia do metody, która obsługuje polecenie. <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> jest obiektem, na którym jest wykonywane polecenie.  
  
 W tym przykładzie tworzona jest Klasa, która podklasuje formant <xref:System.Windows.Controls.Slider> i implementuje <xref:System.Windows.Input.ICommandSource>.  
  
## <a name="example"></a>Przykład  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] udostępnia wiele klas, które implementują <xref:System.Windows.Input.ICommandSource>, takie jak <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.MenuItem>i <xref:System.Windows.Controls.ListBoxItem>.  Źródło polecenia definiuje, jak wywołuje polecenie.   <xref:System.Windows.Controls.Button> i <xref:System.Windows.Controls.MenuItem> wywołać polecenie po kliknięciu.  <xref:System.Windows.Controls.ListBoxItem> wywołuje polecenie po dwukrotnym kliknięciu. Te klasy stają się źródłami poleceń, gdy ich Właściwość <xref:System.Windows.Input.ICommandSource.Command%2A> jest ustawiona.  
  
 Na potrzeby tego przykładu wywołamy polecenie, gdy suwak zostanie przesunięty lub dokładniej, gdy właściwość <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> zostanie zmieniona.  
  
 Poniżej znajduje się definicja klasy.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceClassDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourceclassdefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceClassDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourceclassdefinition)]  
  
 Następnym krokiem jest zaimplementowanie elementów członkowskich <xref:System.Windows.Input.ICommandSource>.  W tym przykładzie właściwości są implementowane jako obiekty <xref:System.Windows.DependencyProperty>.  Dzięki temu właściwości mogą używać powiązania danych.  Aby uzyskać więcej informacji na temat klasy <xref:System.Windows.DependencyProperty>, zobacz [Omówienie właściwości zależności](dependency-properties-overview.md).  Aby uzyskać więcej informacji na temat powiązania danych, zobacz [Omówienie powiązania danych](../../../desktop-wpf/data/data-binding-overview.md).  
  
 Tutaj jest wyświetlana tylko Właściwość <xref:System.Windows.Input.ICommandSource.Command%2A>.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandpropertydefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandpropertydefinition)]  
  
 Poniżej znajduje się <xref:System.Windows.DependencyProperty> zmiany wywołania zwrotnego.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandChanged](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandchanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandChanged](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandchanged)]  
  
 Następnym krokiem jest dodanie i usunięcie polecenia, które jest skojarzone ze źródłem polecenia.  Właściwość <xref:System.Windows.Input.ICommandSource.Command%2A> nie może zostać po prostu zastąpiona po dodaniu nowego polecenia, ponieważ programy obsługi zdarzeń skojarzone z poprzednim poleceniem, jeśli istnieje, należy najpierw usunąć.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcehookunhookcommands)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcehookunhookcommands)]  
  
 Ostatnim krokiem jest utworzenie logiki dla programu obsługi <xref:System.Windows.Input.ICommand.CanExecuteChanged> i metody <xref:System.Windows.Input.ICommand.Execute%2A>.  
  
 Zdarzenie <xref:System.Windows.Input.ICommand.CanExecuteChanged> powiadamia źródło polecenia, że możliwość wykonania polecenia w bieżącym obiekcie docelowym polecenia mogła ulec zmianie.  Gdy źródło polecenia odbiera to zdarzenie, zazwyczaj wywołuje metodę <xref:System.Windows.Input.ICommand.CanExecute%2A> przy użyciu polecenia.  Jeśli polecenie nie może zostać wykonane na bieżącym obiekcie docelowym polecenia, źródło polecenia spowoduje zwykle wyłączenie samego siebie.  Jeśli polecenie można wykonać na bieżącym obiekcie docelowym polecenia, źródło polecenia będzie zazwyczaj umożliwiało samodzielne.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandCanExecuteChanged](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandcanexecutechanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandCanExecuteChanged](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandcanexecutechanged)]  
  
 Ostatnim krokiem jest metoda <xref:System.Windows.Input.ICommand.Execute%2A>.  Jeśli polecenie jest <xref:System.Windows.Input.RoutedCommand>, Metoda <xref:System.Windows.Input.RoutedCommand> <xref:System.Windows.Input.RoutedCommand.Execute%2A> jest wywoływana; w przeciwnym razie wywoływana jest metoda <xref:System.Windows.Input.ICommand> <xref:System.Windows.Input.ICommand.Execute%2A>.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandExecute](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandexecute)]
 [!code-vb[ImplementICommandSource#ImplementICommandExecute](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandexecute)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Input.ICommandSource>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.Input.RoutedCommand>
- [Przegląd poleceń](commanding-overview.md)
