---
title: Jak zastosować rysowanie do modelu 3-D
ms.date: 03/30/2017
helpviewer_keywords:
- drawings [WPF], applying to 3-D models
- 3-D models [WPF], applying drawings to
ms.assetid: 68357577-b7fc-446e-8be9-a8cc7df3a350
ms.openlocfilehash: 311a3ac1d9fa219a3a365d506d9d0c3e8b6bc229
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73459365"
---
# <a name="how-to-apply-a-drawing-to-a-3-d-model"></a>Jak zastosować rysowanie do modelu 3-D

Ten przykład pokazuje, jak używać <xref:System.Windows.Media.DrawingBrush> jako <xref:System.Windows.Media.Media3D.Material> stosowanego do modelu 3-D.

Poniższy kod definiuje <xref:System.Windows.Media.DrawingGroup> jako zawartość <xref:System.Windows.Media.DrawingBrush>.  <xref:System.Windows.Media.DrawingBrush> jest ustawiana jako właściwość <xref:System.Windows.Media.Media3D.DiffuseMaterial.Brush%2A> <xref:System.Windows.Media.Media3D.DiffuseMaterial> zastosowana do płaszczyzny 3-D.

> [!NOTE]
> Często pożądane jest zdefiniowanie złożonych obiektów i wartości, takich jak rysunek poniżej, jako zasoby, które mogą być ponownie używane i upraszczają kod. Aby uzyskać więcej informacji, zobacz [zasoby XAML](../../../desktop-wpf/fundamentals/xaml-resources-define.md) .

[!code-xaml[3DGallery_snip#ApplyDrawingToMaterialInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialinline1)]

## <a name="example"></a>Przykład

Poniższy kod pokazuje cały przykład.

[!code-xaml[3DGallery_snip#ApplyDrawingToMaterialExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialexamplewholepage)]

## <a name="see-also"></a>Zobacz także

- [Zasoby XAML](../../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [Tworzenie sceny 3D](how-to-create-a-3-d-scene.md)
- [Rysowanie obiektów — przegląd](drawing-objects-overview.md)
- [Grafika 3D — przegląd](3-d-graphics-overview.md)
