---
title: Grupowanie danych (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 8f3a0871-6958-4aef-8f6f-493e189fd57d
ms.openlocfilehash: b5a6a3795e02e0638b81824701ad0cbacbcca91a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754463"
---
# <a name="grouping-data-visual-basic"></a>Grupowanie danych (Visual Basic)
Grupowanie odnosi się do operacji umieszczania danych do grup, tak aby elementów w każdej grupie udostępniać wspólny atrybut.  
  
 Poniższa ilustracja przedstawia wyniki grupowania sekwencji znaków. Klucz dla każdej grupy jest znakiem.  
  
 ![Diagram przedstawiający operacji grupowania LINQ.](./media/grouping-data/linq-group-operation.png)  
  
 Metody standardowego operatora zapytań, które grupują elementy danych są wymienione w poniższej sekcji.  
  
## <a name="methods"></a>Metody  
  
|Nazwa metody|Opis|Składnia wyrażeń języka Visual Basic|Więcej informacji|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|GroupBy|Grupuje elementy, które współużytkują wspólny atrybut. Każda grupa jest reprezentowany przez <xref:System.Linq.IGrouping%602> obiektu.|`Group … By … Into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|ToLookup|Wstawia elementy do <xref:System.Linq.Lookup%602> (Słownik jeden do wielu) na podstawie selektora kluczy funkcji.|Nie dotyczy.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>Przykład składni wyrażenia zapytania  
 Poniższy przykład kodu wykorzystuje `Group By` klauzuli grupy liczb całkowitych, na liście według tego, czy jest parzysta lub nieparzysta.  
  
```vb  
Dim numbers As New System.Collections.Generic.List(Of Integer)(  
     New Integer() {35, 44, 200, 84, 3987, 4, 199, 329, 446, 208})  
  
Dim query = From number In numbers   
            Group By Remainder = (number Mod 2) Into Group  
  
Dim sb As New System.Text.StringBuilder()  
For Each group In query  
    sb.AppendLine(If(group.Remainder = 0, vbCrLf & "Even numbers:", vbCrLf & "Odd numbers:"))  
    For Each num In group.Group  
        sb.AppendLine(num)  
    Next  
Next  
  
' Display the results.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' Odd numbers:  
' 35  
' 3987  
' 199  
' 329  
  
' Even numbers:  
' 44  
' 200  
' 84  
' 4  
' 446  
' 208  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Linq>
- [Omówienie operatorów standardowej kwerendy (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Klauzula Group By](../../../../visual-basic/language-reference/queries/group-by-clause.md)
- [Instrukcje: Grupa plików według rozszerzenia (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-group-files-by-extension-linq.md)
- [Instrukcje: Dzielenie pliku na kilka plików za pomocą grup (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-split-a-file-into-many-files-by-using-groups-linq.md)
