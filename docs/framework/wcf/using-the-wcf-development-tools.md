---
title: Używanie narzędzi deweloperskich programu WCF
ms.date: 03/30/2017
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
ms.openlocfilehash: afa62a63aa955dc868791da635418331f93e9e87
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73420682"
---
# <a name="using-the-wcf-development-tools"></a>Używanie narzędzi deweloperskich programu WCF
W tej sekcji opisano narzędzia deweloperskie programu Visual Studio, które mogą pomóc w opracowaniu WCFservice.  
  
 Szablony programu Visual Studio można używać jako podstaw do szybkiego tworzenia własnej usługi, a następnie do debugowania i testowania usługi przy użyciu usługi WCF — hosta i klienta testowego WCF. Narzędzia te wspólnie zapewniają szybkie i bezproblemowe cykle debugowania i testowania, a także uniemożliwiają konieczność przekazania do modelu hostingu na wczesnym etapie.  
 
 > [!NOTE]
 > Począwszy od programu Visual Studio 2017, narzędzia programistyczne WCF nie są instalowane domyślnie. Aby można było korzystać z tych funkcji, należy upewnić się, że składnik Windows Communication Foundation został wybrany w Instalatorze programu Visual Studio.
  
## <a name="the-wcf-developer-tools"></a>Narzędzia deweloperskie WCF  
 [Szablony programu Visual Studio na potrzeby programu WCF](wcf-vs-templates.md)  
  
 Możesz użyć wstępnie zdefiniowanego projektu programu Visual Studio i szablonów elementów w programie Visual Studio, aby szybko tworzyć usługi WCF i otaczające aplikacje.  
  
 [Host usługi WCF (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)  
  
 Automatyczny Host usługi WCF (WcfSvcHost. exe) umożliwia uruchomienie debugera programu Visual Studio (F5) w celu automatycznego hostowania i testowania wdrożonej usługi. Następnie można przetestować usługę przy użyciu klienta testowego WCF (wcfTestClient. exe) lub własnego klienta, aby znaleźć i naprawić wszelkie potencjalne błędy.  
  
 [Testowy klient WCF (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)  
  
 Klient testowy WCF (WcfTestClient. exe) to narzędzie graficznego interfejsu użytkownika, które umożliwia wprowadzanie parametrów dowolnego typu, przesyłanie tych danych do usługi i wyświetlanie odpowiedzi wysyłanej przez usługę. Zapewnia bezproblemowe środowisko testowania usług w połączeniu z hostem usługi WCF.  
  
 [Generowanie klas typów danych z kodu XML](generating-data-type-classes-from-xml.md)  
  
 Dane XML przechowywane w Schowku można wkleić do strony kodowej. Klasy zdefiniowane w danych zostaną przekonwertowane na typy kodu.  
  
## <a name="using-the-tools-without-administrator-privilege"></a>Korzystanie z narzędzi bez uprawnień administratora  
 Aby umożliwić użytkownikom bez uprawnień administratora opracowywanie usług WCF, podczas instalacji programu Visual Studio jest tworzona lista kontroli dostępu (Access Control) dla przestrzeni nazw "http://+:8731/Design_Time_Addresses". Lista ACL jest ustawiona na (UI), która obejmuje wszystkich użytkowników interakcyjnych zalogowanych na komputerze. Administratorzy mogą dodawać lub usuwać użytkowników z tej listy kontroli dostępu lub otwierać dodatkowe porty. Ta lista ACL umożliwia szablonom programu WCF lub WF wysyłanie i odbieranie danych w konfiguracji domyślnej. Umożliwia ona również użytkownikom korzystanie z funkcji Autohost usługi WCF (wcfSvcHost. exe) bez udzielania im uprawnień administratora.  
  
 Dostęp można modyfikować za pomocą narzędzia Netsh. exe w [!INCLUDE[wv](../../../includes/wv-md.md)] na koncie administratora z podwyższonym poziomem uprawnień. Poniżej przedstawiono przykład użycia narzędzia Netsh. exe.  
  
```console  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 Aby uzyskać więcej informacji na temat narzędzia Netsh. exe, zobacz [jak używać narzędzia Netsh. exe i przełączników wiersza polecenia](https://go.microsoft.com/fwlink/?LinkId=97877).  
  
## <a name="see-also"></a>Zobacz także

- [Szablony programu Visual Studio na potrzeby programu WCF](wcf-vs-templates.md)
- [Host usługi WCF (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)
- [Testowy klient WCF (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
