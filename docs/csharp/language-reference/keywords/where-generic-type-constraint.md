---
title: WHERE (ograniczenie typu ogólnego) — C# odwołanie
ms.custom: seodec18
ms.date: 04/12/2018
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: 4e51c5dd226533e7d1ce79a136dba19cbb252f92
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253916"
---
# <a name="where-generic-type-constraint-c-reference"></a>where — Ograniczenie typu ogólnego (odwołanie w C#)

`where` Klauzula w definicji ogólnej określa ograniczenia dotyczące typów, które są używane jako argumenty parametrów typu w typie ogólnym, metodzie, delegatze lub funkcji lokalnej. Ograniczenia mogą określać interfejsy, klasy bazowe lub wymagać typu ogólnego, aby być odwołaniem, wartością lub typem niezarządzanym. Deklarują możliwości, że argument typu musi mieć wartość.

Na przykład można zadeklarować klasę `MyGenericClass`generyczną, w taki sposób, aby parametr `T` typu implementuje <xref:System.IComparable%601> interfejs:

[!code-csharp[using an interface constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#1)]

> [!NOTE]
> Aby uzyskać więcej informacji na temat klauzuli WHERE w wyrażeniu zapytania, zobacz [klauzula WHERE](where-clause.md).

`where` Klauzula może również zawierać ograniczenie klasy bazowej. Ograniczenie klasy bazowej określa, że typ, który ma być używany jako argument typu dla tego typu ogólnego ma określoną klasę jako klasę bazową (lub jest tą klasą bazową), która ma być używana jako argument typu dla tego typu ogólnego. Jeśli jest używane ograniczenie klasy bazowej, musi ono znajdować się przed innymi ograniczeniami tego parametru typu. Niektóre typy są niedozwolone jako ograniczenie klasy bazowej: <xref:System.Object>, <xref:System.Array>, i <xref:System.ValueType>. Przed C# 7,3, <xref:System.Enum> <xref:System.Delegate>, i<xref:System.MulticastDelegate> były również niedozwolone jako ograniczenia klas podstawowych. W poniższym przykładzie przedstawiono typy, które można teraz określić jako klasę bazową:

[!code-csharp[using an interface constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#2)]

Klauzula może określać, że typem `class` jest lub `struct`. `where` Ograniczenie eliminuje konieczność określenia `System.ValueType`ograniczenia klasy bazowej. `struct` `System.ValueType` Typ nie może być używany jako ograniczenie klasy bazowej. W poniższym przykładzie przedstawiono zarówno `class` warunek, jak i: `struct`

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#3)]

`where` Klauzula może`notnull` zawierać ograniczenie. `notnull` Ograniczenie ogranicza parametr typu do typu niedopuszczający wartości null. Ten typ może być typem [wartości](struct.md) lub typem referencyjnym, który nie dopuszcza wartości null. To ograniczenie jest dostępne od [ `nullable enable` ](../../nullable-references.md#nullable-contexts) C# 8,0 do kodu skompilowanego w kontekście. `notnull` W przeciwieństwie do innych ograniczeń, jeśli argument typu narusza `notnull` ograniczenie, kompilator generuje ostrzeżenie zamiast błędu. Ostrzeżenia są generowane tylko w `nullable enable` kontekście. 

> [!IMPORTANT]
> Deklaracje ogólne zawierające `notnull` ograniczenie mogą być używane w kontekście wartości null Oblivious, ale kompilator nie wymusza ograniczenia.

[!code-csharp[using the nonnull constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#NotNull)]

Klauzula może również `unmanaged` zawierać ograniczenie. `where` Ograniczenie ogranicza parametr typu do typów znanych jako [typy niezarządzane.](../builtin-types/unmanaged-types.md) `unmanaged` To `unmanaged` ograniczenie ułatwia zapisanie kodu międzyoperacyjności niskiego poziomu w C#programie. To ograniczenie umożliwia wykonywanie procedur wielokrotnego użytku we wszystkich typach niezarządzanych. Nie można połączyć `class` `struct` ograniczenia z ograniczeniem or. `unmanaged` Ograniczenie wymusza, że typ musi `struct`być: `unmanaged`

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#4)]

Klauzula może również zawierać `new()`ograniczenie konstruktora. `where` To ograniczenie umożliwia utworzenie wystąpienia parametru typu za pomocą `new` operatora. To [ograniczenie New ()](new-constraint.md) umożliwia kompilatorowi, że każdy dostarczony argument typu musi mieć dostępny bez parametrów--lub default--konstruktora. Na przykład:

[!code-csharp[using the new constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#5)]

Ograniczenie jest wyświetlane jako ostatnie `where` w klauzuli. `new()` Nie można połączyć `struct` `unmanaged` ograniczenia z ograniczeniami lub. `new()` Wszystkie typy spełniające te ograniczenia muszą mieć dostępny Konstruktor bez parametrów, co sprawia, `new()` że ograniczenie jest nadmiarowe.

W przypadku wielu parametrów typu należy użyć `where` jednej klauzuli dla każdego parametru typu, na przykład:

[!code-csharp[using multiple where constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#6)]

Można również dołączyć ograniczenia do parametrów typu metod ogólnych, jak pokazano w następującym przykładzie:

[!code-csharp[where constraints with generic methods](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#7)]

Zauważ, że składnia opisująca ograniczenia parametru typu dla delegatów jest taka sama jak w przypadku metod:

[!code-csharp[where constraints with generic methods](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#8)]

Aby uzyskać informacje na temat delegatów ogólnych, zobacz [Delegaty ogólne](../../programming-guide/generics/generic-delegates.md).

Aby uzyskać szczegółowe informacje na temat składni i użycia ograniczeń, zobacz [ograniczenia dotyczące parametrów typu](../../programming-guide/generics/constraints-on-type-parameters.md).

## <a name="c-language-specification"></a>specyfikacja języka C#

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../index.md)
- [Przewodnik programowania w języku C#](../../programming-guide/index.md)
- [Wprowadzenie do typów ogólnych](../../programming-guide/generics/index.md)
- [new, ograniczenie](./new-constraint.md)
- [Ograniczenia dotyczące parametrów typu](../../programming-guide/generics/constraints-on-type-parameters.md)
