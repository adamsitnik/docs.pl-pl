---
title: Przykład wykonania odroczonego (C#)
ms.date: 07/20/2015
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
ms.openlocfilehash: 0816594ad016f19af4c97198160b4bafb9b4b8b4
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/31/2019
ms.locfileid: "70204135"
---
# <a name="deferred-execution-example-c"></a>Przykład wykonania odroczonego (C#)
W tym temacie pokazano, w jaki sposób odroczone wykonywanie i Ocena z opóźnieniem wpływają na wykonywanie zapytań LINQ to XML.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje kolejność wykonywania przy użyciu metody rozszerzenia, która korzysta z odroczonego wykonania. Przykład deklaruje tablicę trzech ciągów. Następnie wykonuje iterację w kolekcji zwróconej przez `ConvertCollectionToUpperCase`.  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```output  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 Należy zauważyć, że podczas iteracji kolekcji zwróconej `ConvertCollectionToUpperCase`przez, każdy element jest pobierany z tablicy ciągów źródłowych i konwertowany na wielkie przed pobraniem następnego elementu z tablicy ciągów źródłowych.  
  
 Można zobaczyć, że cała tablica ciągów nie jest konwertowana na wielkie przed każdym elementem w zwróconej kolekcji w `foreach` pętli w. `Main`  
  
 W następnym temacie w tym samouczku przedstawiono Łączenie łańcuchowe zapytań:  
  
- [Przykład łańcucha kwerend (C#)](./chaining-queries-example.md)  
  
## <a name="see-also"></a>Zobacz także

- [Samouczek: Łączenie łańcuchowe zapytań (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
