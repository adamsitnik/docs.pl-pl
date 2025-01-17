---
title: '\- C# odwołanie'
ms.custom: seodec18
ms.date: 06/21/2019
f1_keywords:
- is_CSharpKeyword
- is
helpviewer_keywords:
- is keyword [C#]
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
ms.openlocfilehash: a04105137fad7cd3a25b869c3aa7fcbe91ed20ab
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/17/2019
ms.locfileid: "69566308"
---
# <a name="is-c-reference"></a>is (odwołanie w C#)

Operator sprawdza, czy wynik wyrażenia jest zgodny z danym typem, lub (Zaczynając od C# 7,0) testuje wyrażenie względem wzorca. `is` Aby uzyskać informacje o operatorze testowania `is` typu, zobacz sekcję [operator is](../operators/type-testing-and-cast.md#is-operator) w artykule operatorion [-Test and Cast](../operators/type-testing-and-cast.md) .

## <a name="pattern-matching-with-is"></a>Dopasowanie wzorca z`is`

Począwszy od C# 7,0, `is` instrukcje i [przełącznik](switch.md) obsługują Dopasowywanie wzorców. `is` Słowo kluczowe obsługuje następujące wzorce:

- [Wzorzec typu](#type-pattern), który sprawdza, czy wyrażenie może być konwertowane do określonego typu i, jeśli może, przerzutuje go do zmiennej tego typu.

- [Wzorzec stałej](#constant-pattern), który sprawdza, czy wyrażenie daje w wyniku określoną wartość stałą.

- [wzorzec var](#var-pattern), dopasowanie, które zawsze powiedzie się i wiąże wartość wyrażenia z nową zmienną lokalną.

### <a name="type-pattern"></a>Wzorzec typu

W przypadku używania wzorca typu do dopasowania do wzorca, `is` sprawdza, czy wyrażenie może być konwertowane do określonego typu i, jeśli może, rzutowania go na zmienną tego typu. Jest to proste rozszerzenie `is` instrukcji, która umożliwia obliczanie i konwersję typu zwięzłego. Ogólna forma `is` wzorca typu jest:

```csharp
   expr is type varname
```

gdzie *Expr* jest wyrażeniem, którego wynikiem jest wystąpienie pewnego typu, *Type* jest nazwą typu, do którego zostanie przekonwertowany wynik *wyrażenia* , a *nazwa_zmiennej* jest obiektem, do którego jest konwertowany wynik *wyrażenia* , jeśli `is` test jest `true`. 

Wyrażenie jest Jeśli `true` *wyrażenie* jest nieobsługiwane `null`, a którykolwiek z następujących warunków jest spełniony: `is`

- *wyrażenie* jest wystąpieniem tego samego typu co *Typ*.

- *wyrażenie* jest wystąpieniem typu, który pochodzi od *typu*. Innymi słowy, wynik *wyrażenia* może być rzutowany na wystąpienie *typu*.

- *wyrażenie* ma typ czasu kompilacji, który jest klasą bazową *typu*, a *wyrażenie* ma typ środowiska uruchomieniowego, który jest *typem* lub pochodzi od *typu*. *Typ czasu kompilacji* zmiennej to typ zmiennej, zgodnie z definicją w swojej deklaracji. *Typ środowiska uruchomieniowego* zmiennej to typ wystąpienia, które jest przypisane do tej zmiennej.

- *wyrażenie* jest wystąpieniem typu, który implementuje interfejs *typu* .

Począwszy od C# 7,1, *wyrażenie* może mieć typ czasu kompilacji zdefiniowany przez parametr typu ogólnego i jego ograniczenia.

Jeśli *wyrażenie* jest `true` i `is` jest używane z `if` instrukcją, *nazwa_zmiennej* jest przypisywana tylko `if` wewnątrz instrukcji. Zakres elementu *nazwa_zmiennej* pochodzi z `is` wyrażenia na końcu `if` bloku otaczającego instrukcję. Użycie elementu *nazwa_zmiennej* w dowolnej innej lokalizacji generuje błąd czasu kompilacji do użycia zmiennej, która nie została przypisana.

Poniższy przykład używa wzorca typu `is` , aby zapewnić implementację <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> metody typu.

[!code-csharp[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

Bez dopasowania do wzorca ten kod może być zapisany w następujący sposób. Użycie dopasowania wzorca typu daje bardziej zwarty, czytelny kod, eliminując konieczność sprawdzenia, czy wynik konwersji to `null`.  

[!code-csharp[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

Wzorzec `is` typu generuje również bardziej zwarty kod podczas określania typu wartości. W poniższym przykładzie używa się `is` wzorca typu, aby określić, czy obiekt `Person` jest `Dog` wystąpieniem, czy przed wyświetleniem wartości odpowiedniej właściwości.

[!code-csharp[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

Odpowiedni kod bez dopasowania do wzorca wymaga oddzielnego przypisania zawierającego jawne rzutowanie.

[!code-csharp[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="constant-pattern"></a>Wzorzec stałej

Podczas wykonywania dopasowania wzorca ze wzorcem stałej, `is` sprawdza, czy wyrażenie jest równe określonej stałej. W C# 6 i wcześniejszych wersjach wzorzec stałej jest obsługiwany przez instrukcję [Switch](switch.md) . Począwszy od C# 7,0, jest to również obsługiwane przez `is` instrukcję. Jego składnia to:

```csharp
   expr is constant
```

gdzie *Expr* jest wyrażeniem, które ma zostać obliczone, a *stała* jest wartością do przetestowania. *stała* może być dowolnym z następujących wyrażeń stałych:

- Wartość literału.

- Nazwa zadeklarowanej `const` zmiennej.

- Stała wyliczenia.

Wyrażenie stałe jest oceniane w następujący sposób:

- Jeśli *wyrażenie* i *stała* są typami całkowitymi, C# operator równości określa, czy wyrażenie zwróci `true` wartość (to znaczy czy `expr == constant`).

- W przeciwnym razie wartość wyrażenia jest określana przez wywołanie metody static [obiektu. Equals (wyrażenie, stała)](xref:System.Object.Equals(System.Object,System.Object)) .  

Poniższy przykład łączy typ i wzorce stałe, aby sprawdzić, czy obiekt jest `Dice` wystąpieniem i, jeśli to jest, aby określić, czy wartość rzutowania indeksu to 6.

[!code-csharp[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]

Sprawdzanie dla `null` można wykonać przy użyciu wzorca stałego. Słowo kluczowe jest obsługiwane `is` przez instrukcję. `null` Jego składnia to:

```csharp
   expr is null
```

W poniższym przykładzie przedstawiono porównanie `null` kontroli:

[!code-csharp[is#11](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern11.cs#11)]

### <a name="var-pattern"></a>wzorzec wariancji

`var` Wzorzec jest wartością przechwycenia dla dowolnego typu lub wartości. Wartość *wyrażenia* jest zawsze przypisywana do zmiennej lokalnej tego samego typu co typ czasu kompilacji *wyrażenia*. Wynik `is` wyrażenia jest zawsze `true`. Jego składnia to:

```csharp
   expr is var varname
```

Poniższy przykład używa wzorca wariancji do przypisania wyrażenia do zmiennej o nazwie `obj`. Następnie zostanie wyświetlona wartość i typ `obj`.

[!code-csharp[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

## <a name="c-language-specification"></a>specyfikacja języka C#
  
Aby uzyskać więcej informacji, zapoznaj się z sekcją [operatora is](~/_csharplang/spec/expressions.md#the-is-operator) w [ C# specyfikacji języka](~/_csharplang/spec/introduction.md) i następujących C# propozycjach języka:

- [Dopasowanie do wzorca](~/_csharplang/proposals/csharp-7.0/pattern-matching.md)
- [Dopasowywanie wzorca do typów ogólnych](~/_csharplang/proposals/csharp-7.1/generics-pattern-match.md)
  
## <a name="see-also"></a>Zobacz także

- [C#odwoła](../index.md)
- [Słowa kluczowe języka C#](index.md)
- [Operatory testowania typu i rzutowania](../operators/type-testing-and-cast.md)
