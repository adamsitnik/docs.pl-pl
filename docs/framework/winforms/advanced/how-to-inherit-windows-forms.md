---
title: 'Porady: Dziedziczenie formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- inherited forms [Windows Forms], creating at run-time
- inheritance [Windows Forms], forms
- Windows Forms, inheritance
ms.assetid: cb3e1c0f-3d2a-4cdc-b0d1-c92eae567ffb
ms.openlocfilehash: 402386e16687162e25e16e5c30c787f7e721fbba
ms.sourcegitcommit: 1e72e2990220b3635cebc39586828af9deb72d8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/26/2019
ms.locfileid: "71306372"
---
# <a name="how-to-inherit-windows-forms"></a>Porady: Dziedziczenie formularzy systemu Windows

Tworzenie nowych Windows Forms przez dziedziczenie z formularzy podstawowych jest wygodnym sposobem duplikowania najlepszych starań bez przechodzenia przez proces całkowitego odtwarzania formularza za każdym razem, gdy jest to wymagane.

Aby uzyskać więcej informacji na temat dziedziczenia formularzy w czasie projektowania przy użyciu okna dialogowego **selektora dziedziczenia** oraz wizualnego rozróżniania poziomów zabezpieczeń dziedziczonych [kontrolek, zobacz How to: Dziedzicz formularze przy użyciu okna dialogowego](how-to-inherit-forms-using-the-inheritance-picker-dialog-box.md)selektora dziedziczenia.

> [!NOTE]
> Aby można było dziedziczyć z formularza, plik lub przestrzeń nazw zawierające ten formularz muszą być wbudowane w plik wykonywalny lub DLL. Aby skompilować projekt, wybierz opcję **Kompiluj** z menu **kompilacja** . Ponadto odwołanie do przestrzeni nazw należy dodać do klasy dziedziczonej w formularzu.

## <a name="inherit-a-form-programmatically"></a>Programowe dziedziczenie formularza

1. W klasie Dodaj odwołanie do przestrzeni nazw zawierającej formularz, z którego chcesz dziedziczyć.

2. W definicji klasy Dodaj odwołanie do formularza, aby dziedziczyć. Odwołanie powinno zawierać przestrzeń nazw, która zawiera formularz, po którym następuje kropka, a następnie nazwę podstawowego formularza.

    ```vb
    Public Class Form2
        Inherits Namespace1.Form1
    ```

    ```csharp
    public class Form2 : Namespace1.Form1
    ```

 Podczas dziedziczenia formularzy należy pamiętać, że problemy mogą wystąpić w odniesieniu do programów obsługi zdarzeń, które są wywoływane dwa razy, ponieważ każde zdarzenie jest obsługiwane przez klasę bazową i dziedziczoną klasy. Aby uzyskać więcej informacji na temat tego, jak uniknąć tego problemu, zobacz [Rozwiązywanie problemów z dziedziczonymi programami obsługi zdarzeń w Visual Basic](../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md).

## <a name="see-also"></a>Zobacz także

- [Inherits, instrukcja](../../../visual-basic/language-reference/statements/inherits-statement.md)
- [Imports, instrukcja (przestrzeń nazw i typ .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [using](../../../csharp/language-reference/keywords/using.md)
- [Efekty modyfikowania wyglądu formularza podstawowego](effects-of-modifying-base-form-appearance.md)
- [Formularze Windows Forms — dziedziczenie wizualizacji](windows-forms-visual-inheritance.md)
