---
title: mc:ProcessContent — Atrybut
ms.date: 03/30/2017
helpviewer_keywords:
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: 2689b2c8-b4dc-4b71-b9bd-f95e619122d7
ms.openlocfilehash: dde304cc2b9db9cb01f9264ca1359b8979512cfa
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458778"
---
# <a name="mcprocesscontent-attribute"></a>mc:ProcessContent — Atrybut
Określa, które elementy [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] powinny nadal mieć zawartość przetworzoną przez odpowiednie elementy nadrzędne, nawet jeśli bezpośredni element nadrzędny może zostać zignorowany przez procesor [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] z powodu określenia [atrybutu MC:](mc-ignorable-attribute.md)Ignore. Atrybut `mc:ProcessContent` obsługuje zgodność znaczników zarówno dla niestandardowego mapowania przestrzeni nazw, jak i dla [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] wersji.  
  
## <a name="xaml-attribute-usage"></a>Użycie atrybutu języka XAML  
  
```xaml  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...  
  mc:ProcessContent="ignorablePrefix:ThisElementCanBeIgnored"  
>  
    <ignorablePrefix:ThisElementCanBeIgnored>  
        [content]  
    </ignorablePrefix:ThisElementCanBeIgnored>  
</object>  
```  
  
## <a name="xaml-values"></a>Wartości XAML  
  
|||  
|-|-|  
|*ignorablePrefix*|Dowolny prawidłowy ciąg prefiksu na specyfikację XML 1,0.|  
|*ignorableUri*|Dowolny prawidłowy identyfikator URI służący do wyznaczania przestrzeni nazw, zgodnie ze specyfikacją XML 1,0.|  
|*ThisElementCanBeIgnored*|Element, który może być ignorowany przez implementacje procesora [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], jeśli nie można rozpoznać typu podstawowego.|  
|*treści*|*ThisElementCanBeIgnored* jest oznaczony jako ignorowany. Jeśli procesor zignoruje ten element, *[zawartość]* jest przetwarzany przez *obiekt*.|  
  
## <a name="remarks"></a>Uwagi  
 Domyślnie procesor [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] zignoruje zawartość w ignorowanym elemencie. Można określić konkretny element według `mc:ProcessContent`, a procesor [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] będzie kontynuował przetwarzanie zawartości w ignorowanym elemencie. Zwykle jest to używane, jeśli zawartość jest zagnieżdżona w kilku tagach, co najmniej jeden z nich jest ignorowany i co najmniej jeden z nich nie jest ignorowany.  
  
 W atrybucie można określić wiele prefiksów, używając separatora spacji, na przykład: `mc:ProcessContent="ignore:Element1 ignore:Element2"`.  
  
 Przestrzeń nazw `http://schemas.openxmlformats.org/markup-compatibility/2006` definiuje inne elementy i atrybuty, które nie są udokumentowane w tym obszarze zestawu SDK. Aby uzyskać więcej informacji, zobacz [Specyfikacja zgodności znaczników XML](https://go.microsoft.com/fwlink/?LinkId=73824).  
  
## <a name="see-also"></a>Zobacz także

- [mc:Ignorable, atrybut](mc-ignorable-attribute.md)
- [Przegląd XAML (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
