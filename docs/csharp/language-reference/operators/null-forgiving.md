---
title: '! (null-łagodniejszej) — C# odwołanie'
ms.date: 10/11/2019
f1_keywords:
- '!_CSharpKeyword'
helpviewer_keywords:
- null-forgiving operator [C#]
- '! operator [C#]'
ms.openlocfilehash: 21bbf8e1253641317750b911e052ee5ff0a0d063
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73036169"
---
# <a name="-null-forgiving-operator-c-reference"></a>! (null-łagodniejszej) — operatorC# (odwołanie)

Dostępne w C# 8,0 i nowszych operatory jednoargumentowe `!` jest operatorem null-łagodniejszej. W włączonym [kontekście dopuszczającym wartość null](../../nullable-references.md#nullable-annotation-context)należy użyć operatora null-łagodniejszej, aby zadeklarować wyrażenie `x` typu referencyjnego nie `null`: `x!`. Prefiks jednoargumentowy `!` operator jest [logicznym operatorem negacji](boolean-logical-operators.md#logical-negation-operator-).

Operator null-łagodniejszej nie ma wpływu w czasie wykonywania. Ma wpływ tylko na analizę przepływu statycznego kompilatora przez zmianę stanu null wyrażenia. W czasie wykonywania wyrażenie `x!` szacuje wynik wyrażenia bazowego `x`.

Aby uzyskać więcej informacji na temat funkcji typów referencyjnych dopuszczających wartość null, zobacz [typy referencyjne dopuszczające wartość null](../../nullable-references.md).

## <a name="examples"></a>Przykłady

Jednym z przypadków użycia operatora null-łagodniejszej jest Testowanie logiki walidacji argumentów. Rozważmy na przykład następujące klasy:

[!code-csharp[Person class](~/samples/csharp/language-reference/operators/NullForgivingOperator.cs#PersonClass)]

Używając [platformy testów MSTest](../../../core/testing/unit-testing-with-mstest.md), można utworzyć następujący test dla logiki walidacji w konstruktorze:

[!code-csharp[Person test](~/samples/csharp/language-reference/operators/NullForgivingOperator.cs#TestPerson)]

Bez operatora null łagodniejszej kompilator generuje następujące ostrzeżenie dla poprzedniego kodu: `Warning CS8625: Cannot convert null literal to non-nullable reference type`. Za pomocą operatora o wartości null-łagodniejszej, należy poinformować kompilator, że oczekiwany jest przebieg `null` i nie powinien być ostrzegany o.

Można również użyć operatora o wartości null-łagodniejszej, gdy wiadomo, że wyrażenie nie może być `null`, ale kompilator nie rozpoznaje tego. W poniższym przykładzie, jeśli metoda `IsValid` zwróci `true`, jego argument nie jest `null` i można bezpiecznie go wywoływać:

[!code-csharp[Use null-forgiving operator](~/samples/csharp/language-reference/operators/NullForgivingOperator.cs#UseNullForgiving)]

Bez operatora null łagodniejszej kompilator generuje następujące ostrzeżenie dla kodu `p.Name`: `Warning CS8602: Dereference of a possibly null reference`.

Jeśli można zmodyfikować metodę `IsValid`, można użyć atrybutu [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute) do informowania kompilatora, że argument metody `IsValid` nie może być `null`, gdy metoda zwróci `true`:

[!code-csharp[Use an attribute](~/samples/csharp/language-reference/operators/NullForgivingOperator.cs#UseAttribute)]

W poprzednim przykładzie nie trzeba używać operatora łagodniejszej o wartości null, ponieważ kompilator ma wystarczającą ilość informacji, aby dowiedzieć się, że `p` nie może być `null` w instrukcji `if`. Aby uzyskać więcej informacji o atrybutach, które umożliwiają podanie dodatkowych informacji o stanie null zmiennej, zobacz [uaktualnianie interfejsów API z atrybutami w celu zdefiniowania oczekiwań o wartości null](../../nullable-attributes.md).

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [operator null-łagodniejszej](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator) w [wersji roboczej specyfikacji typów odwołań dopuszczających wartość null](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md).

## <a name="see-also"></a>Zobacz także

- [C#odwoła](../index.md)
- [Operatory języka C#](index.md)
- [Samouczek: Projektowanie przy użyciu typów referencyjnych dopuszczających wartość null](../../tutorials/nullable-reference-types.md)
