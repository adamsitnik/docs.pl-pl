---
title: WSStreamedHttpBinding
ms.date: 03/30/2017
ms.assetid: 97ce4d3d-ca6f-45fa-b33b-2429bb84e65b
ms.openlocfilehash: e684a5157d5510d22cfdd14d7b0d930c3b40c476
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73423702"
---
# <a name="wsstreamedhttpbinding"></a>WSStreamedHttpBinding

W przykładzie pokazano, jak utworzyć powiązanie, które jest przeznaczone do obsługi scenariuszy przesyłania strumieniowego, gdy używany jest transport HTTP.

> [!NOTE]
> Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.

> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , aby pobrać wszystkie próbki Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)]. Ten przykład znajduje się w następującym katalogu.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Binding\WSStreamedHttpBinding`

 Poniżej przedstawiono procedurę tworzenia i konfigurowania nowego powiązania standardowego.

1. Tworzenie nowego powiązania standardowego

    Standardowe powiązania w Windows Communication Foundation (WCF), takie jak basicHttpBinding i netTcpBinding, konfigurują podstawowe transporty i stos kanałów dla określonych wymagań. W tym przykładzie `WSStreamedHttpBinding` konfiguruje stos kanałów do obsługi przesyłania strumieniowego. Domyślnie usługa WS-Security i niezawodna obsługa komunikatów nie są dodawane do stosu kanałów, ponieważ obie funkcje nie są obsługiwane przez przesyłanie strumieniowe. Nowe powiązanie jest zaimplementowane w klasie `WSStreamedHttpBinding`, która pochodzi od <xref:System.ServiceModel.Channels.Binding>. `WSStreamedHttpBinding` zawiera następujące elementy powiązania: <xref:System.ServiceModel.Channels.HttpTransportBindingElement>, <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>, <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>i <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>. Klasa udostępnia metodę `CreateBindingElements()`, aby skonfigurować wynikowy stos powiązań, jak pokazano w poniższym przykładowym kodzie.

    ```csharp
    public override BindingElementCollection CreateBindingElements()
    {
        // return collection of BindingElements
        BindingElementCollection bindingElements = new BindingElementCollection();

        // the order of binding elements within the collection is important: layered channels are applied in the order included, followed by
        // the message encoder, and finally the transport at the end
        if (flowTransactions)
        {
            bindingElements.Add(transactionFlow);
        }
        bindingElements.Add(textEncoding);

        // add transport (http or https)
        bindingElements.Add(transport);
        return bindingElements.Clone();
    }
    ```

2. Dodawanie obsługi konfiguracji

    Aby uwidocznić transport poprzez konfigurację, przykład implementuje dwie więcej klas —`WSStreamedHttpBindingConfigurationElement` i `WSStreamedHttpBindingSection`. Klasa `WSStreamedHttpBindingSection` jest <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602>, który uwidacznia `WSStreamedHttpBinding` do systemu konfiguracji WCF. Zbiorcza implementacja jest delegowana do `WSStreamedHttpBindingConfigurationElement`, który pochodzi z <xref:System.ServiceModel.Configuration.StandardBindingElement>. Klasa `WSStreamedHttpBindingConfigurationElement` ma właściwości, które odpowiadają właściwościom `WSStreamedHttpBinding`i funkcje do mapowania każdego elementu konfiguracji do powiązania.

    Zarejestruj program obsługi przy użyciu systemu konfiguracji, dodając następującą sekcję do pliku konfiguracji usługi.

    ```xml
    <configuration>
      <system.serviceModel>
        <extensions>
          <bindingExtensions>
            <add name="wsStreamedHttpBinding" type="Microsoft.ServiceModel.Samples.WSStreamedHttpBindingCollectionElement, WSStreamedHttpBinding, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null" />
          </bindingExtensions>
        </extensions>
      </system.serviceModel>
    </configuration>
    ```

    Do programu obsługi można odwoływać się z sekcji konfiguracji serviceModel.

    ```xml
    <configuration>
      <system.serviceModel>
        <client>
          <endpoint
                    address="https://localhost/servicemodelsamples/service.svc"
                    bindingConfiguration="Binding"
                    binding="wsStreamedHttpBinding"
                    contract="Microsoft.ServiceModel.Samples.IStreamedEchoService"/>
        </client>
      </system.serviceModel>
    </configuration>
    ```

### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład

1. Zainstaluj ASP.NET 4,0 przy użyciu następującego polecenia.

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. Upewnij się, że wykonano kroki opisane w [temacie Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).

3. Upewnij się, że wykonano [instrukcje instalacji certyfikatu serwera Internet Information Services (IIS)](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md).

4. Aby skompilować rozwiązanie, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).

5. Aby uruchomić przykład w konfiguracji między maszynami, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).

6. Po wyświetleniu okna klienta wpisz "Sample. txt". W katalogu powinna znajdować się "kopia przykładowa. txt".

## <a name="the-wsstreamedhttpbinding-sample-service"></a>Przykładowa usługa WSStreamedHttpBinding

Przykładowa usługa, która używa `WSStreamedHttpBinding`, znajduje się w podkatalogu usługi. Implementacja `OperationContract` używa `MemoryStream`, aby najpierw pobrać wszystkie dane ze strumienia przychodzącego przed zwróceniem `MemoryStream`. Przykładowa usługa jest hostowana przez Internet Information Services (IIS).

```csharp
[ServiceContract]
public interface IStreamedEchoService
{
    [OperationContract]
    Stream Echo(Stream data);
}

public class StreamedEchoService : IStreamedEchoService
{
    public Stream Echo(Stream data)
    {
        MemoryStream dataStorage = new MemoryStream();
        byte[] byteArray = new byte[8192];
        int bytesRead = data.Read(byteArray, 0, 8192);
        while (bytesRead > 0)
        {
            dataStorage.Write(byteArray, 0, bytesRead);
            bytesRead = data.Read(byteArray, 0, 8192);
        }
        data.Close();
        dataStorage.Seek(0, SeekOrigin.Begin);

        return dataStorage;
    }
}
```

## <a name="the-wsstreamedhttpbinding-sample-client"></a>Przykładowy klient WSStreamedHttpBinding

Klient, który jest używany do współdziałania z usługą za pomocą `WSStreamedHttpBinding`, znajduje się w podkatalogu klienta. Ponieważ certyfikat używany w tym przykładzie jest certyfikatem testowym utworzonym przy użyciu programu Makecert. exe, podczas próby uzyskania dostępu do adresu HTTPS w przeglądarce, takiego jak https://localhost/servicemodelsamples/service.svc, zostanie wyświetlony alert zabezpieczeń. Aby umożliwić klientowi WCF współpracuję z certyfikatem testowym, do klienta został dodany dodatkowy kod, aby pominąć alert zabezpieczeń. Kod i towarzysząca Klasa nie są wymagane w przypadku korzystania z certyfikatów produkcyjnych.

```csharp
// WARNING: This code is only required for test certificates such as those created by makecert. It is
// not recommended for production code.
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");
```
