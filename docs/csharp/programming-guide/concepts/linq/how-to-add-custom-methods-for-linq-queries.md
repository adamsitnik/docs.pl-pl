---
title: 'Instrukcje: Dodaj niestandardowe metody dla zapytań LINQ (C#)'
ms.date: 07/20/2015
ms.assetid: 1a500f60-2e10-49fb-8b2a-d8d08e4817cb
ms.openlocfilehash: fcf6814c8b3076a18e807a378796094a9ce2cf84
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594149"
---
# <a name="how-to-add-custom-methods-for-linq-queries-c"></a>Instrukcje: Dodaj niestandardowe metody dla zapytań LINQ (C#)

Można rozszerzać zestaw metod, których można użyć dla zapytań LINQ przez dodanie metod rozszerzających do <xref:System.Collections.Generic.IEnumerable%601> interfejsu. Na przykład oprócz standardowej średniej lub maksymalnej operacji można utworzyć niestandardową metodę agregującą, aby obliczyć pojedynczą wartość z sekwencji wartości. Możesz również utworzyć metodę, która działa jako filtr niestandardowy lub Przekształć dane dla sekwencji wartości i zwraca nową sekwencję. Przykładami takich metod są <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Skip%2A>, i <xref:System.Linq.Enumerable.Reverse%2A>.

Rozszerzając <xref:System.Collections.Generic.IEnumerable%601> interfejs, można zastosować niestandardowe metody do dowolnej wyliczalnej kolekcji. Aby uzyskać więcej informacji, zobacz [metody rozszerzenia](../../classes-and-structs/extension-methods.md).

## <a name="adding-an-aggregate-method"></a>Dodawanie metody agregującej

Metoda agregująca oblicza pojedynczą wartość z zestawu wartości. LINQ zawiera kilka metod agregujących, <xref:System.Linq.Enumerable.Average%2A>w <xref:System.Linq.Enumerable.Min%2A>tym, <xref:System.Linq.Enumerable.Max%2A>i. Można utworzyć własną metodę agregującą, dodając metodę rozszerzenia do <xref:System.Collections.Generic.IEnumerable%601> interfejsu.

Poniższy przykład kodu pokazuje, jak utworzyć metodę rozszerzenia wywołana `Median` , aby obliczyć medianę dla sekwencji liczb typu. `double`

```csharp
public static class LINQExtension
{
    public static double Median(this IEnumerable<double> source)
    {
        if (source.Count() == 0)
        {
            throw new InvalidOperationException("Cannot compute median for an empty set.");
        }

        var sortedList = from number in source
                         orderby number
                         select number;

        int itemIndex = (int)sortedList.Count() / 2;

        if (sortedList.Count() % 2 == 0)
        {
            // Even number of items.
            return (sortedList.ElementAt(itemIndex) + sortedList.ElementAt(itemIndex - 1)) / 2;
        }
        else
        {
            // Odd number of items.
            return sortedList.ElementAt(itemIndex);
        }
    }
}
```

Ta metoda rozszerzenia jest wywoływana dla każdej wyliczalnej kolekcji w taki sam sposób, w jaki wywołujemy <xref:System.Collections.Generic.IEnumerable%601> inne metody agregacji z interfejsu.

Poniższy przykład kodu pokazuje, `Median` jak używać metody dla tablicy typu. `double`

```csharp
double[] numbers1 = { 1.9, 2, 8, 4, 5.7, 6, 7.2, 0 };

var query1 = numbers1.Median();

Console.WriteLine("double: Median = " + query1);
```

```csharp
/*
 This code produces the following output:

 Double: Median = 4.85
*/
```

### <a name="overloading-an-aggregate-method-to-accept-various-types"></a>Przeciążanie metody agregującej w celu zaakceptowania różnych typów

Można przeciążyć metodę agregacji, aby akceptować sekwencje różnych typów. Standardowe podejście polega na utworzeniu przeciążenia dla każdego typu. Innym rozwiązaniem jest utworzenie przeciążenia, które będzie miało typ ogólny i przekonwertować go na określony typ za pomocą delegata. Można również połączyć oba podejścia.

#### <a name="to-create-an-overload-for-each-type"></a>Aby utworzyć Przeciążenie dla każdego typu

Można utworzyć określone Przeciążenie dla każdego typu, który ma być obsługiwany. Poniższy przykład kodu przedstawia Przeciążenie `Median` metody `integer` dla typu.

```csharp
//int overload

public static double Median(this IEnumerable<int> source)
{
    return (from num in source select (double)num).Median();
}
```

Teraz można wywoływać `Median` przeciążenia dla obu `integer` typów i `double` typy, jak pokazano w poniższym kodzie:

```csharp
double[] numbers1 = { 1.9, 2, 8, 4, 5.7, 6, 7.2, 0 };

var query1 = numbers1.Median();

Console.WriteLine("double: Median = " + query1);
```

```csharp
int[] numbers2 = { 1, 2, 3, 4, 5 };

var query2 = numbers2.Median();

Console.WriteLine("int: Median = " + query2);
```

```csharp
/*
 This code produces the following output:

 Double: Median = 4.85
 Integer: Median = 3
*/
```

#### <a name="to-create-a-generic-overload"></a>Aby utworzyć Przeciążenie ogólne

Można również utworzyć Przeciążenie, które akceptuje sekwencję obiektów ogólnych. To przeciążenie przyjmuje delegat jako parametr i używa go do konwersji sekwencji obiektów typu ogólnego do określonego typu.

Poniższy kod przedstawia Przeciążenie `Median` metody, która <xref:System.Func%602> przyjmuje delegat jako parametr. Ten delegat pobiera obiekt typu ogólnego T i zwraca obiekt typu `double`.

```csharp
// Generic overload.

public static double Median<T>(this IEnumerable<T> numbers,
                       Func<T, double> selector)
{
    return (from num in numbers select selector(num)).Median();
}
```

Teraz można wywołać `Median` metodę dla sekwencji obiektów dowolnego typu. Jeśli typ nie ma własnego przeciążenia metody, należy przekazać parametr delegata. W C#programie można użyć wyrażenia lambda do tego celu. Ponadto, tylko w Visual Basic, jeśli używasz `Aggregate` klauzuli or `Group By` zamiast wywołania metody, można przekazać dowolną wartość lub wyrażenie, które znajduje się w zakresie tej klauzuli.

Poniższy przykładowy kod pokazuje, `Median` jak wywołać metodę dla tablicy liczb całkowitych i tablicy ciągów. Dla ciągów, mediany dla długości ciągów w tablicy jest obliczany. W przykładzie pokazano, <xref:System.Func%602> jak przekazać parametr delegata `Median` do metody dla każdego przypadku.

```csharp
int[] numbers3 = { 1, 2, 3, 4, 5 };

/*
  You can use the num=>num lambda expression as a parameter for the Median method
  so that the compiler will implicitly convert its value to double.
  If there is no implicit conversion, the compiler will display an error message.
*/

var query3 = numbers3.Median(num => num);

Console.WriteLine("int: Median = " + query3);

string[] numbers4 = { "one", "two", "three", "four", "five" };

// With the generic overload, you can also use numeric properties of objects.

var query4 = numbers4.Median(str => str.Length);

Console.WriteLine("String: Median = " + query4);

/*
 This code produces the following output:

 Integer: Median = 3
 String: Median = 4
*/
```

## <a name="adding-a-method-that-returns-a-collection"></a>Dodawanie metody zwracającej kolekcję

<xref:System.Collections.Generic.IEnumerable%601> Interfejs można rozszerzyć za pomocą niestandardowej metody zapytania, która zwraca sekwencję wartości. W tym przypadku metoda musi zwracać kolekcję typu <xref:System.Collections.Generic.IEnumerable%601>. Takie metody mogą służyć do zastosowania filtrów lub transformacji danych do sekwencji wartości.

Poniższy przykład pokazuje, jak utworzyć metodę rozszerzenia o nazwie `AlternateElements` , która zwraca każdy inny element w kolekcji, rozpoczynając od pierwszego elementu.

```csharp
// Extension method for the IEnumerable<T> interface.
// The method returns every other element of a sequence.

public static IEnumerable<T> AlternateElements<T>(this IEnumerable<T> source)
{
    List<T> list = new List<T>();

    int i = 0;

    foreach (var element in source)
    {
        if (i % 2 == 0)
        {
            list.Add(element);
        }

        i++;
    }

    return list;
}
```

Można wywołać tę metodę rozszerzenia dla każdej wyliczalnej kolekcji tak samo jak w przypadku wywołania innych metod <xref:System.Collections.Generic.IEnumerable%601> z interfejsu, jak pokazano w poniższym kodzie:

```csharp
string[] strings = { "a", "b", "c", "d", "e" };

var query = strings.AlternateElements();

foreach (var element in query)
{
    Console.WriteLine(element);
}
/*
 This code produces the following output:

 a
 c
 e
*/
```

## <a name="see-also"></a>Zobacz także

- <xref:System.Collections.Generic.IEnumerable%601>
- [Metody rozszerzeń](../../classes-and-structs/extension-methods.md)
