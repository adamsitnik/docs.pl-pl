---
title: Wznowienie bez błędu
ms.date: 07/20/2015
f1_keywords:
- vbrID20
ms.assetid: f9631804-fd36-4443-b36c-30db827e6176
ms.openlocfilehash: 61332486b20af66af24eac06b222a38353578c16
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055163"
---
# <a name="resume-without-error"></a>Wznowienie bez błędu
A `Resume` instrukcji znajdowały się poza kodu obsługi błędu lub kod wyniósł do procedury obsługi błędów, nawet jeśli wystąpił błąd braku.  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
1. Przenieś `Resume` instrukcji do obsługi błędów lub usuń go.  
  
2. Dlatego przechodzi do etykiety nie może występować między procedurami, wyszukaj procedury dla etykiety, która identyfikuje procedurę obsługi błędów. Jeśli okaże się zduplikowane etykiety, określona jako obiekt docelowy `GoTo` instrukcję, która nie jest `On Error GoTo` instrukcji, zmień wiersz etykiety zgadza się z jego zamierzonym obiektem docelowym.  
  
## <a name="see-also"></a>Zobacz także

- [Resume, instrukcja](../../../visual-basic/language-reference/statements/resume-statement.md)
- [On Error, instrukcja](../../../visual-basic/language-reference/statements/on-error-statement.md)
