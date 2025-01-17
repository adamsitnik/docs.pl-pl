---
title: Konfigurowanie usługi aktywacji procesów systemu Windows do użycia z programem Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 1d50712e-53cd-4773-b8bc-a1e1aad66b78
ms.openlocfilehash: 7ab62bda5e579bcd80a7403d9af3a7e7f9836647
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487004"
---
# <a name="configuring-the-windows-process-activation-service-for-use-with-windows-communication-foundation"></a>Konfigurowanie usługi aktywacji procesów systemu Windows do użycia z programem Windows Communication Foundation
W tym temacie opisano kroki wymagane do skonfigurowania usługi aktywacji procesów systemu Windows (znany także jako WAS) w [!INCLUDE[wv](../../../../includes/wv-md.md)] do hostowania usług Windows Communication Foundation (WCF) protokołów sieciowych usług, które nie komunikują się za pośrednictwem protokołu HTTP. W poniższych sekcjach opisano w krokach dla tej konfiguracji:  
  
- Zainstalować (lub Potwierdź instalację) składników aktywacji programu WCF, które są wymagane.  
  
- Utwórz witrynę WAS za pomocą powiązań protokołów sieciowych, które mają być używane lub dodać nowe powiązanie protokołu do istniejącej lokacji.  
  
- Tworzenie aplikacji do hostowania usług, a następnie włącz tej aplikacji do korzystania z protokołów sieciowych wymaganych.  
  
- Tworzenie usługi WCF, która udostępnia punkt końcowy protokołu HTTP.  
  
## <a name="configuring-a-site-with-non-http-bindings"></a>Konfigurowanie lokacji za pomocą powiązania bez HTTP  
 Aby użyć powiązania protokołu HTTP z WAS, powiązania witryny, należy dodać do konfiguracji WAS. Magazyn konfiguracji dla WAS jest plik applicationHost.config znajdujący się w katalogu %windir%\system32\inetsrv\config. Ten magazyn konfiguracji jest współużytkowana przez WAS i usług IIS 7.0.  
  
 applicationHost.config to plik tekstowy XML, który można otworzyć za pomocą dowolnego edytora tekstu standardowego (np. Notatnika). Jednak narzędzie wiersza polecenia konfiguracji usług IIS 7.0 (appcmd.exe) jest najlepszym sposobem dodawania powiązania protokołu HTTP witryny.  
  
 Następujące polecenie dodaje powiązanie witryny net.tcp, do domyślnej witryny sieci Web przy użyciu appcmd.exe (to polecenie jest wprowadzana jako jeden wiersz).  
  
```console  
appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
```  
  
 To polecenie dodaje nowe powiązanie net.tcp do domyślnej witryny sieci Web przez dodanie wiersza zostało wskazane poniżej do pliku applicationHost.config.  
  
```xml  
<sites>  
    <site name="Default Web Site" id="1">  
        <bindings>  
            <binding protocol="HTTP" bindingInformation="*:80:" />  
            //The following line is added by the command.  
            <binding protocol="net.tcp" bindingInformation="808:*" />  
        </bindings>  
    </site>  
</sites>  
```  
  
## <a name="enabling-an-application-to-use-non-http-protocols"></a>Włączanie aplikacji do użycia protokołów innych niż HTTP  
 Można włączyć lub wyłączyć protocolsat poszczególnych sieci na poziomie aplikacji. Następujące polecenie przedstawia sposób Włącz protokoły HTTP i net.tcp dla aplikacji, która działa w `Default Web Site`.  
  
```console  
appcmd.exe set app "Default Web Site/appOne" /enabledProtocols:net.tcp  
```  
  
 Lista włączone protokoły można również ustawić \<applicationDefaults > element konfiguracji XML witryny jest przechowywany w pliku ApplicationHost.config.  
  
 Następujący kod XML z pliku applicationHost.config ilustruje lokacji powiązane z protokołów HTTP i protokołów innych niż HTTP. Dodatkowej konfiguracji, które są wymagane do obsługi protokołów innych niż HTTP nazywa z komentarzami.  
  
```xml  
<sites>  
    <site name="Default Web Site" id="1">  
    <application path="/">  
        <virtualDirectory path="/" physicalPath="D:\inetpub\wwwroot" />  
    </application>  
       <bindings>  
            //The following two lines are added by the command.  
            <binding protocol="HTTP" bindingInformation="*:80:" />  
            <binding protocol="net.tcp" bindingInformation="808:*" />  
       </bindings>  
    </site>  
    <siteDefaults>  
        <logFile   
        customLogPluginClsid="{FF160663-DE82-11CF-BC0A-00AA006111E0}"  
          directory="D:\inetpub\logs\LogFiles" />  
        <traceFailedRequestsLogging   
          directory="D:\inetpub\logs\FailedReqLogFiles" />  
    </siteDefaults>  
    <applicationDefaults   
      applicationPool="DefaultAppPool"   
      //The following line is inserted by the command.  
      enabledProtocols="http, net.tcp" />  
    <virtualDirectoryDefaults allowSubDirConfig="true" />  
</sites>  
```  
  
 Jeśli spróbujesz aktywować usługi przy użyciu WAS dla Aktywacja bez HTTP i nie zostanie zainstalowany i skonfigurowany WAS może zostać wyświetlony następujący błąd:  
  
```output  
[InvalidOperationException: The protocol 'net.tcp' does not have an implementation of HostedTransportConfiguration type registered.]   System.ServiceModel.AsyncResult.End(IAsyncResult result) +15778592   System.ServiceModel.Activation.HostedHttpRequestAsyncResult.End(IAsyncResult result) +15698937   System.ServiceModel.Activation.HostedHttpRequestAsyncResult.ExecuteSynchronous(HttpApplication context, Boolean flowContext) +265   System.ServiceModel.Activation.HttpModule.ProcessRequest(Object sender, EventArgs e) +227   System.Web.SyncEventExecutionStep.System.Web.HttpApplication.IExecutionStep.Execute() +80   System.Web.HttpApplication.ExecuteStep(IExecutionStep step, Boolean& completedSynchronously) +171  
```  
  
 Jeśli zostanie wyświetlony ten błąd, upewnij się, WAS dla Aktywacja bez HTTP jest zainstalowana i poprawnie skonfigurowana. Aby uzyskać więcej informacji, zobacz [jak: Instalowanie i konfigurowanie składników aktywacji programu WCF](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md).  
  
## <a name="building-a-wcf-service-that-uses-was-for-non-http-activation"></a>Tworzenie usługi WCF Service, używa DOTYCZYŁO Aktywacja bez HTTP  
 Po wykonaniu kroków, aby zainstalować i skonfigurować WAS (zobacz [jak: Instalowanie i konfigurowanie składników aktywacji programu WCF](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)), konfigurowanie usługi do użycia WAS aktywacji jest podobne do konfigurowania usługi, który znajduje się w usługach IIS.  
  
 Aby uzyskać szczegółowe instrukcje dotyczące tworzenia usługi WCF aktywacji WAS, zobacz [jak: Hostowanie usługi WCF w WAS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md).  
  
## <a name="see-also"></a>Zobacz także

- [Hosting w usłudze aktywacji procesów systemu Windows](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)
- [Windows Server AppFabric funkcje hostingu](https://go.microsoft.com/fwlink/?LinkId=201276)
