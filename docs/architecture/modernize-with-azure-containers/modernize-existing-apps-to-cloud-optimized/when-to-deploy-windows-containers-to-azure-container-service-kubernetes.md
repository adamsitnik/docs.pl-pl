---
title: Kiedy należy wdrażać kontenery systemu Windows w celu Azure Container Service (to jest Kubernetes)
description: Modernizacja istniejących aplikacji .NET za pomocą chmury platformy Azure i kontenerów systemu Windows | Kiedy należy wdrażać kontenery systemu Windows w celu Azure Container Service (to jest Kubernetes)
ms.date: 04/30/2018
ms.openlocfilehash: 903082deba635dd0dfc22d0186fbc589f8d05b92
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/08/2019
ms.locfileid: "68676911"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a>Kiedy należy wdrażać kontenery systemu Windows w celu Azure Container Service (to jest Kubernetes)

Azure Container Service optymalizuje konfigurację popularnych narzędzi i technologii typu "open source" przeznaczonych dla platformy Azure. Uzyskasz otwarte rozwiązanie, które oferuje przenośność dla kontenerów i konfiguracji aplikacji. Wybierasz rozmiar, liczbę hostów i narzędzia programu Orchestrator. Azure Container Service obsługuje infrastrukturę.

Jeśli już pracujesz z koordynatorami typu "open source", takimi jak Kubernetes, Docker Swarm lub DC/OS, nie musisz zmieniać istniejących praktyk zarządzania w celu przenoszenia obciążeń kontenera do chmury. Skorzystaj z narzędzi do zarządzania aplikacjami, które są już znane, i Połącz się za pośrednictwem standardowych punktów końcowych interfejsu API dla wybranego koordynatora.

Wszystkie te koordynatorzy są dojrzałymi środowiskami, jeśli używasz kontenerów platformy Docker systemu Linux, ale może to być tylko w wersji zapoznawczej dla kontenerów Windows.

Na przykład w Kubernetes, obsługa kontenerów jest natywna (obywatel pierwszej klasy), więc korzystanie z kontenerów systemu Windows na Kubernetes jest również skuteczne (w wersji zapoznawczej w usłudze ACS od początku 2018).

Ważna Uwaga: rozwijająca się i "więcej PaaS" wersja usług ACS (Azure Container Service) dla Kubernetes to AKS (usługa Azure Kubernetes Service), jednak kontenery systemu Windows nadal nie są obsługiwane w przypadku wersji Q2 2018, ale będzie ona dostępna wkrótce.

>[!div class="step-by-step"]
>[Poprzedni](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
>[dalej](choosing-azure-compute-options-for-container-based-applications.md)
