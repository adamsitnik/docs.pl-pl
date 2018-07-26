---
title: Metody dotyczące architektury — aplikacje niekorzystające z serwera
description: Wprowadzenie do architektury zbliża się do tworzenia aplikacji opartych na chmurze przedsiębiorstwa, z architektury N-warstwowej, aby bez użycia serwera.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: b080e029fb1214ebf4d2717902c3b6d4af06d254
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/03/2018
ms.locfileid: "37404961"
---
# <a name="architecture-approaches"></a><span data-ttu-id="f7681-103">Metody dotyczące architektury</span><span class="sxs-lookup"><span data-stu-id="f7681-103">Architecture approaches</span></span>

<span data-ttu-id="f7681-104">Informacje o istniejących podejścia do projektowania aplikacji dla przedsiębiorstw pomaga wyjaśnienia roli bez użycia serwera.</span><span class="sxs-lookup"><span data-stu-id="f7681-104">Understanding existing approaches to architecting enterprise apps helps clarify the role played by serverless.</span></span> <span data-ttu-id="f7681-105">Istnieje wiele metod i wzorce, które ewoluował za pośrednictwem dekad Wytwarzanie oprogramowania i mieć własne zalety i wady.</span><span class="sxs-lookup"><span data-stu-id="f7681-105">There are many approaches and patterns that evolved over decades of software development, and all have their own pros and cons.</span></span> <span data-ttu-id="f7681-106">W wielu przypadkach ostatecznego rozwiązania nie może obejmować podejmowania decyzji na temat podejścia do jednego, ale mogą integrować kilka metod.</span><span class="sxs-lookup"><span data-stu-id="f7681-106">In many cases, the ultimate solution may not involve deciding on a single approach but may integrate several approaches.</span></span> <span data-ttu-id="f7681-107">Scenariusze migracji często oznaczać między innymi przesunięcie z architektury jednej metody do drugiej za pomocą podejście hybrydowe.</span><span class="sxs-lookup"><span data-stu-id="f7681-107">Migration scenarios often involve shifting from one architecture approach to another through a hybrid approach.</span></span>

<span data-ttu-id="f7681-108">W tym rozdziale omówiono obu wzorców architektury logiczne i fizyczne aplikacji dla przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="f7681-108">This chapter provides an overview of both logical and physical architecture patterns for enterprise applications.</span></span>

## <a name="architecture-patterns"></a><span data-ttu-id="f7681-109">Wzorce architektury</span><span class="sxs-lookup"><span data-stu-id="f7681-109">Architecture patterns</span></span>

<span data-ttu-id="f7681-110">Współczesne aplikacje biznesowe, należy wykonać różne wzorce architektury.</span><span class="sxs-lookup"><span data-stu-id="f7681-110">Modern business applications follow a variety of architecture patterns.</span></span> <span data-ttu-id="f7681-111">W tej sekcji przedstawia przegląd typowych wzorców.</span><span class="sxs-lookup"><span data-stu-id="f7681-111">This section represents a survey of common patterns.</span></span> <span data-ttu-id="f7681-112">Wzorce wymienione w tym miejscu nie są zawsze wszystkie najlepsze rozwiązania, ale pokazują różne podejścia.</span><span class="sxs-lookup"><span data-stu-id="f7681-112">The patterns listed here aren't necessarily all best practices, but illustrate different approaches.</span></span>

<span data-ttu-id="f7681-113">Aby uzyskać więcej informacji, zobacz [przewodnik dotyczący architektury aplikacji platformy Azure](https://docs.microsoft.com/azure/architecture/guide/).</span><span class="sxs-lookup"><span data-stu-id="f7681-113">For more information, see [Azure application architecture guide](https://docs.microsoft.com/azure/architecture/guide/).</span></span>

## <a name="monoliths"></a><span data-ttu-id="f7681-114">Monolitycznych projektów</span><span class="sxs-lookup"><span data-stu-id="f7681-114">Monoliths</span></span>

<span data-ttu-id="f7681-115">Wzorzec monolitu wielu aplikacji biznesowych, postępuj zgodnie z.</span><span class="sxs-lookup"><span data-stu-id="f7681-115">Many business applications follow a monolith pattern.</span></span> <span data-ttu-id="f7681-116">Starsze aplikacje są często implementowane jako monolitycznych projektów.</span><span class="sxs-lookup"><span data-stu-id="f7681-116">Legacy applications are often implemented as monoliths.</span></span> <span data-ttu-id="f7681-117">We wzorcu monolitu wszystkie problemy w aplikacji znajdują się w jednym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="f7681-117">In the monolith pattern, all application concerns are contained in a single deployment.</span></span> <span data-ttu-id="f7681-118">Wszystko — od interfejsu użytkownika do wywołania bazy danych znajduje się w tej samej bazy kodu.</span><span class="sxs-lookup"><span data-stu-id="f7681-118">Everything from user interface to database calls is included in the same codebase.</span></span>

![Architektura monolitu](./media/monolith-architecture.png)

<span data-ttu-id="f7681-120">Ma kilka zalet tego podejścia monolitu.</span><span class="sxs-lookup"><span data-stu-id="f7681-120">There are several advantages to the monolith approach.</span></span> <span data-ttu-id="f7681-121">Często jest łatwo ściągnąć jednej bazy kodu i rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="f7681-121">It's often easy to pull down a single code base and start working.</span></span> <span data-ttu-id="f7681-122">Zwiększania obciążenia czasu może być krótszy, a tworzenie środowisk testowych jest proste i polega na zapewnieniu nowej kopii.</span><span class="sxs-lookup"><span data-stu-id="f7681-122">Ramp up time may be less, and creating test environments is as simple as providing a new copy.</span></span> <span data-ttu-id="f7681-123">Monolityczna mogą być przeznaczone do obejmują wiele składników i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7681-123">The monolith may be designed to include multiple components and applications.</span></span>

<span data-ttu-id="f7681-124">Niestety wzorzec monolitu zwykle podziału na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="f7681-124">Unfortunately, the monolith pattern tends to break down at scale.</span></span> <span data-ttu-id="f7681-125">Główne wady podejścia monolitu obejmują:</span><span class="sxs-lookup"><span data-stu-id="f7681-125">Major disadvantages of the monolith approach include:</span></span>

* <span data-ttu-id="f7681-126">Trudno działać równolegle w tej samej bazy kodu.</span><span class="sxs-lookup"><span data-stu-id="f7681-126">Difficult to work in parallel in the same code base.</span></span>
* <span data-ttu-id="f7681-127">Każda zmiana, niezależnie od tego, jak prosta wymaga wdrażania nowej wersji całej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7681-127">Any change, no matter how trivial, requires deploying a new version of the entire application.</span></span>
* <span data-ttu-id="f7681-128">Refaktoryzacja potencjalnie ma wpływ na całą aplikację.</span><span class="sxs-lookup"><span data-stu-id="f7681-128">Refactoring potentially impacts the entire application.</span></span>
* <span data-ttu-id="f7681-129">Często jest jedynym rozwiązaniem skalowanie do tworzenia wielu kopii monolitu dużej ilości zasobów.</span><span class="sxs-lookup"><span data-stu-id="f7681-129">Often the only solution to scale is to create multiple, resource-intensive copies of the monolith.</span></span>
* <span data-ttu-id="f7681-130">Rozwiń węzeł systemów lub innych systemów drogą kupna, integracji może być trudne.</span><span class="sxs-lookup"><span data-stu-id="f7681-130">As systems expand or other systems are acquired, integration can be difficult.</span></span>
* <span data-ttu-id="f7681-131">Może być trudne do testowania ze względu na konieczność konfigurowania całej monolitu.</span><span class="sxs-lookup"><span data-stu-id="f7681-131">It may be difficult to test due to the need to configure the entire monolith.</span></span>
* <span data-ttu-id="f7681-132">Ponowne wykorzystanie kodu staje się wyzwaniem i często inne aplikacje znajdą się o własne kopie kodu.</span><span class="sxs-lookup"><span data-stu-id="f7681-132">Code reuse is challenging and often other apps end up having their own copies of code.</span></span>

<span data-ttu-id="f7681-133">Wiele firm wyszukiwania w chmurze jako okazję do migrowania aplikacji monolitu i Refaktoryzuj je w tym samym czasie na więcej wzorców można używać.</span><span class="sxs-lookup"><span data-stu-id="f7681-133">Many businesses look to the cloud as an opportunity to migrate monolith applications and at the same time refactor them to more usable patterns.</span></span> <span data-ttu-id="f7681-134">Są często umożliwiające rozbicie poszczególnych aplikacji i składników, aby mogła być utrzymywane, wdrożyć i skalować oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="f7681-134">It's common to break out the individual applications and components to allow them to be maintained, deployed, and scaled separately.</span></span>

## <a name="n-layer-applications"></a><span data-ttu-id="f7681-135">N warstwy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7681-135">N-Layer applications</span></span>

<span data-ttu-id="f7681-136">Aplikacja N-warstwy logiki aplikacji partycji do określonej warstwy.</span><span class="sxs-lookup"><span data-stu-id="f7681-136">N-layer application partition application logic into specific layers.</span></span> <span data-ttu-id="f7681-137">Najbardziej typowe warstwy obejmują:</span><span class="sxs-lookup"><span data-stu-id="f7681-137">The most common layers include:</span></span>

* <span data-ttu-id="f7681-138">Interfejs użytkownika</span><span class="sxs-lookup"><span data-stu-id="f7681-138">User interface</span></span>
* <span data-ttu-id="f7681-139">Logika biznesowa</span><span class="sxs-lookup"><span data-stu-id="f7681-139">Business logic</span></span>
* <span data-ttu-id="f7681-140">Dostęp do danych</span><span class="sxs-lookup"><span data-stu-id="f7681-140">Data access</span></span>

<span data-ttu-id="f7681-141">Inne warstwy mogą obejmować oprogramowanie pośredniczące, przetwarzanie wsadowe i interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f7681-141">Other layers may include middleware, batch processing, and API.</span></span> <span data-ttu-id="f7681-142">Należy zauważyć, że warstwy logiczne.</span><span class="sxs-lookup"><span data-stu-id="f7681-142">It's important to note the layers are logical.</span></span> <span data-ttu-id="f7681-143">Mimo że są one tworzone w izolacji, ich wszystkich można wdrażać na tej samej platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="f7681-143">Although they're developed in isolation, they may all be deployed to the same target platform.</span></span>

![Architektura N-warstwy](./media/n-layer-architecture.png)

<span data-ttu-id="f7681-145">Ma kilka zalet podejście N warstwy, w tym:</span><span class="sxs-lookup"><span data-stu-id="f7681-145">There are several advantages to the N-Layer approach, including:</span></span>

* <span data-ttu-id="f7681-146">Refaktoryzacja jest izolowane do warstwy.</span><span class="sxs-lookup"><span data-stu-id="f7681-146">Refactoring is isolated to a layer.</span></span>
* <span data-ttu-id="f7681-147">Zespoły mogą niezależnie tworzenie, testowanie, wdrażanie i obsługa oddzielnych warstw.</span><span class="sxs-lookup"><span data-stu-id="f7681-147">Teams can independently build, test, deploy, and maintain separate layers.</span></span>
* <span data-ttu-id="f7681-148">Odpowiedniki warstwy, na przykład warstwa danych mogą uzyskiwać dostęp do wielu baz danych bez konieczności wprowadzania zmian w warstwie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7681-148">Layers can be swapped out, for example the data layer may access multiple databases without requiring changes to the UI layer.</span></span>

<span data-ttu-id="f7681-149">Aplikacje niewymagające użycia serwera może służyć do zaimplementować jedną lub więcej warstw.</span><span class="sxs-lookup"><span data-stu-id="f7681-149">Serverless may be used to implement one or more layers.</span></span>

## <a name="microservices"></a><span data-ttu-id="f7681-150">Mikrousługi</span><span class="sxs-lookup"><span data-stu-id="f7681-150">Microservices</span></span>

<span data-ttu-id="f7681-151">**[Mikrousługi](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)**  architektury zawiera typowe cechy, które obejmują:</span><span class="sxs-lookup"><span data-stu-id="f7681-151">**[Microservices](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)** architectures contain common characteristics that include:</span></span>

* <span data-ttu-id="f7681-152">Aplikacje składają się z kilku małych usług.</span><span class="sxs-lookup"><span data-stu-id="f7681-152">Applications are composed of several small services.</span></span>
* <span data-ttu-id="f7681-153">Każda usługa jest uruchamiana we własnym procesie.</span><span class="sxs-lookup"><span data-stu-id="f7681-153">Each service runs in its own process.</span></span>
* <span data-ttu-id="f7681-154">Usługi są wyrównane wokół domeny biznesowej.</span><span class="sxs-lookup"><span data-stu-id="f7681-154">Services are aligned around business domains.</span></span>
* <span data-ttu-id="f7681-155">Usługi komunikują się za pośrednictwem interfejsów API uproszczone, zazwyczaj przy użyciu protokołu HTTP jako transportu.</span><span class="sxs-lookup"><span data-stu-id="f7681-155">Services communicate over lightweight APIs, typically using HTTP as the transport.</span></span>
* <span data-ttu-id="f7681-156">Usługi można wdrożyć i uaktualniane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="f7681-156">Services can be deployed and upgraded independently.</span></span>
* <span data-ttu-id="f7681-157">Usługi nie są zależne od pojedynczym magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="f7681-157">Services aren't dependent on a single data store.</span></span>
* <span data-ttu-id="f7681-158">System został zaprojektowany z błędem, pamiętając, a aplikacja może nadal działać, nawet wtedy, gdy niektóre usługi nie.</span><span class="sxs-lookup"><span data-stu-id="f7681-158">The system is designed with failure in mind, and the app may still run even when certain services fail.</span></span>

<span data-ttu-id="f7681-159">Mikrousługi nie muszą być wzajemnego do innych metod architektury.</span><span class="sxs-lookup"><span data-stu-id="f7681-159">Microservices don't have to be mutual to other architecture approaches.</span></span> <span data-ttu-id="f7681-160">Na przykład architektury N-warstwowej, może używać mikrousług dla warstwy środkowej.</span><span class="sxs-lookup"><span data-stu-id="f7681-160">For example, an N-Tier architecture may use microservices for the middle tier.</span></span> <span data-ttu-id="f7681-161">Istnieje również możliwość mikrousługi w na różne sposoby, z katalogów wirtualnych na hostach usług IIS do kontenerów.</span><span class="sxs-lookup"><span data-stu-id="f7681-161">It's also possible to implement microservices in a variety of ways, from virtual directories on IIS hosts to containers.</span></span> <span data-ttu-id="f7681-162">Cechy mikrousług były szczególnie idealne rozwiązanie w przypadku implementacji bez użycia serwera.</span><span class="sxs-lookup"><span data-stu-id="f7681-162">The characteristics of microservices make them especially ideal for serverless implementations.</span></span>

![Architektura Mikrousług](./media/microservices-architecture.png)

<span data-ttu-id="f7681-164">Zalety architektury mikrousług obejmują:</span><span class="sxs-lookup"><span data-stu-id="f7681-164">The pros of microservices architectures include:</span></span>

* <span data-ttu-id="f7681-165">Refaktoryzacja często jest izolowane do jednej usługi.</span><span class="sxs-lookup"><span data-stu-id="f7681-165">Refactoring is often isolated to a single service.</span></span>
* <span data-ttu-id="f7681-166">Usługi można uaktualnić niezależnie od siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="f7681-166">Services can be upgraded independently of each other.</span></span>
* <span data-ttu-id="f7681-167">Elastyczność i elastyczność, mogą być dostosowane do wymagań poszczególnych usług.</span><span class="sxs-lookup"><span data-stu-id="f7681-167">Resiliency and elasticity can be tuned to the demands of individual services.</span></span>
* <span data-ttu-id="f7681-168">Programowanie może się zdarzyć w sposób równoległy między różnymi zespołami i platform.</span><span class="sxs-lookup"><span data-stu-id="f7681-168">Development can happen in parallel across disparate teams and platforms.</span></span>
* <span data-ttu-id="f7681-169">Łatwiej można pisać testy kompleksowe usługi izolowanym.</span><span class="sxs-lookup"><span data-stu-id="f7681-169">It's easier to write comprehensive tests for isolated services.</span></span>

<span data-ttu-id="f7681-170">Mikrousługi są dostarczane z własnych wyzwaniom, w tym:</span><span class="sxs-lookup"><span data-stu-id="f7681-170">Microservices come with their own challenges, including:</span></span>

* <span data-ttu-id="f7681-171">Określanie, jakie usługi są dostępne i jak ich wywołania.</span><span class="sxs-lookup"><span data-stu-id="f7681-171">Determining what services are available and how to call them.</span></span>
* <span data-ttu-id="f7681-172">Zarządzanie cyklem życia usługi.</span><span class="sxs-lookup"><span data-stu-id="f7681-172">Managing the lifecycle of services.</span></span>
* <span data-ttu-id="f7681-173">Zrozumienie, jak usługi współdziałają ze sobą cała aplikacja.</span><span class="sxs-lookup"><span data-stu-id="f7681-173">Understanding how services fit together in the overall application.</span></span>
* <span data-ttu-id="f7681-174">Testowanie pełnego wywołań wykonanych dla różnych usług.</span><span class="sxs-lookup"><span data-stu-id="f7681-174">Full system testing of calls made across disparate services.</span></span>

<span data-ttu-id="f7681-175">Ostatecznie są wszystkie te wyzwania związane z tym sięgnięcie do korzyści z bez użycia serwera, które zostały omówione w dalszej części rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="f7681-175">Ultimately there are solutions to address all of these challenges, including tapping into the benefits of serverless that are discussed later.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f7681-176">[Poprzednie](index.md)
[dalej](architecture-deployment-approaches.md)</span><span class="sxs-lookup"><span data-stu-id="f7681-176">[Previous](index.md)
[Next](architecture-deployment-approaches.md)</span></span>