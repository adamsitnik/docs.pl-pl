---
title: Projekt zdarzenia
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- pre-events
- events [.NET Framework], design guidelines
- member design guidelines, events
- event handlers [.NET Framework], event design guidelines
- post-events
- signatures, event handling
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
author: KrzysztofCwalina
ms.openlocfilehash: 530c68ea5342263acd07f8dc8a8c8ce889652503
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026448"
---
# <a name="event-design"></a>Projekt zdarzenia
Zdarzenia są najczęściej używane formularza wywołania zwrotne (konstrukcji, zezwalających na platformę, by mogą wywoływać kodu użytkownika). Inne mechanizmy wywołania zwrotnego dołączone elementy członkowskie, biorąc delegatów, wirtualne elementy członkowskie i oparte na interfejsie wtyczki. Dane z badań użyteczność wskazać, że większość deweloperów bardziej komfortowo, jednocześnie za pomocą zdarzeń, niż użytkownicy korzystają z innych mechanizmów wywołania zwrotnego. Zdarzenia są dobrze zintegrowane z Visual Studio i wielu języków.  
  
 Ważne jest, aby zwrócić uwagę na dwie grupy zdarzeń: zdarzenia wywoływane przed wykonaniem stan zmiany systemu, nazywany zdarzeń poprzedzających i zdarzenia wywoływane po zmianie stanu, wywoływana po zdarzenia. Oto przykład zdarzenia poprzedzającego `Form.Closing`, które jest wywoływane przed zamknięciem formularza. Oto przykład zdarzenia po `Form.Closed`, które jest wywoływane po zamknięciu formularza.  
  
 **✓ DO** używany jest termin "raise" dla zdarzenia, a nie "fire" lub "wyzwolenia".  
  
 **✓ DO** użyj <xref:System.EventHandler%601?displayProperty=nameWithType> zamiast ręcznego tworzenia nowych delegatów, które mają być używane jako procedury obsługi zdarzeń.  
  
 **✓ CONSIDER** przy użyciu podklasą <xref:System.EventArgs> jako argument zdarzenia, jeśli nie masz pewności absolutnie zdarzenie nie będzie trzeba do przenoszenia danych do obsługi metody zdarzeń w takim przypadku można zastosować `EventArgs` wpisać bezpośrednio.  
  
 Jeśli dostarczasz interfejsu API przy użyciu `EventArgs` bezpośrednio, nigdy nie będą mogli dodawać żadnych danych, które mają znajdować się ze zdarzeniem bez przerywania zgodność. Jeśli używasz podklasę, nawet jeśli początkowo całkowicie pusty, można dodać właściwości do podklasy w razie potrzeby.  
  
 **✓ DO** Użyj chronione metody wirtualnej, aby wywołać każdego zdarzenia. To ma zastosowanie tylko do niestatycznego zdarzenia niezapieczętowane klasy, aby nie struktury, zapieczętowane klasy lub zdarzenia statyczne.  
  
 Przeznaczenie metody jest sposób dla klasy pochodnej do obsługi zdarzeń za pomocą zastąpienia. Zastępowanie jest bardziej elastyczna, szybsze i bardziej naturalny sposób obsługi zdarzeń klasy podstawowej w klasach pochodnych. Zgodnie z Konwencją Nazwa metody powinna rozpoczynać się "On" i występować z nazwą zdarzenia.  
  
 Klasa pochodna może zrezygnować z wywoływać implementację podstawową metody w jego zastąpienie. Należy przygotować to przez nieumieszczenie jakiegokolwiek przetwarzania w metodzie, która jest wymagana dla klasy bazowej działać poprawnie.  
  
 **✓ DO** przyjmować jeden parametr do metody chronionych, która wywołuje zdarzenie.  
  
 Powinien zostać nazwany parametr `e` , należy wpisać jako klasa argumentów zdarzenia.  
  
 **X DO NOT** należy przekazać wartość null jako nadawcę podczas wywołaniem Niestatyczne zdarzenia.  
  
 **✓ DO** przekazać wartości null jako nadawcę, gdy wywołaniem zdarzenia statyczne.  
  
 **X DO NOT** przekazać wartości null jako parametr danych zdarzenia, gdy wywołanie zdarzenia.  
  
 Należy przekazać `EventArgs.Empty` Jeśli nie chcesz przekazywać żadnych danych do metody obsługi zdarzeń. Deweloperzy oczekiwać, że ten parametr nie mają one wartość null.  
  
 **✓ CONSIDER** wywoływanie zdarzeń, które użytkownik końcowy może anulować. Dotyczy to tylko zdarzeń poprzedzających.  
  
 Użyj <xref:System.ComponentModel.CancelEventArgs?displayProperty=nameWithType> lub jego podklasy jako argumentu zdarzenia, aby zezwolić użytkownikom na anulowanie zdarzenia.  
  
### <a name="custom-event-handler-design"></a>Projekt programu obsługi zdarzeń niestandardowych  
 Istnieją przypadki, w którym `EventHandler<T>` nie można użyć, np. gdy struktura potrzebuje do pracy z wcześniejszych wersji środowiska CLR, która nie obsługuje typów ogólnych. W takich przypadkach może być konieczne projektowania i tworzenia delegata obsługi zdarzeń niestandardowych.  
  
 **✓ DO** zwracany typ void na użytek obsługi zdarzeń.  
  
 Program obsługi zdarzeń można wywołać wiele obsługi metod, prawdopodobnie na wielu obiektach zdarzeń. Jeśli zezwolono na metody obsługi zdarzeń w celu zwrócenia wartości, może to być wiele wartości zwracane dla każdego wywołania zdarzenia.  
  
 **✓ DO** użyj `object` jako typ pierwszego parametru metody obsługi zdarzeń i nadaj mu `sender`.  
  
 **✓ DO** użyj <xref:System.EventArgs?displayProperty=nameWithType> ani jej podklasy jako typ drugiego parametru obsługi zdarzeń i nadaj mu `e`.  
  
 **X DO NOT** ma więcej niż dwa parametry dotyczące programu obsługi zdarzeń.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*  
  
 *Przedrukowano za uprawnienie Pearson edukacji, Inc. z [wytyczne dotyczące projektowania Framework: Konwencje, Idiomy i wzorców dla wielokrotnego użytku, do bibliotek .NET, wydanie 2](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina i Brad Abrams publikowane 22 Oct 2008 przez Addison Wesley Professional w ramach serii rozwoju Windows firmy Microsoft.*  
  
## <a name="see-also"></a>Zobacz także

- [Element członkowski — zalecenia dotyczące projektowania](../../../docs/standard/design-guidelines/member.md)
- [Struktura — zalecenia dotyczące projektowania](../../../docs/standard/design-guidelines/index.md)
