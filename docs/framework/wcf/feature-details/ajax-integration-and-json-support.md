---
title: Obsługa integracji AJAX i notacji JSON
ms.date: 03/30/2017
helpviewer_keywords:
- AJAX integration and JSON support [WCF]
ms.assetid: 3851a8fc-d861-4ac1-873c-96af0343d3a7
ms.openlocfilehash: a3d9c29f3223624653f2d568bb351d90334a4318
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781618"
---
# <a name="ajax-integration-and-json-support"></a>Obsługa integracji AJAX i notacji JSON
Windows Communication Foundation (WCF) obsługuje ASP.NET asynchronicznego języki JavaScript i XML (technologia AJAX) i formatu JavaScript Object Notation (JSON) w danych umożliwiają usługi WCF do udostępnienia operacje klientom AJAX. Klienci AJAX są stron sieci Web, wykonywanie kodu JavaScript i uzyskiwania dostępu do tych usług WCF za pomocą żądania HTTP. Tematy w tej sekcji zawierają informacje dotyczące tej pomocy technicznej i sposobie jego implementowania.  
  
 Aby dowiedzieć się więcej o technologii ASP.NET AJAX i integracji z programem ASP.NET 2.0, zobacz [omówienie technologii AJAX programu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=96725).  
  
## <a name="in-this-section"></a>W tej sekcji  
 [Tworzenie usług WCF w technologii AJAX na platformie ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)  
 W tym artykule opisano, jak usługi WCF mogą łączyć się z klientami AJAX przez dodanie odpowiednich punktów końcowych AJAX, albo za pośrednictwem konfiguracji lub przy użyciu usługi fabryka hostów, dostosowane do generowania hosta usługi, która automatycznie konfiguruje punktu końcowego AJAX.  
  
 [Tworzenie usług AJAX WCF bez platformy ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md)  
 W tym artykule opisano sposób tworzenia usługi WCF bez za pomocą programu ASP.NET.  
  
 [Obsługa formatu JSON i innych formatów transferowania danych](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)  
 W tym artykule opisano obsługi formatu JSON, zwykle używane (zamiast XML) do obsługi komunikatów z usługami ASP.NET AJAX.  
  
 [Instrukcje: Migrowanie usług internetowych platformy ASP.NET z włączoną obsługą technologii AJAX do programu WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)  
 W tym artykule opisano, jak przeprowadzić migrację usługi sieci Web platformy ASP.NET z obsługą technologii AJAX do usługi sieci WCF Web.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>
- [Model programowania protokołu HTTP sieci Web w programie WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
