---
title: Konwersje jawne i niejawne (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- conversions [Visual Basic], type
- variables [Visual Basic], changing data type
- casting
- conversions [Visual Basic], data type
- type conversion [Visual Basic], implicit conversions
- CType function [Visual Basic], conversions
- casting, data types
- data type conversion [Visual Basic], explicit
- type conversion [Visual Basic], explicit conversions
- data types [Visual Basic], casting
- conversions [Visual Basic], implicit
- explicit data type conversions [Visual Basic]
- conversions [Visual Basic]
- changing data types [Visual Basic]
- conversions [Visual Basic], explicit
- data type conversion [Visual Basic], implicit
- implicit data type conversions [Visual Basic]
ms.assetid: 77de1659-af8a-492c-967e-e7ef60ccce66
ms.openlocfilehash: 4bcf2d76a2983294f244b72f286842a92fb5e64e
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512866"
---
# <a name="implicit-and-explicit-conversions-visual-basic"></a>Konwersje jawne i niejawne (Visual Basic)

Niejawna *Konwersja* nie wymaga żadnej specjalnej składni w kodzie źródłowym. W poniższym przykładzie Visual Basic niejawnie konwertuje wartość `k` do wartości zmiennoprzecinkowej o pojedynczej precyzji przed przypisaniem do. `q`

```vb
Dim k As Integer
Dim q As Double
' Integer widens to Double, so you can do this with Option Strict On.
k = 432
q = k
```

*Jawna konwersja* używa słowa kluczowego konwersji typu. Visual Basic udostępnia kilka takich słów kluczowych, które przekształcają wyrażenie w nawiasy z żądanym typem danych. Te słowa kluczowe działają podobnie do funkcji, ale kompilator generuje kod wewnętrznie, więc wykonywanie jest nieco szybsze niż w przypadku wywołania funkcji.

W poniższym rozszerzeniu poprzedniego przykładu `CInt` słowo kluczowe konwertuje wartość z `q` powrotem na liczbę całkowitą przed przypisaniem do `k`.

```vb
' q had been assigned the value 432 from k.
q = Math.Sqrt(q)
k = CInt(q)
' k now has the value 21 (rounded square root of 432).
```

## <a name="conversion-keywords"></a>Słowa kluczowe konwersji

W poniższej tabeli przedstawiono dostępne słowa kluczowe konwersji.

|Słowo kluczowe konwersji typu|Konwertuje wyrażenie na typ danych|Dozwolone typy danych wyrażenia do przekonwertowania|
|---|---|---|
|`CBool`|[Boolean, typ danych](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy, i `String`wyliczane),,`Object`|
|`CByte`|[Byte, typ danych](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|Dowolny typ liczbowy (w `SByte` tym i typy wyliczeniowe `Boolean`) `String`,,,`Object`|
|`CChar`|[Char, typ danych](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`String`, `Object`|
|`CDate`|[Date, typ danych](../../../../visual-basic/language-reference/data-types/date-data-type.md)|`String`, `Object`|
|`CDbl`|[Double, typ danych](../../../../visual-basic/language-reference/data-types/double-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CDec`|[Decimal, typ danych](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CInt`|[Integer, typ danych](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CLng`|[Long, typ danych](../../../../visual-basic/language-reference/data-types/long-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CObj`|[Object, typ danych](../../../../visual-basic/language-reference/data-types/object-data-type.md)|Dowolny typ|
|`CSByte`|[SByte, typ danych](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|Dowolny typ liczbowy (w `Byte` tym i typy wyliczeniowe `Boolean`) `String`,,,`Object`|
|`CShort`|[Short, typ danych](../../../../visual-basic/language-reference/data-types/short-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CSng`|[Single, typ danych](../../../../visual-basic/language-reference/data-types/single-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CStr`|[String, typ danych](../../../../visual-basic/language-reference/data-types/string-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean`, `Char`, `Char` Array, `Date`,`Object`|
|`CType`|Typ określony po przecinku (`,`)|Podczas konwertowania na *Typ danych podstawowych* (włącznie z tablicą typu elementarnego) te same typy, które są dozwolone dla odpowiedniego słowa kluczowego konwersji<br /><br /> Podczas konwertowania na *Typ danych złożonych*, interfejsy, które implementuje, oraz klasy, z których dziedziczy<br /><br /> Podczas konwertowania na klasę lub strukturę, w której jest przeciążona `CType`, ta klasa lub struktura|
|`CUInt`|[UInteger, typ danych](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CULng`|[ULong, typ danych](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|
|`CUShort`|[UShort, typ danych](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|Dowolny typ liczbowy (w `Byte`tym `SByte`typy wyliczeniowe), `Boolean` `String`,,`Object`|

## <a name="the-ctype-function"></a>Funkcja CType

[Funkcja CType](../../../../visual-basic/language-reference/functions/ctype-function.md) działa na dwóch argumentach. Pierwszy jest wyrażeniem, które ma zostać przekonwertowane, a drugi to docelowy typ danych lub Klasa obiektu. Należy zauważyć, że pierwszy argument musi być wyrażeniem, a nie typem.

`CType`jest *funkcją wbudowaną*, co oznacza, że skompilowany kod wykonuje konwersję, często bez generowania wywołania funkcji. Zwiększa to wydajność.

Aby porównać `CType` z innymi słowami kluczowymi konwersji, zobacz [operator DirectCast](../../../../visual-basic/language-reference/operators/directcast-operator.md) i [operator TryCast](../../../../visual-basic/language-reference/operators/trycast-operator.md).

### <a name="elementary-types"></a>Typy elementarne

Poniższy przykład ilustruje użycie `CType`.

```vb
k = CType(q, Integer)
' The following statement coerces w to the specific object class Label.
f = CType(w, Label)
```

### <a name="composite-types"></a>Typy złożone

Można użyć `CType` do przekonwertowania wartości na złożone typy danych, a także do typów podstawowych. Można go również użyć do przekształcenia klasy Object na typ jednego z jego interfejsów, jak w poniższym przykładzie.

```vb
' Assume class cZone implements interface iZone.
Dim h As Object
' The first argument to CType must be an expression, not a type.
Dim cZ As cZone
' The following statement coerces a cZone object to its interface iZone.
h = CType(cZ, iZone)
```

### <a name="array-types"></a>Typy tablic

`CType`można również skonwertować typy danych tablicy, jak w poniższym przykładzie.

```vb
Dim v() As classV
Dim obArray() As Object
' Assume some object array has been assigned to obArray.
' Check for run-time type compatibility.
If TypeOf obArray Is classV()
    ' obArray can be converted to classV.
    v = CType(obArray, classV())
End If
```

Aby uzyskać więcej informacji i zapoznać się z przykładem, zobacz [konwersje tablic](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md).

### <a name="types-defining-ctype"></a>Typy definiujące CType

Można zdefiniować `CType` dla zdefiniowanej klasy lub struktury. Pozwala to na konwertowanie wartości do i z typu klasy lub struktury. Aby uzyskać więcej informacji i zapoznać się z [przykładem, zobacz How to: Zdefiniuj operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)konwersji.

> [!NOTE]
> Wartości używane ze słowem kluczowym konwersji muszą być prawidłowe dla docelowego typu danych lub wystąpił błąd. Na przykład, jeśli `Long` spróbujesz skonwertować `Integer`do `Long` , wartość `Integer` musi znajdować się w zakresie prawidłowym dla typu danych.

> [!CAUTION]
> Określanie `CType` , aby konwertować z jednego typu klasy na inny błąd w czasie wykonywania, jeśli typ źródłowy nie pochodzi od typu docelowego. Taka awaria zgłasza <xref:System.InvalidCastException> wyjątek.

Jeśli jednak jeden z typów jest zdefiniowaną strukturą lub klasą, a jeśli zdefiniowano `CType` ją w tej strukturze lub klasy, konwersja może się powieść, jeśli spełnia wymagania. `CType` Zobacz [How to: Zdefiniuj operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)konwersji.

Wykonywanie jawnej konwersji jest również znane jako *rzutowanie* wyrażenia do danego typu danych lub klasy obiektu.

## <a name="see-also"></a>Zobacz także

- [Konwersje typów w Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [Konwertowanie między ciągami a innymi typami danych](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [Instrukcje: Konwertuj obiekt na inny typ w Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [Struktury](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Typy danych](../../../../visual-basic/language-reference/data-types/index.md)
- [Funkcje konwersji typu](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Rozwiązywanie problemów związanych z typami danych](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
