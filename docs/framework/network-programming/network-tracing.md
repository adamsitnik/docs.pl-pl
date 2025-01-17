---
title: Śledzenie sieci w .NET Framework
ms.date: 03/30/2017
helpviewer_keywords:
- debugging [.NET Framework], network tracing
- methods, network tracing
- Networking
- trace enabled debugging
- network tracing, about network tracing
- network tracing
- network, network tracing
- traffic tracing
- tracing [.NET Framework], network
- deploying applications [.NET Framework], network traffic
- capturing network traffic
- Internet, network tracing
- Network Resources
- output, network tracing
- method invocations
ms.assetid: e993b7c3-087f-45d8-9c02-9dded936d804
ms.openlocfilehash: afb9c3a04258b543e373b6973e576f71f90d7003
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047593"
---
# <a name="network-tracing-in-the-net-framework"></a>Śledzenie sieci w .NET Framework
Mechanizm śledzenia sieci w środowisku .NET Framework umożliwia dostęp do informacji o wywołaniach metod i ruchu sieciowym generowanym przez zarządzaną aplikację. Funkcja ułatwia debugowanie aplikacji na etapie ich tworzenia oraz analizowanie już wdrożonych aplikacji. Dane wyjściowe funkcji śledzenia sieci można adaptować, dostosowując je do różnych scenariuszy fazy programowania i środowiska produkcyjnego.  
  
 Aby włączyć śledzenie sieci w środowisku .NET Framework, należy wskazać miejsce docelowe danych wyjściowych funkcji oraz dodać jej ustawienia konfiguracyjne do pliku konfiguracyjnego aplikacji lub maszyny. Opisy plików konfiguracji i sposobu ich użycia można znaleźć w temacie [pliki konfiguracji](../configure-apps/index.md). Informacje o sposobie włączania funkcji śledzenia sieci znajdują się w temacie [Włączanie śledzenia sieci](enabling-network-tracing.md). Aby uzyskać informacje o ustawieniach, które należy dodać do pliku konfiguracji, zobacz [How to: Skonfiguruj śledzenie](how-to-configure-network-tracing.md)sieci.  
  
 Po włączeniu śledzenia można przechwytywać informacje o śledzeniu, które są wyprowadzane przez klasy **System.NET** . Do składowych klasy sieciowej generujących dane ze śledzenia obowiązuje następująca uwaga zawarta w sekcji Uwaga w dokumentacji biblioteki klas środowiska NET Framework:  
  
> [!NOTE]
> Ten element członkowski generuje informacje ze śledzenia pod warunkiem włączenia funkcji śledzenia sieci w aplikacji. Aby dowiedzieć się więcej, zobacz Śledzenie sieci.  
  
## <a name="see-also"></a>Zobacz także

- [Włączanie śledzenia sieci](enabling-network-tracing.md)
- [Instrukcje: Konfigurowanie śledzenia sieci](how-to-configure-network-tracing.md)
- [Interpretowanie śledzenia sieci](interpreting-network-tracing.md)
- [Śledzenie i instrumentacja aplikacji](../debug-trace-profile/tracing-and-instrumenting-applications.md)
