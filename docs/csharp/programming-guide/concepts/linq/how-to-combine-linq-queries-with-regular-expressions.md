---
title: 'Instrukcje: Połącz zapytania LINQ z wyrażeniami regularnymi (C#)'
ms.date: 07/20/2015
ms.assetid: 6b003b65-20a4-4ca2-929e-2ee3f215aecc
ms.openlocfilehash: 7e3540dfe6d93f5262790bce615cc7fe3f1fbb93
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594047"
---
# <a name="how-to-combine-linq-queries-with-regular-expressions-c"></a>Instrukcje: Połącz zapytania LINQ z wyrażeniami regularnymi (C#)
Ten przykład pokazuje, <xref:System.Text.RegularExpressions.Regex> jak używać klasy do tworzenia wyrażenia regularnego w celu uzyskania bardziej złożonego dopasowania w ciągach tekstowych. Zapytanie LINQ ułatwia filtrowanie według dokładnie plików, które mają być przeszukiwane przy użyciu wyrażenia regularnego, oraz do kształtowania wyników.  
  
## <a name="example"></a>Przykład  
  
```csharp  
class QueryWithRegEx  
{  
    public static void Main()  
    {  
        // Modify this path as necessary so that it accesses your version of Visual Studio.  
        string startFolder = @"C:\Program Files (x86)\Microsoft Visual Studio 14.0\";  
        // One of the following paths may be more appropriate on your computer.  
        //string startFolder = @"C:\Program Files (x86)\Microsoft Visual Studio\2017\";  
  
        // Take a snapshot of the file system.  
        IEnumerable<System.IO.FileInfo> fileList = GetFiles(startFolder);  
  
        // Create the regular expression to find all things "Visual".  
        System.Text.RegularExpressions.Regex searchTerm =  
            new System.Text.RegularExpressions.Regex(@"Visual (Basic|C#|C\+\+|Studio)");  
  
        // Search the contents of each .htm file.  
        // Remove the where clause to find even more matchedValues!  
        // This query produces a list of files where a match  
        // was found, and a list of the matchedValues in that file.  
        // Note: Explicit typing of "Match" in select clause.  
        // This is required because MatchCollection is not a   
        // generic IEnumerable collection.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = System.IO.File.ReadAllText(file.FullName)  
            let matches = searchTerm.Matches(fileText)  
            where matches.Count > 0  
            select new  
            {  
                name = file.FullName,  
                matchedValues = from System.Text.RegularExpressions.Match match in matches  
                                select match.Value  
            };  
  
        // Execute the query.  
        Console.WriteLine("The term \"{0}\" was found in:", searchTerm.ToString());  
  
        foreach (var v in queryMatchingFiles)  
        {  
            // Trim the path a bit, then write   
            // the file name in which a match was found.  
            string s = v.name.Substring(startFolder.Length - 1);  
            Console.WriteLine(s);  
  
            // For this file, write out all the matching strings  
            foreach (var v2 in v.matchedValues)  
            {  
                Console.WriteLine("  " + v2);  
            }  
        }  
  
        // Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    // This method assumes that the application has discovery   
    // permissions for all folders under the specified path.  
    static IEnumerable<System.IO.FileInfo> GetFiles(string path)  
    {  
        if (!System.IO.Directory.Exists(path))  
            throw new System.IO.DirectoryNotFoundException();  
  
        string[] fileNames = null;  
        List<System.IO.FileInfo> files = new List<System.IO.FileInfo>();  
  
        fileNames = System.IO.Directory.GetFiles(path, "*.*", System.IO.SearchOption.AllDirectories);  
        foreach (string name in fileNames)  
        {  
            files.Add(new System.IO.FileInfo(name));  
        }  
        return files;  
    }  
}  
```  
  
 Należy zauważyć, że można także zbadać <xref:System.Text.RegularExpressions.MatchCollection> obiekt, który jest zwracany `RegEx` przez wyszukiwanie. W tym przykładzie tylko wartość każdego dopasowania jest generowana w wynikach. Można jednak używać LINQ do wykonywania wszelkiego rodzaju filtrowania, sortowania i grupowania w tej kolekcji. Ponieważ <xref:System.Text.RegularExpressions.MatchCollection> jest kolekcją nieogólną <xref:System.Collections.IEnumerable> , należy jawnie określać typ zmiennej zakresu w zapytaniu.  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Utwórz projekt C# aplikacji konsolowej z `using` dyrektywami dla przestrzeni nazw System. LINQ i system.IO.  
  
## <a name="see-also"></a>Zobacz także

- [LINQ i ciągi (C#)](./linq-and-strings.md)
- [LINQ i katalogi plików (C#)](./linq-and-file-directories.md)
