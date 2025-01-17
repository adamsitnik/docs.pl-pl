---
title: Nazwy składowych typu
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], names
- methods [.NET Framework], names
- type members
- properties [.NET Framework], names
- fields, names
- field names
- names [.NET Framework], type members
- members [.NET Framework], type
ms.assetid: af5a0903-36af-4c2a-b848-cf959affeaa5
author: KrzysztofCwalina
ms.openlocfilehash: b4da14575d29582814d32a3050087b7acc0da802
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353708"
---
# <a name="names-of-type-members"></a>Nazwy składowych typu
Typy składowe są elementami członkowskimi: metodami, właściwościami, zdarzeniami, konstruktorami i polami. W poniższych sekcjach opisano wskazówki dotyczące nazewnictwa elementów członkowskich typu.  
  
## <a name="names-of-methods"></a>Nazwy metod  
 Ponieważ metody są metodą podjęcia działania, wskazówki dotyczące projektowania wymagają, aby nazwy metod były czasownikami lub wyrażeniami czasownikowymi. Poniższe wytyczne umożliwiają również odróżnianie nazw metod od nazw właściwości i typów, które są frazami rzeczownikmi lub przymiotnikami.  
  
 **✓ DO** Nadaj nazwy metody, które mogą lub fraz zlecenie.  
  
```csharp  
public class String {  
    public int CompareTo(...);  
    public string[] Split(...);  
    public string Trim();  
}  
```  
  
## <a name="names-of-properties"></a>Nazwy właściwości  
 W przeciwieństwie do innych elementów członkowskich, właściwości powinny zawierać frazę rzeczowników lub nazwy przymiotników. Oznacza to, że Właściwość odwołuje się do danych, a nazwa właściwości odzwierciedla to. PascalCasing jest zawsze używana dla nazw właściwości.  
  
 **✓ DO** nazwę właściwości, za pomocą rzeczownik, rzeczownik frazy lub przymiotnik.  
  
 **X DO NOT** mają właściwości, które zgodna z nazwą metody "Get", jak w poniższym przykładzie:  
  
 `public string TextWriter { get {...} set {...} }`  
 `public string GetTextWriter(int value) { ... }`  
  
 Ten wzorzec zazwyczaj wskazuje, że właściwość powinna być w rzeczywistości metodą.  
  
 **✓ DO** nazwy właściwości kolekcji o liczbie mnogiej frazę opisujące elementy w kolekcji, zamiast korzystać z pojedynczej frazy, a następnie "List" lub "Collection".  
  
 **✓ DO** nazwy właściwości logiczne z frazą wyraził (`CanSeek` zamiast `CantSeek`). Opcjonalnie można również prefiksować właściwości logiczne z "is", "" lub "ma", ale tylko wtedy, gdy dodaje wartość.  
  
 **✓ CONSIDER** zapewnia taką samą nazwę jak jego typ właściwości.  
  
 Na przykład następująca Właściwość prawidłowo pobiera i ustawia wartość wyliczenia o nazwie `Color`, więc właściwość ma nazwę `Color`:  
  
```csharp  
public enum Color {...}  
public class Control {  
    public Color Color { get {...} set {...} }  
}  
```  
  
## <a name="names-of-events"></a>Nazwy zdarzeń  
 Zdarzenia zawsze odwołują się do niektórych akcji, takich, które są wykonywane lub takie, które wystąpiły. W związku z tym, podobnie jak w przypadku metod, zdarzenia są nazwane przy użyciu czasowników, a w celu wskazania czasu, gdy zdarzenie jest zgłaszane, używana jest wartość zlecenia.  
  
 **✓ DO** nazwy zdarzeń za pomocą zlecenie lub zlecenia frazę.  
  
 Przykładami mogą być `Clicked`, `Painting`, `DroppedDown` i tak dalej.  
  
 **✓ DO** nadać nazwy zdarzenia przy użyciu koncepcji przed i po nim, za pomocą obecny i czasy w przeszłości.  
  
 Na przykład zdarzenie zamknięcia, które jest wywoływane przed zamknięciem okna, zostanie wywołane `Closing`, a jeden, który jest wywoływany po zamknięciu okna, zostanie wywołany `Closed`.  
  
 **X DO NOT** Użyj "Before" lub "After" prefiksy lub postfixes, aby wskazać, przed i po zdarzenia. Użyj obecnych i ostatnich dziesiątek tak samo, jak zostało to opisane.  
  
 **✓ DO** nazwy programów obsługi zdarzeń (używany jako typy zdarzeń delegaty) wraz z sufiksem "EventHandler", jak pokazano w poniższym przykładzie:  
  
 `public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`  
  
 **✓ DO** korzystanie z dwóch parametrów o nazwie `sender` i `e` w procedurze obsługi zdarzeń.  
  
 Parametr Sender reprezentuje obiekt, który spowodował zdarzenie. Parametr nadawcy jest zazwyczaj typu `object`, nawet jeśli można użyć bardziej określonego typu.  
  
 **✓ DO** nazwy zdarzeń klasy argumentu z sufiksem "EventArgs".  
  
## <a name="names-of-fields"></a>Nazwy pól  
 Wskazówki dotyczące nazewnictwa pól mają zastosowanie do statycznych pól publicznych i chronionych. Pola wewnętrzne i prywatne nie są objęte wskazówkami, a pola Public lub Protected instance są niedozwolone w [wytycznych dotyczących projektowania elementu członkowskiego](../../../docs/standard/design-guidelines/member.md).  
  
 **✓ DO** Użyj PascalCasing w nazwach pól.  
  
 **✓ DO** nazwać pola, przy użyciu rzeczownik, rzeczownik frazy lub przymiotnik.  
  
 **X DO NOT** używać prefiksu dla nazw pól.  
  
 Na przykład nie umożliwia "g_" lub "s_" oznaczają pola statyczne.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*  
  
 *Reprinted przez uprawnienie Pearson Education, Inc. od [Framework — wytyczne dotyczące projektowania: Konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, druga wersja @ no__t-0 przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*  
  
## <a name="see-also"></a>Zobacz także

- [Struktura — zalecenia dotyczące projektowania](../../../docs/standard/design-guidelines/index.md)
- [Wskazówki dotyczące nazewnictwa](../../../docs/standard/design-guidelines/naming-guidelines.md)
