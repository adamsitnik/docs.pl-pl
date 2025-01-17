---
title: Co nowego w programie .NET Core 2.1
description: Dowiedz się więcej o nowych funkcjach dostępnych w programie .NET Core 2,1.
dev_langs:
- csharp
- vb
ms.date: 10/10/2018
ms.openlocfilehash: 603e7ae4ffb9e6a4bb477af9597d6948bd63f55e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73100751"
---
# <a name="whats-new-in-net-core-21"></a>Co nowego w programie .NET Core 2.1

Program .NET Core 2,1 zawiera ulepszenia i nowe funkcje w następujących obszarach:

- [Narzędzi](#tooling)
- [Przewinięcie do przodu](#roll-forward)
- [Wdrażanie](#deployment)
- [Pakiet zgodności systemu Windows](#windows-compatibility-pack)
- [Ulepszenia kompilacji JIT](#jit-compiler-improvements)
- [Zmiany interfejsu API](#api-changes)

## <a name="tooling"></a>Narzędzia

Zestaw .NET Core 2,1 SDK (v 2.1.300), narzędzia dołączone do programu .NET Core 2,1, obejmują następujące zmiany i ulepszenia:

### <a name="build-performance-improvements"></a>Ulepszenia wydajności kompilacji

Głównym fokusem platformy .NET Core 2,1 jest poprawa wydajności czasu kompilacji, szczególnie w przypadku kompilacji przyrostowych. Te ulepszenia wydajności dotyczą zarówno kompilacji wiersza polecenia, jak i programu `dotnet build` oraz do kompilacji w programie Visual Studio. Niektóre indywidualne obszary poprawy obejmują:

- W przypadku rozpoznawania zasobów pakietu, rozpoznawania tylko zasobów używanych przez kompilację, a nie wszystkich zasobów.

- Buforowanie odwołań do zestawów.

- Korzystanie z długotrwałych serwerów kompilacji zestawu SDK, które są procesami, które rozciągają się na poszczególne wywołania `dotnet build`. Eliminują one konieczność kompilowania dużych bloków kodu przy każdym uruchomieniu `dotnet build`. Procesy serwera kompilacji można automatycznie kończyć przy użyciu następującego polecenia:

   ```dotnetcli
   dotnet buildserver shutdown
   ```

### <a name="new-cli-commands"></a>Polecenia nowej infrastruktury CLI

Kilka narzędzi, które były dostępne tylko dla każdego projektu, przy użyciu [`DotnetCliToolReference`](../tools/extensibility.md) , są teraz dostępne jako część zestaw .NET Core SDK. Dostępne są następujące narzędzia:

- `dotnet watch` udostępnia obserwatora systemu plików, który czeka na zmianę pliku przed wykonaniem określonego zestawu poleceń. Na przykład następujące polecenie automatycznie ponownie kompiluje bieżący projekt i generuje pełne dane wyjściowe za każdym razem, gdy plik zostanie zmieniony:

   ```dotnetcli
   dotnet watch -- --verbose build
   ```

   Zanotuj opcję `--`, która poprzedza opcję `--verbose`. Ogranicza opcje przekazane bezpośrednio do polecenia `dotnet watch` z argumentów, które są przekazane do procesu podrzędnego `dotnet`. Bez niej opcja `--verbose` dotyczy polecenia `dotnet watch`, a nie polecenia `dotnet build`.
  
   Aby uzyskać więcej informacji, zobacz [opracowywanie aplikacji ASP.NET Core przy użyciu czujki dotnet](/aspnet/core/tutorials/dotnet-watch).

- `dotnet dev-certs` generuje i zarządza certyfikatami używanymi podczas opracowywania aplikacji ASP.NET Core.

- `dotnet user-secrets` zarządza wpisami tajnymi w magazynie kluczy tajnych użytkownika w aplikacjach ASP.NET Core.

- `dotnet sql-cache` tworzy tabelę i indeksy w bazie danych Microsoft SQL Server, która ma być używana na potrzeby rozproszonej pamięci podręcznej.

- `dotnet ef` to narzędzie do zarządzania bazami danych, obiektami <xref:Microsoft.EntityFrameworkCore.DbContext> i migracjami w aplikacjach Entity Framework Core. Aby uzyskać więcej informacji, zobacz [EF Core narzędzia wiersza polecenia programu .NET](/ef/core/miscellaneous/cli/dotnet).

### <a name="global-tools"></a>Narzędzia globalne

Program .NET Core 2,1 obsługuje *Narzędzia globalne* — czyli narzędzia niestandardowe, które są dostępne globalnie w wierszu polecenia. Model rozszerzalności we wcześniejszych wersjach platformy .NET Core wykonał niestandardowe narzędzia dostępne dla każdego projektu, tylko przy użyciu [`DotnetCliToolReference`](../tools/extensibility.md#consuming-per-project-tools).

Aby zainstalować narzędzie globalne, należy użyć polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) . Na przykład:

```dotnetcli
dotnet tool install -g dotnetsay
```

Po zainstalowaniu narzędzie można uruchomić z wiersza polecenia, określając nazwę narzędzia. Aby uzyskać więcej informacji, zobacz [Omówienie narzędzi globalnych platformy .NET Core](../tools/global-tools.md).

### <a name="tool-management-with-the-dotnet-tool-command"></a>Zarządzanie narzędziem za pomocą polecenia `dotnet tool`

W zestawie SDK platformy .NET Core 2,1 wszystkie operacje narzędzi używają `dotnet tool` polecenia. Dostępne są następujące opcje:

- [`dotnet tool install`](../tools/dotnet-tool-install.md) , aby zainstalować narzędzie.

- [`dotnet tool update`](../tools/dotnet-tool-update.md) w celu odinstalowania i ponownego zainstalowania narzędzia, które efektywnie go aktualizuje.

- [`dotnet tool list`](../tools/dotnet-tool-list.md) , aby wyświetlić listę aktualnie zainstalowanych narzędzi.

- [`dotnet tool uninstall`](../tools/dotnet-tool-uninstall.md) w celu odinstalowania aktualnie zainstalowanych narzędzi.

## <a name="roll-forward"></a>Przewinięcie do przodu

Wszystkie aplikacje .NET Core, począwszy od platformy .NET Core 2,0, automatycznie przekazują do najnowszej *wersji pomocniczej* zainstalowanej w systemie.

Począwszy od platformy .NET Core 2,0, jeśli wersja platformy .NET Core, z którą została skompilowana aplikacja, nie jest obecna w czasie wykonywania, aplikacja jest uruchamiana automatycznie względem najnowszej zainstalowanej *pomocniczej wersji* platformy .NET Core. Innymi słowy, jeśli aplikacja jest skompilowana przy użyciu platformy .NET Core 2,0, a program .NET Core 2,0 nie jest obecny w systemie hosta, ale .NET Core 2,1 to, aplikacja działa z platformą .NET Core 2,1.

> [!IMPORTANT]
> To zachowanie z przekazaniem do przodu nie ma zastosowania do wersji zapoznawczej. Domyślnie nie dotyczy to również wersji głównych, ale można to zmienić przy użyciu poniższych ustawień.

To zachowanie można zmienić, zmieniając ustawienie dla opcji przechodzenie do przodu w przypadku braku kandydata udostępnionego platformy. Dostępne są następujące ustawienia:

- `0` — Wyłącz zachowanie przekazujące wersje pomocnicze. W przypadku tego ustawienia aplikacja skompilowana dla programu .NET Core 2.0.0 będzie przeniesiona do wersji .NET Core 2.0.1, ale nie do platformy .NET Core 2.2.0 lub .NET Core 3.0.0.
- `1` — Włącz zachowanie przekazujące wersje pomocnicze. Jest to wartość domyślna dla tego ustawienia. W przypadku tego ustawienia aplikacja skompilowana dla programu .NET Core 2.0.0 będzie przeniesiona do programu .NET Core 2.0.1 lub .NET Core 2.2.0, w zależności od tego, który z nich jest zainstalowany, ale nie zostanie przesunięty do programu .NET Core 3.0.0.
- `2` — Włącz proste i główne zachowanie podczas przekazywania wersji. Jeśli ta wartość jest ustawiona, są uwzględniane różne wersje główne, więc aplikacja skompilowana dla platformy .NET Core 2.0.0 przejdzie do usługi .NET Core 3.0.0.

To ustawienie można zmienić na jeden z trzech sposobów:

- Ustaw żądaną wartość zmiennej środowiskowej `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX`.

- Dodaj następujący wiersz z odpowiednią wartością do pliku *. runtimeconfig. JSON* :

   ```json
   "rollForwardOnNoCandidateFx" : 0
   ```

- Korzystając z [interfejs wiersza polecenia platformy .NET Core narzędzi](../tools/index.md), Dodaj następującą opcję z odpowiednią wartością do polecenia programu .NET Core, takiego jak `run`:

   ```dotnetcli
   dotnet run --rollForwardOnNoCandidateFx=0
   ```

Wersja poprawki do przodu jest niezależna od tego ustawienia i jest wykonywana po zastosowaniu dowolnych dodatkowych lub głównych wersji do przodu.

## <a name="deployment"></a>wdrażania

### <a name="self-contained-application-servicing"></a>Obsługa aplikacji samodzielnych

`dotnet publish` teraz publikuje aplikacje samodzielne przy użyciu wersji środowiska uruchomieniowego z obsługą. Po opublikowaniu aplikacji samodzielnej przy użyciu zestawu .NET Core 2,1 SDK (v 2.1.300) aplikacja zawiera najnowszą wersję środowiska uruchomieniowego, znaną przez ten zestaw SDK. Po uaktualnieniu do najnowszego zestawu SDK opublikujesz go przy użyciu najnowszej wersji środowiska uruchomieniowego platformy .NET Core. Dotyczy to środowiska uruchomieniowego .NET Core 1,0 i nowszych.

Samodzielny publikowanie jest zależne od wersji środowiska uruchomieniowego w systemie NuGet.org. Na maszynie nie trzeba mieć obsługiwanego środowiska uruchomieniowego.

Przy użyciu zestawu SDK platformy .NET Core 2,0 aplikacje samodzielne są publikowane przy użyciu środowiska uruchomieniowego 2.0.0 platformy .NET Core, chyba że inna wersja jest określona za pośrednictwem właściwości `RuntimeFrameworkVersion`. W przypadku tego nowego zachowania nie trzeba już ustawiać tej właściwości, aby wybrać nowszą wersję środowiska uruchomieniowego dla aplikacji samodzielnej. Najprostszym podejściem do przodu jest zawsze Publikowanie przy użyciu zestawu SDK platformy .NET Core 2,1 (v 2.1.300).

Aby uzyskać więcej informacji, zobacz [samodzielne wdrożenie środowiska uruchomieniowego wdrożenia](../deploying/runtime-patch-selection.md).
## <a name="windows-compatibility-pack"></a>Pakiet zgodności systemu Windows

Podczas przenoszenia istniejącego kodu z .NET Framework do programu .NET Core można użyć [pakietu zgodności systemu Windows](https://www.nuget.org/packages/Microsoft.Windows.Compatibility). Zapewnia dostęp do 20 000 więcej interfejsów API, niż są dostępne w programie .NET Core. Te interfejsy API obejmują typy w przestrzeni nazw <xref:System.Drawing?displayProperty=nameWithType>, Klasa <xref:System.Diagnostics.EventLog>, WMI, liczniki wydajności, usługi systemu Windows oraz typy i składowe rejestru systemu Windows.

## <a name="jit-compiler-improvements"></a>Udoskonalenia kompilatora JIT

Platforma .NET Core obejmuje nową technologię kompilatora JIT o nazwie *kompilacja warstwowa* (znana również jako *Optymalizacja adaptacyjna*), która może znacząco poprawić wydajność. Kompilacja warstwowa jest ustawieniem zgody.

Jednym z ważnych zadań wykonywanych przez kompilator JIT jest optymalizacja wykonywania kodu. Jednak w przypadku niewielkich ścieżek kodu kompilator może poświęcać więcej czasu na optymalizację kodu niż środowisko uruchomieniowe spędza na uruchamianiu niezoptymalizowanego kodu. Kompilacja warstwowa wprowadza dwa etapy kompilacji JIT:

- **Pierwsza warstwa**, która generuje kod tak szybko, jak to możliwe.

- **Druga warstwa**, która generuje zoptymalizowany kod dla tych metod, które są wykonywane często. Druga warstwa kompilacji jest wykonywana równolegle w celu zwiększenia wydajności.

Możesz zdecydować się na kompilację warstwową na dwa sposoby.

- Aby użyć kompilacji warstwowej we wszystkich projektach, które używają zestawu SDK platformy .NET Core 2,1, ustaw następujące zmienne środowiskowe:

  ```console
  COMPlus_TieredCompilation="1"
  ```

- Aby użyć kompilacji warstwowej dla każdego projektu, należy dodać właściwość `<TieredCompilation>` do `<PropertyGroup>` sekcji pliku projektu MSBuild, jak pokazano w poniższym przykładzie:

   ```xml
   <PropertyGroup>
      <!-- other property definitions -->

      <TieredCompilation>true</TieredCompilation>
   </PropertyGroup>
   ```

## <a name="api-changes"></a>Zmiany interfejsu API

### <a name="spant-and-memoryt"></a>`Span<T>` i `Memory<T>`

Platforma .NET Core 2,1 zawiera nowe typy, które ułatwiają pracę z tablicami i innymi typami pamięci. Nowe typy obejmują:

- <xref:System.Span%601?displayProperty=nameWithType> i <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>.

- <xref:System.Memory%601?displayProperty=nameWithType> i <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>.

Bez tych typów, podczas przekazywania takich elementów jako części tablicy lub sekcji buforu pamięci należy wykonać kopię części danych przed przekazaniem jej do metody. Te typy zapewniają wirtualny widok tych danych, który eliminuje konieczność dodatkowej alokacji pamięci i operacji kopiowania.

Poniższy przykład używa wystąpienia <xref:System.Span%601> i <xref:System.Memory%601>, aby zapewnić wirtualny widok 10 elementów tablicy.

[!code-csharp[Span\<T>](~/samples/core/whats-new/whats-new-in-21/cs/program.cs)]

[!code-vb[Memory\<T>](~/samples/core/whats-new/whats-new-in-21/vb/program.vb)]

### <a name="brotli-compression"></a>Kompresja Brotli

Program .NET Core 2,1 dodaje obsługę kompresji i dekompresji Brotli. Brotli to algorytm kompresji bezstratnego ogólnego przeznaczenia, który jest zdefiniowany w [dokumencie RFC 7932](https://www.ietf.org/rfc/rfc7932.txt) i jest obsługiwany przez większość przeglądarek sieci Web i głównych serwerów sieci Web. Można użyć klasy <xref:System.IO.Compression.BrotliStream?displayProperty=nameWithType> opartej na strumieniu lub <xref:System.IO.Compression.BrotliEncoder?displayProperty=nameWithType> i <xref:System.IO.Compression.BrotliDecoder?displayProperty=nameWithType> klas. Poniższy przykład ilustruje kompresję z klasą <xref:System.IO.Compression.BrotliStream>:

[!code-csharp[Brotli compression](~/samples/core/whats-new/whats-new-in-21/cs/brotli.cs#1)]

[!code-vb[Brotli compression](~/samples/core/whats-new/whats-new-in-21/vb/brotli.vb#1)]

Zachowanie <xref:System.IO.Compression.BrotliStream> jest takie samo jak <xref:System.IO.Compression.DeflateStream> i <xref:System.IO.Compression.GZipStream>, co ułatwia konwertowanie kodu, który wywołuje te interfejsy API do <xref:System.IO.Compression.BrotliStream>.

### <a name="new-cryptography-apis-and-cryptography-improvements"></a>Nowe ulepszone interfejsy API kryptografii i kryptografii

Program .NET Core 2,1 zawiera liczne ulepszenia interfejsów API kryptografii:

- <xref:System.Security.Cryptography.Pkcs.SignedCms?displayProperty=nameWithType> jest dostępna w pakiecie System. Security. Cryptography. PKCS. Implementacja jest taka sama jak Klasa <xref:System.Security.Cryptography.Pkcs.SignedCms> w .NET Framework.

- Nowe przeciążenia metod <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHash%2A?displayProperty=nameWithType> i <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString%2A?displayProperty=nameWithType> akceptują identyfikator algorytmu wyznaczania wartości skrótu, aby umożliwić wywołującym pobieranie wartości odcisków palca certyfikatu przy użyciu algorytmów innych niż SHA-1.

- Dostępne są nowe interfejsy API kryptografii opartej na <xref:System.Span%601>ach, takie jak mieszanie, HMAC, generowanie losowe, Kryptografia, generowanie sygnatur asymetryczne, przetwarzanie sygnatur asymetryczne i szyfrowanie RSA.

- Wydajność <xref:System.Security.Cryptography.Rfc2898DeriveBytes?displayProperty=nameWithType> została ulepszona o około 15% przy użyciu implementacji opartej na <xref:System.Span%601>.

- Nowa Klasa <xref:System.Security.Cryptography.CryptographicOperations?displayProperty=nameWithType> obejmuje dwie nowe metody:

  - <xref:System.Security.Cryptography.CryptographicOperations.FixedTimeEquals%2A> pobiera stałą ilość czasu, aby zwrócić w przypadku wszystkich dwóch danych wejściowych o tej samej długości, co sprawia, że jest to odpowiednie do użycia w weryfikacji kryptograficznej, aby uniknąć współtworzenia informacji w kanale bocznym.

  - <xref:System.Security.Cryptography.CryptographicOperations.ZeroMemory%2A> to procedura czyszczenia pamięci, której nie można zoptymalizować.

- Metoda static <xref:System.Security.Cryptography.RandomNumberGenerator.Fill%2A?displayProperty=nameWithType> wypełnia <xref:System.Span%601> losowo wartościami.

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms?displayProperty=nameWithType> jest teraz obsługiwana w systemach Linux i macOS.

- Krzywa eliptyczna — Diffie-Hellmana (ECDH) jest teraz dostępna w rodzinie klasy <xref:System.Security.Cryptography.ECDiffieHellman?displayProperty=nameWithType>. Powierzchnia obszaru jest taka sama jak w .NET Framework.

- Wystąpienie zwrócone przez <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> może szyfrować lub odszyfrowywać za pomocą OAEP przy użyciu skrótu SHA-2, a także generować lub weryfikować podpisy przy użyciu RSA-PSS.

### <a name="sockets-improvements"></a>Ulepszenia gniazd

Platforma .NET Core zawiera nowy typ, <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> i ponownie zapisany <xref:System.Net.Http.HttpMessageHandler?displayProperty=nameWithType>, który stanowi podstawę interfejsów API sieci wyższego poziomu.  na przykład <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> jest podstawą implementacji <xref:System.Net.Http.HttpClient>. W poprzednich wersjach programu .NET Core interfejsy API wyższego poziomu były oparte na natywnych implementacjach sieci.

Implementacja Sockets wprowadzona w programie .NET Core 2,1 ma wiele zalet:

- Znaczący wzrost wydajności w porównaniu z poprzednią implementacją.

- Wyeliminowanie zależności platformy, co upraszcza wdrażanie i obsługę.

- Spójne zachowanie na wszystkich platformach .NET Core.

<xref:System.Net.Http.SocketsHttpHandler> to domyślna implementacja programu .NET Core 2,1. Można jednak skonfigurować aplikację tak, aby używała starszej klasy <xref:System.Net.Http.HttpClientHandler>, wywołując metodę <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType>:

```csharp
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", false);
```

```vb
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", False)
```

Można również użyć zmiennej środowiskowej, aby zrezygnować z użycia implementacji Sockets na podstawie <xref:System.Net.Http.SocketsHttpHandler>. W tym celu ustaw wartość `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` na `false` lub 0.

W systemie Windows można również użyć opcji <xref:System.Net.Http.WinHttpHandler?displayProperty=nameWithType>, która opiera się na implementacji natywnej lub klasy <xref:System.Net.Http.SocketsHttpHandler> przez przekazanie wystąpienia klasy do konstruktora <xref:System.Net.Http.HttpClient>.

W systemie Linux i macOS można skonfigurować tylko <xref:System.Net.Http.HttpClient> dla poszczególnych procesów. W systemie Linux należy wdrożyć [libcurl](https://curl.haxx.se/libcurl/) , jeśli chcesz użyć starej implementacji <xref:System.Net.Http.HttpClient>. (Jest instalowany z platformą .NET Core 2,0).

## <a name="see-also"></a>Zobacz także

- [Co nowego w programie .NET Core](index.md)
- [Nowe funkcje w EF Core 2,1](/ef/core/what-is-new/ef-core-2.1)
- [Co nowego w ASP.NET Core 2,1](/aspnet/core/aspnetcore-2.1)
