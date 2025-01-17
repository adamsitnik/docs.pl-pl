---
title: Implements — Klauzula (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.ImplementsClause
helpviewer_keywords:
- interface implementation [Visual Basic], reimplementation
- interface members [Visual Basic], reimplementation
- interface members [Visual Basic], Implements keyword
- interface members
- members [Visual Basic], reimplementation
- interface implementation [Visual Basic], Implements keyword
- interface members [Visual Basic], implementing
- Implements keyword [Visual Basic]
- Implements statement [Visual Basic], about Implements
- members [Visual Basic], implementing
- members [Visual Basic], Implements keyword
- reimplementation
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
ms.openlocfilehash: dcd20f21a989c327dcfcf27d5638d500b6e4b6da
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929318"
---
# <a name="implements-clause-visual-basic"></a>Implements — Klauzula (Visual Basic)
Wskazuje, że składowa klasy lub struktury dostarcza implementację dla składowej zdefiniowanej w interfejsie.  
  
## <a name="remarks"></a>Uwagi  
Słowo kluczowe nie jest takie samo jak [instrukcja Implements.](../../../visual-basic/language-reference/statements/implements-statement.md) `Implements` Możesz użyć `Implements` instrukcji, aby określić, że Klasa lub struktura implementuje jeden lub więcej interfejsów, a następnie dla każdego elementu członkowskiego `Implements` używa słowa kluczowego, aby określić, który interfejs i który element członkowski implementuje.

Jeśli klasa lub struktura implementuje interfejs, musi zawierać `Implements` instrukcję bezpośrednio po [instrukcji klasy](../../../visual-basic/language-reference/statements/class-statement.md) lub [instrukcji struktury](../../../visual-basic/language-reference/statements/structure-statement.md)i musi zaimplementować wszystkie elementy członkowskie zdefiniowane przez interfejs.

## <a name="reimplementation"></a>Reimplementacja  
W klasie pochodnej można wykonać ponowną implementację elementu członkowskiego interfejsu, który został już zaimplementowany przez klasę bazową. Różni się to od przesłaniania składowej klasy bazowej w następujących aspektach:

- Składowa klasy bazowej nie musi być zaimplementowana [, aby](../../../visual-basic/language-reference/modifiers/overridable.md) można ją było ponownie zaimplementować.
- Można wykonać ponowną implementację elementu członkowskiego z inną nazwą.

`Implements` Słowo kluczowe może być używane w następujących kontekstach:

- [Event, instrukcja](../../../visual-basic/language-reference/statements/event-statement.md)
- [Function, instrukcja](../../../visual-basic/language-reference/statements/function-statement.md)
- [Instrukcja Property](../../../visual-basic/language-reference/statements/property-statement.md)
- [Sub, instrukcja](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>Zobacz także

- [Implements, instrukcja](../../../visual-basic/language-reference/statements/implements-statement.md)
- [Instrukcja Interface](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Class, instrukcja](../../../visual-basic/language-reference/statements/class-statement.md)
- [Structure, instrukcja](../../../visual-basic/language-reference/statements/structure-statement.md)
