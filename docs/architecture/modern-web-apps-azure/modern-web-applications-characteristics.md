---
title: Charakterystyka nowoczesnych aplikacji internetowych
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Charakterystyki nowoczesnych aplikacji sieci Web
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: d3848f3b0cf993930bfc3801ce40c5eac30f094d
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2019
ms.locfileid: "70374087"
---
# <a name="characteristics-of-modern-web-applications"></a>Charakterystyki nowoczesnych aplikacji sieci Web

> "… przy odpowiednim projekcie funkcje są tanie. To podejście jest uciążliwy, ale nadal kończy się powodzeniem ".  
> _\-Dennis Ritchie_

Nowoczesne aplikacje sieci Web mają wyższy poziom oczekiwań użytkowników i większe wymagania niż kiedykolwiek wcześniej. Oczekuje się, że dzisiejsze aplikacje sieci Web będą dostępne 24/7 z dowolnego miejsca na świecie i mogą być używane praktycznie dla każdego urządzenia lub rozmiaru ekranu. Aplikacje sieci Web muszą być bezpieczne, elastyczne i skalowalne, aby sprostać wzrostom popytu. Coraz bardziej złożone scenariusze powinny być obsługiwane przez bogate środowiska użytkownika, które są tworzone na kliencie przy użyciu języka JavaScript, i wydajnie komunikują się za pośrednictwem interfejsów API sieci Web.

ASP.NET Core jest zoptymalizowany pod kątem nowoczesnych aplikacji internetowych i scenariuszy hostingu opartych na chmurze. Jego Modularna konstrukcja umożliwia aplikacjom zależą tylko te funkcje, które faktycznie używają, podnoszenie poziomu zabezpieczeń i wydajności aplikacji przy jednoczesnym zmniejszeniu wymagań dotyczących zasobów hostingu.

## <a name="reference-application-eshoponweb"></a>Aplikacja referencyjna: eShopOnWeb

Te wskazówki obejmują aplikację referencyjną _eShopOnWeb_, która pokazuje niektóre z zasad i zaleceń. Aplikacja jest prostym sklepem online, który obsługuje przeglądanie katalogów koszul, kawy mugs i innych elementów marketingowych. Aplikacja referencyjna jest świadomie prosta, aby ułatwić jej zrozumienie.

![eShopOnWeb](./media/image2-1.png)

**Rysunek 2-1.** eShopOnWeb

> ### <a name="reference-application"></a>Aplikacja referencyjna
>
> - **eShopOnWeb**  
>   <https://github.com/dotnet/eShopOnWeb>

## <a name="cloud-hosted-and-scalable"></a>Hostowane w chmurze i skalowalne

ASP.NET Core jest zoptymalizowany dla chmury (chmura publiczna, Chmura prywatna, dowolna chmura), ponieważ ma małą ilość pamięci i wysoką przepływność. Mniejsza część aplikacji ASP.NET Core oznacza, że możesz obsługiwać więcej z nich na tym samym sprzęcie i płacisz za mniejszą liczbę zasobów przy korzystaniu z usług hostingu zgodnie z rzeczywistym użyciem. Wyższa przepływność polega na tym, że można obsłużyć większą liczbę klientów z aplikacji przy użyciu tego samego sprzętu, co jeszcze bardziej zmniejsza konieczność inwestowania w serwery i infrastrukturę hostingu.

## <a name="cross-platform"></a>Wiele platform

ASP.NET Core to platforma międzyplatformowa i może działać w systemach Linux, macOS i Windows. Spowoduje to otwarcie wielu nowych opcji związanych z tworzeniem i wdrażaniem aplikacji skompilowanych za pomocą ASP.NET Core. Kontenery platformy Docker — zarówno Linux, jak i Windows — mogą hostować ASP.NET Core aplikacje, umożliwiając im korzystanie z zalet [kontenerów i mikrousług](../microservices/index.md).

## <a name="modular-and-loosely-coupled"></a>Modularna i luźno sprzężona

Pakiety NuGet są członkami pierwszej klasy w oprogramowaniu .NET Core, a ASP.NET Core aplikacje składają się z wielu bibliotek za poorednictwem narzędzia NuGet. Ten stopień szczegółowości funkcjonalności pomaga zapewnić, że aplikacje są zależne od tych, które są wymagane, i które z nich korzystają, zmniejszając powierzchnię obszaru powierzchnia i luki w zabezpieczeniach.

ASP.NET Core również w pełni obsługuje [iniekcję zależności](https://deviq.com/dependency-injection/), zarówno wewnętrznie, jak i na poziomie aplikacji. Interfejsy mogą mieć wiele implementacji, które mogą być wymieniane w razie konieczności. Iniekcja zależności umożliwia aplikacjom swobodne dołączenie do tych interfejsów, a nie konkretnych implementacji, ułatwiając ich rozbudowanie, konserwację i testowanie.

## <a name="easily-tested-with-automated-tests"></a>Łatwe testowanie przy użyciu testów automatycznych

Aplikacje ASP.NET Core obsługują testy jednostkowe, a ich luźny sprzężenie i obsługa iniekcji zależności ułatwiają wymianę problemów z infrastrukturą przy użyciu fałszywych implementacji do celów testowych. ASP.NET Core dostarcza również TestServer, których można używać do hostowania aplikacji w pamięci. Testy funkcjonalne mogą następnie wprowadzać żądania do tego serwera znajdującego się w pamięci, wykonując pełny stos aplikacji (w tym oprogramowanie pośredniczące, routing, powiązanie modelu, filtry itp.) i uzyskując odpowiedź, a wszystko to w części czasu, w którym zajmie się hostem aplikacji na rzeczywistym serwerze i wykonaj żądania przez warstwę sieciową. Te testy są szczególnie łatwe do zapisu i cenne dla interfejsów API, które są coraz ważniejsze w nowoczesnych aplikacjach sieci Web.

## <a name="traditional-and-spa-behaviors-supported"></a>Obsługiwane zachowania tradycyjne i SPA

Tradycyjne aplikacje sieci Web mają niewielkie zachowanie po stronie klienta, ale zamiast tego na serwerze są wykorzystywane wszystkie nawigowanie, zapytania i aktualizacje, które mogą być wymagane przez aplikację. Każda nowa Operacja wykonywana przez użytkownika zostanie przetłumaczona na nowe żądanie sieci Web, a wynikiem jest pełna ponowna załadowanie strony w przeglądarce użytkownika końcowego. Klasyczne platformy typu Model-View-Controller (MVC) zwykle postępują zgodnie z tą metodą, przy czym każde nowe żądanie odpowiadające innej akcji kontrolera, która z kolei będzie współpracować z modelem i zwracać widok. Niektóre poszczególne operacje na danej stronie można rozszerzyć przy użyciu funkcji AJAX (asynchroniczne skrypty JavaScript i XML), ale ogólna architektura aplikacji używała wielu różnych widoków MVC i punktów końcowych adresów URL. Ponadto ASP.NET Core MVC obsługuje również Razor Pages, prostszy sposób organizowania stron w stylu MVC.

Aplikacje jednostronicowe (aplikacji jednostronicowych) z kolei obejmują bardzo kilka dynamicznie generowanych obciążeń stron po stronie serwera (jeśli istnieją). Wiele aplikacji jednostronicowych jest inicjowanych w statycznym pliku HTML, który ładuje niezbędne biblioteki JavaScript do uruchamiania i uruchamiania aplikacji. Aplikacje te sprawiają duże wykorzystanie interfejsów API sieci Web na potrzeby swoich potrzeb dotyczących danych i zapewniają znacznie bogatsze środowiska użytkownika.

Wiele aplikacji sieci Web obejmuje połączenie tradycyjnego zachowania aplikacji sieci Web (zazwyczaj dla zawartości) i aplikacji jednostronicowych (w przypadku interakcji z interakcją). ASP.NET Core obsługuje zarówno MVC (widoki, oparte na stronach), jak i interfejsy API sieci Web w tej samej aplikacji, przy użyciu tego samego zestawu narzędzi i odpowiednich bibliotek struktury.

## <a name="simple-development-and-deployment"></a>Proste programowanie i wdrażanie

Aplikacje ASP.NET Core mogą być zapisywane przy użyciu prostych edytorów tekstu i interfejsów wiersza polecenia lub w pełni funkcjonalnych środowisk programistycznych, takich jak Visual Studio. Aplikacje monolityczne są zwykle wdrażane w jednym punkcie końcowym. Wdrożenia mogą być łatwo zautomatyzowane w ramach potoku ciągłej integracji i ciągłego dostarczania (CD). Oprócz tradycyjnych narzędzi ciągłej integracji/ciągłego wdrażania, platforma Microsoft Azure oferuje zintegrowaną obsługę repozytoriów Git i umożliwia automatyczne wdrażanie aktualizacji w miarę ich tworzenia w określonej gałęzi lub tagu usługi git.

## <a name="traditional-aspnet-and-web-forms"></a>Tradycyjne ASP.NET i formularze sieci Web

Oprócz ASP.NET Core, tradycyjne ASP.NET 4. x nadal są niezawodną i niezawodną platformą do tworzenia aplikacji sieci Web. ASP.NET obsługuje modele programistyczne MVC i Web API, a także formularze sieci Web, które są dobrze dostosowane do programowania aplikacji opartych na stronach i oferuje bogaty ekosystem składników innych firm. System Windows Azure oferuje doskonałą od dawna dbaą obsługę aplikacji ASP.NET 4. x i wielu programistów zna tę platformę.

> ### <a name="references--modern-web-applications"></a>Odwołania — nowoczesne aplikacje sieci Web
>
> - **Wprowadzenie do platformy ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/>
> - **Sześć najważniejszych korzyści ASP.NET Core, które różnią się i lepiej**  
>   <https://blog.trigent.com/six-key-benefits-of-asp-net-core-1-0-which-make-it-different-better/>
> - **Testowanie w ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/testing/>

>[!div class="step-by-step"]
>[Poprzedni](index.md)Następny
>[](choose-between-traditional-web-and-single-page-apps.md)
