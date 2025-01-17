---
ms.openlocfilehash: 3b3df8ad736f8f1c6a09e3349379b8c689cf731c
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2019
ms.locfileid: "68235583"
---
### <a name="default-value-of-servicepointmanagersecurityprotocol-is-securityprotocoltypesystemdefault"></a>Wartość domyślna ServicePointManager.SecurityProtocol to SecurityProtocolType.System.Default

|   |   |
|---|---|
|Szczegóły|Począwszy od aplikacji przeznaczonych dla platformy .NET Framework 4.7, wartością domyślną <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> właściwość <xref:System.Net.SecurityProtocolType.SystemDefault?displayProperty=nameWithType>. Ta zmiana umożliwia sieciowych interfejsów API opartych na SslStream (na przykład FTP, HTTPS i SMTP) dziedziczyć domyślnych protokołów zabezpieczeń systemu operacyjnego, zamiast używać zakodowanych wartości, które są zdefiniowane w programie .NET Framework w programie .NET Framework. Wartość domyślna jest zależna od systemu operacyjnego i konfiguracji niestandardowych wykonywane przez administratora systemu. Aby uzyskać informacje na domyślnym protokołem SChannel w każdej wersji systemu operacyjnego Windows, zobacz [protokołów TLS/SSL (dostawca SSP Schannel)](https://docs.microsoft.com/windows/desktop/SecAuthN/protocols-in-tls-ssl--schannel-ssp-).</p>Dla aplikacji przeznaczonych dla starszej wersji programu .NET Framework, wartość domyślna <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> właściwości zależy od wersji programu .NET Framework docelowa. Zobacz [sieci części przekierowania zmiany dotyczące migracji z .NET Framework 4.5.2 i 4.6](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#networking) Aby uzyskać więcej informacji.|
|Sugestia|Ta zmiana ma wpływ na aplikacje, których platformą docelową jest program .NET Framework 4.7 lub nowszej wersji. </br>Jeśli wolisz używać zdefiniowanego protokołu, a nie opierając się na ustawienie domyślne systemu, można jawnie ustawić wartość <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> właściwości.</br>Jeśli ta zmiana jest niepożądany, można zrezygnować z jej przez dodanie ustawienia konfiguracji do [ \<runtime >](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) sekcji w pliku konfiguracji aplikacji. W poniższym przykładzie pokazano oba <code>&lt;runtime&gt;</code> sekcji i <code>Switch.System.Net.DontEnableSystemDefaultTlsVersions</code> rezygnacji przełącznika:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Net.DontEnableSystemDefaultTlsVersions=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Scope|Mały|
|Wersja|4.7|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType></li></ul>|
