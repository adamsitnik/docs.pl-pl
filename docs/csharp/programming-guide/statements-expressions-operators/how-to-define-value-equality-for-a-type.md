---
title: 'Porady: Definiowanie równości wartości dla typu - C# Programming Guide'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- overriding Equals method [C#]
- object equivalence [C#]
- Equals method [C#], overriding
- value equality [C#]
- equivalence [C#]
ms.assetid: 4084581e-b931-498b-9534-cf7ef5b68690
ms.openlocfilehash: 0e1c736c7a2826c1218cb078a6e9f874b3b72c3c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64755011"
---
# <a name="how-to-define-value-equality-for-a-type-c-programming-guide"></a>Porady: Definiowanie równości wartości dla typu (C# Programming Guide)

Po zdefiniowaniu klasy lub struktury, możesz zdecydować, czy warto tworzyć niestandardowych definicji równości wartość (lub odpowiednik) dla typu. Zazwyczaj równość wartości zaimplementować w sytuacji, gdy oczekiwano obiektów tego typu do dodania do kolekcji jakieś lub w przypadku, gdy ich głównym celem jest zapisanie zestawu pól lub właściwości. Swojej definicji równości wartość można oprzeć na porównanie wszystkie pola i właściwości w typie lub można utworzyć definicję na podzbiorze. Jednak w obu przypadkach, a w klas i struktur, implementacji należy wykonać pięć gwarancje równoważności:  
  
1. `x.Equals(x)` Zwraca `true`. Jest to właściwość zwrotnej.  
  
2. `x.Equals(y)` zwraca taką samą wartość jak `y.Equals(x)`. Jest to właściwość symetryczne.  
  
3. Jeśli `(x.Equals(y) && y.Equals(z))` zwraca `true`, następnie `x.Equals(z)` zwraca `true`. Jest to właściwość przechodnie.  
  
4. Kolejne wywołania `x.Equals(y)` zwracają taką samą wartość, tak długo, jak obiekty odwołuje się x i y nie są modyfikowane.  
  
5. `x.Equals(null)` Zwraca `false`. Jednak `null.Equals(null)` zgłasza wyjątek; nie stosuje reguły dwóch powyżej.  
  
 Wszystkie struktury, który zdefiniujesz już ma domyślną implementację równość wartości, która jest dziedziczona z <xref:System.ValueType?displayProperty=nameWithType> zastępowania <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> metody. Ta implementacja używa odbicia, aby sprawdzić wszystkie pola i właściwości w typie. Chociaż ta implementacja daje poprawne wyniki, jest stosunkowo powolny w porównaniu do niestandardowych implementacji, które piszesz specjalnie dla typu.  
  
 Szczegóły implementacji na równoważność wartości są różne klasy i struktury. Zarówno klasy i struktury wymagają jednak te same podstawowe kroki do wykonania porównania:  
  
1. Zastąp [wirtualnego](../../language-reference/keywords/virtual.md) <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> metody. W większości przypadków, implementacja `bool Equals( object obj )` wywołać tylko do określonego typu `Equals` metodę, która jest implementacją <xref:System.IEquatable%601?displayProperty=nameWithType> interfejsu. (Zobacz krok 2).  
  
2. Implementowanie <xref:System.IEquatable%601?displayProperty=nameWithType> interfejs, dostarczając specyficznych dla typu `Equals` metody. Jest to, gdy wykonywane jest porównanie równoważności rzeczywistych. Na przykład można zdecydować zdefiniować równości, porównując tylko jeden lub dwa pola w danego typu. Nie zgłaszają wyjątki od `Equals`. Aby uzyskać tylko do klasy: Ta metoda powinna zbadać tylko pola, które są zadeklarowane w klasie. Powinien wywoływać `base.Equals` zbadanie pola, które znajdują się w klasie bazowej. (Nie należy tego robić, jeśli typ dziedziczy bezpośrednio z <xref:System.Object>, ponieważ <xref:System.Object> implementacji <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> przeprowadza sprawdzanie odwołania równości.)  
  
3. Opcjonalne, ale zalecane: Przeciążenia [ == ](../../language-reference/operators/equality-operators.md#equality-operator-) i [! =](../../language-reference/operators/equality-operators.md#inequality-operator-) operatorów.  
  
4. Zastąp <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType> tak, aby dwa obiekty, które mają równość wartości w taki sam wygenerować wartość skrótu.  
  
5. Opcjonalne: Aby zapewnić obsługę definicji dla "większe niż" lub "poniżej", należy zaimplementować <xref:System.IComparable%601> interfejsu dla danego typu, a także przeciążać [ <= ](../../language-reference/operators/comparison-operators.md#less-than-or-equal-operator-) i [ >= ](../../language-reference/operators/comparison-operators.md#greater-than-or-equal-operator-) operatorów.  
  
 Pierwszy przykład, który następuje po pokazuje implementację klasy. Drugi przykład przedstawia implementację struktury.  

## <a name="example"></a>Przykład

 Poniższy przykład pokazuje, jak zaimplementować równość wartości w klasie (typ odwołania).  
  
 [!code-csharp[csProgGuideStatements#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#19)]  
  
 W klasach (typy referencyjne) Domyślna implementacja obu <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> metody wykonuje porównanie równości odwołań, nie sprawdzanie równości wartości. Gdy implementujący zastępuje metodę wirtualną, celem jest zapewnienie semantyka porównania wartości.  
  
 `==` i `!=` operatory mogą być używane z klasy, nawet wtedy, gdy klasa nie przeciążać je. Jednak to zachowanie domyślne jest sprawdzania równości odwołań. W klasie, jeśli przeładujesz `Equals` metody powinien przeciążać `==` i `!=` operatorów, ale nie jest wymagane.  

## <a name="example"></a>Przykład

 Poniższy przykład pokazuje, jak zaimplementować równość wartości w strukturze (typ wartości):  
  
 [!code-csharp[csProgGuideStatements#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#20)]  
  
 Dla struktur, domyślna Implementacja klasy <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> (czyli wersji zastąpione w <xref:System.ValueType?displayProperty=nameWithType>) przeprowadza sprawdzanie równość wartości przy użyciu odbicia do porównywania wartości każdego pola w typie. Gdy implementujący zastępuje wirtualny `Equals` metody w strukturze, celem jest, aby zapewnić bardziej wydajny sposób sprawdzanie równość wartości i, opcjonalnie, na podstawie na pewien podzbiór właściwości lub pola struktury.  
  
 [ == ](../../language-reference/operators/equality-operators.md#equality-operator-) i [! =](../../language-reference/operators/equality-operators.md#inequality-operator-) operatorów nie może działać na struktury, chyba że struktura jawnie je przeciążenia.  
  
## <a name="see-also"></a>Zobacz także

- [Porównywanie równości](equality-comparisons.md)
- [Przewodnik programowania w języku C#](../index.md)
