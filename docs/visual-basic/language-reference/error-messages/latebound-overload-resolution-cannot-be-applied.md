---
title: Ustalanie przeciążenia późnego wiązania nie może zostać zastosowane w elemencie „<procedurename>”, ponieważ wystąpienie uzyskujące dostęp jest typem interfejsu
ms.date: 07/20/2015
f1_keywords:
- vbc30933
- bc30933
helpviewer_keywords:
- overload resolution [Visual Basic], with late-bound argument
- BC30933
ms.assetid: 8182eea0-dd34-4d6e-9ca0-41d8713e9dc4
ms.openlocfilehash: 1fe3c4a29b542302b3615459142a3c565aa8244f
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/26/2019
ms.locfileid: "68513021"
---
# <a name="latebound-overload-resolution-cannot-be-applied-to-procedurename-because-the-accessing-instance-is-an-interface-type"></a>Nie można zastosować rozpoznawania przeciążenia ustalanie do elementu\<"procedurname >", ponieważ wystąpienie dostępu jest typu interfejsu

Kompilator próbuje rozpoznać odwołania do przeciążonej właściwości lub procedury, ale odwołanie nie powiedzie się, ponieważ argument jest typu `Object` , a odwołujący obiekt ma typ danych interfejsu. `Object` Argument wymusza, aby kompilator rozpoznał odwołanie jako późne powiązanie.

W tych okolicznościach kompilator rozpoznaje Przeciążenie za pomocą klasy implementującej, a nie za pomocą interfejsu bazowego. Jeśli Klasa zmienia nazwę jednej ze przeciążonych wersji, kompilator nie traktuje tej wersji jako przeciążenia, ponieważ jej nazwa jest inna. To z kolei powoduje, że kompilator ignoruje wersję o zmienionej nazwie, gdy mogło być to poprawny wybór w celu rozpoznania odwołania.

**Identyfikator błędu:** BC30933

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

- Służy `CType` do rzutowania argumentu z `Object` na typ określony przez sygnaturę przeciążenia, które chcesz wywołać.

  Należy zauważyć, że nie jest on pomocny do rzutowania obiektu odwołującego na podstawowy interfejs. Należy rzutować argument, aby uniknąć tego błędu.

## <a name="example"></a>Przykład

W poniższym przykładzie pokazano wywołanie przeciążonej `Sub` procedury, która powoduje ten błąd w czasie kompilacji.

```vb
Module m1
    Interface i1
        Sub s1(ByVal p1 As Integer)
        Sub s1(ByVal p1 As Double)
    End Interface
    Class c1
        Implements i1
        Public Overloads Sub s1(ByVal p1 As Integer) Implements i1.s1
        End Sub
        Public Overloads Sub s2(ByVal p1 As Double) Implements i1.s1
        End Sub
    End Class
    Sub Main()
        Dim refer As i1 = New c1
        Dim o1 As Object = 3.1415
        ' The following reference is INVALID and causes a compiler error.
        refer.s1(o1)
    End Sub
End Module
```

W poprzednim przykładzie, jeśli kompilator zezwolił `s1` na zapisanie, rozdzielczość odbywa się za pomocą klasy `c1` , a nie interfejsu `i1`. Oznacza to, że kompilator nie będzie rozważany `s2` , ponieważ jego nazwa jest inna `c1`w, mimo że jest to poprawny wybór zdefiniowany przez `i1`.

Błąd można poprawić, zmieniając wywołanie jednego z następujących wierszy kodu:

```vb
refer.s1(CType(o1, Integer))
refer.s1(CType(o1, Double))
```

Każdy z powyższych wierszy kodu jawnie rzutuje `Object` zmienną `o1` na jeden z typów parametrów zdefiniowanych dla przeciążenia.

## <a name="see-also"></a>Zobacz także

- [Przeciążanie procedury](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)
- [Rozpoznanie przeciążenia](../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)
- [Funkcja CType](../../../visual-basic/language-reference/functions/ctype-function.md)
