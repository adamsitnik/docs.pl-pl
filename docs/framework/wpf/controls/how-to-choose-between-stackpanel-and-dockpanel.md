---
title: 'Instrukcje: Wybieranie między elementami StackPanel i DockPanel'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [WPF], DockPanel
- DockPanel control [WPF], StackPanel control compared to
- StackPanel control [WPF], DockPanel control compared to
- controls [WPF], StackPanel
ms.assetid: f9239086-451f-42e6-81f7-ef89ef349742
ms.openlocfilehash: 8338421dfb1bea856c15edf9d324cec955584f9f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911246"
---
# <a name="how-to-choose-between-stackpanel-and-dockpanel"></a>Instrukcje: Wybieranie między elementami StackPanel i DockPanel
Ten przykład pokazuje, jak wybrać między za pomocą <xref:System.Windows.Controls.StackPanel> lub <xref:System.Windows.Controls.DockPanel> kiedy stos zawartość <xref:System.Windows.Controls.Panel>.  
  
## <a name="example"></a>Przykład  
 Chociaż można używać <xref:System.Windows.Controls.DockPanel> lub <xref:System.Windows.Controls.StackPanel> na stosie elementów podrzędnych, dwie kontrolki nie zawsze działają tak samo. Na przykład kolejność umieszczenie elementów podrzędnych może mieć wpływ na rozmiar elementów podrzędnych na <xref:System.Windows.Controls.DockPanel> , ale nie <xref:System.Windows.Controls.StackPanel>. Takie zachowanie różnych <xref:System.Windows.Controls.StackPanel> miary w kierunku układania na <xref:System.Double>.<xref:System.Double.PositiveInfinity>; jednak <xref:System.Windows.Controls.DockPanel> mierzy tylko dostępny rozmiar.  
  
 W poniższym przykładzie pokazano to główną różnicą między <xref:System.Windows.Controls.DockPanel> i <xref:System.Windows.Controls.StackPanel>.  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Controls.StackPanel>
- <xref:System.Windows.Controls.DockPanel>
- [Panele — omówienie](panels-overview.md)
