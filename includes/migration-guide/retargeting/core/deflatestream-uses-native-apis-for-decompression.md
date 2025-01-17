---
ms.openlocfilehash: 897bb0b0650c633b87a792516c62566f491ec3fd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61762658"
---
### <a name="deflatestream-uses-native-apis-for-decompression"></a>Dekompresja DeflateStream używa natywnych interfejsów API

|   |   |
|---|---|
|Szczegóły|Począwszy od programu .NET Framework 4.7.2, implementacja dekompresji w <code>T:System.IO.Compression.DeflateStream</code> klasy zmienił się na domyślnie używają natywnych interfejsów API Windows. Zazwyczaj powoduje to zwiększenie wydajności istotne. Określanie wartości docelowej wersji .NET Framework 4.7.2 lub użyj wyższej natywnych implementacji wszystkich aplikacji .NET. Ta zmiana może spowodować pewne różnice w zachowaniu, które obejmują:<ul><li>Komunikaty o wyjątkach mogą się różnić. Jednakże typ wyjątku pozostaje taki sam.</li><li>Czasami specjalne, np. nie ma wystarczającej ilości pamięci do ukończenia operacji, mogą być traktowane inaczej.</li><li>Są to znane różnic w nagłówku strumienia gzip analizy (Uwaga: tylko <code>GZipStream</code> ustawione dekompresji ma to wpływ na):</li><li>Wyjątki podczas analizowania nieprawidłowe nagłówki mogą być generowane w różnym czasie.</li><li>Natywnych implementacji wymusza na to, że wartości dla niektórych zarezerwowanej flagi w nagłówku strumienia gzip (czyli [limit](http://www.zlib.org/rfc-gzip.html#header-trailer)) są ustawione zgodnie ze specyfikacją, co może spowodować zgłoszenie wyjątku, gdzie wcześniej nieprawidłowe wartości zostały zignorowane.</li></ul>|
|Sugestia|Jeśli dekompresja z natywnymi interfejsami API ma niekorzystny wpływ na zachowanie aplikacji, można zrezygnować z tej funkcji, dodając <code>Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression</code> przełączyć się do <code>runtime</code> sekcji w pliku app.config i ustawieniem dla niego <code>true</code>:<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot; ?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|Zakres|Mały|
|Wersja|4.7.2|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.IO.Compression.DeflateStream?displayProperty=nameWithType></li><li><xref:System.IO.Compression.GZipStream?displayProperty=nameWithType></li></ul>|
