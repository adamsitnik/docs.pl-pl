---
title: 'Instrukcje: Przerwij i Połącz instrukcje w kodzie (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb._
helpviewer_keywords:
- colons (:)
- line continuation
- _ line-continuation character
- ': line separator character'
- Visual Basic code, line breaks in
- Visual Basic code, line breaks
- Visual Basic code, line continuation
- long lines of code
- line terminator
- line-continuation sequence
- underscores [Visual Basic], in code
- statements [Visual Basic], line continuation in
- line breaks [Visual Basic], in code
- line-continuation character [Visual Basic]
- Visual Basic code, line continuation in
- statements [Visual Basic], line breaks in
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
ms.openlocfilehash: a0a77b161d81271a4cb7eecf2982a287debee6a5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991727"
---
# <a name="how-to-break-and-combine-statements-in-code-visual-basic"></a>Instrukcje: Przerwij i Połącz instrukcje w kodzie (Visual Basic)

Podczas pisania kodu można czasami tworzyć długie instrukcje, które wymagają przewijania w poziomie w edytorze kodu. Chociaż nie ma to wpływu na sposób działania kodu, utrudnia użytkownikowi lub innym osobom odczytywanie kodu w postaci, w jakiej jest wyświetlany na monitorze. W takich przypadkach należy rozważyć rozdzielenie pojedynczej długiej instrukcji na kilka wierszy.

## <a name="to-break-a-single-statement-into-multiple-lines"></a>Aby przerwać pojedynczą instrukcję do wielu wierszy

Użyj znaku kontynuacji wiersza, który jest podkreśleniem (`_`), w punkcie, w którym ma zostać przerwana linia. Znak podkreślenia musi być bezpośrednio poprzedzony spacją, po którym następuje terminator wiersza (znak powrotu karetki) lub (począwszy od wersji 16,0) komentarz, po którym następuje znak powrotu karetki.

  > [!NOTE]
  > W niektórych przypadkach, jeśli pominięto znak kontynuacji wiersza, kompilator Visual Basic niejawnie kontynuuje instrukcję w następnym wierszu kodu. Aby uzyskać listę elementów składni, dla których można pominąć znak kontynuacji wiersza, zobacz "niejawne kontynuacja wiersza" w [instrukcjach](../../../visual-basic/programming-guide/language-features/statements.md).

  W poniższym przykładzie instrukcja jest dzielona na cztery wiersze z znakami kontynuacji wiersza kończącymi wszystkie oprócz ostatniego wiersza.

  [!code-vb[VbVbcnConventions#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#20)]

  Użycie tej sekwencji sprawia, że kod będzie łatwiejszy do odczytania, zarówno w trybie online, jak i podczas drukowania.

  Znak kontynuacji wiersza musi być ostatnim znakiem w wierszu. Nie można wykonać kolejnej czynności w tym samym wierszu.

  Istnieją pewne ograniczenia, w których można użyć znaku kontynuacji wiersza; na przykład nie można użyć go w środku nazwy argumentu. Możesz przerwać listę argumentów za pomocą znaku kontynuacji wiersza, ale poszczególne nazwy argumentów muszą pozostać nienaruszone.

  Nie można kontynuować komentarza przy użyciu znaku kontynuacji wiersza. Kompilator nie bada znaków w komentarzu pod kątem specjalnego znaczenia. W przypadku komentarza z wieloma wierszami należy powtórzyć symbol`'`komentarza () w każdym wierszu.

 Chociaż umieszczenie każdej instrukcji w osobnym wierszu jest zalecaną metodą, Visual Basic umożliwia również umieszczenie wielu instrukcji w tym samym wierszu.

## <a name="to-place-multiple-statements-on-the-same-line"></a>Aby umieścić wiele instrukcji w tym samym wierszu

Rozdziel instrukcje średnikami (`:`), jak w poniższym przykładzie:

  [!code-vb[VbVbcnConventions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#10)]

## <a name="see-also"></a>Zobacz także

- [Konwencje dotyczące struktury programów i kodu](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [Instrukcje](../../../visual-basic/programming-guide/language-features/statements.md)
