---
title: <type1>'<typename>musi implementować<methodname>'dla interfejsu'<interfacename>'
ms.date: 07/20/2015
f1_keywords:
- vbc30149
- bc30149
helpviewer_keywords:
- BC30149
ms.assetid: 29d1b7f4-dca7-478c-bbe7-c657f342c183
ms.openlocfilehash: c387b0225375f4675042bef593b23a084305b4fd
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591596"
---
# <a name="type1typename-must-implement-methodname-for-interface-interfacename"></a>\<type1 > '\<typename >' musi implementować '\<methodname >' dla interfejsu '\<interfacename >'
Klasa lub struktura oświadczenia do implementacji interfejsu, ale nie implementuje procedury zdefiniowanej przez interfejs. Każdy element członkowski interfejsu musi być zaimplementowany.  
  
 **Identyfikator błędu:** BC30149  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
1. Zadeklaruj procedurę o tej samej nazwie i podpisie, zgodnie z definicją w interfejsie. Pamiętaj, aby uwzględnić co najmniej następującą instrukcję `End Function` lub `End Sub`.  
  
2. Dodaj klauzulę `Implements` na końcu instrukcji `Function` lub `Sub`. Na przykład:  
  
    ```vb  
    Public Sub DoSomething() Implements IBaseInterface.DoSomething  
    ```  
  
## <a name="see-also"></a>Zobacz także

- [Implements, instrukcja](../../../visual-basic/language-reference/statements/implements-statement.md)
- [Interfejsy](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
