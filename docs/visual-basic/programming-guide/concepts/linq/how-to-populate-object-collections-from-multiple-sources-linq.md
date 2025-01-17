---
title: 'Instrukcje: Wypełnianie kolekcji Object z wielu źródeł (LINQ) (Visual Basic)'
ms.date: 06/22/2018
ms.assetid: 63062a22-e6a9-42c0-b357-c7c965f58f33
ms.openlocfilehash: 21474758cffd15c0cb4193cdb2a7bc33c981c938
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586205"
---
# <a name="how-to-populate-object-collections-from-multiple-sources-linq-visual-basic"></a>Instrukcje: Wypełnianie kolekcji Object z wielu źródeł (LINQ) (Visual Basic)

W tym przykładzie przedstawiono sposób scalania danych z różnych źródeł w sekwencji nowych typów.

> [!NOTE]
> Nie należy próbować dołączyć dane w pamięci lub dane w systemie plików z danymi, które są nadal w bazie danych. Takie sprzężeń między domenami może przynieść niezdefiniowane wyniki ze względu na różne sposoby, w którym można zdefiniować operacji łączenia zapytań bazy danych i innych typów źródeł. Ponadto istnieje ryzyko, takie działanie może spowodować wyjątek braku pamięci, gdy ilość danych w bazie danych jest wystarczająco duży. Aby dołączyć dane z bazy danych do danych w pamięci, należy najpierw wywołać `ToList` lub `ToArray` w bazie danych zapytania, a następnie wykonaj sprzężenia na zwrócona kolekcja.

## <a name="to-create-the-data-file"></a>Aby utworzyć plik danych

- Skopiuj pliki names.csv i scores.csv w folderze projektu, zgodnie z opisem w [jak: Łączenie zawartości niepodobnych plików (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-join-content-from-dissimilar-files-linq.md).

## <a name="example"></a>Przykład

Poniższy przykład pokazuje, jak używać typu nazwanego `Student` do przechowywania scalane dane z dwóch kolekcji w pamięci ciągów, które symulują dane arkusza kalkulacyjnego w formacie CSV. Pierwsza kolekcja ciągów reprezentuje identyfikatory i nazwy studentów, a druga kolekcja reprezentuje identyfikator uczniów (w pierwszej kolumnie) i cztery wyniki egzamin. Identyfikator jest używany jako klucza obcego.

```vb
Imports System.Collections.Generic
Imports System.Linq

Class Student
    Public FirstName As String
    Public LastName As String
    Public ID As Integer
    Public ExamScores As List(Of Integer)
End Class

Class PopulateCollection

    Shared Sub Main()

        ' Merge content from spreadsheets into a list of Student objects.

        ' These data files are defined in How to: Join Content from
        ' Dissimilar Files (LINQ).

        ' Each line of names.csv consists of a last name, a first name, and an
        ' ID number, separated by commas. For example, Omelchenko,Svetlana,111
        Dim names As String() = System.IO.File.ReadAllLines("../../../names.csv")

        ' Each line of scores.csv consists of an ID number and four test
        ' scores, separated by commas. For example, 111, 97, 92, 81, 60
        Dim scores As String() = System.IO.File.ReadAllLines("../../../scores.csv")

        ' The following query merges the content of two dissimilar spreadsheets
        ' based on common ID values.
        ' Multiple From clauses are used instead of a Join clause
        ' in order to store the results of scoreLine.Split.
        ' Note the dynamic creation of a list of integers for the
        ' ExamScores member. The first item is skipped in the split string
        ' because it is the student ID, not an exam score.
        Dim queryNamesScores = From nameLine In names
                          Let splitName = nameLine.Split(New Char() {","})
                          From scoreLine In scores
                          Let splitScoreLine = scoreLine.Split(New Char() {","})
                          Where Convert.ToInt32(splitName(2)) = Convert.ToInt32(splitScoreLine(0))
                          Select New Student() With {
                               .FirstName = splitName(1), .LastName = splitName(0), .ID = splitName(2),
                               .ExamScores = (From scoreAsText In splitScoreLine Skip 1
                                             Select Convert.ToInt32(scoreAsText)).ToList()}

        ' Optional. Store the query results for faster access in future
        ' queries. This could be useful with very large data files.
        Dim students As List(Of Student) = queryNamesScores.ToList()

        ' Display each student's name and exam score average.
        For Each s In students
            Console.WriteLine("The average score of " & s.FirstName & " " &
                              s.LastName & " is " & s.ExamScores.Average())
        Next

        ' Keep console window open in debug mode.
        Console.WriteLine("Press any key to exit.")
        Console.ReadKey()
    End Sub
End Class

' Output:
' The average score of Svetlana Omelchenko is 82.5
' The average score of Claire O'Donnell is 72.25
' The average score of Sven Mortensen is 84.5
' The average score of Cesar Garcia is 88.25
' The average score of Debra Garcia is 67
' The average score of Fadi Fakhouri is 92.25
' The average score of Hanying Feng is 88
' The average score of Hugo Garcia is 85.75
' The average score of Lance Tucker is 81.75
' The average score of Terry Adams is 85.25
' The average score of Eugene Zabokritski is 83
' The average score of Michael Tucker is 92
```

W [wybierz klauzuli](../../../../visual-basic/language-reference/queries/select-clause.md) klauzuli inicjatora obiektu jest używany do utworzenia wystąpienia każdy nowość `Student` obiektu przy użyciu danych z dwóch źródeł.

Jeśli nie masz do przechowywania wyników zapytania, typy anonimowe może być bardziej wygodne niż nazwane typy. Nazwane typy są wymagane w przypadku przekazania wyników zapytania, poza metodą wykonywania zapytania. Poniższy przykład wykonuje to samo zadanie, jak w poprzednim przykładzie, ale używa typów anonimowych zamiast nazwane typy:

```vb
' Merge the data by using an anonymous type.
' Note the dynamic creation of a list of integers for the
' ExamScores member. We skip 1 because the first string
' in the array is the student ID, not an exam score.
Dim queryNamesScores2 =
    From nameLine In names
    Let splitName = nameLine.Split(New Char() {","})
    From scoreLine In scores
    Let splitScoreLine = scoreLine.Split(New Char() {","})
    Where Convert.ToInt32(splitName(2)) = Convert.ToInt32(splitScoreLine(0))
    Select New With
           {.Last = splitName(0),
            .First = splitName(1),
            .ExamScores = (From scoreAsText In splitScoreLine Skip 1
                           Select Convert.ToInt32(scoreAsText)).ToList()}

' Display each student's name and exam score average.
For Each s In queryNamesScores2
    Console.WriteLine("The average score of " & s.First & " " &
                      s.Last & " is " & s.ExamScores.Average())
Next
```

## <a name="see-also"></a>Zobacz także

- [LINQ i ciągi (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
