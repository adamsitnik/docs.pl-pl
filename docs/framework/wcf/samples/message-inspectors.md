---
title: Inspektorzy komunikatów
ms.date: 03/30/2017
ms.assetid: 9bd1f305-ad03-4dd7-971f-fa1014b97c9b
ms.openlocfilehash: 01553084aa049688cd05fa36e46fb6f67983fb21
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73424150"
---
# <a name="message-inspectors"></a>Inspektorzy komunikatów
W tym przykładzie przedstawiono sposób wdrażania i konfigurowania inspektorów komunikatów klienta i usługi.  
  
 Inspektor komunikatów jest obiektem rozszerzalności, który może być używany w środowisku uruchomieniowym klienta i w środowisku uruchomieniowym w ramach usługi lub przez konfigurację oraz który może sprawdzać i modyfikować komunikaty po ich otrzymaniu lub przed wysłaniem.  
  
 Ten przykład służy do implementowania podstawowego mechanizmu sprawdzania poprawności komunikatów klienta i usługi, który weryfikuje komunikaty przychodzące względem zestawu konfigurowalnych dokumentów schematu XML. Należy zauważyć, że ten przykład nie sprawdza poprawności komunikatów dla każdej operacji. Jest to celowe uproszczenie.  
  
## <a name="message-inspector"></a>Inspektor komunikatów  
 Inspektorzy komunikatów klienta implementują interfejs <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> i inspektorów komunikatów usługi implementują interfejs <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector>. Implementacje mogą być połączone w jedną klasę, aby utworzyć inspektora komunikatów, który działa po obu stronach. Ten przykład implementuje ten połączony Inspektor komunikatów. Inspektor jest zbudowany w zestawie schematów, do których są sprawdzane komunikaty przychodzące i wychodzące, i umożliwia deweloperom określenie, czy wiadomości przychodzące lub wychodzące są weryfikowane oraz czy inspektor znajduje się w trybie wysyłania lub klienta, który ma wpływ na obsługę błędów, jak opisano w dalszej części tego tematu.  
  
```csharp  
public class SchemaValidationMessageInspector : IClientMessageInspector, IDispatchMessageInspector  
{  
    XmlSchemaSet schemaSet;  
    bool validateRequest;  
    bool validateReply;  
    bool isClientSide;  
    [ThreadStatic]  
    bool isRequest;  
  
    public SchemaValidationMessageInspector(XmlSchemaSet schemaSet,  
         bool validateRequest, bool validateReply, bool isClientSide)  
    {  
        this.schemaSet = schemaSet;  
        this.validateReply = validateReply;  
        this.validateRequest = validateRequest;  
        this.isClientSide = isClientSide;  
    }  
```  
  
 Każdy inspektor komunikatów usługi (dyspozytora) musi zaimplementować dwie <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector> metody <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A> i <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%28System.ServiceModel.Channels.Message%40%2CSystem.Object%29>.  
  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A> jest wywoływany przez dyspozytora, gdy otrzyma komunikat, przetworzony przez stos kanału i przypisany do usługi, ale zanim zostanie on rozszeregowany i wysłany do operacji. Jeśli komunikat przychodzący został zaszyfrowany, komunikat jest już odszyfrowany, gdy dociera do Inspektora komunikatów. Metoda pobiera `request` komunikat przekazaną jako parametr referencyjny, który umożliwia kontrolowanie, manipulowanie lub zamienienie komunikatu w miarę potrzeb. Wartością zwracaną może być dowolny obiekt i jest używany jako obiekt stanu korelacji, który jest przesyłany do <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%2A>, gdy usługa zwróci odpowiedź do bieżącej wiadomości. W tym przykładzie <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A> deleguje inspekcję (walidację) wiadomości do prywatnej, lokalnej metody `ValidateMessageBody` i nie zwraca obiektu stanu korelacji. Ta metoda zapewnia, że żadne nieprawidłowe komunikaty nie są przekazywane do usługi.  
  
```csharp  
object IDispatchMessageInspector.AfterReceiveRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel, System.ServiceModel.InstanceContext instanceContext)  
{  
    if (validateRequest)  
    {  
        // inspect the message. If a validation error occurs,  
        // the thrown fault exception bubbles up.  
        ValidateMessageBody(ref request, true);  
    }  
    return null;  
}  
```  
  
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%28System.ServiceModel.Channels.Message%40%2CSystem.Object%29> jest wywoływana za każdym razem, gdy odpowiedź jest gotowa do wysłania do klienta lub w przypadku komunikatów jednokierunkowych, gdy komunikat przychodzący został przetworzony. Pozwala to na stosowanie rozszerzeń w sposób symetryczny, niezależnie od unikatowy MEP. Podobnie jak w przypadku <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>, komunikat jest przenoszona jako parametr odwołania i może być sprawdzany, modyfikowany lub zastępowany. Sprawdzanie poprawności komunikatu wykonywanego w tym przykładzie jest ponownie delegowane do metody `ValidMessageBody`, ale obsługa błędów walidacji jest nieco inna w tym przypadku.  
  
 W przypadku wystąpienia w usłudze błędu sprawdzania poprawności metoda `ValidateMessageBody` zgłasza wyjątki pochodne <xref:System.ServiceModel.FaultException>. W <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.AfterReceiveRequest%2A>te wyjątki można umieścić w infrastrukturze modelu usług, gdzie są one automatycznie przekształcane w błędy protokołu SOAP i przekazywane do klienta. W <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector.BeforeSendReply%2A>, <xref:System.ServiceModel.FaultException> wyjątki nie mogą być umieszczane w infrastrukturze, ponieważ przekształcenie wyjątków błędów zgłaszanych przez usługę występuje przed wywołaniem inspektora komunikatów. W związku z tym Następująca implementacja przechwytuje znany wyjątek `ReplyValidationFault` i zastępuje komunikat odpowiedzi z jawnym komunikatem o błędzie. Dzięki tej metodzie implementacja usługi nie zwraca żadnych nieprawidłowych komunikatów.  
  
```csharp  
void IDispatchMessageInspector.BeforeSendReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
{  
    if (validateReply)  
    {  
        // Inspect the reply, catch a possible validation error   
        try  
        {  
            ValidateMessageBody(ref reply, false);  
        }  
        catch (ReplyValidationFault fault)  
        {  
            // if a validation error occurred, the message is replaced  
            // with the validation fault.  
            reply = Message.CreateMessage(reply.Version,   
                    fault.CreateMessageFault(), reply.Headers.Action);  
        }  
    }  
```  
  
 Inspektor komunikatów klienta jest bardzo podobny. Dwie metody, które muszą być zaimplementowane z <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> są <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.AfterReceiveReply%2A> i <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A>.  
  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A> jest wywoływana, gdy wiadomość została złożona przez aplikację kliencką lub przez program formatujący operacje. Podobnie jak w przypadku inspektorów komunikatów dyspozytora, komunikat można tylko sprawdzić lub całkowicie zastąpić. W tym przykładzie Inspektor delegowany do tej samej metody pomocnika lokalnego `ValidateMessageBody`, która również jest używana dla inspektorów komunikatów wysyłania.  
  
 Różnica w zachowaniu między walidacją klienta i usługi (zgodnie z definicją w konstruktorze) polega na tym, że Walidacja klienta zgłasza wyjątki lokalne, które są umieszczane w kodzie użytkownika, ponieważ są one wykonywane lokalnie, a nie z powodu błędu usługi. Ogólnie rzecz biorąc, reguła jest taka, że inspektorzy dyspozytorów usługi zgłaszają błędy i inspektorzy klienta zgłaszają wyjątki.  
  
 Ta <xref:System.ServiceModel.Dispatcher.IClientMessageInspector.BeforeSendRequest%2A> implementacja gwarantuje, że do usługi nie są wysyłane żadne nieprawidłowe komunikaty.  
  
```csharp  
object IClientMessageInspector.BeforeSendRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel)  
{  
    if (validateRequest)  
    {  
        ValidateMessageBody(ref request, true);  
    }  
    return null;  
}  
```  
  
 Implementacja `AfterReceiveReply` gwarantuje, że żadne nieprawidłowe komunikaty odebrane z usługi nie są przekazywane do kodu użytkownika klienta.  
  
```csharp  
void IClientMessageInspector.AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
{  
    if (validateReply)  
    {  
        ValidateMessageBody(ref reply, false);  
    }  
}  
```  
  
 Tym konkretnym inspektorem komunikatów jest metoda `ValidateMessageBody`. Aby wykonać swoją prace, zawija walidację <xref:System.Xml.XmlReader> wokół poddrzewa zawartości treści przesłanego komunikatu. Czytnik jest wypełniany zestawem schematów, które znajdują się w Inspektorze komunikatów, a wywołanie zwrotne walidacji jest ustawione na delegata odwołujący się do `InspectionValidationHandler` zdefiniowanego obok tej metody. Aby przeprowadzić walidację, komunikat jest odczytywany i umieszczany w buforze do <xref:System.Xml.XmlDictionaryWriter>kopii zapasowej w strumieniu pamięci. Jeśli w procesie wystąpi błąd lub ostrzeżenie z walidacją, wywoływana jest metoda wywołania zwrotnego.  
  
 Jeśli wystąpi błąd, tworzony jest nowy komunikat, który kopiuje właściwości i nagłówki z oryginalnej wiadomości i używa teraz zweryfikowanych sprawdzonych w strumieniu pamięci, które są opakowane przez <xref:System.Xml.XmlDictionaryReader> i dodawane do komunikatu zastępczego.  
  
```csharp  
void ValidateMessageBody(ref System.ServiceModel.Channels.Message message, bool isRequest)  
{  
    if (!message.IsFault)  
    {  
        XmlDictionaryReaderQuotas quotas =   
                new XmlDictionaryReaderQuotas();  
        XmlReader bodyReader =   
            message.GetReaderAtBodyContents().ReadSubtree();  
        XmlReaderSettings wrapperSettings =   
                              new XmlReaderSettings();  
        wrapperSettings.CloseInput = true;  
        wrapperSettings.Schemas = schemaSet;  
        wrapperSettings.ValidationFlags =   
                                XmlSchemaValidationFlags.None;  
        wrapperSettings.ValidationType = ValidationType.Schema;  
        wrapperSettings.ValidationEventHandler += new   
           ValidationEventHandler(InspectionValidationHandler);  
        XmlReader wrappedReader = XmlReader.Create(bodyReader,   
                                            wrapperSettings);  
  
        // pull body into a memory backed writer to validate  
        this.isRequest = isRequest;  
        MemoryStream memStream = new MemoryStream();  
        XmlDictionaryWriter xdw =  
              XmlDictionaryWriter.CreateBinaryWriter(memStream);  
        xdw.WriteNode(wrappedReader, false);  
        xdw.Flush(); memStream.Position = 0;  
        XmlDictionaryReader xdr =   
        XmlDictionaryReader.CreateBinaryReader(memStream, quotas);  
  
        // reconstruct the message with the validated body  
        Message replacedMessage =   
            Message.CreateMessage(message.Version, null, xdr);  
        replacedMessage.Headers.CopyHeadersFrom(message.Headers);  
        replacedMessage.Properties.CopyProperties(message.Properties);  
        message = replacedMessage;  
    }  
}  
```  
  
 Metoda `InspectionValidationHandler` jest wywoływana przez walidację <xref:System.Xml.XmlReader> za każdym razem, gdy wystąpi błąd walidacji schematu lub ostrzeżenie. Następująca implementacja działa tylko z błędami i ignoruje wszystkie ostrzeżenia.  
  
 Przy pierwszym rozważaniu może być możliwe wstrzyknięcie <xref:System.Xml.XmlReader> weryfikacji do wiadomości za pomocą Inspektora komunikatów i przeprowadzenie walidacji, gdy komunikat jest przetwarzany i bez buforowania komunikatu. Oznacza to jednak, że to wywołanie zwrotne zgłasza wyjątki walidacji w infrastrukturze modelu usług lub w kodzie użytkownika, ponieważ wykryto nieprawidłowe węzły XML, co skutkuje nieprzewidywalnym zachowaniem. Metoda buforowania umożliwia ochronę kodu użytkownika przed nieprawidłowymi komunikatami.  
  
 Jak wspomniano wcześniej, wyjątki zgłoszone przez program obsługi różnią się między klientem a usługą. W ramach usługi wyjątki są wyprowadzane z <xref:System.ServiceModel.FaultException>, na kliencie wyjątki są regularnie wyjątkami niestandardowymi.  
  
```csharp  
        void InspectionValidationHandler(object sender, ValidationEventArgs e)  
{  
    if (e.Severity == XmlSeverityType.Error)  
    {  
        // We are treating client and service side validation errors  
        // differently here. Client side errors cause exceptions  
        // and are thrown straight up to the user code. Service side  
        // validations cause faults.  
        if (isClientSide)  
        {  
            if (isRequest)  
            {  
                throw new RequestClientValidationException(e.Message);  
            }  
            else  
            {  
                throw new ReplyClientValidationException(e.Message);  
            }  
        }  
        else  
        {  
            if (isRequest)  
            {  
                // this fault is caught by the ServiceModel   
                // infrastructure and turned into a fault reply.  
                throw new RequestValidationFault(e.Message);  
             }  
             else  
             {  
                // this fault is caught and turned into a fault message  
                // in BeforeSendReply in this class  
                throw new ReplyValidationFault(e.Message);  
              }  
          }  
      }  
    }  
```  
  
## <a name="behavior"></a>Zachowanie  
 Inspektorzy komunikatów są rozszerzeniami środowiska uruchomieniowego klienta lub środowiska uruchomieniowego wysyłania. Takie rozszerzenia są konfigurowane przy użyciu *zachowań*. Zachowanie jest klasą, która zmienia zachowanie środowiska uruchomieniowego modelu usług, zmieniając domyślną konfigurację lub dodając do niej rozszerzenia (na przykład inspektorów komunikatów).  
  
 Poniższa klasa `SchemaValidationBehavior` jest zachowaniem używanym do dodawania inspektora komunikatów tego przykładu do klienta lub środowiska uruchomieniowego wysyłania. Implementacja jest raczej podstawowa w obu przypadkach. W <xref:System.ServiceModel.Description.IEndpointBehavior.ApplyClientBehavior%2A> i <xref:System.ServiceModel.Description.IEndpointBehavior.ApplyDispatchBehavior%2A>Inspektor komunikatów jest tworzony i dodawany do <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> kolekcji odpowiedniego środowiska uruchomieniowego.  
  
```csharp  
public class SchemaValidationBehavior : IEndpointBehavior  
{  
    XmlSchemaSet schemaSet;   
    bool validateRequest;   
    bool validateReply;  
  
    public SchemaValidationBehavior(XmlSchemaSet schemaSet, bool   
                           inspectRequest, bool inspectReply)  
    {  
        this.schemaSet = schemaSet;  
        this.validateReply = inspectReply;  
        this.validateRequest = inspectRequest;  
    }  
    #region IEndpointBehavior Members  
  
    public void AddBindingParameters(ServiceEndpoint endpoint,   
       System.ServiceModel.Channels.BindingParameterCollection   
                                            bindingParameters)  
    {  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint,   
            System.ServiceModel.Dispatcher.ClientRuntime clientRuntime)  
    {  
        SchemaValidationMessageInspector inspector =   
           new SchemaValidationMessageInspector(schemaSet,   
                      validateRequest, validateReply, true);  
            clientRuntime.MessageInspectors.Add(inspector);  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint,   
         System.ServiceModel.Dispatcher.EndpointDispatcher   
                                          endpointDispatcher)  
    {  
        SchemaValidationMessageInspector inspector =   
           new SchemaValidationMessageInspector(schemaSet,   
                        validateRequest, validateReply, false);  
   endpointDispatcher.DispatchRuntime.MessageInspectors.Add(inspector);  
    }  
  
   public void Validate(ServiceEndpoint endpoint)  
   {  
   }  
  
    #endregion  
}  
```  
  
> [!NOTE]
> To konkretne zachowanie nie jest podwójne jako atrybut i dlatego nie można go dodać deklaratywnie do typu kontraktu typu usługi. Jest to podjęcie decyzji o projekcie, ponieważ kolekcja schematów nie może zostać załadowana w deklaracji atrybutu i odwołująca się do dodatkowej lokalizacji konfiguracji (na przykład ustawienia aplikacji) w tym atrybucie oznacza tworzenie elementu konfiguracji, który nie jest spójny z pozostałą częścią konfiguracji modelu usług. W związku z tym takie zachowanie można dodać wyłącznie za pomocą kodu i rozszerzenia konfiguracji modelu usług.  
  
## <a name="adding-the-message-inspector-through-configuration"></a>Dodawanie inspektora komunikatów za pomocą konfiguracji  
 W przypadku konfigurowania zachowania niestandardowego w punkcie końcowym w pliku konfiguracji aplikacji model usługi wymaga realizatorów do utworzenia *elementu rozszerzenia* konfiguracji reprezentowanego przez klasę pochodną <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>. To rozszerzenie należy dodać do sekcji konfiguracyjnej modelu usługi dla rozszerzeń, jak pokazano na poniższym rozszerzeniu opisanym w tej sekcji.  
  
```xml  
<system.serviceModel>  
…  
   <extensions>  
      <behaviorExtensions>  
        <add name="schemaValidator" type="Microsoft.ServiceModel.Samples.SchemaValidationBehaviorExtensionElement, MessageInspectors, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
      </behaviorExtensions>  
    </extensions>  
…  
</system.serviceModel>  
```  
  
 Rozszerzenia można dodać w pliku konfiguracji aplikacji lub ASP.NET, który jest najbardziej typowym wyborem lub w pliku konfiguracyjnym komputera.  
  
 Po dodaniu rozszerzenia do zakresu konfiguracji zachowanie można dodać do konfiguracji zachowania, tak jak pokazano w poniższym kodzie. Konfiguracje zachowań są elementami wielokrotnego użytku, które można zastosować do wielu punktów końcowych zgodnie z wymaganiami. Ponieważ określone zachowanie należy skonfigurować tutaj implementuje <xref:System.ServiceModel.Description.IEndpointBehavior>, jest ono prawidłowe tylko w odpowiedniej sekcji konfiguracji w pliku konfiguracyjnym.  
  
```xml  
<system.serviceModel>  
   <behaviors>  
      …  
     <endpointBehaviors>  
        <behavior name="HelloServiceEndpointBehavior">  
          <schemaValidator validateRequest="True" validateReply="True">  
            <schemas>  
              <add location="messages.xsd" />    
            </schemas>  
          </schemaValidator>  
        </behavior>  
      </endpointBehaviors>  
      …  
    </behaviors>  
</system.serviceModel>  
```  
  
 Element `<schemaValidator>`, który konfiguruje inspektora komunikatów, jest obsługiwany przez klasę `SchemaValidationBehaviorExtensionElement`. Klasa uwidacznia dwie właściwości publiczne Boolean o nazwie `ValidateRequest` i `ValidateReply`. Oba te elementy są oznaczone <xref:System.Configuration.ConfigurationPropertyAttribute>. Ten atrybut stanowi połączenie między właściwościami kodu i atrybutami XML, które mogą być widoczne w poprzednim elemencie konfiguracji XML. Klasa ma również właściwość `Schemas`, która jest dodatkowo oznaczona <xref:System.Configuration.ConfigurationCollectionAttribute> i jest typu `SchemaCollection`, który jest również częścią tego przykładu, ale pominięto w tym dokumencie dla zwięzłości. Ta właściwość wraz z kolekcją i klasą elementów kolekcji `SchemaConfigElement` kopię zapasową elementu `<schemas>` w poprzednim fragmencie konfiguracji i umożliwia dodanie kolekcji schematów do zestawu walidacji.  
  
 Zastąpiona metoda `CreateBehavior` przekształca dane konfiguracji w obiekt zachowań, gdy środowisko uruchomieniowe szacuje dane konfiguracyjne podczas kompilacji klienta lub punktu końcowego.  
  
```csharp  
public class SchemaValidationBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public SchemaValidationBehaviorExtensionElement()  
    {  
    }  
  
    public override Type BehaviorType   
    {   
        get  
        {  
            return typeof(SchemaValidationBehavior);  
        }   
    }  
  
    protected override object CreateBehavior()  
    {  
        XmlSchemaSet schemaSet = new XmlSchemaSet();  
        foreach (SchemaConfigElement schemaCfg in this.Schemas)  
        {  
            Uri baseSchema = new   
                Uri(AppDomain.CurrentDomain.BaseDirectory);  
            string location = new   
                Uri(baseSchema,schemaCfg.Location).ToString();  
            XmlSchema schema =   
                XmlSchema.Read(new XmlTextReader(location), null);  
            schemaSet.Add(schema);  
        }  
     return new   
     SchemaValidationBehavior(schemaSet,ValidateRequest,ValidateReply);  
    }  
  
[ConfigurationProperty("validateRequest",DefaultValue=false,IsRequired=false)]  
public bool ValidateRequest  
{  
    get { return (bool)base["validateRequest"]; }  
    set { base["validateRequest"] = value; }  
}  
  
[ConfigurationProperty("validateReply", DefaultValue = false, IsRequired = false)]  
        public bool ValidateReply  
        {  
            get { return (bool)base["validateReply"]; }  
            set { base["validateReply"] = value; }  
        }  
  
     //Declare the Schema collection property.  
     //Note: the "IsDefaultCollection = false" instructs   
     //.NET Framework to build a nested section of   
     //the kind <Schema> ...</Schema>.  
    [ConfigurationProperty("schemas", IsDefaultCollection = true)]  
    [ConfigurationCollection(typeof(SchemasCollection),  
        AddItemName = "add",  
        ClearItemsName = "clear",  
        RemoveItemName = "remove")]  
    public SchemasCollection Schemas  
    {  
        get  
        {  
            SchemasCollection SchemasCollection =  
            (SchemasCollection)base["schemas"];  
            return SchemasCollection;  
        }  
    }  
}  
```  
  
## <a name="adding-message-inspectors-imperatively"></a>Bezwzględne Dodawanie inspektorów komunikatów  
 Oprócz atrybutów, które nie są obsługiwane w tym przykładzie z powodu podanej wcześniej przyczyny) i konfiguracji, zachowania można łatwo dodać do środowiska uruchomieniowego klienta i usługi przy użyciu własnego kodu. W tym przykładzie jest to wykonywane w aplikacji klienckiej w celu przetestowania inspektora komunikatów klienta. Klasa `GenericClient` pochodzi od <xref:System.ServiceModel.ClientBase%601>, która uwidacznia konfigurację punktu końcowego w kodzie użytkownika. Przed niejawnie otwartym klientem można zmienić konfigurację punktu końcowego, na przykład przez dodanie zachowań, jak pokazano w poniższym kodzie. Dodanie zachowania usługi jest w dużym stopniu odpowiednikiem techniki klienta pokazanej w tym miejscu i musi zostać wykonane przed otwarciem hosta usługi.  
  
```csharp  
try  
{  
    Console.WriteLine("*** Call 'Hello' with generic client, with client behavior");  
    GenericClient client = new GenericClient();  
  
    // Configure client programmatically, adding behavior  
    XmlSchema schema = XmlSchema.Read(new StreamReader("messages.xsd"),   
                                                          null);  
    XmlSchemaSet schemaSet = new XmlSchemaSet();  
    schemaSet.Add(schema);  
    client.Endpoint.Behaviors.Add(new   
                SchemaValidationBehavior(schemaSet, true, true));  
  
    Console.WriteLine("--- Sending valid client request:");  
    GenericCallValid(client, helloAction);  
    Console.WriteLine("--- Sending invalid client request:");  
    GenericCallInvalid(client, helloAction);  
  
    client.Close();  
}  
catch (Exception e)  
{  
    DumpException(e);  
}  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład  
  
1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Aby skompilować rozwiązanie, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3. Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , aby pobrać wszystkie próbki Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)]. Ten przykład znajduje się w następującym katalogu.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageInspectors`  
