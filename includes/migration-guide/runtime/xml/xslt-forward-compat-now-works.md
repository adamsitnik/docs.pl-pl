---
ms.openlocfilehash: 2dd97fcce13ed1ac7baf4cd02f5881d31d7a9c4b
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804686"
---
### <a name="xslt-forward-compat-now-works"></a>Działa teraz zgodności do przodu XSLT

|   |   |
|---|---|
|Szczegóły|W programie .NET Framework 4 zgodność specyfikacji XSLT 1.0 ma następujące problemy:<ul><li>Ładowanie arkusza stylów kończyło się niepowodzeniem, jeśli jego wersja miała wartość 2.0, a analizator napotkał nierozpoznaną konstrukcję specyfikacji XSLT 1.0.</li><li><code>xsl:sort</code> Konstrukcja nie doprowadziła do sortowania danych, jeśli ustawiono wersję arkusza stylów 1.1.</li></ul>W .NET Framework 4.5 te problemy zostały rozwiązane i tryb zgodności w przód wersji XSLT 1.0 działa poprawnie.|
|Sugestia|Większość aplikacji powinna być nienaruszona, jednak dane będą sortowane inaczej w niektórych przypadkach skoro sort jest zachowana. Jeśli <code>xsl:sort</code> jest używany w arkuszach stylów 1.1, upewnij się, że aplikacje nie były w zależności od kolejności nieposortowana danych. Jeśli aplikacje polegają na 4.0 sortowanie zachowanie, Usuń <code>xsl:sort</code> z arkusza stylów.|
|Zakres|Krawędź|
|Wersja|4.5|
|Typ|Środowisko uruchomieniowe|
|Dotyczy interfejsów API|<ul><li><xref:System.Xml.Xsl.XslCompiledTransform?displayProperty=nameWithType></li></ul>|
