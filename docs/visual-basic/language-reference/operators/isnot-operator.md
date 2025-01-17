---
title: IsNot — Operator (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.isnot
helpviewer_keywords:
- IsNot operator [Visual Basic]
ms.assetid: 8dd2bcdb-0166-48a2-9094-60dfb448f36c
ms.openlocfilehash: 32e8f9532244679d2994b0e3d98279d75f7e77b4
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701038"
---
# <a name="isnot-operator-visual-basic"></a>IsNot — Operator (Visual Basic)

Porównuje dwie zmienne odwołań do obiektów.

## <a name="syntax"></a>Składnia

```vb
result = object1 IsNot object2
```

## <a name="parts"></a>Części
 `result` jest wymagana. Wartość `Boolean`.

 `object1` jest wymagana. Dowolna zmienna lub wyrażenie `Object`.

 `object2` jest wymagana. Dowolna zmienna lub wyrażenie `Object`.

## <a name="remarks"></a>Uwagi
 Operator `IsNot` Określa, czy dwa odwołania do obiektów odwołują się do różnych obiektów. Jednak nie wykonuje porównania wartości. Jeśli `object1` i `object2` odwołują się do dokładnie tego samego wystąpienia obiektu, `result` jest `False`; Jeśli tak nie jest, `result` jest `True`.

 `IsNot` jest przeciwieństwem operatora `Is`. Zaletą `IsNot` jest możliwość uniknięcia składni niewygodna z `Not` i `Is`, co może być trudne do odczytania.

 Można użyć operatorów `Is` i `IsNot` do testowania zarówno obiektów wczesnych, jak i z późnym wiązaniem.

## <a name="example"></a>Przykład
 Poniższy przykład kodu używa operatora `Is` i operatora `IsNot` do wykonania tego samego porównania.

 [!code-vb[VbVbalrOperators#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#29)]

## <a name="see-also"></a>Zobacz także

- [Is, operator](is-operator.md)
- [TypeOf, operator](typeof-operator.md)
- [Pierwszeństwo operatorów w Visual Basic](operator-precedence.md)
- [Instrukcje: testowanie, czy dwa obiekty są takie same](../../programming-guide/language-features/operators-and-expressions/how-to-test-whether-two-objects-are-the-same.md)
