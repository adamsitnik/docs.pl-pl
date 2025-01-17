---
title: Parametry połączenia w Entity Framework ADO.NET
ms.date: 10/15/2018
ms.assetid: 78d516bc-c99f-4865-8ff1-d856bc1a01c0
ms.openlocfilehash: 392e51022dc0f98b9fad656b9f950cd25588f31a
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040330"
---
# <a name="connection-strings-in-the-adonet-entity-framework"></a>Parametry połączenia w Entity Framework ADO.NET

Parametry połączenia zawierają informacje inicjujące, które są przesyłane jako parametr z dostawcy danych do źródła danych. Składnia jest zależna od dostawcy danych, a parametry połączenia są analizowane podczas próby otwarcia połączenia. Parametry połączenia używane przez Entity Framework zawierają informacje służące do nawiązywania połączenia z podstawowym dostawcą danych ADO.NET, który obsługuje Entity Framework. Zawierają również informacje o wymaganym modelu i plikach mapowania.

Parametry połączenia są używane przez dostawcę EntityClient podczas uzyskiwania dostępu do modelu i mapowania metadanych oraz łączenia ze źródłem danych. Parametry połączenia mogą być dostępne lub ustawiane za pomocą właściwości <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> <xref:System.Data.EntityClient.EntityConnection>. Klasy <xref:System.Data.EntityClient.EntityConnectionStringBuilder> można użyć do programistycznego konstruowania lub dostępu do parametrów w parametrach połączenia. Aby uzyskać więcej informacji, zobacz [How to: build The EntityConnection Connection String](how-to-build-an-entityconnection-connection-string.md).

[Narzędzia Entity Data Model](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100)) generują parametry połączenia, które są przechowywane w pliku konfiguracyjnym aplikacji. <xref:System.Data.Objects.ObjectContext> automatycznie pobiera te informacje o połączeniu podczas tworzenia zapytań dotyczących obiektów. Do <xref:System.Data.EntityClient.EntityConnection> używany przez wystąpienie <xref:System.Data.Objects.ObjectContext> można uzyskać dostęp z właściwości <xref:System.Data.Objects.ObjectContext.Connection%2A>. Aby uzyskać więcej informacji, zobacz [Zarządzanie połączeniami i transakcjami](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100)).

## <a name="connection-string-syntax"></a>Składnia parametrów połączenia

Aby dowiedzieć się więcej o składni ogólnej parametrów połączenia, zobacz [składnia parametrów połączenia | Parametry połączenia w ADO.NET](../connection-strings.md#connection-string-syntax).

## <a name="connection-string-parameters"></a>Parametry parametrów połączenia

Poniższa tabela zawiera listę prawidłowych nazw wartości słów kluczowych w <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A>.

|Kodu|Opis|
|-------------|-----------------|
|`Provider`|Wymagane, jeśli nie określono słowa kluczowego `Name`. Nazwa dostawcy, która jest używana do pobierania obiektu <xref:System.Data.Common.DbProviderFactory> dla podstawowego dostawcy. Ta wartość jest stała.<br /><br /> Gdy słowo kluczowe `Name` nie jest uwzględnione w parametrach połączenia jednostki, wymagana jest niepusta wartość dla słowa kluczowego `Provider`. To słowo kluczowe jest wzajemnie wykluczane za pomocą słowa kluczowego `Name`.|
|`Provider Connection String`|Opcjonalny. Określa parametry połączenia specyficzne dla dostawcy, które są przesyłane do bazowego źródła danych. Te parametry połączenia zawierają prawidłowe pary słowo kluczowe/wartość dla dostawcy danych. Nieprawidłowy `Provider Connection String` spowoduje wystąpienie błędu czasu wykonywania, gdy zostanie on oceniony przez źródło danych.<br /><br /> To słowo kluczowe jest wzajemnie wykluczane za pomocą słowa kluczowego `Name`.<br /><br /> Upewnij się, że wartość jest wyprowadzana zgodnie z ogólną składnią [parametrów połączenia ADO.NET](../connection-strings.md). Rozważmy na przykład następujące parametry połączenia: `Server=serverName; User ID = userID`. Musi zostać zmieniony, ponieważ zawiera średnik. Ponieważ nie zawiera podwójnych cudzysłowów, mogą one być używane do ucieczki:<br /><br /> `Provider Connection String ="Server=serverName; User ID = userID";`|
|`Metadata`|Wymagane, jeśli nie określono słowa kluczowego `Name`. Rozdzielana potokami lista katalogów, plików i lokalizacji zasobów, w których mają być wyszukiwane metadane i informacje dotyczące mapowania. Oto przykład:<br /><br /> `Metadata=`<br /><br /> `c:\model &#124; c:\model\sql\mapping.msl;`<br /><br /> Spacje po każdej stronie separatora potoku są ignorowane.<br /><br /> To słowo kluczowe jest wzajemnie wykluczane za pomocą słowa kluczowego `Name`.|
|`Name`|Aplikacja może opcjonalnie określić nazwę połączenia w pliku konfiguracyjnym aplikacji, który zawiera wymagane wartości parametrów połączenia słowo kluczowe/wartość. W takim przypadku nie można podawać ich bezpośrednio w parametrach połączenia. Słowo kluczowe `Name` nie jest dozwolone w pliku konfiguracji.<br /><br /> Gdy słowo kluczowe `Name` nie jest uwzględnione w parametrach połączenia, wymagane są niepuste wartości dla słowa kluczowego dostawcy.<br /><br /> To słowo kluczowe wykluczają się wzajemnie poza wszystkimi innymi słowami kluczowymi parametrów połączenia.|

Poniżej przedstawiono przykład parametrów połączenia dla [modelu sprzedaży AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) przechowywanego w pliku konfiguracyjnym aplikacji:

## <a name="model-and-mapping-file-locations"></a>Modelowanie i mapowanie lokalizacji plików

`Metadata` parametr zawiera listę lokalizacji dla dostawcy `EntityClient` do wyszukiwania modeli i plików mapowania. Pliki modelu i mapowania często są wdrażane w tym samym katalogu, w którym znajduje się plik wykonywalny aplikacji. Te pliki można również wdrożyć w określonej lokalizacji lub jako zasób osadzony w aplikacji.

Zasoby osadzone są określone w następujący sposób:

`Metadata=res://<assemblyFullName>/<resourceName>`

W celu zdefiniowania lokalizacji osadzonego zasobu dostępne są następujące opcje:

|Opcja|Opis|
|-|-|
|`assemblyFullName`|Pełna nazwa zestawu z osadzonym zasobem. Nazwa zawiera prostą nazwę, nazwę wersji, obsługiwaną kulturę i klucz publiczny w następujący sposób:<br /><br /> `ResourceLib, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`<br /><br /> Zasoby mogą być osadzone w dowolnym zestawie, który jest dostępny dla aplikacji.<br /><br /> Jeśli określisz symbol wieloznaczny (\*) dla `assemblyFullName`, środowisko uruchomieniowe Entity Framework przeszuka zasoby w następujących lokalizacjach w następującej kolejności:<br /><br /> 1. wywołujący zestaw.<br />2. zestawy, do których się odwołuje.<br />3. zestawy w katalogu bin aplikacji.<br /><br /> Jeśli pliki nie znajdują się w jednej z tych lokalizacji, zostanie zgłoszony wyjątek. **Uwaga:**  W przypadku użycia symbolu wieloznacznego (*) Entity Framework musi przeszukać wszystkie zestawy dla zasobów o poprawnej nazwie. Aby zwiększyć wydajność, należy określić nazwę zestawu zamiast symbolu wieloznacznego.|
|`resourceName`|Nazwa dołączonego zasobu, na przykład AdventureWorksModel. csdl. Usługi metadanych szukają tylko plików lub zasobów z jednym z następujących rozszerzeń: CSDL, SSDL lub MSL. Jeśli nie określono `resourceName`, wszystkie zasoby metadanych zostaną załadowane. Zasoby powinny mieć unikatowe nazwy w obrębie zestawu. Jeśli wiele plików o tej samej nazwie jest zdefiniowanych w różnych katalogach w zestawie, `resourceName` musi zawierać strukturę folderu przed nazwą zasobu, na przykład nazwa_folderu. FileName. csdl.<br /><br /> `resourceName` nie jest wymagana, jeśli dla `assemblyFullName`określono symbol wieloznaczny (*).|

> [!NOTE]
> Aby zwiększyć wydajność, Osadź zasoby w zestawie wywołującym, z wyjątkiem scenariuszy innych niż sieci Web, w których nie ma odwołań do podstawowych mapowań i plików metadanych w zestawie wywołującym.

Poniższy przykład ładuje wszystkie pliki modelu i mapowania z zestawu wywołującego, przywoływanych zestawów i innych zestawów w katalogu bin aplikacji.

```csharp
Metadata=res://*/
```

Poniższy przykład ładuje plik z modelem CSDL z zestawu AdventureWorks i ładuje pliki. ssdl i model. MSL z domyślnego katalogu uruchomionej aplikacji.

```csharp
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|model.ssdl|model.msl
```

Poniższy przykład ładuje trzy określone zasoby z określonego zestawu.

```csharp
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.ssdl|
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.msl
```

Poniższy przykład ładuje wszystkie osadzone zasoby z rozszerzeniami. csdl,. MSL i. ssdl z zestawu.

```csharp
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/
```

Poniższy przykład ładuje wszystkie zasoby w względnej ścieżce pliku oraz "datadir\metadata\\" z załadowanej lokalizacji zestawu.

```csharp
Metadata=datadir\metadata\
```

Poniższy przykład ładuje wszystkie zasoby w względnej ścieżce pliku z załadowanej lokalizacji zestawu.

```csharp
Metadata=.\
```

## <a name="support-for-the-124datadirectory124-substitution-string-and-the-web-application-root-operator-"></a>&#124;Obsługa ciągu podstawiania&#124; usługi DataDirectory i głównego operatora aplikacji sieci Web (~)

`DataDirectory` i operator ~ są używane w <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> jako część słów kluczowych `Metadata` i `Provider Connection String`. <xref:System.Data.EntityClient.EntityConnection> przekazuje odpowiednio `DataDirectory` i operator ~ do <xref:System.Data.Metadata.Edm.MetadataWorkspace> i dostawcy magazynu.

|Termin|Opis|
|----------|-----------------|
|`&#124;DataDirectory&#124;`|Jest rozpoznawana jako ścieżka względna do plików mapowania i metadanych. Jest to wartość, która jest ustawiana za pomocą metody `AppDomain.SetData("DataDirectory", objValue)`. Ciąg podstawienia `DataDirectory` musi być ujęty w znaki potoku i nie może zawierać żadnego odstępu między jego nazwą a znakami potoku. W nazwie `DataDirectory` nie jest rozróżniana wielkość liter.<br /><br /> Jeśli katalog fizyczny o nazwie "DataDirectory" musi zostać przesłany jako element członkowski listy ścieżek metadanych, Dodaj znak odstępu do jednej lub obu stron nazwy. Na przykład: `Metadata="DataDirectory1 &#124; DataDirectory &#124; DataDirectory2"`. Aplikacja ASP.NET rozpoznaje &#124;katalog DataDirectory&#124; w folderze "\<root >/App_Data".|
|~|Jest rozpoznawany jako katalog główny aplikacji sieci Web. Znak ~ w położeniu wiodącym jest zawsze interpretowany jako operator główny aplikacji sieci Web (~), chociaż może reprezentować prawidłowy podkatalog lokalny. Aby odwołać się do takiego lokalnego podkatalogu, użytkownik powinien jawnie przekazać `./~`.|

`DataDirectory` i operator ~ powinien być określony tylko na początku ścieżki, nie są rozwiązywane w żadnym innym miejscu. Entity Framework spróbuje rozwiązać `~/data`, ale będzie traktować `/data/~` jako ścieżkę fizyczną.

Ścieżka rozpoczynająca się od `DataDirectory` lub operatora ~ nie może rozpoznać ścieżki fizycznej poza gałęzią `DataDirectory` i operatorem ~. Na przykład następujące ścieżki zostaną rozwiązane: `~`, `~/data`, `~/bin/Model/SqlServer`. Nie można rozwiązać następujących ścieżek: `~/..`, `~/../other`.

`DataDirectory` i operator ~ można rozszerzyć w celu uwzględnienia podkatalogów w następujący sposób: `|DataDirectory|\Model`, `~/bin/Model`

Rozpoznawanie ciągu podstawienia `DataDirectory` i operatora ~ nie jest cykliczne. Na przykład gdy `DataDirectory` zawiera znak `~`, wystąpi wyjątek. Zapobiega to nieskończonej rekursji.

## <a name="see-also"></a>Zobacz także

- [Praca z dostawcami danymi](working-with-data-providers.md)
- [Zagadnienia dotyczące wdrażania](deployment-considerations.md)
- [Zarządzanie połączeniami i transakcjami](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [Parametry połączeń](../connection-strings.md)
