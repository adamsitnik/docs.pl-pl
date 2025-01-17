---
title: Użycie obiektów DrawingVisual
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- visual layer [WPF], DrawingVisual objects
- DrawingVisual objects in visual layer [WPF]
ms.assetid: 0b4e711d-e640-40cb-81c3-8f5c59909b7d
ms.openlocfilehash: 4e6fc89b64f7b0acc1a0077708d567eb97e2868e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962828"
---
# <a name="using-drawingvisual-objects"></a>Użycie obiektów DrawingVisual
Ten temat zawiera omówienie sposobu używania <xref:System.Windows.Media.DrawingVisual> obiektów [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] w warstwie wizualnej.  
  
<a name="drawingvisual_object"></a>   
## <a name="drawingvisual-object"></a>Obiekt użycie DrawingVisual  
 <xref:System.Windows.Media.DrawingVisual> Jest lekkim klasą rysowania, która jest używana do renderowania kształtów, obrazów lub tekstu. Ta klasa jest uznawana za uproszczoną, ponieważ nie zapewnia obsługi układu ani zdarzeń, co zwiększa jego wydajność. Z tego powodu rysunki są idealnym rozwiązaniem dla tła i clipartów.  
  
<a name="drawingvisual_host_container"></a>   
## <a name="drawingvisual-host-container"></a>Kontener hosta użycie DrawingVisual  
 Aby można było używać <xref:System.Windows.Media.DrawingVisual> obiektów, należy utworzyć kontener hosta dla obiektów. Obiekt kontenera hosta musi być pochodną <xref:System.Windows.FrameworkElement> klasy, która zapewnia obsługę układu i obsługi zdarzeń, której nie ma w <xref:System.Windows.Media.DrawingVisual> klasie. Obiekt kontenera hosta nie wyświetla żadnych widocznych właściwości, ponieważ jego głównym celem jest zawieranie obiektów podrzędnych. Jednak Właściwość kontenera hosta musi być ustawiona na <xref:System.Windows.Visibility.Visible>; w przeciwnym razie żaden z elementów podrzędnych nie będzie widoczny. <xref:System.Windows.UIElement.Visibility%2A>  
  
 Podczas tworzenia obiektu kontenera hosta dla obiektów wizualnych należy przechowywać odwołania do obiektów wizualnych w <xref:System.Windows.Media.VisualCollection>elemencie. Użyj metody <xref:System.Windows.Media.VisualCollection.Add%2A> , aby dodać obiekt wizualny do kontenera hosta. W poniższym przykładzie tworzony jest obiekt kontenera hosta i trzy obiekty wizualne są dodawane do niego <xref:System.Windows.Media.VisualCollection>.  
  
 [!code-csharp[DrawingVisualSample#100](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[DrawingVisualSample#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#100)]  
  
> [!NOTE]
> Aby uzyskać kompletny przykład kodu, z którego został wyodrębniony poprzedni przykład kodu, zobacz [test trafień za pomocą przykładu DrawingVisuals](https://go.microsoft.com/fwlink/?LinkID=159994).  
  
<a name="creating_drawingvisual_objects"></a>   
## <a name="creating-drawingvisual-objects"></a>Tworzenie obiektów użycie DrawingVisual  
 Podczas tworzenia <xref:System.Windows.Media.DrawingVisual> obiektu nie ma zawartości rysunku. Możesz dodać tekst, grafikę lub zawartość obrazu, pobierając obiekt <xref:System.Windows.Media.DrawingContext> i rysując go. Jest zwracany przez <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A> wywołanie metody <xref:System.Windows.Media.DrawingVisual> obiektu. <xref:System.Windows.Media.DrawingContext>  
  
 Aby narysować prostokąt do <xref:System.Windows.Media.DrawingContext>, <xref:System.Windows.Media.DrawingContext.DrawRectangle%2A> Użyj metody <xref:System.Windows.Media.DrawingContext> obiektu. Podobne metody istnieją do rysowania innych typów zawartości. Po zakończeniu rysowania zawartości w <xref:System.Windows.Media.DrawingContext>programie <xref:System.Windows.Media.DrawingContext.Close%2A> Wywołaj metodę, aby zamknąć <xref:System.Windows.Media.DrawingContext> i zachować zawartość.  
  
 W poniższym przykładzie <xref:System.Windows.Media.DrawingVisual> tworzony jest obiekt, a prostokąt jest rysowany w jego <xref:System.Windows.Media.DrawingContext>.  
  
 [!code-csharp[DrawingVisualSample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[DrawingVisualSample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
<a name="creating_overrides"></a>   
## <a name="creating-overrides-for-frameworkelement-members"></a>Tworzenie zastąpień dla elementów członkowskich FrameworkElement  
 Obiekt kontenera hosta jest odpowiedzialny za zarządzanie kolekcją obiektów wizualnych. Wymaga to zastąpienia elementu członkowskiego kontenera hosta dla klasy pochodnej <xref:System.Windows.FrameworkElement> .  
  
 Na poniższej liście opisano dwa elementy członkowskie, które należy zastąpić:  
  
- <xref:System.Windows.FrameworkElement.GetVisualChild%2A>: Zwraca element podrzędny o określonym indeksie z kolekcji elementów podrzędnych.  
  
- <xref:System.Windows.FrameworkElement.VisualChildrenCount%2A>: Pobiera liczbę elementów podrzędnych wizualizacji w tym elemencie.  
  
 W poniższym przykładzie zaimplementowano zastąpienia dla dwóch <xref:System.Windows.FrameworkElement> elementów członkowskich.  
  
 [!code-csharp[DrawingVisualSample#102](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#102)]
 [!code-vb[DrawingVisualSample#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#102)]  
  
<a name="providing_hit_testing_support"></a>   
## <a name="providing-hit-testing-support"></a>Zapewnianie obsługi testowania trafień  
 Obiekt kontenera hosta może zapewnić obsługę zdarzeń, nawet jeśli nie wyświetla żadnych widocznych właściwości — jednak <xref:System.Windows.UIElement.Visibility%2A> właściwość musi być ustawiona na. <xref:System.Windows.Visibility.Visible> Dzięki temu można utworzyć procedurę obsługi zdarzeń dla kontenera hosta, który może zalewkować zdarzenia myszy, takie jak wydanie lewego przycisku myszy. Procedura obsługi zdarzeń może następnie zaimplementować testowanie trafień przez wywołanie <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> metody. <xref:System.Windows.Media.HitTestResultCallback> Parametr metody odnosi się do procedury zdefiniowanej przez użytkownika, której można użyć do określenia wyniku działania testu trafień.  
  
 W poniższym przykładzie obsługa testowania trafień jest zaimplementowana dla obiektu kontenera hosta i jego elementów podrzędnych.  
  
 [!code-csharp[DrawingVisualSample#103](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#103)]
 [!code-vb[DrawingVisualSample#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#103)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Media.DrawingVisual>
- <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>
- [Renderowanie grafiki WPF — przegląd](wpf-graphics-rendering-overview.md)
- [Test trafienia w warstwie wizualizacji](hit-testing-in-the-visual-layer.md)
