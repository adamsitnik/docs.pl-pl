---
title: Optional (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Optional
- vb.optional
helpviewer_keywords:
- Optional keyword [Visual Basic], contexts
- Optional keyword [Visual Basic]
ms.assetid: 4571ce88-a539-4115-b230-54eb277c6aa7
ms.openlocfilehash: 3758f17634395236abf2cd7059418bf6f8b6c062
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630923"
---
# <a name="optional-visual-basic"></a>Optional (Visual Basic)

Określa, że argument procedury może zostać pominięty, gdy procedura jest wywoływana.

## <a name="remarks"></a>Uwagi

Dla każdego opcjonalnego parametru należy określić wyrażenie stałe jako wartość domyślną tego parametru. Jeśli wyrażenie zwróci wartość [Nothing](../../../visual-basic/language-reference/nothing.md), wartością domyślną parametru typ danych jest jako wartość domyślna.

Jeśli lista parametrów zawiera opcjonalny parametr, każdy parametr, który następuje po nim musi być również opcjonalny.

`Optional` Modyfikator może być używany w tych kontekstach:

- [Declare, instrukcja](../../../visual-basic/language-reference/statements/declare-statement.md)

- [Function, instrukcja](../../../visual-basic/language-reference/statements/function-statement.md)

- [Instrukcja Property](../../../visual-basic/language-reference/statements/property-statement.md)

- [Sub, instrukcja](../../../visual-basic/language-reference/statements/sub-statement.md)

> [!NOTE]
> Podczas wywoływania procedury z parametrami opcjonalnymi lub bez nich można przekazać argumenty według pozycji lub według nazwy. Aby uzyskać więcej informacji, zobacz [przekazywanie argumentów według pozycji i według nazwy](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md).

> [!NOTE]
> Można także zdefiniować procedurę z opcjonalnymi parametrami przy użyciu przeciążenia. Jeśli masz jeden opcjonalny parametr, możesz zdefiniować dwie przeciążone wersje procedury, jedną, która akceptuje parametr i jeden, który nie jest. Aby uzyskać więcej informacji, zobacz przeciążanie [procedur](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md).

## <a name="example"></a>Przykład

W poniższym przykładzie zdefiniowano procedurę, która ma opcjonalny parametr.

```vb
Public Function FindMatches(ByRef values As List(Of String),
                            ByVal searchString As String,
                            Optional ByVal matchCase As Boolean = False) As List(Of String)

    Dim results As IEnumerable(Of String)

    If matchCase Then
        results = From v In values
                  Where v.Contains(searchString)
    Else
        results = From v In values
                  Where UCase(v).Contains(UCase(searchString))
    End If

    Return results.ToList()
End Function
```

## <a name="example"></a>Przykład

W poniższym przykładzie pokazano, jak wywołać procedurę z argumentami przekazaną przez pozycję i z argumentami przekazaną przez nazwę. Procedura ma dwa parametry opcjonalne.

[!code-vb[VbVbalrKeywords#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class8.vb#21)]

## <a name="see-also"></a>Zobacz także

- [Lista parametrów](../../../visual-basic/language-reference/statements/parameter-list.md)
- [Parametry opcjonalne](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)
- [Słowa kluczowe](../../../visual-basic/language-reference/keywords/index.md)
