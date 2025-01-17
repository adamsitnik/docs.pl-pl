---
ms.openlocfilehash: 9520f8c6b6671917f5694bc602293a00e2dab82d
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71217060"
---
### <a name="ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes"></a>Element ZipArchiveEntry nie obsługuje już archiwów z niespójnymi rozmiarami wpisów

Archiwa zip wyświetlają rozmiar skompresowany i nieskompresowany w katalogu centralnym i nagłówku lokalnym.  Dane wejściowe również wskazują jego rozmiar.  W programie .NET Core 2,2 i starszych wersjach te wartości nigdy nie były sprawdzane pod kątem spójności. Począwszy od platformy .NET Core 3,0, są one teraz.

#### <a name="change-description"></a>Zmień opis

W programie .NET Core 2,2 i starszych wersjach <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType> program kończy się powodzeniem nawet wtedy, gdy nagłówek lokalny nie zgadza się z centralnym nagłówkiem pliku zip. Dane są dekompresowane do momentu osiągnięcia końca skompresowanego strumienia, nawet jeśli jego długość przekracza rozmiar nieskompresowanych plików wymieniony w katalogu centralnym/nagłówku lokalnym.

Począwszy od platformy .NET Core 3,0, <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType> Metoda sprawdza, czy nagłówek lokalny i nagłówek centralny zgadzają się na skompresowane i nieskompresowane rozmiary wpisu.  Jeśli tak nie jest, metoda zgłasza <xref:System.IO.InvalidDataException> rozmiar i/lub listę deskryptorów danych w archiwum, które nie zgadzają się z katalogiem centralnym pliku zip. Podczas odczytywania wpisu dekompresowane dane są obcinane do rozmiaru nieskompresowanego pliku wymienionego w nagłówku.

Ta zmiana została wprowadzona w celu upewnienia <xref:System.IO.Compression.ZipArchiveEntry> się, że poprawnie reprezentuje rozmiar danych i że tylko ta ilość danych jest odczytywana.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="recommended-action"></a>Zalecana akcja

Ponownie spakować wszystkie archiwum zip, które wykazuje te problemy.

#### <a name="category"></a>Kategoria

CoreFx

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFileExtensions.ExtractToDirectory%2A?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFile.ExtractToDirectory%2A?displayProperty=nameWithType>

<!--

### Affected APIs

`M:System.IO.Compression.ZipArchiveEntry.Open`
`Overload:System.IO.Compression.ZipFileExtensions.ExtractToDirectory%2A`
`Overload:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A`
`Overload:System.IO.Compression.ZipFile.ExtractToDirectory%2A`

-->
