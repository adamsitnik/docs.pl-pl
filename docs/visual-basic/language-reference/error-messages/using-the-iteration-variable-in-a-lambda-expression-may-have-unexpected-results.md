---
title: Użycie zmiennej iteracyjnej w wyrażeniu lambda może spowodować nieoczekiwane wyniki
ms.date: 07/20/2015
f1_keywords:
- vbc42324
- bc42324
helpviewer_keywords:
- BC42324
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
ms.openlocfilehash: 3335da503b6fb9c33e44266997cc945214a3a365
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/29/2019
ms.locfileid: "64913087"
---
# <a name="using-the-iteration-variable-in-a-lambda-expression-may-have-unexpected-results"></a>Użycie zmiennej iteracyjnej w wyrażeniu lambda może spowodować nieoczekiwane wyniki
Użycie zmiennej iteracyjnej w wyrażeniu lambda może spowodować nieoczekiwane wyniki. Zamiast tego należy utworzyć zmienną lokalną, w ramach pętli i przypisać jej wartość zmiennej iteracji.  
  
 To ostrzeżenie jest wyświetlane, gdy używasz Zmienna iteracji pętli w wyrażeniu lambda, która jest zadeklarowana wewnątrz pętli. Na przykład poniższy przykład powoduje, że ostrzeżenia są wyświetlane.  
  
```vb  
For i As Integer = 1 To 10  
    ' The warning is given for the use of i.  
    Dim exampleFunc As Func(Of Integer) = Function() i  
Next  
```  
  
 Poniższy przykład pokazuje nieoczekiwane wyniki, które mogą wystąpić.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            array1(i) = Function() i  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
 `For` Pętli tworzy tablicę wyrażeń lambda, z których każda zwraca wartość zmiennej iteracji pętli `i`. Gdy wyrażenia lambda są obliczane w `For Each` pętli, można by oczekiwać zobaczyć, 0, 1, 2, 3 i 4 wyświetlane, kolejnych wartości `i` w `For` pętli. Zamiast tego zobacz końcowa wartość `i` wyświetlane pięć razy:  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 Domyślnie ta wiadomość jest ostrzeżenie. Aby uzyskać więcej informacji na temat ukrywania ostrzeżenia lub traktowanie ostrzeżeń jako błędy, zobacz [Konfigurowanie ostrzeżeń w języku Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Identyfikator błędu:** BC42324  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Przypisz wartość zmiennej iteracyjnej do zmiennej lokalnej, a następnie użyć zmiennej lokalnej w wyrażeniu lambda.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            Dim j = i  
            array1(i) = Function() j  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
## <a name="see-also"></a>Zobacz także

- [Wyrażenia lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
