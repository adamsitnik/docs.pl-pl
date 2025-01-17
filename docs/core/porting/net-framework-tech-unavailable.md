---
title: Technologie .NET Framework niedostępne w programie .NET Core
description: Informacje na temat technologii .NET Framework, które są niedostępne w programie .NET Core
author: cartermp
ms.date: 04/30/2019
ms.openlocfilehash: 47f93268c44682afeba87cde17fe9c39811b37bf
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73739709"
---
# <a name="net-framework-technologies-unavailable-on-net-core"></a>Technologie .NET Framework niedostępne w programie .NET Core

Niektóre technologie dostępne dla bibliotek .NET Framework nie są dostępne do użycia z platformą .NET Core, takich jak AppDomains, komunikacja zdalna, zabezpieczenia dostępu kodu (CAS), przezroczystość zabezpieczeń i system. EnterpriseServices. Jeśli biblioteki są zależne od co najmniej jednej z tych technologii, weź pod uwagę alternatywne podejścia opisane poniżej. Aby uzyskać więcej informacji na temat zgodności interfejsów API, zobacz artykuł [podstawowe zmiany w programie .NET Core](../compatibility/breaking-changes.md) .

Tylko ponieważ interfejs API lub technologia nie jest obecnie zaimplementowana, nie oznacza to, że jest celowo nieobsługiwana. Najpierw należy przeszukać repozytoria usługi GitHub dla platformy .NET Core, aby zobaczyć, czy konkretny problem występuje w drodze projektu, ale jeśli nie można znaleźć takiego wskaźnika, należy zgłosić problem z [repozytorium dotnet/corefx](https://github.com/dotnet/corefx/issues) w witrynie GitHub w celu poproszenia o określone interfejsy API i informacyjn. [Żądania przenoszenia w ramach problemów](https://github.com/dotnet/corefx/labels/port-to-core) są oznaczane etykietą `port-to-core`.

## <a name="appdomains"></a>Domen aplikacji

Domeny aplikacji (AppDomains) izolują aplikacje od siebie. Domeny aplikacji wymagają obsługi środowiska uruchomieniowego i są zwykle dość kosztowne. Tworzenie dodatkowych domen aplikacji nie jest obsługiwane. Nie planujemy dodawania tej funkcji w przyszłości. W przypadku izolacji kodu zaleca się oddzielne procesy lub używanie kontenerów jako alternatywy. W przypadku dynamicznego ładowania zestawów zalecamy nową klasę <xref:System.Runtime.Loader.AssemblyLoadContext>.

Aby ułatwić migrację kodu z .NET Framework, platforma .NET Core uwidacznia część <xref:System.AppDomain>j powierzchni interfejsu API. Niektóre z funkcji API działają normalnie (na przykład <xref:System.AppDomain.UnhandledException?displayProperty=nameWithType>), niektórzy członkowie nie wykonują żadnych operacji (na przykład <xref:System.AppDomain.SetCachePath%2A>), a niektóre z nich zgłaszają <xref:System.PlatformNotSupportedException> (na przykład <xref:System.AppDomain.CreateDomain%2A>). Sprawdź typy, które są używane w odniesieniu do [`System.AppDomain`go źródła odwołania](https://github.com/dotnet/corefx/blob/master/src/Common/src/CoreLib/System/AppDomain.cs) w [repozytorium GitHub/corefx](https://github.com/dotnet/corefx)w serwisie, a następnie wybierz gałąź zgodną z zaimplementowaną wersją.

## <a name="remoting"></a>Komunikacji zdalnej

Komunikacja zdalna .NET została zidentyfikowana jako problematyczna architektura. Jest on używany do komunikacji między domenami, która nie jest już obsługiwana. Ponadto komunikacja zdalna wymaga obsługi środowiska uruchomieniowego, co jest kosztowne do utrzymania. Z tego względu komunikacja zdalna .NET nie jest obsługiwana w przypadku platformy .NET Core i nie planuje się jej dodawania w przyszłości.

W przypadku komunikacji między procesami należy wziąć pod uwagę mechanizmy komunikacji między procesami (IPC) jako alternatywę dla komunikacji zdalnej, na przykład <xref:System.IO.Pipes> lub klasy <xref:System.IO.MemoryMappedFiles.MemoryMappedFile>.

Na wielu maszynach Użyj rozwiązania sieciowego jako alternatywy. Najlepiej użyć niskiego obciążenia protokołu zwykłego tekstu, takiego jak HTTP. Serwer [sieci Web Kestrel](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel), serwer sieci Web używany przez ASP.NET Core, jest opcją w tym miejscu. Należy również rozważyć użycie <xref:System.Net.Sockets> na potrzeby scenariuszy międzymaszynowych opartych na sieci. Aby uzyskać więcej opcji, zobacz [projekty programu .NET Open Source Developer projects: Messaging](https://github.com/Microsoft/dotnet/blob/master/dotnet-developer-projects.md#messaging).

## <a name="code-access-security-cas"></a>Zabezpieczenia dostępu kodu (CAS)

W przypadku korzystania z trybu piaskownicy, który polega na środowisku uruchomieniowym lub środowisku, aby ograniczyć zasoby, których zarządzana aplikacja lub biblioteka jest uruchomiona, [nie jest obsługiwane w .NET Framework](../../framework/misc/code-access-security.md) i dlatego nie jest również obsługiwane w programie .NET Core. W .NET Framework jest zbyt wiele przypadków i środowisko uruchomieniowe, w którym występuje podniesienie uprawnień, aby kontynuować traktowanie urzędów certyfikacji jako granic zabezpieczeń. Ponadto urzędy certyfikacji czynią implementację bardziej skomplikowaną i często mają prawidłowy wpływ na wydajność aplikacji, które nie będą używane.

Użyj granic zabezpieczeń zapewnianych przez system operacyjny, takich jak wirtualizacja, kontenery lub konta użytkowników do uruchamiania procesów z minimalnym zestawem uprawnień.

## <a name="security-transparency"></a>Przejrzystość zabezpieczeń

Podobnie jak w przypadku urzędów certyfikacji, przezroczystość zabezpieczeń oddziela kod w trybie piaskownicy od krytycznego kodu zabezpieczeń w sposób deklaratywny, ale [nie jest już obsługiwany jako granica zabezpieczeń](../../framework/misc/security-transparent-code.md). Ta funkcja jest intensywnie używana przez program Silverlight. 

Użyj granic zabezpieczeń zapewnianych przez system operacyjny, takich jak wirtualizacja, kontenery lub konta użytkowników do uruchamiania procesów z najmniej określonym zestawem uprawnień.

## <a name="systementerpriseservices"></a>System. EnterpriseServices

System. EnterpriseServices (COM+) nie jest obsługiwany przez platformę .NET Core.

>[!div class="step-by-step"]
>[Next](third-party-deps.md)
