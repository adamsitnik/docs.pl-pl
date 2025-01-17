---
title: Anonse — przykład
ms.date: 03/30/2017
ms.assetid: 954a75e4-9a97-41d6-94fc-43765d4205a9
ms.openlocfilehash: 1acf51ebe36872424be1e0fdda65a7d18aa737f2
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045795"
---
# <a name="announcements-sample"></a>Anonse — przykład

Ten przykład pokazuje, jak używać funkcji anonsu funkcji odnajdywania. Anonsy umożliwiają usługom wysyłanie komunikatów anonsu zawierających metadane dotyczące usługi. Domyślnie anons powitalny jest wysyłany podczas uruchamiania usługi i wysyłany jest anons bye po zamknięciu usługi. Anonse mogą być multiemisje lub mogą być wysyłane jako punkt-punkt. Ten przykład składa się z dwóch projektów usługi i klienta.

## <a name="service"></a>Usługa

Ten projekt zawiera samohostowaną usługę kalkulatora. `Main` W metodzie zostanie utworzony host usługi i do niego zostanie dodany punkt końcowy usługi. <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> Następnie jest tworzony. Aby włączyć Anonsy, należy dodać punkt końcowy anonsu do <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>. W tym przypadku standardowym punktem końcowym przy użyciu multiemisji UDP jest dodawany jako punkt końcowy anonsu. Emituje anonse za pośrednictwem dobrze znanego adresu UDP.

```csharp
Uri baseAddress = new Uri("http://localhost:8000/" + Guid.NewGuid().ToString());

// Create a ServiceHost for the CalculatorService type.
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))
{
     serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new WSHttpBinding(), String.Empty);

     ServiceDiscoveryBehavior serviceDiscoveryBehavior = new ServiceDiscoveryBehavior();

     // Announce the availability of the service over UDP multicast
    serviceDiscoveryBehavior.AnnouncementEndpoints.Add(new UdpAnnouncementEndpoint());

    // Make the service discoverable over UDP multicast.
    serviceHost.Description.Behaviors.Add(serviceDiscoveryBehavior);
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());
    serviceHost.Open();
    // ...
}
```

## <a name="client"></a>Klient

W tym projekcie należy zauważyć, że klient obsługuje <xref:System.ServiceModel.Discovery.AnnouncementService>. Co więcej, dwa Delegaty są rejestrowane ze zdarzeniami. Te zdarzenia określają, co klient wykonuje po odebraniu anonsów online i offline.

```csharp
// Create an AnnouncementService instance
AnnouncementService announcementService = new AnnouncementService();

// Subscribe the announcement events
announcementService.OnlineAnnouncementReceived += OnOnlineEvent;
announcementService.OfflineAnnouncementReceived += OnOfflineEvent;
```

Metody `OnOnlineEvent` i`OnOfflineEvent` obsługują odpowiednio Komunikaty anonsu Hello i bye.

```csharp
static void OnOnlineEvent(object sender, AnnouncementEventArgs e)
{
    Console.WriteLine();
    Console.WriteLine("Received an online announcement from {0}:", e.AnnouncementMessage.EndpointDiscoveryMetadata.Address);
PrintEndpointDiscoveryMetadata(e.AnnouncementMessage.EndpointDiscoveryMetadata);
}

static void OnOfflineEvent(object sender, AnnouncementEventArgs e)
{
    Console.WriteLine();
    Console.WriteLine("Received an offline announcement from {0}:", e.AnnouncementMessage.EndpointDiscoveryMetadata.Address);
            PrintEndpointDiscoveryMetadata(e.AnnouncementMessage.EndpointDiscoveryMetadata);
}
```

#### <a name="to-use-this-sample"></a>Aby użyć tego przykładu

1. Ten przykład korzysta z punktów końcowych HTTP i do uruchamiania tego przykładu należy dodać odpowiednie listy ACL adresów URL, aby uzyskać szczegółowe informacje, zobacz [Konfigurowanie protokołu HTTP i https](https://go.microsoft.com/fwlink/?LinkId=70353) . Wykonanie następującego polecenia z podwyższonym poziomem uprawnień powinno spowodować dodanie odpowiednich list ACL. Można zastąpić domenę i nazwę użytkownika dla następujących argumentów, jeśli polecenie nie działa zgodnie z oczekiwaniami. `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`

2. Skompiluj rozwiązanie.

3. Uruchom aplikację Client. exe.

4. Uruchom aplikację Service. exe. Zwróć uwagę, że klient otrzymuje Anons online.

5. Zamknij aplikację Service. exe. Zwróć uwagę, że klient otrzymuje anons w trybie offline.

> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\Announcements`
