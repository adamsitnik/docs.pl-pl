---
title: Grupowanie wyników zapytania (LINQ w C#)
description: Dowiedz się, jak należy zgrupować wyniki za pomocą LINQ w C#.
ms.date: 12/01/2016
ms.assetid: 2e4ec27f-06fb-4de7-8973-0189906d4520
ms.openlocfilehash: 577a358c31fcf5346e7aab7a2e2b6be10fd1beff
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61688465"
---
# <a name="group-query-results"></a>Grupowanie wyników zapytania

Grupowanie jest jednym z najbardziej zaawansowanych funkcji zapytań LINQ. W poniższych przykładach pokazano sposób grupowania danych na różne sposoby:

- Według jedną właściwość.

- Przez pierwszą literę właściwość ciągu.

- Obliczona zakresu liczbowego.

- Logiczną predykat lub innego wyrażenia.

- Przy użyciu klucza złożonego.

Ponadto ostatnie dwa zapytania projektu ich wyniki w nowym typem anonimowym, który zawiera tylko student imienia i nazwiska. Aby uzyskać więcej informacji, zobacz [group — klauzula](../language-reference/keywords/group-clause.md).

## <a name="example"></a>Przykład

Wszystkie przykłady w tym temacie, użyj następujących źródeł danych i klasy pomocnika.

[!code-csharp[csProgGuideLINQ#15](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_1.cs)]

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak należy zgrupować elementy źródłowe przy użyciu pojedynczej właściwości elementu jako klucz grupy. W tym przypadku jest klucz `string`, Nazwisko ucznia. Istnieje również możliwość użycia klucza podciąg. W operacji grupowania używa domyślny moduł porównujący równość dla typu.

Wklej następującą metodę do `StudentClass` klasy. Zmień instrukcji wywołujące w `Main` metody `sc.GroupBySingleProperty()`.

[!code-csharp[csProgGuideLINQ#17](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_2.cs)]

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak należy zgrupować elementy źródłowe przy użyciu coś innego niż właściwość obiektu dla klucza grupy. W tym przykładzie klucz jest pierwszej litery nazwiska uczniów.

Wklej następującą metodę do `StudentClass` klasy. Zmień instrukcji wywołujące w `Main` metody `sc.GroupBySubstring()`.

[!code-csharp[csProgGuideLINQ#18](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_3.cs)]

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak należy zgrupować elementy źródłowe przy użyciu zakresu liczbowego jako klucz grupy. Zapytanie projektów następnie wyniki na typ anonimowy, który zawiera tylko imię i nazwisko oraz zakres percentyl, do której należy studenta. Typ anonimowy jest używana, ponieważ nie jest konieczne użycie pełnej `Student` obiektu, aby wyświetlić wyniki. `GetPercentile` Funkcja pomocnicza, która oblicza percentyl opiera się na średnią ocenę studenta. Metoda zwraca liczbę całkowitą od 0 do 10.

[!code-csharp[csProgGuideLINQ#50](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_4.cs)]

Wklej następującą metodę do `StudentClass` klasy. Zmień instrukcji wywołujące w `Main` metody `sc.GroupByRange()`.

[!code-csharp[csProgGuideLINQ#19](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_5.cs)]

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak należy zgrupować elementy źródłowe przy użyciu wyrażenia logiczne porównania. W tym przykładzie wyrażenie logiczne sprawdza, czy studenta średni egzaminu wynik jest większa niż 75. Tak jak w poprzednich przykładach wyniki zostają odwzorowane w typ anonimowy, ponieważ element pełną źródła nie jest potrzebna. Należy pamiętać, że właściwości typu anonimowego stają się właściwości z `Key` elementu członkowskiego i może zostać oceniony przez nazwę, gdy zapytanie jest wykonywane.

Wklej następującą metodę do `StudentClass` klasy. Zmień instrukcji wywołujące w `Main` metody `sc.GroupByBoolean()`.

[!code-csharp[csProgGuideLINQ#20](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_6.cs)]

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak hermetyzacji klucz, który zawiera wiele wartości za pomocą typu anonimowego. W tym przykładzie pierwsze wartość klucza jest pierwszej litery nazwiska uczniów. Druga wartość klucza jest wartość logiczna określająca, czy uczeń oceniane ponad 85 na pierwszym egzamin. Można uporządkować grupy według dowolnej właściwości w kluczu.

Wklej następującą metodę do `StudentClass` klasy. Zmień instrukcji wywołujące w `Main` metody `sc.GroupByCompositeKey()`.

[!code-csharp[csProgGuideLINQ#21](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_7.cs)]

## <a name="see-also"></a>Zobacz także

- <xref:System.Linq.Enumerable.GroupBy%2A>
- <xref:System.Linq.IGrouping%602>
- [Language Integrated Query (LINQ)](index.md)
- [group, klauzula](../language-reference/keywords/group-clause.md)
- [Typy anonimowe](../programming-guide/classes-and-structs/anonymous-types.md)
- [Wykonanie podzapytania w operacji grupowania](perform-a-subquery-on-a-grouping-operation.md)
- [Tworzenie grup zagnieżdżonych](create-a-nested-group.md)
- [Grupowanie danych](../programming-guide/concepts/linq/grouping-data.md)
