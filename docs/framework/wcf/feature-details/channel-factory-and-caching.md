---
title: Fabryka kanałów i buforowanie
ms.date: 03/30/2017
ms.assetid: 954f030e-091c-4c0e-a7a2-10f9a6b1f529
ms.openlocfilehash: 98b77071204e2c2f98609e6c5bb1ca84a896dd58
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040200"
---
# <a name="channel-factory-and-caching"></a>Fabryka kanałów i buforowanie

Aplikacje klienckie programu WCF używają <xref:System.ServiceModel.ChannelFactory%601> klasy do tworzenia kanału komunikacyjnego z usługą WCF.  Tworzenie <xref:System.ServiceModel.ChannelFactory%601> wystąpień wiąże się z pewnym obciążeniem, ponieważ obejmuje następujące operacje:

- Konstruowanie <xref:System.ServiceModel.Description.ContractDescription> drzewa

- Odzwierciedlanie wszystkich wymaganych typów CLR

- Konstruowanie stosu kanału

- Usuwanie zasobów

Aby zminimalizować obciążenie, usługa WCF może buforować fabryki kanałów w przypadku korzystania z serwera proxy klienta WCF.

> [!TIP]
> Użytkownik ma bezpośrednią kontrolę nad tworzeniem fabryki kanałów w przypadku bezpośredniego <xref:System.ServiceModel.ChannelFactory%601> używania klasy.

Serwery proxy klienta WCF generowane za pomocą [Narzędzia do przesyłania metadanych programu ServiceModel (Svcutil. exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) pochodzą od <xref:System.ServiceModel.ClientBase%601>. <xref:System.ServiceModel.ClientBase%601>definiuje Właściwość statyczną <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> , która definiuje zachowanie buforowania fabryki kanałów. Ustawienia pamięci podręcznej dla określonego typu. Na przykład ustawienie `ClientBase<ITest>.CacheSettings` jednej z wartości zdefiniowanych poniżej będzie miało wpływ tylko na te dane typu `ITest`proxy/ClientBase. Ustawienie pamięci podręcznej dla <xref:System.ServiceModel.ClientBase%601> konkretnego elementu jest niezmienne, gdy tylko zostanie utworzony pierwszy wystąpienie serwera proxy/elementu ClientBase.

## <a name="specifying-caching-behavior"></a>Określanie zachowania buforowania

Zachowanie buforowania jest określone przez ustawienie <xref:System.ServiceModel.ClientBase%601.CacheSetting> właściwości na jedną z następujących wartości.

|Wartość ustawienia pamięci podręcznej|Opis|
|-------------------------|-----------------|
|<xref:System.ServiceModel.CacheSetting.AlwaysOn>|Wszystkie wystąpienia <xref:System.ServiceModel.ClientBase%601> w domenie aplikacji mogą brać udział w pamięci podręcznej. Deweloper stwierdził, że nie ma żadnych niepożądanych implikacji w zabezpieczeniach do buforowania. Buforowanie nie zostanie wyłączone, nawet jeśli są dostępne właściwości "poufne dla <xref:System.ServiceModel.ClientBase%601> zabezpieczeń". Właściwości "z <xref:System.ServiceModel.ClientBase%601> uwzględnieniem zabezpieczeń" są <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>, <xref:System.ServiceModel.ClientBase%601.Endpoint%2A> i <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A>.|
|<xref:System.ServiceModel.CacheSetting.Default>|Tylko wystąpienia <xref:System.ServiceModel.ClientBase%601> utworzone z punktów końcowych zdefiniowanych w plikach konfiguracji uczestniczą w pamięci podręcznej w domenie aplikacji. Wszystkie wystąpienia <xref:System.ServiceModel.ClientBase%601> utworzone programowo w tej domenie aplikacji nie będą uczestniczyły w pamięci podręcznej. Ponadto buforowanie zostanie wyłączone dla wystąpienia <xref:System.ServiceModel.ClientBase%601> po uzyskaniu dostępu do wszystkich właściwości "z uwzględnieniem zabezpieczeń".|
|<xref:System.ServiceModel.CacheSetting.AlwaysOff>|Buforowanie jest wyłączone dla wszystkich wystąpień <xref:System.ServiceModel.ClientBase%601> określonego typu w danej domenie aplikacji.|

Poniższe fragmenty kodu ilustrują sposób użycia <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> właściwości.

```csharp
class Program
{
   static void Main(string[] args)
   {
      ClientBase<ITest>.CacheSettings = CacheSettings.AlwaysOn;
      foreach (string msg in messages)
      {
         using (TestClient proxy = new TestClient (new BasicHttpBinding(), new EndpointAddress(address)))
         {
            // ...
            proxy.Test(msg);
            // ...
         }
      }
   }
}
// Generated by SvcUtil.exe
public partial class TestClient : System.ServiceModel.ClientBase, ITest { }
```

W powyższym kodzie wszystkie wystąpienia programu `TestClient` będą używały tej samej fabryki kanałów.

```csharp
class Program
{
   static void Main(string[] args)
   {
      ClientBase.CacheSettings = CacheSettings.Default;
      int i = 1;
      foreach (string msg in messages)
      {
         using (TestClient proxy = new TestClient ("MyEndpoint", new EndpointAddress(address)))
         {
            if (i == 4)
            {
               ServiceEndpoint endpoint = proxy.Endpoint;
               ... // use endpoint in some way
            }
            proxy.Test(msg);
         }
         i++;
   }
}

// Generated by SvcUtil.exe
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}
```

W powyższym przykładzie wszystkie wystąpienia `TestClient` mogą korzystać z tej samej fabryki kanałów, z wyjątkiem #4 wystąpienia. Wystąpienie #4 będzie używać fabryki kanałów, która została utworzona w celu użycia. To ustawienie będzie działało w scenariuszach, w których konkretny punkt końcowy wymaga różnych ustawień zabezpieczeń z innych punktów końcowych tego samego typu fabryki kanału (w `ITest`tym przypadku).

```csharp
class Program
{
   static void Main(string[] args)
   {
      ClientBase.CacheSettings = CacheSettings.AlwaysOff;
      foreach (string msg in messages)
      {
         using (TestClient proxy = new TestClient ("MyEndpoint", new EndpointAddress(address)))
         {
            proxy.Test(msg);
         }
      }
   }
}

// Generated by SvcUtil.exe
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}
```

W powyższym przykładzie wszystkie wystąpienia `TestClient` byłyby używają różnych fabryk kanałów. Jest to przydatne, gdy każdy punkt końcowy ma inne wymagania dotyczące zabezpieczeń i nie ma sensu buforowania.

## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.ClientBase%601>
- [Kompilowanie klientów](../../../../docs/framework/wcf/building-clients.md)
- [Klienci](../../../../docs/framework/wcf/feature-details/clients.md)
- [Uzyskiwanie dostępu do usług za pomocą klienta WCF](../../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)
- [Instrukcje: Korzystanie z elementu ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)
