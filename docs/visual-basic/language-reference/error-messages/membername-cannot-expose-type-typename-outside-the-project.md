---
title: Element „<membername>” nie może ujawniać typu „<typename>” poza projektem za pomocą elementu <containertype> „<containertypename>”
ms.date: 07/20/2015
f1_keywords:
- bc30909
- vbc30909
helpviewer_keywords:
- BC30909
ms.assetid: ffa7395d-e182-4087-8ce8-079810fdae54
ms.openlocfilehash: ca67e74d7790352bd1842cb8a59fe1525af6e18c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700901"
---
# <a name="membername-cannot-expose-type-typename-outside-the-project-through-containertype-containertypename"></a>element "\<membername >" nie może ujawnić typu "\<typename >" poza projektem za pomocą \<containertype > "\<containertypename >"
Zmienna, parametr procedury lub return funkcji jest ujawniany poza kontenerem, ale jest zadeklarowany jako typ, który nie może być ujawniony poza kontenerem.  
  
 Poniższy kod szkieletowy przedstawia sytuację, która generuje ten błąd.  
  
```vb  
Private Class privateClass  
End Class  
Public Class mainClass  
    Public exposedVar As New privateClass  
End Class  
```  
  
 Typ, który jest zadeklarowany `Protected`, `Friend`, `Protected Friend` lub `Private` ma ograniczony dostęp poza kontekstem deklaracji. Korzystanie z niego jako typu danych zmiennej z mniejszym ograniczonym dostępem mogłoby spowodować pokonanie tego celu. W poprzednim kodzie szkieletowym `exposedVar` jest `Public` i uwidacznia `privateClass` do kodu, który nie powinien mieć do niego dostępu.  
  
 **Identyfikator błędu:** BC30909  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Zmień poziom dostępu zmiennej, parametru procedury lub zwracanej funkcji na co najmniej tak restrykcyjny jak poziom dostępu jego typu danych.  
  
## <a name="see-also"></a>Zobacz także

- [Poziomy dostępu w Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
