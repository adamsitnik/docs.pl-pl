---
title: Element „For Each” w typie „<typename>” jest niejednoznaczny, ponieważ typ implementuje wiele wystąpień elementu „System.Collections.Generic.IEnumerable(Of T)”.
ms.date: 07/20/2015
f1_keywords:
- vbc32096
- bc32096
helpviewer_keywords:
- BC32096
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
ms.openlocfilehash: bdfb6e9b1332db1f049bb2575e97215026efe0dd
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591764"
---
# <a name="for-each-on-type-typename-is-ambiguous-because-the-type-implements-multiple-instantiations-of-systemcollectionsgenericienumerableof-t"></a>"For Each" w typie "\<typename >" jest niejednoznaczny, ponieważ typ implementuje wiele wystąpień elementu "System.Collections.Generic.IEnumerable (Of T)"
A `For Each` Instrukcja określa zmienna iteratora, który ma więcej niż jedną <xref:System.Collections.IEnumerable.GetEnumerator%2A> metody.  
  
 Zmienna iteratora musi być typu, który implementuje <xref:System.Collections.IEnumerable?displayProperty=nameWithType> lub <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> interfejsu w jednym z `Collections` przestrzenie nazw programu .NET Framework. Istnieje możliwość dla klasy zaimplementować więcej niż jeden skonstruowanego interfejsu ogólnego, przy użyciu argumentu innego typu, dla każdego konstrukcji. Jeśli klasa, która wykonuje to jest używany dla zmiennej iteratora, zmienna ma więcej niż jedną <xref:System.Collections.IEnumerable.GetEnumerator%2A> metody. W takim przypadku języka Visual Basic nie można wybrać jakiej metody do wywołania.  
  
 **Identyfikator błędu:** BC32096  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Użyj [DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md) lub [TryCast Operator](../../../visual-basic/language-reference/operators/trycast-operator.md) rzutowanie typu zmiennej iteratora Definiowanie interfejsu <xref:System.Collections.IEnumerable.GetEnumerator%2A> metodę, której chcesz użyć.  
  
## <a name="see-also"></a>Zobacz także

- [For Each...Next, instrukcja](../../../visual-basic/language-reference/statements/for-each-next-statement.md)
- [Interfejsy](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
