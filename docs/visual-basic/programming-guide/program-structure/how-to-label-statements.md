---
title: 'Instrukcje: Instrukcje etykiet (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- colons (:)
- statements [Visual Basic], labels
- ': separator character'
- Visual Basic code, labeling statements
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
ms.openlocfilehash: 9a5f2039716a18011cac3dfd9b011d5b3868c294
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054051"
---
# <a name="how-to-label-statements-visual-basic"></a>Instrukcje: Instrukcje etykiet (Visual Basic)

Bloki instrukcji składają się z wierszy kodu rozdzielanych średnikami. Wiersze kodu poprzedzone ciągiem identyfikującym lub liczbą całkowitą są określane jako *etykiety*. Etykiety instrukcji są używane do oznaczania wiersza kodu w celu zidentyfikowania go do użycia z instrukcjami takimi jak `On Error Goto`.

Etykiety mogą być prawidłowymi identyfikatorami Visual Basic, takimi jak te, które identyfikują elementy programowania — lub literały całkowite. Etykieta musi znajdować się na początku wiersza kodu źródłowego i musi następować dwukropek, niezależnie od tego, czy występuje instrukcja w tym samym wierszu.

Kompilator identyfikuje etykiety, sprawdzając, czy początek wiersza pasuje do żadnego już zdefiniowanego identyfikatora. Jeśli nie, kompilator zakłada, że jest to etykieta.

Etykiety mają własne miejsce deklaracji i nie zakłócają innych identyfikatorów. Zakres etykiety jest treścią metody. Deklaracja etykiety ma pierwszeństwo w każdej niejednoznacznej sytuacji.

> [!NOTE]
> Etykiet można używać tylko w instrukcjach wykonywalnych wewnątrz metod.

## <a name="to-label-a-line-of-code"></a>Aby oznaczyć wiersz kodu

Umieść identyfikator, po którym następuje dwukropek, na początku wiersza kodu źródłowego.

Na przykład następujące wiersze kodu mają etykiety `Jump` i `120`, odpowiednio:

[!code-vb[VbVbalrStatements#708](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#708)]

## <a name="see-also"></a>Zobacz także

- [Instrukcje](../../../visual-basic/programming-guide/language-features/statements.md)
- [Nazwy zadeklarowanych elementów](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [Konwencje dotyczące struktury programów i kodu](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
