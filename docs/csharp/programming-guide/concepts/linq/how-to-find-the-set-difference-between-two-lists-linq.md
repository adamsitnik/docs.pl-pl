---
title: 'Instrukcje: Znajdź różnicę między dwoma listami (LINQ) (C#)'
ms.date: 07/20/2015
ms.assetid: 8e8945f0-4aba-439d-8d5d-c8d1eeef4e71
ms.openlocfilehash: decdbe45afd12581a53ed70ec843ee72f54f0409
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593341"
---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-c"></a>Instrukcje: Znajdź różnicę między dwoma listami (LINQ) (C#)
Ten przykład pokazuje, jak używać LINQ do porównywania dwóch list ciągów i wyprowadzania tych wierszy w names1. txt, ale nie w names2. txt.  
  
### <a name="to-create-the-data-files"></a>Aby utworzyć pliki danych  
  
1. Skopiuj names1. txt i names2. txt do folderu rozwiązania, jak pokazano w [temacie How to: Łączenie i porównywanie kolekcji ciągów (LINQ)C#(](./how-to-combine-and-compare-string-collections-linq.md)).  
  
## <a name="example"></a>Przykład  
  
```csharp  
class CompareLists  
{          
    static void Main()  
    {  
        // Create the IEnumerable data sources.  
        string[] names1 = System.IO.File.ReadAllLines(@"../../../names1.txt");  
        string[] names2 = System.IO.File.ReadAllLines(@"../../../names2.txt");  
  
        // Create the query. Note that method syntax must be used here.  
        IEnumerable<string> differenceQuery =  
          names1.Except(names2);  
  
        // Execute the query.  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt");  
        foreach (string s in differenceQuery)  
            Console.WriteLine(s);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
     The following lines are in names1.txt but not names2.txt  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  
    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
     */  
```  
  
 Niektóre typy operacji zapytania C#w, takie jak <xref:System.Linq.Enumerable.Except%2A>, <xref:System.Linq.Enumerable.Distinct%2A> <xref:System.Linq.Enumerable.Union%2A>,, i <xref:System.Linq.Enumerable.Concat%2A>, można wyrazić tylko w składni opartej na metodzie.  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Utwórz projekt C# aplikacji konsolowej z `using` dyrektywami dotyczącymi przestrzeni nazw System. LINQ i system.IO.  
  
## <a name="see-also"></a>Zobacz także

- [LINQ i ciągi (C#)](./linq-and-strings.md)
