---
title: 'Instrukcje: Przekształcanie pędzla'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], rotating contents
- brushes [WPF], Transform property
- rotating contents of brushes [WPF]
ms.assetid: ebada2f9-f01f-4863-9ea2-c2e4e51610f1
ms.openlocfilehash: a83f3b1c046e94faa8816e8c310f438b4711048a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769378"
---
# <a name="how-to-transform-a-brush"></a>Instrukcje: Przekształcanie pędzla
W tym przykładzie pokazano, jak przekształcić <xref:System.Windows.Media.Brush> obiektów przy użyciu ich właściwości dwóch transformacji: <xref:System.Windows.Media.Brush.RelativeTransform%2A> i <xref:System.Windows.Media.Brush.Transform%2A>.  
  
 W poniższych przykładach używane <xref:System.Windows.Media.RotateTransform> obracanie zawartości <xref:System.Windows.Media.ImageBrush> o 45 stopni.  
  
 Poniższa ilustracja przedstawia <xref:System.Windows.Media.ImageBrush> bez <xref:System.Windows.Media.RotateTransform>, za pomocą <xref:System.Windows.Media.RotateTransform> stosowane do <xref:System.Windows.Media.Brush.RelativeTransform%2A> właściwości i <xref:System.Windows.Media.RotateTransform> stosowane do <xref:System.Windows.Media.Brush.Transform%2A> właściwości.  
  
 ![Pędzel RelativeTransform i przekształcać ustawienia](./media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk_graphicsmm_transformandrelativetransform")  
  
## <a name="example"></a>Przykład  
 Pierwszy przykład dotyczy <xref:System.Windows.Media.RotateTransform> do <xref:System.Windows.Media.Brush.RelativeTransform%2A> właściwość <xref:System.Windows.Media.ImageBrush>. <xref:System.Windows.Media.RotateTransform.CenterX%2A> i <xref:System.Windows.Media.RotateTransform.CenterY%2A> właściwości <xref:System.Windows.Media.RotateTransform> obiektu są ustawione na 0,5, czyli współrzędne względne punktu centralnego tej zawartości. W rezultacie <xref:System.Windows.Media.ImageBrush> zawartości obraca się o jej środka.  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 Drugi przykład dotyczy także <xref:System.Windows.Media.RotateTransform> do <xref:System.Windows.Media.ImageBrush>; Jednakże, w tym przykładzie użyto <xref:System.Windows.Media.Brush.Transform%2A> właściwości zamiast <xref:System.Windows.Media.Brush.RelativeTransform%2A> właściwości.  
  
 Aby obrócić pędzla o jej środka, w przykładzie <xref:System.Windows.Media.RotateTransform.CenterX%2A> i <xref:System.Windows.Media.RotateTransform.CenterY%2A> właściwości <xref:System.Windows.Media.RotateTransform> obiektu współrzędne bezwzględne. Ponieważ pędzel farby prostokąt, który jest 175 pikseli 90, jest punktu centralnego prostokąt (87.5, 45).  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 Aby uzyskać opis sposób <xref:System.Windows.Media.Brush.RelativeTransform%2A> i <xref:System.Windows.Media.Brush.Transform%2A> właściwości pracy, zobacz [Przekształcanie pędzla — Przegląd](brush-transformation-overview.md).  
  
 Aby uzyskać pełny przykład, zobacz [przykład pędzle](https://go.microsoft.com/fwlink/?LinkID=159973). Aby uzyskać więcej informacji na temat pędzle, zobacz [malowanie jednolitymi kolorami i gradientami — Przegląd](painting-with-solid-colors-and-gradients-overview.md).  
  
## <a name="see-also"></a>Zobacz także

- [Przekształcanie pędzla — przegląd](brush-transformation-overview.md)
- [Malowanie jednolitymi kolorami i gradientami — przegląd](painting-with-solid-colors-and-gradients-overview.md)
- [Przekształcenia — przegląd](transforms-overview.md)
