---
title: Tworzenie złożonego interfejsu użytkownika opartego na mikrousługach
description: Architektura mikrousług nie tylko dla zaplecza. Uzyskaj wgląd w widok, który będzie używany w frontonie.
ms.date: 09/20/2018
ms.openlocfilehash: 1861d3bb6e5d4a0226aa8f3f72a2e0d3e83be56f
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275744"
---
# <a name="creating-composite-ui-based-on-microservices"></a>Tworzenie złożonego interfejsu użytkownika opartego na mikrousługach

Architektura mikrousług często zaczyna się od danych i logiki obsługi po stronie serwera, ale w wielu przypadkach interfejs użytkownika jest nadal obsługiwany jako monolitu. Jednak bardziej zaawansowane podejście o nazwie [Micro frontonów](https://martinfowler.com/articles/micro-frontends.html)polega na zaprojektowaniu interfejsu użytkownika aplikacji na podstawie mikrousług. Oznacza to posiadanie złożonego interfejsu użytkownika utworzonego przez mikrousługi, a nie za pomocą mikrousług na serwerze i tylko monolitycznej aplikacji klienckiej, która korzysta z mikrousług. Dzięki tej metodzie kompilacje mikrousług można zakończyć przy użyciu zarówno logiki, jak i wizualnej reprezentacji.

Rysunek 4-20 przedstawia prostsze podejście do korzystania z mikrousług z monolitycznej aplikacji klienckiej. Oczywiście może istnieć usługa ASP.NET MVC między wytwarzaniem kodu HTML i JavaScript. Na rysunku przedstawiono uproszczenie, które oznacza, że masz pojedynczy (monolityczny) interfejs użytkownika, który korzysta z mikrousług, które koncentrują się na logice i danych, a nie w kształcie interfejsu użytkownika (HTML i JavaScript).

![Diagram monolitycznej aplikacji interfejsu użytkownika łączącej się z mikrousługami.](./media/microservice-based-composite-ui-shape-layout/monolith-ui-consume-microservices.png)

**Rysunek 4-20**. Aplikacja monolitycznego interfejsu użytkownika wykorzystująca mikrousługi zaplecza

W przeciwieństwie do złożonego interfejsu użytkownika jest precyzyjnie generowany i składający się z mikrousług. Niektóre mikrousługi mają kształt wizualizacji określonych obszarów interfejsu użytkownika. Zasadniczą różnicą jest to, że masz składniki interfejsu użytkownika klienta (na przykład klasy TypeScript) oparte na szablonach, a ViewModel do kształtowania dla tych szablonów pochodzą z każdej mikrousługi.

W czasie uruchamiania aplikacji klienckiej każdy składnik interfejsu użytkownika klienta (na przykład klasy TypeScript) rejestruje się z mikrousługą infrastruktury, która umożliwia dostarczanie modele widoków w danym scenariuszu. Jeśli mikrousługa zmieni kształt, interfejs użytkownika zmieni się również.

Rysunek 4-21 pokazuje wersję tego podejścia złożonego interfejsu użytkownika. Jest to uproszczone, ponieważ mogą istnieć inne mikrousługi, które agregują części szczegółowe, które są oparte na różnych technikach. Jest to zależne od tego, czy tworzysz tradycyjne podejście sieci Web (ASP.NET MVC) czy SPA (aplikacja jednostronicowa).

![Diagram złożonego interfejsu użytkownika składający się z wielu modeli widoku.](./media/microservice-based-composite-ui-shape-layout/microservice-generate-composite-ui.png)

**Rysunek 4-21**. Przykład złożonej aplikacji interfejsu użytkownika, która jest oparta na mikrousługach zaplecza

Każda z tych mikrousług kompozycji jest podobna do niewielkiej bramy interfejsu API. Jednak w tym przypadku każdy z nich jest odpowiedzialny za niewielki obszar interfejsu użytkownika.

Złożone podejście interfejsu użytkownika, które jest oparte na mikrousługach, może być bardziej trudne lub mniejsze, w zależności od tego, jakie technologie interfejsu użytkownika są używane. Na przykład nie będziesz używać tych samych technik do kompilowania tradycyjnej aplikacji sieci Web, która jest używana do tworzenia SPA lub natywnej aplikacji mobilnej (np. podczas tworzenia aplikacji platformy Xamarin, które mogą być bardziej trudne dla tego podejścia).

Przykładowa aplikacja [eShopOnContainers](https://aka.ms/MicroservicesArchitecture) używa podejścia interfejsu użytkownika monolitycznego z wielu powodów. Po pierwsze jest to wprowadzenie do mikrousług i kontenerów. Złożony interfejs użytkownika jest bardziej zaawansowany, ale wymaga również dalszej złożoności podczas projektowania i opracowywania interfejsu użytkownika. Ponadto eShopOnContainers zapewnia natywną aplikację mobilną opartą na oprogramowaniu Xamarin, która czyni ją bardziej skomplikowaną na kliencie C @ no__t-0.

Zachęcamy jednak do korzystania z następujących odwołań, aby dowiedzieć się więcej na temat złożonego interfejsu użytkownika w oparciu o mikrousługi.

## <a name="additional-resources"></a>Zasoby dodatkowe

- **Micro frontony (blog Martin Fowlera)**  
  <https://martinfowler.com/articles/micro-frontends.html>
  
- **Micro frontony (Michael Geers Site)**  
  <https://micro-frontends.org/>
  
- **Złożony interfejs użytkownika korzystający z ASP.NET (warsztat)**  
  <https://github.com/Particular/Workshop/tree/master/demos/asp-net-core>

- **Ruben Oostinga. Monolityczny fronton w architekturze mikrousług**  
  <https://xebia.com/blog/the-monolithic-frontend-in-the-microservices-architecture/>

- **Mauro Servienti. Wpis tajny lepszej kompozycji interfejsu użytkownika**  
  <https://particular.net/blog/secret-of-better-ui-composition>

- **Viktor Farcic. Dołączanie składników sieci Web frontonu do mikrousług**  
  <https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/>

- **Zarządzanie frontonem w architekturze mikrousług**  
  <https://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html>

>[!div class="step-by-step"]
>[Poprzedni](microservices-addressability-service-registry.md)
>[dalej](resilient-high-availability-microservices.md)
