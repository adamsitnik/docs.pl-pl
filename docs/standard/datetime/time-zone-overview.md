---
title: Strefy czasowe — omówienie
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], about time zones
- transition time [.NET Framework]
- TimeZoneInfo class, about TimeZoneInfo class
- time zones [.NET Framework], creating
- invalid time [.NET Framework]
- fixed rule [.NET Framework]
- ambiguous time [.NET Framework]
- floating rule [.NET Framework]
- daylight saving time [.NET Framework]
- adjustment rule [.NET Framework]
- time zones [.NET Framework], terminology
ms.assetid: c4b7ed01-5e38-4959-a3b6-ef9765d6ccf1
ms.openlocfilehash: 83fa7609c9500bc51581b7b20db3992b4265488b
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73131603"
---
# <a name="time-zone-overview"></a>Strefy czasowe — omówienie

Klasa <xref:System.TimeZoneInfo> upraszcza tworzenie aplikacji obsługujących strefy czasowe. Klasa <xref:System.TimeZone> obsługuje pracę z lokalną strefą czasową i uniwersalnym czasem koordynowanym (UTC). Klasa <xref:System.TimeZoneInfo> obsługuje obie te strefy, a także strefę czasową, o której informacje są wstępnie zdefiniowane w rejestrze. Można również użyć <xref:System.TimeZoneInfo>, aby zdefiniować niestandardowe strefy czasowe, w których system nie ma informacji.

## <a name="time-zone-essentials"></a>Podstawowe informacje o strefie czasowej

Strefa czasowa jest regionem geograficznym, w którym jest używany ten sam czas. Zwykle, ale nie zawsze, sąsiadujące strefy czasowe są jedną godziną. Czas w dowolnej strefie czasowej na świecie może być wyrażony jako przesunięcie od uniwersalnego czasu koordynowanego (UTC).

Wiele stref czasu na świecie obsługuje czas letni. Czas letni próbuje wydłużyć czas letni, przesunięt do przodu o jedną godzinę na wiosnę lub wczesny lato i powraca do normalnego (lub standardowego) czasu w późnych godzinach. Te zmiany do i od czasu standardowego są znane jako reguły korekty.

Przejście do i od czasu letniego w określonej strefie czasowej może być zdefiniowane przez ustaloną lub przepływającą regułę korekty. Reguła ustalonej korekty ustawia określoną datę, w której następuje przejście do lub z czasu letniego. Na przykład przejście od czasu letniego do czasu standardowego przypadające w każdym roku w dniu 25 października następuje po ustalonej regule korekty. Znacznie bardziej typowe są reguły dostosowania zmiennoprzecinkowego, które ustawiają konkretny dzień określonego tygodnia w danym miesiącu w przypadku przejścia do lub z czasu letniego. Na przykład przejście od czasu standardowego do czasu letniego, który występuje w trzeciej niedzielę marca, następuje zgodnie z przepływaną regułą dopasowywania.

W przypadku stref czasowych, które obsługują reguły dostosowania, przejście do i od czasu letniego tworzy dwa rodzaje nietypowego czasu: nieprawidłowe czasy i niejednoznaczne czasy. Nieprawidłowy czas to nieistniejąca godzina utworzona przez przejście od czasu standardowego do czasu letniego. Na przykład, jeśli to przejście występuje w określonym dniu o godzinie 2:00 i powoduje, że czas zmiany na 3:00 rano, każdy odstęp czasu między 2:00 rano i 2:59:99 rano jest nieprawidłowy. Niejednoznaczny czas to czas, który można mapować do dwóch różnych razy w pojedynczej strefie czasowej. Jest on tworzony przez przejście od czasu letniego do czasu standardowego. Na przykład, jeśli to przejście występuje w określonym dniu o godzinie 2:00 i powoduje, że czas zmiany na 1:00 rano, każdy odstęp czasu między 1:00 rano i 1:59:99 rano mogą być interpretowane jako czas standardowy lub czas letni.

## <a name="time-zone-terminology"></a>Terminologia strefy czasowej

W poniższej tabeli opisano terminy często używane podczas pracy z strefami czasowymi i opracowywanie aplikacji obsługujących strefy czasowe.

| Termin            | Definicja |
| --------------- | ---------- |
| Reguła korekty | Reguła określająca, kiedy następuje przejście od czasu standardowego do czasu letniego i z powrotem z czasu letniego na czas standardowy. Każda reguła korekty ma datę początkową i końcową, która określa, kiedy reguła jest stosowana (na przykład Reguła korekty jest stosowana od 1 stycznia 1986 do 31 grudnia 2006), a także różnic (czasu, przez jaki czas standardowy zmienia się w wyniku zastosowania Reguła e korekty) oraz informacje o określonej dacie i godzinie, kiedy przejścia mają być wykonywane w okresie korekty. Przejścia mogą być zgodne z ustaloną lub określoną regułą. |
| Niejednoznaczny czas  | Czas, który można mapować do dwóch różnych razy w jednej strefie czasowej. Występuje, gdy czas zegara jest dostosowywany do tyłu, na przykład podczas przejścia od czasu letniego strefy czasowej do czasu standardowego. Na przykład, jeśli to przejście występuje w określonym dniu o godzinie 2:00 i powoduje, że czas zmiany na 1:00 rano, każdy odstęp czasu między 1:00 rano i 1:59:99 rano mogą być interpretowane jako czas standardowy lub czas letni. |
| Stała reguła      | Reguła korekty, która ustawia określoną datę przejścia na lub z czasu letniego. Na przykład przejście od czasu letniego do czasu standardowego przypadające w każdym roku w dniu 25 października następuje po ustalonej regule korekty. |
| Reguła zmiennoprzecinkowa   | Reguła korekty, która ustawia konkretny dzień określonego tygodnia w danym miesiącu w przypadku przejścia do lub z czasu letniego. Na przykład przejście od czasu standardowego do czasu letniego, który występuje w trzeciej niedzielę marca, następuje zgodnie z przepływaną regułą dopasowywania. |
| Nieprawidłowy czas    | Nieistniejącego czasu, który jest artefaktem przejścia od czasu standardowego do czasu letniego. Występuje, gdy czas zegara jest dostosowywany do przodu, na przykład podczas przejścia ze standardowego czasu strefy czasowej do czasu letniego. Na przykład, jeśli to przejście występuje w określonym dniu o godzinie 2:00 i powoduje, że czas zmiany na 3:00 rano, każdy odstęp czasu między 2:00 rano i 2:59:99 rano jest nieprawidłowy. |
| Czas przejścia | Informacje o określonej zmianie czasu, takie jak zmiana czasu letniego na czas standardowy lub odwrotnie, w określonej strefie czasowej. |

## <a name="time-zones-and-the-timezoneinfo-class"></a>Strefy czasowe i Klasa TimeZoneInfo

W programie .NET obiekt <xref:System.TimeZoneInfo> reprezentuje strefę czasową. Klasa <xref:System.TimeZoneInfo> zawiera metodę <xref:System.TimeZoneInfo.GetAdjustmentRules%2A>, która zwraca tablicę obiektów <xref:System.TimeZoneInfo.AdjustmentRule>. Każdy element tablicy zawiera informacje o przejściu do i od czasu letniego w określonym przedziale czasu. (W przypadku stref czasowych, które nie obsługują czasu letniego, metoda zwraca pustą tablicę). Każdy obiekt <xref:System.TimeZoneInfo.AdjustmentRule> ma <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionStart%2A> i Właściwość <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionEnd%2A>, która definiuje określoną datę i godzinę przejścia do i od czasu letniego. Właściwość <xref:System.TimeZoneInfo.TransitionTime.IsFixedDateRule%2A> wskazuje, czy zmiana jest stała, czy zmienna.

Platforma .NET opiera się na informacjach o strefie czasowej udostępnianych przez system operacyjny Windows i przechowywanych w rejestrze. Ze względu na liczbę stref czasowych ziemi nie wszystkie istniejące strefy czasowe są reprezentowane w rejestrze. Ponadto, ponieważ rejestr jest strukturą dynamiczną, można do niej dodawać lub usuwać wstępnie zdefiniowane strefy czasowe. Na koniec rejestr nie musi zawierać historycznych danych strefy czasowej. Na przykład w systemie Windows XP Rejestr zawiera dane o pojedynczym zestawie korekt strefy czasowej. System Windows Vista obsługuje dynamiczne dane strefy czasowej, co oznacza, że pojedyncza strefa czasowa może mieć wiele reguł korekty, które są stosowane do określonych interwałów lat. Jednak większość stref czasowych, które są zdefiniowane w rejestrze systemu Windows Vista i obsługują czas letni, ma tylko jedną lub dwie wstępnie zdefiniowane reguły korekty.

Zależność klasy <xref:System.TimeZoneInfo> w rejestrze oznacza, że aplikacja obsługująca strefy czasowej nie może mieć pewności, że określona strefa czasowa jest zdefiniowana w rejestrze. W związku z tym próba utworzenia wystąpienia określonej strefy czasowej (innej niż lokalna strefa czasowa lub strefa czasowa reprezentująca czas UTC) powinna korzystać z obsługi wyjątków. Należy również udostępnić pewne metody zezwalania aplikacji na kontynuowanie, jeśli nie można utworzyć wystąpienia wymaganego obiektu <xref:System.TimeZoneInfo> z rejestru.

W celu obsługi braku wymaganej strefy czasowej Klasa <xref:System.TimeZoneInfo> obejmuje metodę <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>, za pomocą której można tworzyć niestandardowe strefy czasowe, które nie znajdują się w rejestrze. Aby uzyskać szczegółowe informacje na temat tworzenia niestandardowej strefy czasowej, zobacz [jak: Tworzenie stref czasowych bez reguł korygowania](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) i [instrukcje: Tworzenie stref czasowych przy użyciu reguł korygowania](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md). Ponadto można użyć metody <xref:System.TimeZoneInfo.ToSerializedString%2A>, aby przekonwertować nowo utworzoną strefę czasową na ciąg i zapisać ją w magazynie danych (na przykład baza danych, plik tekstowy, rejestr lub zasób aplikacji). Następnie można użyć metody <xref:System.TimeZoneInfo.FromSerializedString%2A>, aby przekonwertować ten ciąg z powrotem do <xref:System.TimeZoneInfo> obiektu. Aby uzyskać szczegółowe informacje, zobacz [jak: zapisywanie stref czasowych w zasobie osadzonym](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) i [instrukcje: przywracanie stref czasowych z zasobu osadzonego](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md).

Ponieważ każda strefa czasowa jest określana przez przesunięcie bazowe od czasu UTC, a także przesunięcie od czasu UTC, które odzwierciedla wszelkie istniejące reguły korekty, czas w jednej strefie czasowej może być łatwo konwertowany na godzinę w innej strefie czasowej. W tym celu obiekt <xref:System.TimeZoneInfo> zawiera kilka metod konwersji, w tym:

- <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>, która konwertuje czas UTC na godzinę w określonej strefie czasowej.

- <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A>, która konwertuje godzinę w określonej strefie czasowej na czas UTC.

- <xref:System.TimeZoneInfo.ConvertTime%2A>, która konwertuje czas w jednej określonej strefie czasowej na godzinę w innej wyznaczeniu strefy czasowej.

- <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>, który używa identyfikatorów strefy czasowej (zamiast obiektów <xref:System.TimeZoneInfo>) jako parametrów do konwersji czasu w jednej określonej strefie czasowej na godzinę w innej wyznaczeniej strefie czasowej.

Aby uzyskać szczegółowe informacje o konwertowaniu czasu między strefami czasowymi, zobacz [konwertowanie czasów między strefami czasowymi](../../../docs/standard/datetime/converting-between-time-zones.md).

## <a name="see-also"></a>Zobacz także

- [Daty, godziny i strefy czasowe](../../../docs/standard/datetime/index.md)
