---
title: Nieopakowane komunikaty
ms.date: 03/30/2017
ms.assetid: 019657bd-1f9b-4315-ad74-eaa4e7551ff6
ms.openlocfilehash: 9609160885a46d76c5df54538fc088a3d025ca3b
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044606"
---
# <a name="unwrapped-messages"></a>Nieopakowane komunikaty
Ten przykład pokazuje nieopakowane komunikaty. Domyślnie treść komunikatu jest formatowana w taki sposób, że parametry operacji usługi są opakowane. Poniższy przykład pokazuje `Add` komunikat żądania `ICalculator` do usługi w trybie opakowanym.  
  
```xml  
<s:Envelope   
    xmlns:s="http://www.w3.org/2003/05/soap-envelope"  
    xmlns:a="http://schemas.xmlsoap.org/ws/2005/08/addressing">  
    <s:Header>  
        …  
    </s:Header>  
    <s:Body>  
      <Add xmlns="http://Microsoft.ServiceModel.Samples">  
        <n1>100</n1>  
        <n2>15.99</n2>  
      </Add>  
    </s:Body>  
</s:Envelope>  
```  
  
 Element w treści wiadomości otacza `n1` parametry i `n2`. `<Add>` Z kolei Poniższy przykład pokazuje odpowiedni komunikat w trybie nieopakowanym.  
  
```xml  
<s:Envelope   
    xmlns:s="http://www.w3.org/2003/05/soap-envelope"   
    xmlns:a="http://schemas.xmlsoap.org/ws/2005/08/addressing">  
    <s:Header>  
        ….  
    </s:Header>  
    <s:Body>  
      <n1 xmlns="http://Microsoft.ServiceModel.Samples">100</n1>  
      <n2 xmlns="http://Microsoft.ServiceModel.Samples">15.99</n2>  
    </s:Body>  
  </s:Envelope>  
</MessageLogTraceRecord>  
```  
  
 Nieopakowany komunikat nie otacza `n1` parametrów i `n2` w elemencie zawierającym, są bezpośrednimi elementami podrzędnymi elementu treści protokołu SOAP.  
  
> [!NOTE]
> Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.  
  
 W tym przykładzie nieopakowany komunikat jest tworzony przez zastosowanie <xref:System.ServiceModel.MessageContractAttribute> do typu parametru operacji usługi i typu wartości zwracanej, jak pokazano w poniższym przykładowym kodzie.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    ResponseMessage Add(RequestMessage request);  
    [OperationContract]  
    ResponseMessage Subtract(RequestMessage request);  
    [OperationContract]  
    ResponseMessage Multiply(RequestMessage request);  
    [OperationContract]  
    ResponseMessage Divide(RequestMessage request);  
}  
  
//setting IsWrapped to false means the n1 and n2  
//members will be direct children of the soap body element  
[MessageContract(IsWrapped = false)]  
public class RequestMessage  
{  
    [MessageBodyMember]  
    private double n1;  
    [MessageBodyMember]  
    private double n2;  
    //…  
}  
  
//setting IsWrapped to false means the result  
//member will be a direct child of the soap body element  
[MessageContract(IsWrapped = false)]  
public class ResponseMessage  
{  
    [MessageBodyMember]  
    private double result;  
    //…  
}  
```  
  
 Aby umożliwić wyświetlanie wysyłanych i odbieranych komunikatów, ten przykład używa śledzenia. Ponadto program <xref:System.ServiceModel.WSHttpBinding> został skonfigurowany bez zabezpieczeń, aby zmniejszyć liczbę komunikatów, które rejestruje.  
  
 Wynikowy dziennik śledzenia (c:\logs\Message.log) można wyświetlić za pomocą [narzędzia Podgląd śledzenia usług (SvcTraceViewer. exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md). Aby wyświetlić zawartość wiadomości, wybierz pozycję **komunikaty** w lewym okienku narzędzia Podgląd śledzenia usługi. Dzienniki śledzenia w tym przykładzie są skonfigurowane tak, aby były generowane w folderze C:\LOGS. Utwórz ten folder przed uruchomieniem przykładu i nadaj użytkownikowi uprawnienia do zapisu w tym katalogu.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład  
  
1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Utwórz katalog C:\LOGS na potrzeby rejestrowania komunikatów. Nadaj użytkownikom uprawnienia do zapisu w tym katalogu.  
  
3. Aby skompilować C# lub Visual Basic wersję .NET rozwiązania, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4. Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Message\Unwrapped`  
