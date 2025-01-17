---
title: Wybieranie między tradycyjnymi aplikacjami internetowymi i aplikacjami jednostronicowymi
description: Dowiedz się, jak wybierać między tradycyjnymi aplikacjami sieci Web i aplikacjami jednostronicowymi (aplikacji jednostronicowych) podczas kompilowania aplikacji sieci Web.
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 9ede64249705aba3f22a9663b8a258e41f030aca
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73739457"
---
# <a name="choose-between-traditional-web-apps-and-single-page-apps-spas"></a>Wybór między tradycyjnymi Web Apps i aplikacjami jednostronicowymi (aplikacji jednostronicowych)

> "Atwoodeme: Każda aplikacja, którą można napisać w języku JavaScript, zostanie ostatecznie zapisywana w języku JavaScript".  
> _\- Jan Atwoodem_

Obecnie istnieją dwa ogólne podejścia do tworzenia aplikacji sieci Web: tradycyjne aplikacje sieci Web, które wykonują większość logiki aplikacji na serwerze i aplikacje jednostronicowe (aplikacji jednostronicowych), które wykonują większość logiki interfejsu użytkownika w przeglądarce internetowej. Komunikacja z serwerem sieci Web polega głównie na użyciu interfejsów API sieci Web. Podejście hybrydowe jest również możliwe, najprostszym hostem co najmniej jednej aplikacji podrzędnej, podobnej do SPA, w ramach większej tradycyjnej aplikacji sieci Web.

Należy używać tradycyjnych aplikacji sieci Web, gdy:

- Wymagania po stronie klienta aplikacji są proste lub nawet tylko do odczytu.

- Aplikacja musi działać w przeglądarkach bez obsługi języka JavaScript.

- Twój zespół nie zna technik programowania JavaScript i języka TypeScript.

Należy użyć SPA, gdy:

- Aplikacja musi uwidocznić rozbudowany interfejs użytkownika z wieloma funkcjami.

- Zespół jest zaznajomiony z programowaniem kodu JavaScript i/lub języka TypeScript.

- Aplikacja musi już uwidocznić interfejs API dla innych klientów (wewnętrznych lub publicznych).

Ponadto struktury SPA wymagają większej wiedzy o architekturze i zabezpieczeniach. Są one większe, ze względu na częste aktualizacje i nowe platformy niż tradycyjne aplikacje sieci Web. Konfigurowanie zautomatyzowanych procesów kompilacji i wdrażania oraz korzystanie z opcji wdrażania, takich jak kontenery, są trudniejsze w przypadku aplikacji SPA niż tradycyjne aplikacje sieci Web.

Ulepszenia środowiska użytkownika wykonywane przez model SPA muszą zostać odważone względem tych zagadnień.

## <a name="blazor"></a>Blazor

ASP.NET Core 3,0 wprowadza nowy model umożliwiający tworzenie rozbudowanego, interaktywnego i składającego się interfejsu użytkownika o nazwie Blazor. Po stronie serwera Blazor umożliwiają deweloperom tworzenie interfejsu użytkownika przy użyciu Razor na serwerze i dla tego kodu do dostarczenia do przeglądarki i wykonywanie po stronie klienta przy użyciu [zestawu webassembly](https://webassembly.org/). ASP.NET Core 3,0 nadal jest w fazie opracowywania, ale powinno się oczekiwać, że więcej informacji na temat tej technologii znajduje się w aktualizacji 3,0 do tej książki elektronicznej. Aby uzyskać więcej informacji na temat Blazor, zobacz [Rozpoczynanie pracy z Blazor](https://blazor.net/docs/get-started.html).

## <a name="when-to-choose-traditional-web-apps"></a>Kiedy należy wybrać tradycyjne aplikacje sieci Web

Poniżej znajduje się bardziej szczegółowy opis przedstawionych wcześniej powodów dotyczących wybierania tradycyjnych aplikacji sieci Web.

**Twoja aplikacja ma proste, prawdopodobnie tylko do odczytu wymagania po stronie klienta**

Wiele aplikacji sieci Web jest używanych głównie w sposób tylko do odczytu przez ogromną większość użytkowników. Aplikacje tylko do odczytu (lub do odczytu) są znacznie prostsze niż te, które utrzymują i manipulują dużą ilością. Na przykład aparat wyszukiwania może składać się z jednego punktu wejścia z polem tekstowym i drugą stroną do wyświetlania wyników wyszukiwania. Anonimowi użytkownicy mogą łatwo wprowadzać żądania i nie ma potrzeby dla logiki po stronie klienta. Podobnie aplikacja publiczna lub publiczny systemu zarządzania zawartością zwykle składa się głównie z zawartości z małym zachowaniem po stronie klienta. Takie aplikacje można łatwo utworzyć jako tradycyjne aplikacje sieci Web oparte na serwerze, które wykonują logikę na serwerze sieci Web i Renderuj HTML do wyświetlania w przeglądarce. Oznacza to, że każda unikatowa Strona witryny ma własny adres URL, który może być oznaczony zakładką i indeksowany przez aparaty wyszukiwania (domyślnie bez konieczności dodawania go jako osobnej funkcji aplikacji) również w takich scenariuszach.

**Aplikacja musi działać w przeglądarkach bez obsługi języka JavaScript**

Aplikacje sieci Web, które muszą działać w przeglądarkach z ograniczoną lub nie obsługą języka JavaScript, powinny być zapisywane przy użyciu tradycyjnych przepływów pracy aplikacji sieci Web (lub co najmniej może powracać do takiego zachowania). Aplikacji jednostronicowych wymaga, aby kod JavaScript po stronie klienta działał; Jeśli nie jest on dostępny, aplikacji jednostronicowych nie jest dobrym rozwiązaniem.

**Twój zespół nie zna technik programowania JavaScript i języka TypeScript**

Jeśli Twój zespół nie zna języka JavaScript lub TypeScript, ale jest zaznajomiony z programowaniem aplikacji sieci Web po stronie serwera, to prawdopodobnie będzie możliwe szybsze dostarczanie tradycyjnej aplikacji sieci Web niż SPA. O ile nie jest wymagane uczenie się programu aplikacji jednostronicowych lub środowisko użytkownika zapewniane przez SPA, tradycyjne aplikacje sieci Web to bardziej wydajny wybór dla zespołów, które już znają ich Kompilowanie.

## <a name="when-to-choose-spas"></a>Kiedy należy wybrać aplikacji jednostronicowych

Poniżej znajduje się bardziej szczegółowy opis sytuacji, w której można wybrać styl aplikacji jednostronicowej dla aplikacji sieci Web.

**Aplikacja musi uwidaczniać rozbudowany interfejs użytkownika z wieloma funkcjami**

Aplikacji jednostronicowych może obsługiwać rozbudowane funkcje po stronie klienta, które nie wymagają ponownego załadowania strony, ponieważ użytkownicy podejmują działania lub Przechodź między obszarami aplikacji. Aplikacji jednostronicowych może szybciej ładować, pobierać dane w tle, a akcje poszczególnych użytkowników są większe, ponieważ pełne obciążenia stron są rzadkie. Aplikacji jednostronicowych może obsługiwać aktualizacje przyrostowe, zapisując częściowo zakończone formularze lub dokumenty bez konieczności klikania przycisku w celu przesłania formularza. Aplikacji jednostronicowych może obsługiwać rozbudowane zachowania po stronie klienta, na przykład przeciąganie i upuszczanie, znacznie łatwiejsze niż tradycyjne aplikacje. Aplikacji jednostronicowych może być zaprojektowana tak, aby działała w trybie rozłączenia, po wprowadzeniu aktualizacji do modelu po stronie klienta, które zostały ostatecznie zsynchronizowane z serwerem po ponownym nawiązaniu połączenia. Jeśli wymagania dotyczące aplikacji zawierają rozbudowane funkcje, które wykraczają poza typowe oferty formularzy HTML, należy wybrać aplikację w stylu SPA.

Należy pamiętać, że często aplikacji jednostronicowych muszą implementować funkcje, które są wbudowane w tradycyjne aplikacje sieci Web, takie jak wyświetlanie zrozumiałego adresu URL na pasku adresu odzwierciedlające bieżącą operację (i Umożliwianie użytkownikom zakładek lub głębokiego linku do tego adresu URL w celu powrotu do niego). Aplikacji jednostronicowych powinien również zezwalać użytkownikom na używanie przycisków Wstecz i do przodu przeglądarki z wynikami, które nie są w ich przypadku niewidoczne.

**Twój zespół zna język JavaScript i/lub programowanie TypeScript**

Pisanie aplikacji jednostronicowych wymaga znajomości języka JavaScript i/lub technik programowania po stronie klienta i bibliotek. Zespół powinien być kompetentny do pisania nowoczesnego kodu JavaScript przy użyciu struktury SPA, takiej jak kątowy.

> ### <a name="references--spa-frameworks"></a>References — platformy SPA
>
> - **Angular**  
>   <https://angular.io>
> - **Porównanie struktur języka JavaScript**  
>   <https://jsreport.io/the-ultimate-guide-to-javascript-frameworks/>

**Aplikacja musi już udostępnić interfejs API innym (wewnętrznym lub publicznym) klientom**

Jeśli obsługujesz już internetowy interfejs API do użytku przez innych klientów, może być konieczne mniejsze nakłady pracy w celu utworzenia implementacji SPA, która wykorzystuje te interfejsy API zamiast odtwarzania logiki w formularzu po stronie serwera. Aplikacji jednostronicowych wykonywać wiele interfejsów API sieci Web, aby wysyłać zapytania i aktualizować dane, gdy użytkownicy współpracują z aplikacją.

## <a name="decision-table--traditional-web-or-spa"></a>Tabela decyzyjna — tradycyjne sieci Web lub SPA

Poniższa tabela decyzji podsumowuje niektóre podstawowe czynniki, które należy wziąć pod uwagę podczas wybierania między tradycyjną aplikacją sieci Web a SPA.

| **1U**                                           | **Tradycyjna aplikacja internetowa** | **Aplikacja jednostronicowa** |
| ---------------------------------------------------- | ----------------------- | --------------------------- |
| Wymagana znajomość zespołu w języku JavaScript/TypeScript | **Mniejsze**             | **Wymagane**                |
| Obsługa przeglądarek bez obsługi skryptów                   | **Obsługiwał**           | **Nieobsługiwane**           |
| Minimalne zachowanie aplikacji po stronie klienta             | **Dobrze dopasowane**         | **Zbyt obszerne**                |
| Zaawansowane wymagania dotyczące interfejsu użytkownika            | **Separator**             | **Dobrze dopasowane**             |

>[!div class="step-by-step"]
>[Poprzedni](modern-web-applications-characteristics.md)
>[dalej](architectural-principles.md)
