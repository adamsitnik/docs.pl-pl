---
title: HTTP
ms.date: 03/30/2017
helpviewer_keywords:
- protocols, HTTP
- sending data, HTTP
- HttpWebResponse class, sending and receiving data
- HTTP
- receiving data, HTTP
- application protocols, HTTP
- Internet, HTTP
- network resources, HTTP
- HTTP, about HTTP
- HttpWebRequest class, sending and receiving data
ms.assetid: 985fe5d8-eb71-4024-b361-41fbdc1618d8
ms.openlocfilehash: c8c799a50e5d63bbf411c338eb9e93f85a942bb0
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71048008"
---
# <a name="http"></a>HTTP
.NET Framework zapewnia kompleksową pomoc techniczną dla protokołu HTTP, która stanowi większość całego ruchu internetowego z <xref:System.Net.HttpWebRequest> klasami i. <xref:System.Net.HttpWebResponse> Klasy pochodne <xref:System.Net.WebRequest> i <xref:System.Net.WebResponse>, są zwracane domyślnie za każdym razem, gdy metoda <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> statyczna napotka identyfikator URI rozpoczynający się od ciągu "http" lub "https". W większości przypadków klasy **WebRequest** i **WebResponse** zapewniają wszystko, co jest niezbędne do wykonania żądania, ale jeśli potrzebujesz dostępu do funkcji specyficznych dla protokołu HTTP udostępnianych jako właściwości, można rzutowanie te klasy na **HttpWebRequest** lub **HttpWebResponse**.  
  
 **HttpWebRequest** i **HttpWebResponse** hermetyzują standardową transakcję http żądanie i odpowiedź i zapewniają dostęp do typowych nagłówków HTTP. Te klasy obsługują również większość funkcji protokołu HTTP 1,1, w tym przetwarzanie potokowe, wysyłanie i pobieranie danych w fragmentach, uwierzytelnianiu, wstępnemu uwierzytelnianiu, szyfrowaniu, obsłudze serwera proxy, weryfikacji certyfikatu serwera i zarządzaniu połączeniami. Niestandardowe nagłówki i nagłówki, które nie są przekazywane za pomocą właściwości, mogą być przechowywane w i dostępne za pomocą właściwości **Headers** .  
  
 **HttpWebRequest** jest domyślną klasą używaną przez **WebRequest** i nie musi być zarejestrowana przed przekazaniem identyfikatora URI do metody **WebRequest. Create** .  
  
 Można sprawić, aby aplikacja automatycznie przekierowała protokół HTTP przez ustawienie <xref:System.Net.HttpWebRequest.AllowAutoRedirect%2A> dla właściwości **wartości true** (wartość domyślna). Aplikacja będzie przekierowywać żądania, a <xref:System.Net.HttpWebResponse.ResponseUri%2A> Właściwość **HttpWebResponse** będzie zawierać rzeczywisty zasób sieci Web, który odpowiedział na żądanie. Jeśli ustawisz **AllowAutoRedirect** na **false**, aplikacja musi być w stanie obsłużyć przekierowania jako błędy protokołu HTTP.  
  
 Aplikacje odbierają błędy protokołu HTTP przez przechwycenie <xref:System.Net.WebException> <xref:System.Net.WebException.Status%2A> z zestawem <xref:System.Net.WebExceptionStatus>do. Właściwość zawiera WebResponse wysyłany przez serwer i wskazuje rzeczywisty błąd http. <xref:System.Net.WebException.Response%2A>  
  
## <a name="see-also"></a>Zobacz także

- [Dostęp do Internetu za pośrednictwem serwera proxy](accessing-the-internet-through-a-proxy.md)
- [Korzystanie z protokołów aplikacji](using-application-protocols.md)
- [Instrukcje: Dostęp do właściwości specyficznych dla protokołu HTTP](how-to-access-http-specific-properties.md)
