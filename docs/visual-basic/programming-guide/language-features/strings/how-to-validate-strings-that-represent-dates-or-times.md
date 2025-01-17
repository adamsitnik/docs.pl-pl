---
title: 'Instrukcje: Sprawdzanie poprawności ciągów reprezentujących daty lub godziny (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], validating
- String data type [Visual Basic], validation
ms.assetid: ae7d4b29-3436-4032-bdbf-4650eb1c8e19
ms.openlocfilehash: f24ff05e48327c21c02eb92b07db17266f743a80
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024615"
---
# <a name="how-to-validate-strings-that-represent-dates-or-times-visual-basic"></a>Instrukcje: Sprawdzanie poprawności ciągów reprezentujących daty lub godziny (Visual Basic)
Poniższy kod ustawia przykład `Boolean` wartość, która wskazuje, czy ciąg reprezentuje prawidłowej daty i godziny.  
  
## <a name="example"></a>Przykład  
 [!code-vb[VbVbcnRegEx#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#2)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Zastąp `("01/01/03")` i `"9:30 PM"` z daty i godziny, którą chcesz zweryfikować. Można zastąpić ciąg z innego ciągu ustalonych `String` zmiennej, lub z metodą, zwraca wartość typu ciąg, takie jak `InputBox`.  
  
## <a name="robust-programming"></a>Niezawodne programowanie  
 Ta metoda służy do sprawdzenia ciągu przed próby skonwertowania `String` do `DateTime` zmiennej. Najpierw Sprawdzanie daty lub godziny, można uniknąć generowania wyjątku w czasie wykonywania.  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.Information.IsDate%2A>
- <xref:Microsoft.VisualBasic.Interaction.InputBox%2A>
- [Sprawdzanie poprawności ciągów w Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)
