---
title: Używanie klasy Message
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1d62bfb-2aa3-4170-b6f8-c93d3afdbbed
ms.openlocfilehash: 76ac5fad653604c7abe403def72d31696d26b547
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967845"
---
# <a name="using-the-message-class"></a>Używanie klasy Message
<xref:System.ServiceModel.Channels.Message> Klasa ma podstawowe znaczenie dla Windows Communication Foundation (WCF). Cała komunikacja między klientami i usługami ostatecznie powoduje <xref:System.ServiceModel.Channels.Message> , że wystąpienia są wysyłane i odbierane.  
  
 Zazwyczaj nie można bezpośrednio korzystać z <xref:System.ServiceModel.Channels.Message> klasy. Zamiast tego konstrukcje modelu usługi WCF, takie jak kontrakty danych, kontrakty komunikatów i kontrakty operacji, służą do opisywania komunikatów przychodzących i wychodzących. Jednak w niektórych zaawansowanych scenariuszach można bezpośrednio korzystać z <xref:System.ServiceModel.Channels.Message> klasy. Na przykład możesz chcieć użyć <xref:System.ServiceModel.Channels.Message> klasy:  
  
- Jeśli potrzebujesz alternatywnej metody tworzenia wychodzącej zawartości wiadomości (na przykład podczas tworzenia komunikatu bezpośrednio z pliku na dysku), zamiast serializacji obiektów .NET Framework.  
  
- Gdy potrzebujesz alternatywnej metody używania przychodzącej zawartości wiadomości (na przykład, gdy chcesz zastosować transformację XSLT do nieprzetworzonej zawartości XML) zamiast deserializacji do .NET Framework obiektów.  
  
- Gdy konieczne jest zaradzenie sobie z komunikatami w ogólny sposób, niezależnie od zawartości komunikatu (na przykład podczas routingu lub przekazywania komunikatów podczas kompilowania routera, równoważenia obciążenia lub systemu publikowania/subskrybowania).  
  
 Przed rozpoczęciem <xref:System.ServiceModel.Channels.Message> korzystania z klasy zapoznaj się z architekturą transferu danych w programie WCF w temacie [Omówienie architektury transfer danych](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md).  
  
 A <xref:System.ServiceModel.Channels.Message> to kontener ogólnego przeznaczenia dla danych, ale jego konstrukcja jest ściśle zgodna z projektem komunikatu w protokole SOAP. Podobnie jak w przypadku protokołu SOAP komunikat ma zarówno treść wiadomości, jak i nagłówki. Treść wiadomości zawiera rzeczywiste dane ładunku, podczas gdy nagłówki zawierają dodatkowe nazwane kontenery danych. Reguły odczytu i zapisu treści i nagłówki są różne, na przykład nagłówki są zawsze buforowane w pamięci i mogą być dostępne w dowolnej kolejności, a treść może być odczytana tylko raz i mogą być przesyłane strumieniowo. Zwykle w przypadku korzystania z protokołu SOAP treść komunikatu jest mapowana na treść protokołu SOAP, a nagłówki komunikatów są mapowane na nagłówki protokołu SOAP.  
  
## <a name="using-the-message-class-in-operations"></a>Korzystanie z klasy Message w operacjach  
 <xref:System.ServiceModel.Channels.Message> Klasy można użyć jako parametru wejściowego operacji, wartości zwracanej operacji lub obu tych elementów. Jeśli <xref:System.ServiceModel.Channels.Message> jest używany w dowolnym miejscu operacji, obowiązują następujące ograniczenia:  
  
- Operacja nie może mieć żadnych `out` parametrów `ref` ani.  
  
- Nie może istnieć więcej niż jeden `input` parametr. Jeśli parametr jest obecny, musi być komunikatem lub typem kontraktu komunikatu.  
  
- Typem zwracanym musi być albo `void` `Message`lub typ kontraktu komunikatu.  
  
 Poniższy przykład kodu zawiera prawidłowy kontrakt operacji.  
  
 [!code-csharp[C_UsingTheMessageClass#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#1)]
 [!code-vb[C_UsingTheMessageClass#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#1)]  
  
## <a name="creating-basic-messages"></a>Tworzenie podstawowych komunikatów  
 Klasa zawiera statyczne `CreateMessage` metody fabryki, których można użyć do tworzenia podstawowych komunikatów. <xref:System.ServiceModel.Channels.Message>  
  
 Wszystkie `CreateMessage` przeciążenia pobierają parametr wersji typu <xref:System.ServiceModel.Channels.MessageVersion> , który wskazuje wersje protokołu SOAP i WS-Addressing do użycia w wiadomości. Jeśli chcesz używać tych samych wersji protokołu co komunikat przychodzący, możesz użyć <xref:System.ServiceModel.OperationContext.IncomingMessageVersion%2A> właściwości <xref:System.ServiceModel.OperationContext> w wystąpieniu uzyskanym <xref:System.ServiceModel.OperationContext.Current%2A> we właściwości. Większość `CreateMessage` przeciążenia ma również parametr ciągu, który wskazuje akcję protokołu SOAP, która ma być używana dla wiadomości. Aby wyłączyć generowanie kopert protokołu `None` SOAP, można ustawić wersję programu. komunikat składa się tylko z treści.  
  
## <a name="creating-messages-from-objects"></a>Tworzenie komunikatów z obiektów  
 Najbardziej podstawowe `CreateMessage` Przeciążenie, które pobiera tylko wersję i akcję, tworzy komunikat z pustą treścią. Inne Przeciążenie pobiera dodatkowy <xref:System.Object> parametr; spowoduje to utworzenie komunikatu, którego treść jest serializowaną reprezentacją danego obiektu. <xref:System.Runtime.Serialization.DataContractSerializer> Użyj domyślnych ustawień serializacji. Jeśli chcesz użyć innego serializatora lub chcesz `DataContractSerializer` skonfigurować inaczej, `CreateMessage` Użyj `XmlObjectSerializer` przeciążenia, które również pobiera parametr.  
  
 Na przykład, aby zwrócić obiekt w komunikacie, można użyć poniższego kodu.  
  
 [!code-csharp[C_UsingTheMessageClass#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#2)]
 [!code-vb[C_UsingTheMessageClass#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#2)]  
  
## <a name="creating-messages-from-xml-readers"></a>Tworzenie komunikatów z poziomu czytników XML  
 Istnieją przeciążenia, które <xref:System.Xml.XmlReader> pobierają lub <xref:System.Xml.XmlDictionaryReader> dla treści zamiast do obiektu. `CreateMessage` W takim przypadku treść wiadomości zawiera kod XML, który wynika z odczytu z przekazaną wartość czytnika XML. Na przykład poniższy kod zwraca komunikat z zawartością treści odczytaną z pliku XML.  
  
 [!code-csharp[C_UsingTheMessageClass#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#3)]
 [!code-vb[C_UsingTheMessageClass#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#3)]  
  
 Ponadto istnieją <xref:System.Xml.XmlReader> przeciążenia, które pobierają lub <xref:System.Xml.XmlDictionaryReader> reprezentują cały komunikat, a nie tylko treść. `CreateMessage` Te przeciążenia również pobierają parametr `maxSizeOfHeaders` liczby całkowitej. Nagłówki są zawsze buforowane w pamięci, gdy tylko zostanie utworzony komunikat, a ten parametr ogranicza ilość buforu, który ma miejsce. Ważne jest, aby ustawić ten parametr na wartość bezpieczną, jeśli plik XML pochodzi z niezaufanego źródła, aby zmniejszyć prawdopodobieństwo ataku typu "odmowa usługi". Wersja protokołu SOAP i WS-Addressing wiadomości, która reprezentuje czytnik XML, musi być zgodna z wersjami wskazanymi przy użyciu parametru Version.  
  
## <a name="creating-messages-with-bodywriter"></a>Tworzenie komunikatów za pomocą BodyWriter  
 Jedno `CreateMessage` Przeciążenie`BodyWriter` Pobiera wystąpienie opisujące treść wiadomości. A `BodyWriter` jest klasą abstrakcyjną, która może być pochodną, aby dostosować sposób tworzenia treści wiadomości. Można utworzyć własną `BodyWriter` klasę pochodną do opisywania treści wiadomości w niestandardowy sposób. Należy zastąpić `BodyWriter.OnWriteBodyContents` metodę, która <xref:System.Xml.XmlDictionaryWriter>przyjmuje; ta metoda jest odpowiedzialna za napisanie treści.  
  
 Moduły zapisujące treści mogą być buforowane lub niebuforowane (przesyłane strumieniowo). Elementy zapisujące buforowanej treści mogą dowolnie wypełniać zawartość dowolnej liczby razy, podczas gdy strumieniowo mogą zapisywać zawartość tylko raz. Właściwość `IsBuffered` wskazuje, czy moduł zapisujący treści jest buforowany, czy nie. Można ustawić tę wartość dla składnika zapisywania treści przez wywołanie chronionego `BodyWriter` konstruktora, który `isBuffered` przyjmuje parametr Boolean. Moduł zapisywania treści obsługuje tworzenie zbuforowanego składnika zapisywania treści z niebuforowanego składnika zapisywania treści. Można zastąpić metodę, `OnCreateBufferedCopy` aby dostosować ten proces. Domyślnie bufor w pamięci, który zawiera kod XML zwracany przez `OnWriteBodyContents` jest używany. `OnCreateBufferedCopy`przyjmuje parametr `maxBufferSize` liczby całkowitej; w przypadku zastąpienia tej metody nie należy tworzyć buforów o rozmiarze większym niż ten maksymalny rozmiar.  
  
 `BodyWriter` `OnCreateBufferedCopy` Klasa`OnWriteBodyContents` zawiera metody`CreateBufferedCopy` i, które są zasadniczo cienkimi otokami i metodami, odpowiednio. `WriteBodyContents` Te metody wykonują sprawdzanie stanu, aby upewnić się, że nie można uzyskać dostępu do niebuforowanego składnika zapisywania treści więcej niż raz. Te metody są wywoływane bezpośrednio tylko podczas tworzenia niestandardowych `Message` klas pochodnych opartych `BodyWriters`na.  
  
## <a name="creating-fault-messages"></a>Tworzenie komunikatów o błędach  
 Do tworzenia komunikatów o `CreateMessage` błędach SOAP można użyć pewnych przeciążeń. Najbardziej podstawowe z nich <xref:System.ServiceModel.Channels.MessageFault> to obiekt, który opisuje błąd. Inne przeciążenia są udostępniane dla wygody. Pierwsze takie Przeciążenie pobiera `FaultCode` ciąg i przyczynę i `MessageFault` tworzy przy `MessageFault.CreateFault` użyciu tych informacji. Inne Przeciążenie pobiera obiekt szczegółowy, a także przekazuje go `CreateFault` wraz z kodem błędu i przyczynie. Na przykład następująca operacja zwraca błąd.  
  
 [!code-csharp[C_UsingTheMessageClass#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#4)]
 [!code-vb[C_UsingTheMessageClass#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#4)]  
  
## <a name="extracting-message-body-data"></a>Wyodrębnianie danych treści wiadomości  
 `Message` Klasa obsługuje wiele sposobów wyodrębniania informacji z jej treści. Mogą one być klasyfikowane do następujących kategorii:  
  
- Pobieranie całej treści komunikatu w jednym miejscu do składnika zapisywania XML. Jest to nazywane *pisaniem wiadomości*.  
  
- Pobieranie czytnika XML przez treść wiadomości. Dzięki temu można później uzyskać dostęp do treści wiadomości, jeśli jest to wymagane. Jest to nazywane odczytywaniem *wiadomości*.  
  
- Cała wiadomość, łącznie z jej treścią, może zostać skopiowana do buforu <xref:System.ServiceModel.Channels.MessageBuffer> w pamięci typu. Jest to nazywane kopiowaniem *wiadomości*.  
  
 Możesz uzyskać dostęp do treści `Message` tylko raz, niezależnie od tego, w jaki sposób jest on dostępny. Obiekt komunikatu ma `State` właściwość, która początkowo została ustawiona jako utworzona. Trzy metody dostępu opisane na powyższej liście ustawiają stan do zapisu, odczytu i kopiowania odpowiednio. `Close` Ponadto metoda może ustawić stan na zamknięty, gdy treść wiadomości nie jest już wymagana. Treść komunikatu może być dostępna tylko w stanie utworzonym i nie ma możliwości powrotu do stanu utworzonego po zmianie stanu.  
  
## <a name="writing-messages"></a>Pisanie wiadomości  
 Metoda zapisuje zawartość treści danego `Message` wystąpienia do danego składnika zapisywania XML. <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29> Metoda ta jest taka sama, z tą różnicą, że zawartość treści jest umieszczona w odpowiednim elemencie otoki (na`soap:body`przykład < >). <xref:System.ServiceModel.Channels.Message.WriteBody%2A> Na koniec <xref:System.ServiceModel.Channels.Message.WriteMessage%2A> zapisuje cały komunikat, włącznie z zapakowaniem koperty protokołu SOAP i nagłówkami. Jeśli protokół SOAP jest wyłączony (<xref:System.ServiceModel.Channels.Message.Version> is <xref:System.ServiceModel.Channels.MessageVersion.None?displayProperty=nameWithType>), wszystkie trzy metody wykonują te same czynności: zapisuje zawartość treści komunikatu.  
  
 Na przykład poniższy kod zapisuje treść wiadomości przychodzącej do pliku.  
  
 [!code-csharp[C_UsingTheMessageClass#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#5)]
 [!code-vb[C_UsingTheMessageClass#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#5)]  
  
 Dwie dodatkowe metody pomocnika zapisują niektóre Tagi elementu początkowego protokołu SOAP. Te metody nie uzyskują dostępu do treści wiadomości, dlatego nie zmieniają stanu komunikatu. Należą do nich następujące elementy:  
  
- <xref:System.ServiceModel.Channels.Message.WriteStartBody%2A>zapisuje element start body, na przykład `<soap:Body>`.  
  
- <xref:System.ServiceModel.Channels.Message.WriteStartEnvelope%2A>zapisuje element Start Envelope, na przykład `<soap:Envelope>`.  
  
 Aby zapisać odpowiednie Tagi elementu końcowego, wywołaj `WriteEndElement` dla odpowiedniego składnika zapisywania XML. Te metody są rzadko wywoływane bezpośrednio.  
  
## <a name="reading-messages"></a>Odczytywanie wiadomości  
 Podstawowym sposobem odczytywania treści wiadomości jest wywołanie <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>. Możesz użyć kopii zapasowej <xref:System.Xml.XmlDictionaryReader> , która pozwala odczytać treść wiadomości. Należy zauważyć, <xref:System.ServiceModel.Channels.Message> że przejścia do stanu <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> odczytu zaraz po wywołaniu jest wywoływany, a nie w przypadku używania zwróconego czytnika XML.  
  
 Metoda <xref:System.ServiceModel.Channels.Message.GetBody%2A> ta umożliwia również dostęp do treści wiadomości jako obiekt z określonym typem. Wewnętrznie, ta metoda używa `GetReaderAtBodyContents`i dlatego przechodzi stan komunikatu <xref:System.ServiceModel.Channels.MessageState.Read> do stanu (zobacz <xref:System.ServiceModel.Channels.Message.State%2A> Właściwość).  
  
 Dobrym sposobem jest sprawdzenie <xref:System.ServiceModel.Channels.Message.IsEmpty%2A> właściwości, w tym przypadku treść komunikatu jest pusta i <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A> zgłasza <xref:System.InvalidOperationException>. Ponadto, jeśli jest to odebrana wiadomość (na przykład odpowiedź), można również sprawdzić <xref:System.ServiceModel.Channels.Message.IsFault%2A>, która wskazuje, czy komunikat zawiera błąd.  
  
 Najbardziej podstawowe Przeciążenie <xref:System.ServiceModel.Channels.Message.GetBody%2A> deserializacji treści komunikatu do wystąpienia typu (wskazywanego przez parametr ogólny) <xref:System.Runtime.Serialization.DataContractSerializer> przy użyciu skonfigurowanych ustawień <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A> domyślnych i z wyłączonym limitem przydziału. Jeśli chcesz użyć innego aparatu serializacji lub skonfigurować `DataContractSerializer` program w sposób inny niż domyślny, <xref:System.ServiceModel.Channels.Message.GetBody%2A> Użyj przeciążenia, które przyjmuje <xref:System.Runtime.Serialization.XmlObjectSerializer>.  
  
 Na przykład poniższy kod wyodrębnia dane z treści wiadomości zawierającej serializowany `Person` obiekt i drukuje nazwisko osoby.  
  
 [!code-csharp[C_UsingTheMessageClass#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#6)]
 [!code-vb[C_UsingTheMessageClass#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#6)]  
  
## <a name="copying-a-message-into-a-buffer"></a>Kopiowanie wiadomości do buforu  
 Czasami konieczne jest uzyskanie dostępu do treści wiadomości więcej niż jeden raz, na przykład w celu przekazania tego samego komunikatu do wielu miejsc docelowych w ramach systemu subskrybenta wydawcy. W takim przypadku konieczne jest buforowanie całego komunikatu (w tym treści) w pamięci. Można to zrobić przez wywołanie metody <xref:System.ServiceModel.Channels.Message.CreateBufferedCopy%28System.Int32%29>. Ta metoda przyjmuje parametr liczby całkowitej, który reprezentuje maksymalny rozmiar buforu i tworzy bufor nie większy niż ten rozmiar. Ważne jest, aby ustawić tę wartość na bezpieczną, jeśli wiadomość pochodzi z niezaufanego źródła.  
  
 Bufor jest zwracany jako <xref:System.ServiceModel.Channels.MessageBuffer> wystąpienie. Dostęp do danych w buforze można uzyskać na kilka sposobów. Podstawowym sposobem jest wywołanie <xref:System.ServiceModel.Channels.Message.CreateMessage%2A> do tworzenia `Message` wystąpień z bufora.  
  
 Innym sposobem, aby uzyskać dostęp do danych w buforze, jest <xref:System.Xml.XPath.IXPathNavigable> implementacja interfejsu <xref:System.ServiceModel.Channels.MessageBuffer> , który implementuje Klasa w celu bezpośredniego dostępu do bazowego kodu XML. Niektóre <xref:System.ServiceModel.Channels.MessageBuffer.CreateNavigator%2A> przeciążenia umożliwiają tworzenie <xref:System.Xml.XPath> nawigatorów chronionych przez limit przydziału węzłów, ograniczając liczbę węzłów XML, które można odwiedzać. Pozwala to zapobiec atakom typu "odmowa usługi" na podstawie długiego czasu przetwarzania. Ta oferta jest domyślnie wyłączona. Niektóre `CreateNavigator` przeciążenia umożliwiają <xref:System.Xml.XmlSpace> określenie`XmlSpace.None`, jak biały znak ma być obsługiwany w kodzie XML przy użyciu wyliczenia, z wartością domyślną.  
  
 Końcowym sposobem uzyskiwania dostępu do zawartości bufora komunikatów jest zapisanie jej zawartości w strumieniu przy użyciu <xref:System.ServiceModel.Channels.Message.WriteMessage%2A>.  
  
 Poniższy przykład demonstruje proces pracy z `MessageBuffer`: komunikat przychodzący jest przekazywany do wielu adresatów, a następnie rejestrowany do pliku. Bez buforowania nie jest to możliwe, ponieważ treść komunikatu może być następnie dostępna tylko raz.  
  
 [!code-csharp[C_UsingTheMessageClass#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#7)]
 [!code-vb[C_UsingTheMessageClass#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#7)]  
  
 `MessageBuffer` Klasa ma inne składowe. Metodę <xref:System.ServiceModel.Channels.MessageBuffer.Close%2A> można wywołać, aby zwolnić zasoby, gdy zawartość buforu nie jest już wymagana. <xref:System.ServiceModel.Channels.MessageBuffer.BufferSize%2A> Właściwość zwraca rozmiar przydzieloną bufora. <xref:System.ServiceModel.Channels.MessageBuffer.MessageContentType%2A> Właściwość zwraca typ zawartości MIME wiadomości.  
  
## <a name="accessing-the-message-body-for-debugging"></a>Uzyskiwanie dostępu do treści wiadomości na potrzeby debugowania  
 Na potrzeby debugowania można wywołać <xref:System.ServiceModel.Channels.Message.ToString%2A> metodę, aby otrzymać reprezentację wiadomości jako ciąg. Ta reprezentacja jest zwykle zgodna ze sposobem, w jaki komunikat będzie wyglądał w sieci, jeśli został zakodowany za pomocą kodera tekstu, z tą różnicą, że kod XML będzie lepiej sformatowany do czytelności. Jedynym wyjątkiem jest treść wiadomości. Treść można odczytać tylko raz i `ToString` nie zmienia stanu komunikatu. W `ToString` związku z tym metoda może nie być w stanie uzyskać dostępu do treści i może zastąpić symbol zastępczy (na przykład "..." lub trzy kropki) zamiast treści wiadomości. W związku z tym nie `ToString` należy używać do rejestrowania komunikatów, jeśli treść wiadomości jest ważna.  
  
## <a name="accessing-other-message-parts"></a>Uzyskiwanie dostępu do innych części komunikatów  
 W celu uzyskania dostępu do informacji o komunikacie innym niż zawartość treści są udostępniane różne właściwości. Jednak tych nie można wywołać po zamknięciu wiadomości:  
  
- <xref:System.ServiceModel.Channels.Message.Headers%2A> Właściwość reprezentuje nagłówki komunikatów. Zapoznaj się z sekcją "Praca z nagłówkami" w dalszej części tego tematu.  
  
- <xref:System.ServiceModel.Channels.Message.Properties%2A> Właściwość reprezentuje właściwości komunikatu, które są fragmentami nazwanych danych dołączonymi do wiadomości, które zazwyczaj nie są emitowane podczas wysyłania komunikatu. Zapoznaj się z sekcją "Praca z właściwościami" w dalszej części tego tematu.  
  
- Właściwość wskazuje wersję protokołu SOAP i WS-Addressing skojarzoną z wiadomością lub `None` Jeśli protokół SOAP jest wyłączony. <xref:System.ServiceModel.Channels.Message.Version%2A>  
  
- Ta <xref:System.ServiceModel.Channels.Message.IsFault%2A> Właściwość zwraca `true` wartość, jeśli komunikat jest komunikatem o błędzie protokołu SOAP.  
  
- <xref:System.ServiceModel.Channels.Message.IsEmpty%2A> Właściwość zwraca`true` , jeśli komunikat jest pusty.  
  
 Można użyć metody, <xref:System.ServiceModel.Channels.Message.GetBodyAttribute%28System.String%2CSystem.String%29> Aby uzyskać dostęp do określonego atrybutu w elemencie otoki treści (na `<soap:Body>`przykład) identyfikowanego przez określoną nazwę i przestrzeń nazw. Jeśli taki atrybut nie zostanie znaleziony, `null` jest zwracany. Tę metodę można wywołać tylko wtedy, `Message` gdy jest w stanie Created (gdy treść komunikatu nie została jeszcze uzyskana).  
  
## <a name="working-with-headers"></a>Praca z nagłówkami  
 Może zawierać dowolną liczbę nazwanych fragmentów XML o nazwie *Headers.* `Message` Każdy fragment zwykle jest mapowany do nagłówka SOAP. Nagłówki są dostępne przez `Headers` właściwość typu. <xref:System.ServiceModel.Channels.MessageHeaders> <xref:System.ServiceModel.Channels.MessageHeaders>jest kolekcją <xref:System.ServiceModel.Channels.MessageHeaderInfo> obiektów i dostęp do poszczególnych nagłówków można uzyskać za pomocą jego <xref:System.Collections.IEnumerable> interfejsu lub indeksatora. Na przykład poniższy kod wyświetla listę nazw wszystkich nagłówków w `Message`.  
  
 [!code-csharp[C_UsingTheMessageClass#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#8)]
 [!code-vb[C_UsingTheMessageClass#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#8)]  
  
#### <a name="adding-removing-finding-headers"></a>Dodawanie, usuwanie i znajdowanie nagłówków  
 Można dodać nowy nagłówek na końcu wszystkich istniejących nagłówków przy użyciu <xref:System.ServiceModel.Channels.MessageHeaders.Add%2A> metody. Możesz użyć metody, <xref:System.ServiceModel.Channels.MessageHeaders.Insert%2A> aby wstawić nagłówek w określonym indeksie. Istniejące nagłówki są przesuwane dla wstawionego elementu. Nagłówki są uporządkowane według ich indeksu, a pierwszy dostępny indeks to 0. Różnych <xref:System.ServiceModel.Channels.MessageHeaders.CopyHeadersFrom%2A> przeciążeń metod można użyć do dodawania nagłówków z `MessageHeaders` innego `Message` wystąpienia. Niektóre przeciążenia kopiowania jednego pojedynczego nagłówka, podczas gdy inne kopiują wszystkie z nich. <xref:System.ServiceModel.Channels.MessageHeaders.Clear%2A> Metoda usuwa wszystkie nagłówki. <xref:System.ServiceModel.Channels.MessageHeaders.RemoveAt%2A> Metoda usuwa nagłówek w określonym indeksie (przesunięcie wszystkich nagłówków po nim). <xref:System.ServiceModel.Channels.MessageHeaders.RemoveAll%2A> Metoda usuwa wszystkie nagłówki z określoną nazwą i przestrzenią nazw.  
  
 Pobierz konkretny nagłówek przy użyciu <xref:System.ServiceModel.Channels.MessageHeaders.FindHeader%2A> metody. Ta metoda przyjmuje nazwę i przestrzeń nazw nagłówka do znalezienia i zwraca jego indeks. Jeśli nagłówek występuje więcej niż jeden raz, zgłaszany jest wyjątek. Jeśli nagłówek nie zostanie znaleziony, zwraca wartość-1.  
  
 W modelu nagłówka SOAP nagłówki mogą mieć `Actor` wartość określającą zamierzony odbiorcę nagłówka. Najbardziej podstawowe `FindHeader` Przeciążenie przeszukiwane są tylko nagłówki przeznaczone dla końcowego odbiorcy wiadomości. Jednak inne Przeciążenie pozwala określić, które `Actor` wartości są uwzględniane w wyszukiwaniu. Aby uzyskać więcej informacji, zobacz specyfikację protokołu SOAP.  
  
 Podano <xref:System.ServiceModel.Channels.MessageHeaders> metodę kopiowania nagłówków z <xref:System.ServiceModel.Channels.MessageHeaderInfo> kolekcji do tablicy obiektów. <xref:System.ServiceModel.Channels.MessageHeaders.CopyTo%28System.ServiceModel.Channels.MessageHeaderInfo%5B%5D%2CSystem.Int32%29>  
  
 Aby uzyskać dostęp do danych XML w nagłówku, można wywołać <xref:System.ServiceModel.Channels.MessageHeaders.GetReaderAtHeader%2A> i zwrócić czytnik XML dla określonego indeksu nagłówka. Jeśli chcesz zdeserializować zawartość nagłówka do obiektu, użyj <xref:System.ServiceModel.Channels.MessageHeaders.GetHeader%60%601%28System.Int32%29> lub jeden z innych przeciążeń. Najbardziej podstawowe przeciążenia deserializacji nagłówków przy użyciu <xref:System.Runtime.Serialization.DataContractSerializer> skonfigurowane w sposób domyślny. Jeśli chcesz użyć innego serializatora lub innej konfiguracji `DataContractSerializer`, użyj jednego z przeciążeń, które `XmlObjectSerializer`zajmie. Istnieją również przeciążenia, które pobierają nazwę nagłówka, przestrzeń nazw i opcjonalnie listę `Actor` wartości zamiast indeksu; jest to `FindHeader` kombinacja i `GetHeader`.  
  
## <a name="working-with-properties"></a>Praca z właściwościami  
 `Message` Wystąpienie może zawierać dowolną liczbę nazwanych obiektów dowolnego typu. Dostęp do tej kolekcji uzyskuje `Properties` się za pomocą `MessageProperties`właściwości typu. Kolekcja implementuje <xref:System.Collections.Generic.IDictionary%602> interfejs i działa jako mapowanie z <xref:System.String> do <xref:System.Object>. Zwykle wartości właściwości nie są mapowane bezpośrednio do żadnej części wiadomości w sieci, ale zamiast tego udostępniają różne wskazówki przetwarzania komunikatów do różnych kanałów w stosie kanału WCF lub <xref:System.ServiceModel.Channels.MessageHeaders.CopyTo%28System.ServiceModel.Channels.MessageHeaderInfo%5B%5D%2CSystem.Int32%29> w środowisku usługi. Aby zapoznać się z przykładem, zobacz [Omówienie architektury transfer danych](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md).  
  
## <a name="inheriting-from-the-message-class"></a>Dziedziczenie z klasy Message  
 Jeśli wbudowane typy komunikatów utworzone za pomocą `CreateMessage` nie spełniają wymagań, Utwórz klasę pochodzącą `Message` od klasy.  
  
### <a name="defining-the-message-body-contents"></a>Definiowanie zawartości treści wiadomości  
 Istnieją trzy podstawowe metody uzyskiwania dostępu do danych w treści wiadomości: zapisywanie, odczytywanie i kopiowanie do buforu. <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A>Te operacje ostatecznie powodują <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents%2A>, i <xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A> metody są wywoływane odpowiednio, w klasie `Message`pochodnej. Klasa bazowa `Message` gwarantuje, że tylko jedna z tych metod jest wywoływana dla każdego `Message` wystąpienia i nie jest wywoływana więcej niż raz. Klasa bazowa gwarantuje również, że metody nie są wywoływane na zamkniętej wiadomości. Nie ma potrzeby śledzenia stanu komunikatu w implementacji.  
  
 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A>jest metodą abstrakcyjną i musi być zaimplementowana. Najbardziej podstawowym sposobem zdefiniowania zawartości treści wiadomości jest zapisanie przy użyciu tej metody. Na przykład następujący komunikat zawiera liczbę losową 100 000 od 1 do 20.  
  
 [!code-csharp[C_UsingTheMessageClass#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#9)]
 [!code-vb[C_UsingTheMessageClass#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#9)]  
  
 Metody <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents> i<xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A> mają domyślne implementacje, które działają w większości przypadków. Domyślne wywołanie <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A>implementacji, buforowanie wyników i pracy z wynikowym buforem. Jednak w niektórych przypadkach może to być niewystarczające. W poprzednim przykładzie odczytywanie komunikatu powoduje, że elementy XML w formacie 100 000 są buforowane, co może nie być pożądane. Możesz chcieć przesłonić <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents> , aby zwracać niestandardową <xref:System.Xml.XmlDictionaryReader> klasę pochodną, która obsługuje liczby losowe. Następnie można przesłonić <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%2A> , aby użyć czytnika zwracanego przez <xref:System.ServiceModel.Channels.Message.OnGetReaderAtBodyContents> metodę, jak pokazano w poniższym przykładzie.  
  
 [!code-csharp[C_UsingTheMessageClass#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_usingthemessageclass/cs/source.cs#10)]
 [!code-vb[C_UsingTheMessageClass#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_usingthemessageclass/vb/source.vb#10)]  
  
 Analogicznie, możesz chcieć przesłonić `OnCreateBufferedCopy` , aby zwrócić własną `MessageBuffer` klasę pochodną.  
  
 Oprócz udostępniania treści wiadomości, Klasa pochodna komunikatu musi również przesłaniać `Version`właściwości, `Headers`i `Properties` .  
  
 Należy pamiętać, że w przypadku utworzenia kopii komunikatu kopia będzie używać nagłówków wiadomości z oryginału.  
  
### <a name="other-members-that-can-be-overridden"></a>Inne elementy członkowskie, które mogą zostać zastąpione  
 Można zastąpić <xref:System.ServiceModel.Channels.Message.OnWriteStartEnvelope%2A>metody,, <xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A>i <xref:System.ServiceModel.Channels.Message.OnWriteStartBody%2A> , aby określić sposób, w jaki koperty protokołu SOAP, nagłówki protokołu SOAP i Tagi początkowe elementu treści protokołu SOAP są zapisywane. Zwykle są one zgodne `<soap:Envelope>`z `<soap:Header>`, i `<soap:Body>`. Te metody nie powinny zwykle zapisywać niczego w przypadku, <xref:System.ServiceModel.Channels.Message.Version> gdy właściwość <xref:System.ServiceModel.Channels.MessageVersion.None>zwraca.  
  
> [!NOTE]
> Domyślna implementacja `OnGetReaderAtBodyContents` `OnWriteBodyContents` wywołań `OnWriteStartEnvelope` i`OnWriteStartBody` przed wywołaniem i buforowaniem wyników. Nagłówki nie są zapisywane.  
  
 Zastąp <xref:System.ServiceModel.Channels.Message.OnWriteMessage%2A> metodę, aby zmienić sposób, w jaki cały komunikat jest zbudowany z różnych elementów. Metoda jest wywoływana z <xref:System.ServiceModel.Channels.Message.WriteMessage%2A> i z implementacji domyślnej <xref:System.ServiceModel.Channels.Message.OnCreateBufferedCopy%2A>. `OnWriteMessage` Należy zauważyć, <xref:System.ServiceModel.Channels.Message.WriteMessage%2A> że zastąpienie nie jest najlepszym rozwiązaniem. Lepszym rozwiązaniem jest przesłonięcie `On` odpowiednich metod (na <xref:System.ServiceModel.Channels.Message.OnWriteStartEnvelope%2A>przykład <xref:System.ServiceModel.Channels.Message.OnWriteStartHeaders%2A>,, i <xref:System.ServiceModel.Channels.BodyWriter.OnWriteBodyContents%2A>.  
  
 Przesłoń <xref:System.ServiceModel.Channels.Message.OnBodyToString%2A> , aby przesłonić sposób reprezentowania treści wiadomości podczas debugowania. Wartość domyślna to reprezentujący trzy kropki ("..."). Należy zauważyć, że ta metoda może być wywoływana wiele razy, gdy stan wiadomości jest inny niż zamknięty. Implementacja tej metody nigdy nie powinna spowodować żadnej akcji, która musi zostać wykonana tylko raz (na przykład odczyt z strumienia "tylko do przodu").  
  
 Zastąp <xref:System.ServiceModel.Channels.Message.OnGetBodyAttribute%2A> metodę, aby zezwolić na dostęp do atrybutów w elemencie treści protokołu SOAP. Ta metoda może być wywoływana dowolną liczbę razy, ale `Message` typ podstawowy gwarantuje, że jest wywoływana tylko wtedy, gdy komunikat jest w stanie created. Nie jest wymagane sprawdzanie stanu w implementacji. Domyślna implementacja zawsze zwraca wartość `null`, która wskazuje, że nie ma żadnych atrybutów elementu body.  
  
 Jeśli obiekt musi wykonać jakiekolwiek specjalne czyszczenie, gdy treść komunikatu nie jest już wymagana, można przesłonić <xref:System.ServiceModel.Channels.Message.OnClose%2A>. `Message` Domyślna implementacja nie robi nic.  
  
 Właściwości `IsEmpty` i`IsFault` można przesłonić. Domyślnie obie zwracają `false`.
