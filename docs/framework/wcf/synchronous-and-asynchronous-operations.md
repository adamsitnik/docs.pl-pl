---
title: Operacje synchroniczne i asynchroniczne
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], synchronous operations
- service contracts [WCF], asynchronous operations
ms.assetid: db8a51cb-67e6-411b-9035-e5821ed350c9
ms.openlocfilehash: 61dfa257676d6c274d846300c7ccae75a219cf4c
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73424896"
---
# <a name="synchronous-and-asynchronous-operations"></a>Operacje synchroniczne i asynchroniczne
W tym temacie omówiono implementowanie i wywoływanie asynchronicznych operacji usługi.  
  
 Wiele aplikacji wywołuje metody asynchronicznie, ponieważ umożliwia aplikacjom kontynuowanie pracy przydatnej podczas wywołania metody. Usługi Windows Communication Foundation (WCF) i klienci mogą uczestniczyć w asynchronicznych wywołaniach operacji na dwóch odrębnych poziomach aplikacji, co zapewnia aplikacjom WCF jeszcze większą elastyczność w celu zmaksymalizowania równowagi przepływności w odniesieniu do współdziałania .  
  
## <a name="types-of-asynchronous-operations"></a>Typy operacji asynchronicznych  
 Wszystkie kontrakty usługi w programie WCF, niezależnie od typów parametrów i zwracanych wartości, używają atrybutów programu WCF w celu określenia określonego wzorca komunikatów między klientem i usługą. Funkcja WCF automatycznie kieruje komunikaty przychodzące i wychodzące do odpowiedniej operacji usługi lub uruchamia kod klienta.  
  
 Klient posiada tylko kontrakt usługi, który określa wzorzec wymiany komunikatów dla określonej operacji. Klienci mogą oferować deweloperom dowolny model programistyczny, który wybiera, tak długo, jak jest przestrzegany wzorzec wymiany komunikatów. Dzięki temu usługi mogą również implementować operacje w dowolny sposób, tak długo, jak jest zaobserwowany określony wzorzec komunikatu.  
  
 Niezależność kontraktu usługi z implementacji usługi lub klienta umożliwia następujące formy wykonywania asynchronicznego w aplikacjach WCF:  
  
- Klienci mogą asynchronicznie wywoływać operacje żądania/odpowiedzi przy użyciu synchronicznej wymiany komunikatów.  
  
- Usługi mogą asynchronicznie zaimplementować operację żądania/odpowiedzi przy użyciu synchronicznej wymiany komunikatów.  
  
- Wymiana komunikatów może być jednokierunkowa niezależnie od implementacji klienta lub usługi.  
  
### <a name="suggested-asynchronous-scenarios"></a>Sugerowane scenariusze asynchroniczne  
 Użyj metody asynchronicznej w implementacji operacji usługi, jeśli implementacja usługi operacji powoduje wywołanie blokujące, takie jak wykonywanie operacji we/wy. Gdy jesteś w implementacji operacji asynchronicznej, spróbuj wywołać asynchroniczne operacje i metody, aby w miarę możliwości rozciągnąć asynchroniczną ścieżkę wywołania. Na przykład Wywołaj `BeginOperationTwo()` z poziomu `BeginOperationOne()`.  
  
- Użycie asynchronicznej metody w kliencie lub wywoływanie aplikacji w następujących przypadkach:  
  
- Jeśli wywołujesz operacje z aplikacji warstwy środkowej. (Aby uzyskać więcej informacji na temat takich scenariuszy, zobacz [aplikacje klienckie warstwy środkowej](./feature-details/middle-tier-client-applications.md)).  
  
- Jeśli wywołujesz operacje na stronie ASP.NET, używaj stron asynchronicznych.  
  
- Jeśli wywołujesz operacje z dowolnej aplikacji, która jest jednowątkowa, taka jak Windows Forms lub Windows Presentation Foundation (WPF). W przypadku korzystania z asynchronicznego modelu wywoływania opartego na zdarzeniach zdarzenie wynikowe jest zgłaszane w wątku interfejsu użytkownika, co umożliwia dodanie czasu odpowiedzi do aplikacji bez konieczności samodzielnego obsłużenia wielu wątków.  
  
- Ogólnie rzecz biorąc, jeśli istnieje wybór między wywołaniem synchronicznym i asynchronicznym, wybierz wywołanie asynchroniczne.  
  
### <a name="implementing-an-asynchronous-service-operation"></a>Implementowanie asynchronicznej operacji usługi  
 Operacje asynchroniczne można zaimplementować przy użyciu jednej z trzech następujących metod:  
  
1. Wzorzec asynchroniczny oparty na zadaniach  
  
2. Wzorzec asynchroniczny oparty na zdarzeniach  
  
3. Wzorzec asynchroniczny IAsyncResult  
  
#### <a name="task-based-asynchronous-pattern"></a>Wzorzec asynchroniczny oparty na zadaniach  
 Wzorzec asynchroniczny oparty na zadaniach jest preferowanym sposobem implementacji operacji asynchronicznych, ponieważ jest najłatwiejszym i najbardziej prostym do przodu. Aby użyć tej metody, wystarczy zaimplementować operację usługi i określić zwracany typ zadania\<T >, gdzie T jest typem zwracanym przez operację logiczną. Na przykład:  
  
```csharp  
public class SampleService:ISampleService   
{   
   // ...  
   public async Task<string> SampleMethodTaskAsync(string msg)   
   {   
      return Task<string>.Factory.StartNew(() =>   
      {   
         return msg;   
      });   
   }  
   // ...  
}  
```  
  
 Operacja SampleMethodTaskAsync zwraca ciąg\<zadania > ponieważ operacja logiczna zwraca ciąg. Aby uzyskać więcej informacji na temat wzorca asynchronicznego opartego na zadaniach, zobacz [wzorzec asynchroniczny oparty na zadaniach](https://go.microsoft.com/fwlink/?LinkId=232504).  
  
> [!WARNING]
> W przypadku korzystania ze wzorca asynchronicznego opartego na zadaniach T:System.AggregateException może być zgłaszane, jeśli wystąpi wyjątek podczas oczekiwania na zakończenie operacji. Ten wyjątek może wystąpić w przypadku klienta lub usług  
  
#### <a name="event-based-asynchronous-pattern"></a>Wzorzec asynchroniczny oparty na zdarzeniach  
 Usługa, która obsługuje wzorzec asynchroniczny oparty na zdarzeniach, będzie mieć co najmniej jedną operację o nazwie MethodNameAsync. Te metody mogą dublować wersje synchroniczne, które wykonują tę samą operację na bieżącym wątku. Klasa może również mieć zdarzenie MethodNameCompleted i może mieć metodę MethodNameAsyncCancel (lub po prostu CancelAsync). Klient chcący wywołać operację określi procedurę obsługi zdarzeń, która ma być wywoływana po zakończeniu operacji,  
  
 Poniższy fragment kodu ilustruje sposób deklarowania operacji asynchronicznych za pomocą wzorca asynchronicznego opartego na zdarzeniach.  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 Aby uzyskać więcej informacji na temat wzorca asynchronicznego opartego na zdarzeniach, zobacz [wzorzec asynchroniczny oparty na zdarzeniach](https://go.microsoft.com/fwlink/?LinkId=232515).  
  
#### <a name="iasyncresult-asynchronous-pattern"></a>Wzorzec asynchroniczny IAsyncResult  
 Operację usługi można zaimplementować w sposób asynchroniczny za pomocą wzorca programowania asynchronicznego .NET Framework i oznaczyć metodę `<Begin>` z właściwością <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> ustawioną na `true`. W takim przypadku operacja asynchroniczna jest uwidaczniana w metadanych w tym samym formularzu co operacja synchroniczna: jest uwidaczniana jako jedna operacja z komunikatem żądania i komunikatem skorelowanej odpowiedzi. Następnie modele programowania klientów mają wybór. Mogą one reprezentować ten wzorzec jako operację synchroniczną lub asynchronicznie, tak długo, jak w przypadku wywołania usługi do programu Exchange-odpowiedź żądania.  
  
 Ogólnie rzecz biorąc, w przypadku asynchronicznego charakteru systemów nie należy podejmować zależności od wątków.  Najbardziej niezawodnym sposobem przekazywania danych do różnych etapów przetwarzania wysyłania operacji jest korzystanie z rozszerzeń.  
  
 Aby zapoznać się z przykładem, zobacz [How to: implementowanie asynchronicznej operacji usługi](how-to-implement-an-asynchronous-service-operation.md).  
  
 Aby zdefiniować operację kontraktu `X`, która jest wykonywana asynchronicznie niezależnie od tego, jak jest wywoływana w aplikacji klienckiej:  
  
- Zdefiniuj dwie metody przy użyciu wzorca `BeginOperation` i `EndOperation`.  
  
- Metoda `BeginOperation` obejmuje parametry `in` i `ref` dla operacji i zwraca typ <xref:System.IAsyncResult>.  
  
- Metoda `EndOperation` zawiera parametr <xref:System.IAsyncResult>, a także parametry `out` i `ref` i zwraca typ zwracany operacji.  
  
 Na przykład zapoznaj się z następującą metodą.  
  
```csharp  
int DoWork(string data, ref string inout, out string outonly)  
```  
  
```vb  
Function DoWork(ByVal data As String, ByRef inout As String, _out outonly As out) As Integer  
```  
  
 W celu utworzenia operacji asynchronicznej dwie metody:  
  
```csharp  
[OperationContract(AsyncPattern=true)]
IAsyncResult BeginDoWork(string data,
                         ref string inout,
                         AsyncCallback callback,
                         object state);
int EndDoWork(ref string inout, out string outonly, IAsyncResult result);  
```  
  
```vb  
<OperationContract(AsyncPattern := True)>
Function BeginDoWork(ByVal data As String, _
                     ByRef inout As String, _
                     ByVal callback As AsyncCallback, _
                     ByVal state As Object) As IAsyncResult
Function EndDoWork(ByRef inout As String, ByRef outonly As String, ByVal result As IAsyncResult) As Integer  
```  
  
> [!NOTE]
> Atrybut <xref:System.ServiceModel.OperationContractAttribute> jest stosowany tylko do metody `BeginDoWork`. Kontrakt wynikający z jednej operacji WSDL o nazwie `DoWork`.  
  
### <a name="client-side-asynchronous-invocations"></a>Wywołania asynchroniczne po stronie klienta  
 Aplikacja kliencka programu WCF może korzystać z jednego z trzech opisanych asynchronicznie modeli wywołujących  
  
 W przypadku korzystania z modelu opartego na zadaniach, po prostu wywołaj operację za pomocą słowa kluczowego await, jak pokazano w poniższym fragmencie kodu.  
  
```csharp  
await simpleServiceClient.SampleMethodTaskAsync("hello, world");  
```  
  
 Użycie wzorca asynchronicznego opartego na zdarzeniach wymaga dodania procedury obsługi zdarzeń do odebrania powiadomienia o odpowiedzi — a zdarzenie powstałe w wątku interfejsu użytkownika jest automatycznie wywoływane. Aby użyć tej metody, określ opcje polecenia **/Async** i **/TCV: Version35** za pomocą narzędzia do [przesyłania metadanych (Svcutil. exe)](servicemodel-metadata-utility-tool-svcutil-exe.md), jak w poniższym przykładzie.  
  
```console  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async /tcv:Version35  
```  
  
 Gdy to zrobisz, program Svcutil. exe generuje klasę klienta WCF z infrastrukturą zdarzeń, która umożliwia aplikacji wywołującej wdrożenie i przypisanie procedury obsługi zdarzeń w celu otrzymania odpowiedzi i podjęcia odpowiedniej akcji. Pełny przykład można znaleźć w temacie [How to: calling Service Operations asynchronicznie](./feature-details/how-to-call-wcf-service-operations-asynchronously.md).  
  
 Jednak oparty na zdarzeniach model asynchroniczny jest dostępny tylko w [!INCLUDE[netfx35_long](../../../includes/netfx35-long-md.md)]. Ponadto nie jest to obsługiwane nawet w [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] podczas tworzenia kanału klienta WCF przy użyciu <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>. Obiekty kanału klienta WCF umożliwiają Asynchroniczne wywoływanie operacji za pomocą obiektów <xref:System.IAsyncResult?displayProperty=nameWithType>. Aby użyć tej metody, należy określić opcję polecenia **/Async** za pomocą [Narzędzia do przesyłania metadanych modelu ServiceModel (Svcutil. exe)](servicemodel-metadata-utility-tool-svcutil-exe.md), jak w poniższym przykładzie.  
  
```console  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async   
```  
  
 Spowoduje to wygenerowanie kontraktu usługi, w którym każda operacja jest modelowana jako metoda `<Begin>` z właściwością <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> ustawioną na `true` i odpowiadającą jej `<End>`ą metodę. Aby zapoznać się z kompletnym przykładem przy użyciu <xref:System.ServiceModel.ChannelFactory%601>, zobacz [How to: Call operacje asynchronicznie przy użyciu fabryki kanałów](./feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md).  
  
 W obu przypadkach aplikacje mogą wywoływać operację asynchronicznie nawet wtedy, gdy usługa jest zaimplementowana synchronicznie, w taki sam sposób, w jaki aplikacja może używać tego samego wzorca do wywołania asynchronicznej metody synchronicznej. Sposób implementacji operacji nie jest znaczący dla klienta; po nadejściu komunikatu odpowiedzi jego zawartość jest wysyłana do asynchronicznej < klienta `End` > Metoda, a klient pobiera informacje.  
  
### <a name="one-way-message-exchange-patterns"></a>Jednokierunkowe wzorce wymiany komunikatów  
 Można również utworzyć wzorzec wymiany komunikatów asynchronicznych, w którym operacje jednokierunkowe (operacje, dla których <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=nameWithType> jest `true` nie mają skorelowanej odpowiedzi) mogą być wysyłane w dowolnym kierunku przez klienta lub usługę niezależnie od drugiej strony. (W ten sposób jest stosowany wzorzec wymiany komunikatów dupleksowych z komunikatami jednokierunkowymi). W takim przypadku kontrakt usługi określa jednokierunkową wymianę komunikatów, którą każda strona może zaimplementować jako wywołania asynchroniczne lub implementacje, lub nie, zgodnie z potrzebami. Ogólnie rzecz biorąc, gdy kontrakt jest wymianą komunikatów jednokierunkowych, implementacje mogą być w znacznym stopniu asynchroniczne, ponieważ po wysłaniu wiadomości aplikacja nie czeka na odpowiedź i może kontynuować wykonywanie innych czynności.  
  
### <a name="event-based-asynchronous-clients-and-message-contracts"></a>Klientów asynchronicznych opartych na zdarzeniach i kontrakty komunikatów  
 Wskazówki dotyczące projektowania dla asynchronicznego stanu modelu opartego na zdarzeniach, które w przypadku zwrócenia więcej niż jednej wartości są zwracane jako właściwość `Result`, a pozostałe są zwracane jako właściwości w obiekcie <xref:System.EventArgs>. W związku z tym, jeśli klient Importuje metadane przy użyciu opcji poleceń asynchronicznych opartych na zdarzeniach, a operacja zwraca więcej niż jedną wartość, domyślnym obiektem <xref:System.EventArgs> zwraca jedną wartość jako właściwość `Result`, a pozostała część to właściwości @no __t-2 obiektu.  
  
 Jeśli chcesz otrzymać obiekt komunikatu jako właściwość `Result` i mieć wartości zwracane jako właściwości tego obiektu, użyj opcji polecenia **/MessageContract** . Spowoduje to wygenerowanie sygnatury, która zwraca komunikat odpowiedzi jako właściwość `Result` obiektu <xref:System.EventArgs>. Wszystkie wewnętrzne wartości zwracane są następnie właściwościami obiektu komunikat odpowiedzi.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>
- <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A>
