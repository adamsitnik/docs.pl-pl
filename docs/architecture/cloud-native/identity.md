---
title: Tożsamość
description: Tworzenie architektury natywnych aplikacji .NET w chmurze dla platformy Azure | Identity
ms.date: 09/23/2019
ms.openlocfilehash: 4cc7c04bf323d2589777df466321f6801f511b6f
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183050"
---
# <a name="identity"></a>Tożsamość

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Większość aplikacji oprogramowania musi mieć pewną wiedzę na temat użytkownika lub procesu wywołującego je. Użytkownik lub proces, który współdziała z aplikacją, jest znany jako podmiot zabezpieczeń, a proces uwierzytelniania i autoryzacji tych podmiotów jest znany jako Zarządzanie tożsamościami lub po prostu *tożsamość*. Proste aplikacje mogą obejmować wszystkie Zarządzanie tożsamościami w aplikacji, ale takie podejście nie jest dobrze skalowane w przypadku wielu aplikacji i wielu rodzajów podmiotów zabezpieczeń. System Windows obsługuje używanie Active Directory w celu zapewnienia scentralizowanego uwierzytelniania i autoryzacji.

<!-- (insert figure showing Windows AD auth model) -->

Chociaż to rozwiązanie jest skuteczne w sieciach firmowych, nie jest przeznaczone do użycia przez użytkowników ani aplikacje poza domeną usługi AD. W przypadku wzrostu aplikacji internetowych i wzrostu aplikacji natywnych w chmurze modele zabezpieczeń zostały rozbudowane.

W dzisiejszym modelu tożsamości natywnej w chmurze przyjęto, że architektura jest dystrybuowana. Aplikacje można wdrażać w dowolnym miejscu i mogą komunikować się z innymi aplikacjami w dowolnym miejscu. Klienci mogą komunikować się z tymi aplikacjami z dowolnego miejsca, a w rzeczywistości klienci mogą składać się z dowolnej kombinacji platform i urządzeń. Natywne rozwiązania do obsługi tożsamości w chmurze wykorzystują otwarte standardy w celu uzyskania bezpiecznego dostępu do aplikacji od klientów. Ci klienci mają ten zakres od użytkowników ludzkich na komputerach lub telefonach do innych aplikacji hostowanych w dowolnym miejscu w trybie online, a także do ustawiania najważniejszych pól i urządzeń IOT, na których działa dowolna platforma oprogramowania w dowolnym miejscu na świecie.

Nowoczesne natywne rozwiązania do obsługi tożsamości w chmurze zwykle wykorzystują tokeny dostępu wystawione przez usługę bezpiecznego tokenu/serwer (STS) do podmiotu zabezpieczeń po ustaleniu tożsamości. Token dostępu, zazwyczaj token sieci Web JSON (JWT), zawiera *oświadczenia* dotyczące podmiotu zabezpieczeń. Te oświadczenia w minimalnym stopniu obejmują tożsamość użytkownika, ale mogą również zawierać dodatkowe oświadczenia, które mogą być używane przez aplikacje w celu określenia poziomu dostępu do udzielenia podmiotu zabezpieczeń.

<!-- (insert figure showing basic handshake involving a principal, an STS, and an app) -->

Zazwyczaj usługa STS jest odpowiedzialna za uwierzytelnianie podmiotu zabezpieczeń. Określenie poziomu dostępu do zasobów jest pozostawione do innych części aplikacji.

## <a name="references"></a>Odwołania

- [Platforma tożsamości firmy Microsoft](https://docs.microsoft.com/azure/active-directory/develop/)

>[!div class="step-by-step"]
>[Poprzedni](azure-monitor.md)
>[Następny](authentication-authorization.md)
