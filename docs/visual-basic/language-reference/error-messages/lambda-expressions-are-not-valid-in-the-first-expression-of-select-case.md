---
title: Wyrażenia lambda nie są prawidłowe w pierwszym wyrażeniu instrukcji „Select Case"
ms.date: 07/20/2015
f1_keywords:
- bc36635
- vbc36635
helpviewer_keywords:
- BC36635
ms.assetid: 74609979-9c03-4864-bbce-f588aa2e0917
ms.openlocfilehash: e9bf248da980705f070be878208c55b0cc6dae01
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64589726"
---
# <a name="lambda-expressions-are-not-valid-in-the-first-expression-of-a-select-case-statement"></a>Wyrażenia lambda nie są prawidłowe w pierwszym wyrażeniu instrukcji „Select Case"
Nie można użyć wyrażenia lambda wyrażenia testu w `Select Case` instrukcji. Definicje Wyrażenie lambda zwraca funkcje i wyrażenia testu `Select Case` instrukcja musi być typem danych podstawowych.  
  
 Poniższy kod powoduje błąd:  
  
```vb  
' Select Case (Function(arg) arg Is Nothing)  
    ' List of the cases.  
' End Select  
```  
  
 **Identyfikator błędu:** BC36635  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Sprawdź swój kod, aby określić, czy innej konstrukcji warunkowych, takich jak `If...Then...Else` instrukcji, będzie działać dla Ciebie.  
  
- Może być przeznaczone do wywołania funkcji, jak pokazano w poniższym kodzie:  
  
```vb  
Dim num? As Integer  
Select Case ((Function(arg? As Integer) arg Is Nothing)(num))  
    ' List of the cases  
End Select  
```  
  
## <a name="see-also"></a>Zobacz także

- [Wyrażenia lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
- [Dyrektywa #If...Then...#Else](../../../visual-basic/language-reference/statements/if-then-else-statement.md)
- [Instrukcja Select...Case](../../../visual-basic/language-reference/statements/select-case-statement.md)
