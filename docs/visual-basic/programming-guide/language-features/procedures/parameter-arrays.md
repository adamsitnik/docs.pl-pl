---
title: Parameter — Tablice (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- parameter arrays [Visual Basic], about parameter arrays
- ParamArray keyword [Visual Basic], parameter arrays
- Visual Basic code, procedures
- parameters [Visual Basic], parameter arrays
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], indefinite number of argument values
- arrays [Visual Basic], parameter arrays
ms.assetid: c43edfae-9114-4096-9ebc-8c5c957a1067
ms.openlocfilehash: 285a5f10e2394fcb001a652fad66e8128b9fbc1a
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73424616"
---
# <a name="parameter-arrays-visual-basic"></a>Parameter — Tablice (Visual Basic)
Zazwyczaj nie można wywołać procedury z więcej argumentów niż Deklaracja procedury. Jeśli potrzebujesz nieograniczonej liczby argumentów, możesz zadeklarować *tablicę parametrów*, która umożliwia procedurę akceptowania tablicy wartości dla parametru. Podczas definiowania procedury nie trzeba znać liczby elementów w tablicy parametrów. Rozmiar tablicy jest określany indywidualnie przez każde wywołanie procedury.  
  
## <a name="declaring-a-paramarray"></a>Deklarowanie ParamArray  
 Za pomocą słowa kluczowego [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) można zauważyć tablicę parametrów na liście parametrów. Mają zastosowanie następujące zasady:  
  
- Procedura może definiować tylko jedną tablicę parametrów i musi być ostatnim parametrem w definicji procedury.  
  
- Tablica parametrów musi być przenoszona przez wartość. Dobrym sposobem programowania jest jawne dołączenie słowa kluczowego [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) w definicji procedury.  
  
- Tablica parametrów jest automatycznie opcjonalna. Jego wartość domyślna to pusta Jednowymiarowa tablica typu elementu tablicy parametrów.  
  
- Wszystkie parametry poprzedzające tablicę parametrów muszą być wymagane. Tablica parametrów musi być jedynym opcjonalnym parametrem.  
  
## <a name="calling-a-paramarray"></a>Wywoływanie ParamArray  
 Po wywołaniu procedury, która definiuje tablicę parametrów, można podać argument w jednym z następujących sposobów:  
  
- Nic — to znaczy, że można pominąć argument [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) . W takim przypadku pusta tablica jest przenoszona do procedury. Jeśli jawnie przekażesz słowo kluczowe [Nothing](../../../../visual-basic/language-reference/nothing.md) , tablica o wartości null zostanie przekazana do procedury i może skutkować NullReferenceException, jeśli wywołana procedura nie sprawdza tego warunku.
  
- Lista dowolnej liczby argumentów oddzielonych przecinkami. Typ danych każdego argumentu musi być niejawnie konwertowany na typ elementu `ParamArray`.  
  
- Tablica z tym samym typem elementu co typ elementu tablicy parametrów.  
  
 We wszystkich przypadkach kod w procedurze traktuje tablicę parametrów jako tablicę jednowymiarową z elementami tego samego typu danych co typ danych `ParamArray`.  
  
> [!IMPORTANT]
> Za każdym razem, gdy zajmujesz się tablicą, która może być nienieskończona, istnieje ryzyko, że zachodzi taka Wewnętrzna pojemność aplikacji. Jeśli zaakceptujesz tablicę parametrów, należy sprawdzić rozmiar tablicy, do której przeszedł kod wywołujący. Wykonaj odpowiednie kroki, jeśli są zbyt duże dla aplikacji. Aby uzyskać więcej informacji, zobacz [tablice](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## <a name="example"></a>Przykład  
 Poniższy przykład definiuje i wywołuje funkcję `calcSum`. Modyfikator `ParamArray` dla parametru `args` włącza funkcję do akceptowania zmiennej liczby argumentów.  
  
 [!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]  
  
 Poniższy przykład definiuje procedurę z tablicą parametrów i wyprowadza wartości wszystkich elementów tablicy przekazaną do tablicy parametrów.  
  
 [!code-vb[VbVbcnProcedures#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#48)]  
  
 [!code-vb[VbVbcnProcedures#49](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#49)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [Procedury](./index.md)
- [Parametry i argumenty procedur](./procedure-parameters-and-arguments.md)
- [Przekazywanie argumentów według wartości i według odwołania](./passing-arguments-by-value-and-by-reference.md)
- [Przekazywanie argumentów według pozycji i według nazwy](./passing-arguments-by-position-and-by-name.md)
- [Parametry opcjonalne](./optional-parameters.md)
- [Przeciążanie procedury](./procedure-overloading.md)
- [Tablice](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)
