---
title: Architektura syndykacji
ms.date: 03/30/2017
ms.assetid: ed4ca86e-e3d8-4acb-87aa-1921fbc353be
ms.openlocfilehash: 5f93c7a11ed37e411fc584c8de16f141336c7f43
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952643"
---
# <a name="architecture-of-syndication"></a>Architektura syndykacji
Interfejs API zespalania został zaprojektowany z myślą o udostępnianiu modelu programowania neutralnego za pomocą formatu, który umożliwia zapisywanie w sieci zespolonej zawartości w różnych formatach. Abstrakcyjny model danych składa się z następujących klas:  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 Te klasy są mapowane blisko konstrukcji zdefiniowanych w specyfikacji Atom 1,0, chociaż niektóre nazwy są różne.  
  
 W Windows Communication Foundation (WCF) źródła zespolone są modelowane jako inny typ operacji usługi, jedną z nich, w której typ zwracany jest jedną z klas <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>pochodnych. Pobieranie źródła danych jest modelowane jako wymiana komunikatów z żądaniem odpowiedzi. Klient wysyła żądanie do usługi, a usługa odpowiada. Komunikat żądania jest ustawiany za pośrednictwem protokołu infrastruktury (na przykład RAW HTTP), a komunikat odpowiedzi zawiera ładunek, który składa się z powszechnie zrozumiałego formatu zespalania (RSS 2,0 lub Atom 1,0). Usługi, które implementują te wymiany komunikatów, są określane jako usługi zespolone.  
  
 Kontrakt usługi zespolonej składa się z zestawu operacji zwracających wystąpienie <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> klasy. Poniższy przykład ilustruje deklarację interfejsu dla usługi zespolonej.  
  
 [!code-csharp[S_UE_SyndicationBoth#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_syndicationboth/cs/service.cs#0)]  
  
 Obsługa zespalania jest oparta na modelu programowania REST WCF, który definiuje <xref:System.ServiceModel.WebHttpBinding> powiązanie, które jest używane w połączeniu z usługą <xref:System.ServiceModel.Description.WebHttpBehavior> w celu udostępnienia kanałów informacyjnych jako usług. Aby uzyskać więcej informacji o modelu programowania REST WCF, zobacz [Omówienie modelu programowania HTTP sieci Web](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)w programie WCF.  
  
> [!NOTE]
> Specyfikacja Atom 1,0 umożliwia określenie ułamków sekund w którymkolwiek z jego konstrukcji daty. Podczas serializacji i deserializacji implementacji programu WCF ignoruje ułamki sekund.  
  
## <a name="object-model"></a>Model obiektów  
 Model obiektów dla zespalania składa się z grup klas w poniższych tabelach.  
  
 Klasy formatowania:  
  
|Class|Opis|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationFeed> wystąpienie do formatu Atom 1,0.|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationFeed> klasy pochodne do formatu Atom 1,0.|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationItem> wystąpienie do formatu Atom 1,0.|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationItem> klasy pochodne do formatu Atom 1,0.|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationFeed> wystąpienie do formatu RSS 2,0.|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationFeed> klasy pochodne do formatu RSS 2,0.|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationItem> wystąpienie do formatu RSS 2,0.|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601>|Klasa, która serializować <xref:System.ServiceModel.Syndication.SyndicationItem> klasy pochodne do formatu RSS 2,0.|  
  
 Klasy modelu obiektów:  
  
|Class|Opis|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Syndication.SyndicationCategory>|Klasa, która reprezentuje kategorię źródła zespolonego.|  
|<xref:System.ServiceModel.Syndication.SyndicationContent>|Klasa bazowa, która reprezentuje zawartość zespoloną.|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtension>|Klasa, która reprezentuje rozszerzenie elementu zespolonego.|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection>|Kolekcja <xref:System.ServiceModel.Syndication.SyndicationElementExtension> obiektów.|  
|<xref:System.ServiceModel.Syndication.SyndicationFeed>|Klasa, która reprezentuje obiekt kanału informacyjnego najwyższego poziomu.|  
|<xref:System.ServiceModel.Syndication.SyndicationItem>|Klasa, która reprezentuje element kanału informacyjnego.|  
|<xref:System.ServiceModel.Syndication.SyndicationLink>|Klasa, która reprezentuje łącze w ramach zespolonego źródła danych lub elementu.|  
|<xref:System.ServiceModel.Syndication.SyndicationPerson>|Klasa, która reprezentuje konstrukcję osoby atomowej.|  
|<xref:System.ServiceModel.Syndication.SyndicationVersions>|Klasa, która reprezentuje obsługiwane wersje protokołu zespolonego.|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContent>|Klasa, która reprezentuje <xref:System.ServiceModel.Syndication.SyndicationItem> zawartość, która będzie wyświetlana użytkownikowi końcowemu.|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContentKind>|Wyliczenie, które reprezentuje różne typy obsługiwanej zawartości zespolonej.|  
|<xref:System.ServiceModel.Syndication.UrlSyndicationContent>|Klasa, która reprezentuje zawartość zespoloną, która składa się z adresu URL innego zasobu.|  
|<xref:System.ServiceModel.Syndication.XmlSyndicationContent>|Klasa reprezentująca zawartość zespoloną, która nie ma być wyświetlana w przeglądarce.|  
  
 Podstawowe abstrakcje danych w modelu obiektów to źródła i elementy, które odpowiadają <xref:System.ServiceModel.Syndication.SyndicationFeed> klasom i. <xref:System.ServiceModel.Syndication.SyndicationItem> Kanał informacyjny ujawnia niektóre metadane na poziomie kanału informacyjnego (na przykład tytuł, opis i autor), lokalizację do przechowywania nieznanych rozszerzeń oraz zestaw elementów, które tworzą resztę zawartości informacji kanału informacyjnego. Element udostępnia metadane na poziomie elementu (na przykład tytuł, podsumowanie i PublicationDate), lokalizację do przechowywania nieznanych rozszerzeń i element zawartości, który zawiera resztę zawartości informacji o elemencie. Podstawowe abstrakcje kanału informacyjnego i elementu są obsługiwane przez dodatkowe klasy, które reprezentują wspólne konstrukcje danych, do których odwołuje się Specyfikacja Atom 1,0 i RSS.  
  
 Informacje zawarte w wystąpieniu źródła danych mogą być konwertowane na różne formaty XML. Proces konwersji do i z XML jest zarządzany przez <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> klasę. Ta klasa jest abstrakcyjna; konkretne implementacje są dostępne dla Atom 1,0 i RSS 2,0 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> i <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>. Aby skorzystać z klas pochodnego źródła danych <xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601> , <xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601> należy użyć lub, aby określić pochodną klasę kanału informacyjnego. Aby można było użyć pochodnych klas elementów <xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601> , <xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601> Użyj lub, gdy umożliwiają określenie pochodnej klasy Item trzecich, można <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> utworzyć własną implementację, aby obsługiwać różne formaty zespolone.  
  
## <a name="extensibility"></a>Rozszerzalność  
  
- Kluczową funkcją protokołów zespalania jest rozszerzalność. Protokoły Atom 1,0 i RSS 2,0 umożliwiają dodawanie atrybutów i elementów do źródeł zespolonych, które nie są zdefiniowane w specyfikacjach. Model programowania zespolonego WCF zapewnia dwa sposoby pracy z atrybutami i rozszerzeniami niestandardowymi: wyprowadzanie nowej klasy i swobodnego dostępu do nich. Aby uzyskać więcej informacji, zobacz [rozszerzalność zespalania](../../../../docs/framework/wcf/feature-details/syndication-extensibility.md).  
  
## <a name="see-also"></a>Zobacz także

- [Omówienie syndykacji WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)
- [Sposób mapowania modelu obiektu syndykacji programu WCF na kanały informacyjne Atom i RSS](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md)
- [Model programowania protokołu HTTP sieci Web w programie WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
