---
title: 'Instrukcje: Tworzenie niestandardowego trybu widoku dla kontrolki ListView'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView controls [WPF], creating custom View mode
ms.assetid: 71077349-eeb9-4344-ab29-b5df96df3314
ms.openlocfilehash: de11250a2e7529fba3b262e42b6714262738fa90
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910913"
---
# <a name="how-to-create-a-custom-view-mode-for-a-listview"></a>Instrukcje: Tworzenie niestandardowego trybu widoku dla kontrolki ListView
W tym przykładzie pokazano, jak utworzyć niestandardową <xref:System.Windows.Controls.ListView.View%2A> tryb <xref:System.Windows.Controls.ListView> kontroli.  
  
## <a name="example"></a>Przykład  
 Należy użyć <xref:System.Windows.Controls.ViewBase> klasy po utworzeniu widok niestandardowy <xref:System.Windows.Controls.ListView> kontroli. W poniższym przykładzie przedstawiono sposób wyświetlania, która jest wywoływana `PlainView`, który pochodzi od <xref:System.Windows.Controls.ViewBase> klasy.  
  
 [!code-csharp[ListViewCustomView#PlainView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/PlainView.cs#plainview)]
 [!code-vb[ListViewCustomView#PlainView](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/plainview.vb#plainview)]  
  
 Aby zastosować styl do widoku niestandardowego, należy użyć <xref:System.Windows.Style> klasy. W poniższym przykładzie zdefiniowano <xref:System.Windows.Style> dla `PlainView` trybu wyświetlania. W poprzednim przykładzie ten styl jest ustawiona jako wartość <xref:System.Windows.Controls.ViewBase.DefaultStyleKey%2A> właściwość, która jest zdefiniowana dla `PlainView`.  
  
 [!code-xaml[ListViewCustomView#PlainViewStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Themes/Generic.xaml#plainviewstyle)]  
  
 Aby zdefiniować układ danych w trybie widoku niestandardowego, należy zdefiniować <xref:System.Windows.DataTemplate> obiektu. W poniższym przykładzie zdefiniowano <xref:System.Windows.DataTemplate> można wyświetlić dane w `PlainView` trybu wyświetlania.  
  
 [!code-xaml[ListViewCustomView#PlainViewDataTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewdatatemplate)]  
  
 Poniższy przykład pokazuje jak zdefiniować <xref:System.Windows.ResourceKey> dla `PlainView` tryb widoku, który używa <xref:System.Windows.DataTemplate> zdefiniowanego w poprzednim przykładzie.  
  
 [!code-xaml[ListViewCustomView#PlainViewtileView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewtileview)]  
  
 A <xref:System.Windows.Controls.ListView> kontroli można użyć widoku niestandardowego, jeśli ustawisz <xref:System.Windows.Controls.ListView.View%2A> właściwości klucza zasobu. Poniższy przykład pokazuje, jak określić `PlainView` jako tryb widoku dla <xref:System.Windows.Controls.ListView>.  
  
 [!code-csharp[ListViewCustomView#ListViewtileViewmode](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml.cs#listviewtileviewmode)]
 [!code-vb[ListViewCustomView#ListViewtileViewmode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/window1.xaml.vb#listviewtileviewmode)]  
  
 Aby uzyskać pełny przykład, zobacz [ListView przy użyciu wielu widoków (C#)](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp) lub [ListView przy użyciu wielu Views(Visual Basic)](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [Tematy z instrukcjami](listview-how-to-topics.md)
- [ListView — omówienie](listview-overview.md)
- [GridView — omówienie](gridview-overview.md)
