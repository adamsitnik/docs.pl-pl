---
title: 'Instrukcje: Tworzenie kształtu przy użyciu elementu PathGeometry'
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], creating with PathGeometry class
- graphics [WPF], shapes
ms.assetid: 49a4a8b7-e738-45be-8dac-b54a6d8f5b21
ms.openlocfilehash: b0ab703596612524881ab892a1095b0f49cd1551
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904319"
---
# <a name="how-to-create-a-shape-by-using-a-pathgeometry"></a>Instrukcje: Tworzenie kształtu przy użyciu elementu PathGeometry
W tym przykładzie pokazano, jak utworzyć kształt używając <xref:System.Windows.Media.PathGeometry> klasy. <xref:System.Windows.Media.PathGeometry> obiekty składają się z co najmniej jeden <xref:System.Windows.Media.PathFigure> obiektów; każdy <xref:System.Windows.Media.PathFigure> reprezentuje różne "rysunek" lub kształtu. Każdy <xref:System.Windows.Media.PathFigure> sam składa się z co najmniej jeden <xref:System.Windows.Media.PathSegment> obiektów, każdy reprezentuje połączone część rysunek lub kształtu. Segment typy obejmują <xref:System.Windows.Media.LineSegment>, <xref:System.Windows.Media.ArcSegment>, i <xref:System.Windows.Media.BezierSegment>.  
  
## <a name="example"></a>Przykład  
 W poniższym przykładzie użyto <xref:System.Windows.Media.PathGeometry> utworzyć trójkąt. <xref:System.Windows.Media.PathGeometry> Jest wyświetlana przy użyciu <xref:System.Windows.Shapes.Path> elementu.  
  
 [!code-xaml[GeometrySample#49](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#49)]  
  
 Poniższa ilustracja przedstawia kształtem utworzona w poprzednim przykładzie.  
  
 ![A PathGeometry](./media/wcpsdk-graphicsmm-pathgeometry-triangle.gif "wcpsdk_graphicsmm_pathgeometry_triangle")  
Trójkąt utworzone przy PathGeometry  
  
 W poprzednim przykładzie pokazano, jak utworzyć kształt stosunkowo prosty trójkąt. Element <xref:System.Windows.Media.PathGeometry> może również służyć do utworzenia bardziej złożonych kształtów, między innymi, krzywych i łuki. Aby uzyskać przykłady, zobacz [tworzenie łuku eliptycznego](how-to-create-an-elliptical-arc.md), [Utwórz krzywą Beziera trzeciego stopnia](how-to-create-a-cubic-bezier-curve.md), i [Utwórz krzywą Beziera drugiego stopnia](how-to-create-a-quadratic-bezier-curve.md).  
  
 W tym przykładzie jest częścią większego przykładu; Aby uzyskać pełny przykład, zobacz [przykładowe geometrii](https://go.microsoft.com/fwlink/?LinkID=159989).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.GeometryDrawing>
- [Geometria — przegląd](geometry-overview.md)
- [Przykładowe geometrii](https://go.microsoft.com/fwlink/?LinkID=159989)
