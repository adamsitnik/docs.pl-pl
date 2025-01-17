---
title: 'Instrukcje: Wywoływanie okna dialogowego drukowania'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking print dialogs [WPF]
- print dialogs [WPF], invoking
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
ms.openlocfilehash: 4bad8158925fea8af529f70f92aad74e2a6bbec0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254109"
---
# <a name="how-to-invoke-a-print-dialog"></a>Instrukcje: Wywoływanie okna dialogowego drukowania
Aby umożliwić drukowanie z poziomu aplikacji, można po prostu utworzyć i otworzyć <xref:System.Windows.Controls.PrintDialog> obiekt.  
  
## <a name="example"></a>Przykład  
 Kontrolka zawiera pojedynczy punkt wejścia dla, [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]konfiguracji i dla każdego zadania XPS. <xref:System.Windows.Controls.PrintDialog> Kontrolka jest łatwa w użyciu i można ją utworzyć przy użyciu [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] znacznika lub kodu. W poniższym przykładzie pokazano, jak utworzyć wystąpienie i otworzyć formant w kodzie oraz jak drukować z niego. Przedstawiono w nim również, jak upewnić się, że w oknie dialogowym zostanie wyświetlona opcja ustawienia określonego zakresu stron. Przykładowy kod założono, że w katalogu głównym dysku C: znajduje się plik FixedDocumentSequence. XPS.  
  
 [!code-csharp[printdialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 Po otwarciu okna dialogowego użytkownicy będą mogli wybierać spośród drukarek zainstalowanych na komputerze. Będą również mieć możliwość wyboru [składnika zapisywania dokumentów XPS firmy Microsoft](https://go.microsoft.com/fwlink/?LinkId=147319) w celu utworzenia pliku specyfikacji XML Paper Specification (XPS) zamiast drukowania.  
  
> [!NOTE]
> Kontrolka, która została omówiona w tym temacie, <xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType> nie powinna być mylić ze składnikiem Windows Forms. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType>  
  
 Dokładnie mówiąc, można użyć <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> metody bez konieczności otwierania okna dialogowego. W tym sensie formant może być używany jako niewidoczny składnik drukowania. Jednak ze względu na wydajność lepszym <xref:System.Printing.PrintQueue.AddJob%2A> rozwiązaniem jest użycie metody lub jednej z <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> wielu <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> metod <xref:System.Windows.Xps.XpsDocumentWriter>. Aby uzyskać więcej informacji na ten temat, zobacz programowe [Drukowanie plików XPS](how-to-programmatically-print-xps-files.md) i.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Controls.PrintDialog>
- [Dokumenty w WPF](documents-in-wpf.md)
- [Przegląd drukowania](printing-overview.md)
- [Moduł zapisywania dokumentów XPS firmy Microsoft](https://go.microsoft.com/fwlink/?LinkId=147319)
