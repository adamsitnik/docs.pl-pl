---
title: Typ wartości opcjonalnej dla parametru opcjonalnego <parametername> jest niezgodny ze specyfikacją CLS
ms.date: 07/20/2015
f1_keywords:
- BC40042
- vbc40042
helpviewer_keywords:
- BC40042
ms.assetid: 1d6eae29-4ad3-4434-bde4-a53b6051adf5
ms.openlocfilehash: 88f8b7ea1e0a9b4cb115646f40abbf8a567a2b1d
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641391"
---
# <a name="type-of-optional-value-for-optional-parameter-parametername-is-not-cls-compliant"></a>Typ wartości opcjonalnej dla parametru opcjonalnego \<parametername > nie jest zgodny ze specyfikacją CLS
Procedura jest oznaczona jako `<CLSCompliant(True)>` , ale deklaruje [opcjonalnie](../../../visual-basic/language-reference/modifiers/optional.md) parametru z wartością domyślną niezgodnego typu.  
  
 Procedury zachować zgodność z [niezależność od języka i składniki niezależne od języka](../../../standard/language-independence-and-language-independent-components.md) (CLS), jej używać tylko typów zgodnych ze specyfikacją CLS. Dotyczy to typy parametrów, typ zwracany i typy jego zmiennych lokalnych. Ma również zastosowanie do wartościami domyślnymi parametrów opcjonalnych.  
  
 Następujące typy danych Visual Basic nie są zgodne ze specyfikacją CLS:  
  
- [SByte, typ danych](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
- [UInteger, typ danych](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
- [ULong, typ danych](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
- [UShort, typ danych](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Po zastosowaniu <xref:System.CLSCompliantAttribute> atrybut elementu programistycznego, ten atrybut zostanie ustawiony `isCompliant` albo parametr `True` lub `False` aby wskazać, zgodności ani niezgodności. Nie istnieje domyślny dla tego parametru. Ponadto należy podać wartość.  
  
 Jeśli nie zastosujesz <xref:System.CLSCompliantAttribute> elementu, jest uznawane za niezgodne.  
  
 Domyślnie ta wiadomość jest ostrzeżenie. Uzyskać informacje o ukrywaniu ostrzeżenia lub traktowanie ostrzeżeń jako błędy, zobacz [Konfigurowanie ostrzeżeń w języku Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Identyfikator błędu:** BC40042  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Jeśli parametr opcjonalny musi mieć wartość domyślną dla tego konkretnego typu, Usuń <xref:System.CLSCompliantAttribute>. Procedura nie może być zgodne ze specyfikacją CLS.  
  
- Jeśli procedura musi być zgodny ze specyfikacją CLS, należy zmienić typ tę wartość domyślną, do najbliższej typu zgodny ze specyfikacją CLS. Na przykład, zamiast z `UInteger` można użyć `Integer` Jeśli nie potrzebujesz zakres wartości ponad 2 147 483 647. Jeśli potrzebujesz rozszerzonej zakresu, można zastąpić `UInteger` z `Long`.  
  
- Czy komunikowanie się z obiektami automatyzacji lub COM, pamiętać, że niektóre typy mają różnych szerokościach danych niż na platformie .NET Framework. Na przykład `int` często jest 16 bitów w innych środowiskach. Jeśli akceptujesz 16-bitową liczbę całkowitą z takiego składnika, Zadeklaruj go jako `Short` zamiast `Integer` w zarządzanym kodzie języka Visual Basic.
