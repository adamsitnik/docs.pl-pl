---
title: Omówienie modelu programowania usług HTTP w sieci Web przy użyciu programu WCF
ms.date: 03/30/2017
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
ms.openlocfilehash: 8c13ad943bf4ef272c28266e12e175a0a21d5d40
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045230"
---
# <a name="wcf-web-http-programming-model-overview"></a>Omówienie modelu programowania usług HTTP w sieci Web przy użyciu programu WCF
Model programowania HTTP sieci WEB w programie Windows Communication Foundation (WCF) udostępnia podstawowe elementy wymagane do kompilowania usług HTTP sieci WEB za pomocą programu WCF. Usługi HTTP sieci WEB w programie WCF są przeznaczone do uzyskiwania dostępu do szerokiego zakresu potencjalnych klientów, w tym przeglądarek sieci Web, i mają następujące unikatowe wymagania:  
  
- **Identyfikatory URI i przetwarzanie URI** Identyfikatory URI odgrywają centralną rolę w projektowaniu usług HTTP sieci WEB. Model programowania HTTP sieci Web w programie WCF <xref:System.UriTemplate> używa <xref:System.UriTemplateTable> klas i w celu zapewnienia możliwości przetwarzania identyfikatorów URI.  
  
- **Obsługa operacji get i post** Usługi HTTP sieci WEB wykorzystują zlecenie GET do pobierania danych, a także różne czasowniki wywoływania na potrzeby modyfikacji i zdalnego wywoływania danych. Model programowania HTTP sieci Web w programie WCF <xref:System.ServiceModel.Web.WebGetAttribute> korzysta <xref:System.ServiceModel.Web.WebInvokeAttribute> z i do kojarzenia operacji usługi z usługą get i innymi zleceniami http, takimi jak Put, post i DELETE.  
  
- **Wiele formatów danych** Usługi w stylu sieci Web przetwarzają wiele rodzajów danych oprócz komunikatów SOAP. Model programowania HTTP sieci Web w programie WCF <xref:System.ServiceModel.WebHttpBinding> używa <xref:System.ServiceModel.Description.WebHttpBehavior> i do obsługi wielu różnych formatów danych, takich jak dokumenty XML, obiekt danych JSON i strumienie zawartości binarnej, takie jak obrazy, pliki wideo lub zwykły tekst.  
  
 Model programowania HTTP sieci WEB w programie WCF rozszerza zasięg programu WCF w celu uwzględnienia scenariuszy w stylu sieci Web, które obejmują internetowe usługi HTTP, usługi AJAX i JSON oraz źródła danych zespolonych (ATOM/RSS). Aby uzyskać więcej informacji na temat usług AJAX i JSON, zobacz Omówienie [integracji AJAX i notacji JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md). Aby uzyskać więcej informacji na temat zespalania, zobacz [Omówienie zespalania programu WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md).  
  
 Nie ma żadnych dodatkowych ograniczeń dotyczących typów danych, które mogą być zwracane z usługi HTTP w sieci WEB. Dowolny możliwy do serializacji typ można zwrócić z operacji usługi HTTP w sieci WEB. Ponieważ operacje usługi HTTP w sieci WEB mogą być wywoływane przez przeglądarkę sieci Web, istnieje ograniczenie, jakie typy danych można określić w adresie URL. Aby uzyskać więcej informacji na temat typów obsługiwanych domyślnie, zobacz sekcję **parametry ciągu zapytania UriTemplate i adresy URL** poniżej. Zachowanie domyślne można zmienić, dostarczając własną implementację T:System.ServiceModel.Dispatcher.QueryStringConverter, która określa sposób konwersji parametrów określonych w adresie URL do rzeczywistego typu parametru. Aby uzyskać więcej informacji, zobacz<xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
> [!CAUTION]
> Usługi z modelem programowania HTTP sieci WEB w programie WCF nie używają komunikatów protokołu SOAP. Ponieważ protokół SOAP nie jest używany, nie można używać funkcji zabezpieczeń udostępnianych przez program WCF. Można jednak korzystać z zabezpieczeń opartych na transportach przez Hostowanie usługi przy użyciu protokołu HTTPS. Aby uzyskać więcej informacji na temat zabezpieczeń WCF, zobacz [Omówienie zabezpieczeń](../../../../docs/framework/wcf/feature-details/security-overview.md)  
  
> [!WARNING]
> Zainstalowanie rozszerzenia WebDAV dla usług IIS może spowodować zwrócenie błędu HTTP 405 przez usługi sieci Web, ponieważ rozszerzenie WebDAV próbuje obsłużyć wszystkie żądania PUT. Aby obejść ten problem, możesz odinstalować rozszerzenie WebDAV lub wyłączyć rozszerzenie WebDAV dla witryny sieci Web. Aby uzyskać więcej informacji, zobacz [IIS i WebDAV](https://learn.iis.net/page.aspx/357/webdav-for-iis-70/)  
  
## <a name="uri-processing-with-uritemplate-and-uritemplatetable"></a>Przetwarzanie URI przy użyciu elementu UriTemplate i UriTemplate  
 Szablony identyfikatorów URI zapewniają efektywną składnię do wyrażania dużych zestawów identyfikatorów URI zbliżonych do struktury. Na przykład następujący szablon przedstawia zestaw wszystkich trzech segmentów URI rozpoczynających się od "a" i kończy się znakiem "c" bez względu na wartość segmentu pośredniego: a/{segment}/c  
  
 Ten szablon zawiera opis identyfikatorów URI, takich jak następujące:  
  
- a/x/c  
  
- a/y/c  
  
- a/z/c  
  
- i tak dalej.  
  
 W tym szablonie notacja nawiasów klamrowych ("{segment}") wskazuje segment zmiennej zamiast wartości literału.  
  
 .NET Framework udostępnia interfejs API do pracy z szablonami identyfikatorów <xref:System.UriTemplate>URI o nazwie. `UriTemplates`umożliwia wykonywanie następujących czynności:  
  
- Można wywołać jedną z `Bind` metod z zestawem parametrów w celu utworzenia w *pełni zamkniętego identyfikatora URI* zgodnego z szablonem. Oznacza to, że wszystkie zmienne w szablonie URI są zastępowane wartościami rzeczywistymi.  
  
- Możesz wywołać `Match`() z identyfikatorem URI kandydata, który używa szablonu do podziału identyfikatora URI kandydata na jego części składowe i zwraca słownik zawierający różne części identyfikatora URI oznaczonego zgodnie ze zmiennymi w szablonie.  
  
- `Bind`() i `Match`() są odwrotnie, dzięki czemu można wywołać `Match`( `Bind`(x)) i wrócić do tego samego środowiska, które zostało uruchomione.  
  
 Istnieje wiele razy (zwłaszcza na serwerze, gdzie wysłano żądanie do operacji usługi opartej na identyfikatorze URI), które chcesz śledzić zestaw <xref:System.UriTemplate> obiektów w strukturze danych, która może niezależnie zająć się wszystkimi zawartymi przystawki. <xref:System.UriTemplateTable>reprezentuje zestaw szablonów identyfikatorów URI i wybiera najlepsze dopasowanie z uwzględnieniem zestawu szablonów i identyfikatora URI kandydata. Nie jest to powiązane z żadnym konkretnym stosem sieciowym (włączonym WCF), więc można go używać wszędzie tam, gdzie jest to konieczne.  
  
 Model usługi WCF korzysta z <xref:System.UriTemplate> i <xref:System.UriTemplateTable> do kojarzenia operacji usługi z zestawem identyfikatorów URI opisanych przez <xref:System.UriTemplate>. Operacja usługi jest skojarzona z <xref:System.UriTemplate>, przy użyciu <xref:System.ServiceModel.Web.WebGetAttribute> lub <xref:System.ServiceModel.Web.WebInvokeAttribute>. Aby uzyskać więcej informacji <xref:System.UriTemplate> na <xref:System.UriTemplateTable>temat i, zobacz [UriTemplate i UriTemplate](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)  
  
## <a name="webget-and-webinvoke-attributes"></a>Atrybuty WebGet i WebInvoke  
 Usługi HTTP sieci WEB w programie WCF wykorzystują zlecenia pobierania (na przykład HTTP GET) poza różnymi zleceniami wywołania (na przykład HTTP POST, PUT i DELETE). Model programowania HTTP sieci Web w programie WCF umożliwia deweloperom usług sterowanie zarówno szablonem identyfikatora URI, jak i zleceniem skojarzonym <xref:System.ServiceModel.Web.WebGetAttribute> z <xref:System.ServiceModel.Web.WebInvokeAttribute>ich operacjami usługi z i. <xref:System.ServiceModel.Web.WebGetAttribute> Ipozwalanakontrolowaniesposobu,wjakiposzczególneoperacjesąpowiązanezidentyfikatoramiURIimetodamihttpskojarzonymiz<xref:System.ServiceModel.Web.WebInvokeAttribute> tymi identyfikatorami URI. Na przykład dodawanie <xref:System.ServiceModel.Web.WebGetAttribute> i <xref:System.ServiceModel.Web.WebInvokeAttribute> w poniższym kodzie.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,   
                               string newName );  
}  
```  
  
 Poprzedni kod umożliwia wykonywanie następujących żądań HTTP.  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 <xref:System.ServiceModel.Web.WebInvokeAttribute>wartość domyślna to POST, ale można jej użyć również do innych zleceń.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It" -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 Aby wyświetlić pełny przykład usługi WCF korzystającej z modelu programowania HTTP sieci Web w programie WCF, zobacz [How to: Tworzenie podstawowej usługi HTTP sieci Web w programie WCF](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)  
  
## <a name="uritemplate-query-string-parameters-and-urls"></a>Parametry i adresy URL ciągu zapytania UriTemplate  
 Usługi w stylu sieci Web mogą być wywoływane z przeglądarki sieci Web, wpisując adres URL, który jest skojarzony z operacją usługi. Te operacje usługi mogą przyjmować parametry ciągu zapytania, które muszą być określone w postaci ciągu w adresie URL. W poniższej tabeli przedstawiono typy, które mogą być przesyłane w adresie URL oraz używany format.  
  
|Typ|Format|  
|----------|------------|  
|<xref:System.Byte>|0 - 255|  
|<xref:System.SByte>|-128 - 127|  
|<xref:System.Int16>|-32768 - 32767|  
|<xref:System.Int32>|-2,147,483,648 - 2,147,483,647|  
|<xref:System.Int64>|-9,223,372,036,854,775,808 - 9,223,372,036,854,775,807|  
|<xref:System.UInt16>|0 - 65535|  
|<xref:System.UInt32>|0 - 4,294,967,295|  
|<xref:System.UInt64>|0 - 18,446,744,073,709,551,615|  
|<xref:System.Single>|-3.402823 E38-3.402823 E38 (notacja wykładnika nie jest wymagana)|  
|<xref:System.Double>|-1.79769313486232 e308-1.79769313486232 e308 (notacja wykładnika nie jest wymagana)|  
|<xref:System.Char>|Dowolny pojedynczy znak|  
|<xref:System.Decimal>|Dowolna liczba dziesiętna w notacji standardowej (bez wykładnika)|  
|<xref:System.Boolean>|True lub false (bez uwzględniania wielkości liter)|  
|<xref:System.String>|Dowolny ciąg (ciąg o wartości null nie jest obsługiwany i nie są wykonywane żadne ucieczki)|  
|<xref:System.DateTime>|MM/DD/RRRR<br /><br /> MM/DD/RRRR HH: MM: SS [AM&#124;PM]<br /><br /> Rok miesiąca<br /><br /> Miesiąc dnia roku HH: MM: SS [AM&#124;.]|  
|<xref:System.TimeSpan>|DD.HH:MM:SS<br /><br /> Gdzie DD = Days, GG = godziny, MM = min, SS = sekundy|  
|<xref:System.Guid>|Identyfikator GUID, na przykład:<br /><br /> 936DA01F-9ABD-4d9d-80C7-02AF85C822A8|  
|<xref:System.DateTimeOffset>|MM/DD/RRRR HH: MM: SS MM: SS<br /><br /> Gdzie DD = Days, GG = godziny, MM = min, SS = sekundy|  
|Wyliczenia|Wartość wyliczenia na przykład, która definiuje wyliczenie, jak pokazano w poniższym kodzie.<br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> W ciągu zapytania można określić dowolne wartości wyliczeniowe (lub ich odpowiadające wartości całkowite).|  
|Typy, które mają `TypeConverterAttribute` możliwość konwersji typu do i z reprezentacji w postaci ciągu.|Zależy od konwertera typów.|  
  
## <a name="formats-and-the-wcf-web-http-programming-model"></a>Formaty i model programowania HTTP sieci WEB w programie WCF  
 Model programowania HTTP sieci WEB w programie WCF udostępnia nowe funkcje do pracy z wieloma różnymi formatami danych. W warstwie <xref:System.ServiceModel.WebHttpBinding> powiązań może odczytywać i zapisywać następujące różne rodzaje danych:  
  
- XML  
  
- JSON  
  
- Nieprzezroczyste strumienie binarne  
  
 Oznacza to, że model programowania HTTP sieci WEB w programie WCF może obsługiwać dowolny typ danych, ale może to <xref:System.IO.Stream>być programowanie w programie.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)]zapewnia obsługę danych JSON (AJAX), a także źródeł zespolonych (w tym ATOMów i RSS). Aby uzyskać więcej informacji o tych funkcjach, zobacz[Omówienie](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md) integracji z programem WCF w [sieci Web](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)i [Obsługa technologii AJAX oraz obsługi JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md).  
  
## <a name="wcf-web-http-programming-model-and-security"></a>Model programowania i zabezpieczenia protokołu HTTP w sieci WEB WCF  
 Ponieważ model programowania HTTP sieci WEB w programie WCF nie obsługuje protokołów WS-*, jedynym sposobem zabezpieczenia usługi HTTP sieci WEB w programie WCF jest udostępnienie usługi za pośrednictwem protokołu HTTPS przy użyciu protokołu SSL. Aby uzyskać więcej informacji na temat konfigurowania protokołu SSL w usługach IIS 7,0, zobacz [jak zaimplementować protokół SSL w usługach IIS](https://go.microsoft.com/fwlink/?LinkId=131613) .  
  
## <a name="troubleshooting-the-wcf-web-http-programming-model"></a>Rozwiązywanie problemów z modelem programowania HTTP sieci WEB w programie WCF  
 Podczas wywoływania usług HTTP sieci Web w programie <xref:System.ServiceModel.Channels.ChannelFactoryBase%601> WCF przy użyciu programu w celu <xref:System.ServiceModel.Description.WebHttpBehavior> utworzenia kanału <xref:System.ServiceModel.EndpointAddress> program korzysta z zestawu <xref:System.ServiceModel.EndpointAddress> w pliku konfiguracji, <xref:System.ServiceModel.Channels.ChannelFactoryBase%601>nawet jeśli do.  
  
## <a name="see-also"></a>Zobacz także

- [Syndykacja programu WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)
- [Model obiektowy programowania protokołu HTTP sieci Web w programie WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)
- [Model programowania protokołu HTTP sieci Web w programie WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
