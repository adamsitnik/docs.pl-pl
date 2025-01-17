---
title: Interfejsy (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, interfaces
- interfaces [Visual Basic], Visual Basic
- interfaces
- interfaces [Visual Basic]
ms.assetid: 61b06674-12c9-430b-be68-cc67ecee1f5b
ms.openlocfilehash: 968e5d9bb08f168e3c77b40ea42b16dc66e93e64
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956296"
---
# <a name="interfaces-visual-basic"></a>Interfejsy (Visual Basic)
*Interfejsy* definiują właściwości, metody i zdarzenia, które mogą implementować klasy. Interfejsy umożliwiają definiowanie funkcji jako małych grup ściśle powiązanych właściwości, metod i zdarzeń; zmniejsza to problemy ze zgodnością, ponieważ można opracowywać ulepszone implementacje dla interfejsów bez narażania istniejącego kodu. W dowolnym momencie możesz dodać nowe funkcje, opracowując dodatkowe interfejsy i implementacje.  
  
 Istnieje kilka innych powodów, dla których warto chcieć używać interfejsów zamiast dziedziczenia klasy:  
  
- Interfejsy są lepiej dopasowane do sytuacji, w których aplikacje wymagają wielu niepowiązanych typów obiektów, aby zapewnić pewne funkcje.  
  
- Interfejsy są bardziej elastyczne niż klasy bazowe, ponieważ istnieje możliwość zdefiniowania jednej implementacji, która może zaimplementować wiele interfejsów.  
  
- Interfejsy są lepsze w sytuacjach, w których nie trzeba dziedziczyć implementacji z klasy bazowej.  
  
- Interfejsy są przydatne, gdy nie można użyć dziedziczenia klas. Na przykład struktury nie mogą dziedziczyć z klas, ale mogą implementować interfejsy.  
  
## <a name="declaring-interfaces"></a>Deklarowanie interfejsów  
 Definicje interfejsu są ujęte w `Interface` instrukcji `End Interface` i. Postępując zgodnie `Interface` z instrukcją, można dodać opcjonalną `Inherits` instrukcję, która wyświetla jeden lub więcej dziedziczonych interfejsów. `Inherits` Instrukcje muszą poprzedzać wszystkie inne instrukcje w deklaracji poza komentarzem. Pozostałe instrukcje w definicji interfejsu powinny mieć `Event`instrukcje, `Property` `Sub` `Function` `Interface` `Enum` ,,,,, ,i.`Structure` `Class` Interfejsy nie mogą zawierać żadnych kodów implementacji ani instrukcji skojarzonych z kodem implementacji, takimi `End Property`jak `End Sub` lub.  
  
 W przestrzeni nazw instrukcje interfejsu są `Friend` domyślnie, ale mogą być również jawnie zadeklarowane jako `Public` lub `Friend`. Interfejsy zdefiniowane w ramach klas, modułów, interfejsów i struktur są `Public` domyślnie, ale mogą być również jawnie zadeklarowane jako `Public`, `Friend` `Protected`,, lub `Private`.  
  
> [!NOTE]
> `Shadows` Słowo kluczowe może być zastosowane do wszystkich elementów członkowskich interfejsu. Słowo kluczowe może być stosowane do `Sub`, `Function`, i `Property` instrukcji zadeklarowanych w definicji interfejsu. `Overloads` Ponadto `Property` instrukcje mogą `Default`mieć modyfikatory, `ReadOnly`, lub `WriteOnly` . Żaden z innych`Public`modyfikatorów — `Protected` `Friend`, `Private` ,,`Shared`,,,, lub`Overridable`— jest dozwolony. `Overrides` `MustOverride` Aby uzyskać więcej informacji, zobacz [Kontekst deklaracji i domyślne poziomy dostępu](../../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Na przykład poniższy kod definiuje interfejs z jedną funkcją, jedną właściwością i jednym zdarzeniem.  
  
 [!code-vb[VbVbalrOOP#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#17)]  
  
## <a name="implementing-interfaces"></a>Implementowanie interfejsów  
 Zastrzeżony wyraz `Implements` Visual Basic jest używany na dwa sposoby. `Implements` Instrukcja oznacza, że Klasa lub struktura implementuje interfejs. `Implements` Słowo kluczowe oznacza, że element członkowski klasy lub element członkowski struktury implementuje określonego elementu członkowskiego interfejsu.  
  
### <a name="implements-statement"></a>Implements — Instrukcja  
 Jeśli klasa lub struktura implementuje jeden lub więcej interfejsów, musi zawierać `Implements` instrukcję bezpośrednio `Class` po instrukcji or `Structure` . `Implements` Instrukcja wymaga rozdzielonej przecinkami listy interfejsów, które mają być implementowane przez klasę. Klasa lub struktura muszą implementować wszystkie elementy członkowskie interfejsu za `Implements` pomocą słowa kluczowego.  
  
### <a name="implements-keyword"></a>Implements — słowo kluczowe  
 `Implements` Słowo kluczowe wymaga zaimplementowania listy składowych interfejsu rozdzielanych przecinkami. Ogólnie tylko jeden element członkowski interfejsu jest określony, ale można określić wielu członków. Specyfikacja elementu członkowskiego interfejsu składa się z nazwy interfejsu, która musi być określona w instrukcji Implements w klasie; okres; i nazwa funkcji składowej, właściwości lub zdarzenia, które mają zostać zaimplementowane. Nazwa elementu członkowskiego implementującego element członkowski interfejsu może korzystać z dowolnego identyfikatora prawnego i nie jest ograniczona do `InterfaceName_MethodName` Konwencji używanej we wcześniejszych wersjach Visual Basic.  
  
 Na przykład poniższy kod ilustruje sposób deklarowania podprocedury o nazwie `Sub1` implementującej metodę interfejsu:  
  
 [!code-vb[VbVbalrOOP#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#69)]  
  
 Typy parametrów i zwracane typy składowej implementującej muszą być zgodne z właściwością interfejsu lub deklaracją elementu członkowskiego w interfejsie. Najbardziej typowym sposobem implementacji elementu interfejsu jest element członkowski, który ma taką samą nazwę jak interfejs, jak pokazano w poprzednim przykładzie.  
  
 Aby zadeklarować implementację metody interfejsu, można użyć dowolnych atrybutów, które są prawne dla deklaracji metody wystąpienia, `Overloads`w `Overrides`tym `Overridable`, `Public`, `Private`, `Protected`,,, `Friend` ,`Protected Friend`, `MustOverride` ,i`Static`. `Default` Atrybut `Shared` nie jest dozwolony, ponieważ definiuje klasę, a nie metodę wystąpienia.  
  
 Korzystając `Implements`z programu, można również napisać pojedynczą metodę, która implementuje wiele metod zdefiniowanych w interfejsie, tak jak w poniższym przykładzie:  
  
 [!code-vb[VbVbalrOOP#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#70)]  
  
 Do zaimplementowania elementu członkowskiego interfejsu można użyć prywatnego elementu członkowskiego. Gdy prywatny element członkowski implementuje element członkowski interfejsu, ten element członkowski jest dostępny w interfejsie, mimo że nie jest dostępny bezpośrednio dla zmiennych obiektów klasy.  
  
### <a name="interface-implementation-examples"></a>Przykłady implementacji interfejsu  
 Klasy implementujące interfejs muszą implementować wszystkie jego właściwości, metody i zdarzenia.  
  
 W poniższym przykładzie zdefiniowano dwa interfejsy. Drugi interfejs, `Interface2`, dziedziczy `Interface1` i definiuje dodatkową właściwość i metodę.  
  
 [!code-vb[VbVbalrOOP#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#39)]  
  
 Następny przykład implementuje `Interface1`interfejs zdefiniowany w poprzednim przykładzie:  
  
 [!code-vb[VbVbalrOOP#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#40)]  
  
 Ostatni przykład implementuje `Interface2`, w tym metodę dziedziczoną z `Interface1`:  
  
 [!code-vb[VbVbalrOOP#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#41)]  
  
 Można zaimplementować właściwość ReadOnly z właściwością ReadWrite (oznacza to, że nie trzeba deklarować jej jako tylko do odczytu w klasie implementującej).  Implementacja interfejsu niesie obietnice zwiększenia do wdrożenia co najmniej elementów członkowskich, które deklaruje interfejs, ale można zaoferować więcej funkcji, takich jak umożliwienie zapisu właściwości.  
  
## <a name="related-topics"></a>Tematy pokrewne  
  
|Tytuł|Opis|  
|-----------|-----------------|  
|[Przewodnik: tworzenie i implementowanie interfejsów](../../../../visual-basic/programming-guide/language-features/interfaces/walkthrough-creating-and-implementing-interfaces.md)|Zawiera szczegółową procedurę, która przeprowadzi Cię przez proces definiowania i implementowania własnego interfejsu.|  
|[Wariancje w interfejsach ogólnych](../../concepts/covariance-contravariance/variance-in-generic-interfaces.md)|Omawia kowariancję i kontrawariancja w interfejsach ogólnych i zawiera listę podstawowych interfejsów w .NET Framework.|
