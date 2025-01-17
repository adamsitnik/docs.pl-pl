---
title: 'Instrukcje: wybieranie między żądaniami HTTP POST i HTTP GET dla punktów końcowych AJAX ASP.NET'
ms.date: 03/30/2017
ms.assetid: b47de82a-4c92-4af6-bceb-a5cb8bb8ede9
ms.openlocfilehash: 6de32c798e7d0db5ad2d8f6666d6c5d1714250d5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991566"
---
# <a name="how-to-choose-between-http-post-and-http-get-requests-for-aspnet-ajax-endpoints"></a>Instrukcje: wybieranie między żądaniami HTTP POST i HTTP GET dla punktów końcowych AJAX ASP.NET

Windows Communication Foundation (WCF) umożliwia utworzenie usługi, która uwidacznia punkt końcowy z obsługą technologii AJAX ASP.NET, który można wywołać z JavaScript w witrynie sieci Web klienta. Podstawowe procedury tworzenia takich usług zostały omówione w [temacie How to: Użyj konfiguracji, aby dodać punkt końcowy](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md) ASP.NET AJAX i [instrukcje: Dodaj punkt końcowy ASP.NET AJAX bez użycia opcji](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)Configuration.  
  
 ASP.NET AJAX obsługuje operacje wykorzystujące zlecenia HTTP POST i HTTP GET z wartością domyślną POST protokołu HTTP. Podczas tworzenia operacji, która nie ma efektów ubocznych i zwraca dane, które rzadko lub nigdy nie są zmieniane, należy zamiast tego użyć protokołu HTTP GET. Wyniki operacji pobierania mogą być buforowane, co oznacza, że wiele wywołań tej samej operacji może spowodować tylko jedno żądanie do usługi. Buforowanie nie jest wykonywane przez program WCF, ale może być wykonywane na dowolnym poziomie (w przeglądarce użytkownika, na serwerze proxy i na innych poziomach). Buforowanie jest korzystne, jeśli chcesz zwiększyć wydajność usługi, ale może nie być akceptowalne, jeśli dane często ulegają zmianie lub jeśli operacja wykonuje pewne działania.  
  
 Na przykład w przypadku projektowania usługi do zarządzania biblioteką muzyczną użytkownika, operacja, która wyszukuje wykonawcę na podstawie tytułu albumu z używania GET, ale operacja, która dodaje album do osobistej kolekcji użytkownika, musi używać wpisu POST.  
  
 Aby kontrolować okres istnienia pamięci podręcznej, <xref:System.ServiceModel.Web.OutgoingWebResponseContext> należy użyć typu. Na przykład podczas projektowania usługi, która zwraca prognozy pogody, które są aktualizowane co godzinę, należy użyć funkcji GET, ale ograniczyć czas trwania pamięci podręcznej na godzinę lub mniejszą, aby uniemożliwić użytkownikom usługi dostęp do starych danych.  
  
 W przypadku korzystania z usług ze strony ASP.NET AJAX, która używa kontrolki Menedżera skryptów, nie ma żadnej różnicy niezależnie od tego, czy operacja korzysta z mechanizmu GET, czy po nim, zapewnia wydawanie prawidłowego typu żądania.  
  
 Operacje HTTP GET używają wszelkich parametrów wejściowych obsługiwanych przez operacje POST, w tym złożone typy kontraktów danych. Jednak w większości przypadków zaleca się uniknięcie zbyt wielu parametrów lub parametrów, które są zbyt złożone w operacjach pobierania, ponieważ zmniejsza to wydajność buforowania.  
  
 W tym temacie przedstawiono sposób wybierania między poleceniem get i post przez <xref:System.ServiceModel.Web.WebGetAttribute> dodanie <xref:System.ServiceModel.Web.WebInvokeAttribute> atrybutów lub do odpowiednich operacji w kontrakcie usługi. Pozostałe kroki (do wdrożenia, skonfigurowania i hostowania usługi), które są wymagane do uruchomienia usługi, są podobne do tych, które są używane przez dowolną ASP.NET AJAX usługi w programie WCF.  
  
 Operacja oznaczona przy użyciu <xref:System.ServiceModel.Web.WebGetAttribute> zawsze używa żądania GET. Operacja oznaczona przy użyciu <xref:System.ServiceModel.Web.WebInvokeAttribute>elementu lub nie jest oznaczona z żadnym z tych dwóch atrybutów, używa żądania post. Umożliwia korzystanie z innych czasowników HTTP, innych niż get i post (takich jak Put i Delete) <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> za pośrednictwem właściwości. <xref:System.ServiceModel.Web.WebInvokeAttribute> Jednak te czasowniki nie są obsługiwane przez ASP.NET AJAX. Jeśli zamierzasz używać usługi ze stron ASP.NET przy użyciu formantu Menedżera skryptów, nie używaj <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> właściwości.  
  
 Aby zapoznać się z przykładowym przełączaniem do pobrania, zobacz [podstawowe przykładowe usługi AJAX](../../../../docs/framework/wcf/samples/basic-ajax-service.md) .  
  
 Aby zapoznać się z przykładem korzystającym z funkcji POST, zapoznaj się z [usługą AJAX przy użyciu przykładu http post](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md) .  
  
## <a name="to-create-a-wcf-service-that-responds-to-http-get-or-http-post-requests"></a>Aby utworzyć usługę WCF, która odpowiada na żądania HTTP GET lub HTTP POST
  
1. Zdefiniuj podstawową umowę usługi WCF z interfejsem oznaczonym przy użyciu <xref:System.ServiceModel.ServiceContractAttribute> atrybutu. Oznacz każdą operację za pomocą <xref:System.ServiceModel.OperationContractAttribute>. <xref:System.ServiceModel.Web.WebGetAttribute> Dodaj atrybut, aby określić, że operacja powinna odpowiedzieć na żądania HTTP GET. Można również dodać <xref:System.ServiceModel.Web.WebInvokeAttribute> atrybut, aby jawnie określić wpis http, lub nie określić atrybutu, który domyślnie przyjmuje wartość http post.
  
    ```csharp
    [ServiceContract]  
    public interface IMusicService  
    {  
        //This operation uses a GET method.  
        [OperationContract]  
        [WebGet]  
        string LookUpArtist(string album);  
  
        //This operation will use a POST method.  
        [OperationContract]  
        [WebInvoke]  
        void AddAlbum(string user, string album);  
  
        //This operation will use POST method by default  
        //since nothing else is explicitly specified.  
        [OperationContract]  
        string[] GetAlbums(string user);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2. Zaimplementuj kontrakt `MusicService` `IMusicService` usługi za pomocą.
  
    ```csharp
    public class MusicService : IMusicService  
    {  
        public void AddAlbum(string user, string album)  
        {  
            //Add implementation here.  
        }  
  
         //Other operations omitted…  
    }  
    ```  
  
3. Utwórz nowy plik o nazwie usługa z rozszerzeniem SVC w aplikacji. Edytuj ten plik, dodając odpowiednie [ \@](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) informacje o dyrektywie ServiceHost dla usługi. Określ, że <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> ma być używana [ \@w dyrektywie ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) , aby automatycznie konfigurować punkt końcowy ASP.NET AJAX.  
  
    ```
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.MusicService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
## <a name="to-call-the-service"></a>Aby wywołać usługę  
  
1. Możesz testować operacje pobrania usługi bez kodu klienta, korzystając z przeglądarki. Na przykład jeśli skonfigurowano usługę pod `http://example.com/service.svc` adresem, nastąpi `http://example.com/service.svc/LookUpArtist?album=SomeAlbum` ponowne wprowadzenie do paska adresu przeglądarki i spowoduje, że odpowiedź zostanie pobrana lub wyświetlona.
  
2. Usługi można używać w taki sam sposób jak inne usługi ASP.NET AJAX, wprowadzając adres URL usługi do kolekcji scripts formantu ASP.NET AJAX Script Manager. Aby zapoznać się z przykładem, zobacz [podstawową usługę AJAX](../../../../docs/framework/wcf/samples/basic-ajax-service.md).
  
## <a name="see-also"></a>Zobacz także

- [Tworzenie usług WCF w technologii AJAX na platformie ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)
- [Instrukcje: Migrowanie usług sieci Web ASP.NET z obsługą technologii AJAX do programu WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)
