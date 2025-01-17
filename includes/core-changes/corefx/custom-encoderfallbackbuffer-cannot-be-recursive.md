---
ms.openlocfilehash: 58d1c8cd3aff52703522391c14348bd81c108587
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/09/2019
ms.locfileid: "72237430"
---
### <a name="custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively"></a>Niestandardowe wystąpienia EncoderFallbackBuffer nie mogą podlegać rekursywnie

Wystąpienia niestandardowe <xref:System.Text.EncoderFallbackBuffer> nie mogą podlegać rekursywnie. Implementacja <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> musi spowodować sekwencję znaków, która jest konwertowany na kodowanie docelowe. W przeciwnym razie wystąpi wyjątek.

#### <a name="change-description"></a>Zmień opis

Podczas operacji transkodowania typu "Character-to-Byte" środowisko uruchomieniowe wykrywa nieprawidłowo sformułowane lub niewymienialne sekwencje UTF-16 i dostarcza te znaki do metody <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>. Metoda `Fallback` Określa, które znaki powinny zostać zastąpione dla oryginalnych danych nieprzekonwertowanych. te znaki są opróżniane przez wywołanie <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> w pętli.

Środowisko uruchomieniowe następnie próbuje transkodowanie te znaki podstawiania do kodowania docelowego. Jeśli ta operacja zakończy się pomyślnie, środowisko uruchomieniowe kontynuuje transkodowanie z miejsca, w którym jest pozostawione w oryginalnym ciągu wejściowym.

W programie .NET Core w wersji zapoznawczej 7 i starszych wersjach niestandardowe implementacje <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> mogą zwracać sekwencje znaków, które nie są konwertowane na kodowanie docelowe. Jeśli podstawiane znaki nie mogą być transkodowane do kodowania docelowego, środowisko uruchomieniowe wywołuje metodę <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> ponownie z znakami podstawiania, oczekiwany jest metoda <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> zwracająca nową sekwencję podstawiania. Ten proces jest kontynuowany do momentu, gdy środowisko uruchomieniowe ostatecznie zobaczy dobrze sformułowane, Zastępcze podstawienie lub dopóki nie zostanie osiągnięta maksymalna liczba rekursji.

Począwszy od platformy .NET Core 3,0, niestandardowe implementacje <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> muszą zwracać sekwencje znaków, które są konwertowane na kodowanie docelowe. Jeśli podstawiane znaki nie mogą być transkodowane do kodowania docelowego, zostanie zgłoszony <xref:System.ArgumentException>. Środowisko wykonawcze nie będzie już powodowało wywołań cyklicznych do wystąpienia <xref:System.Text.EncoderFallbackBuffer>.

To zachowanie ma zastosowanie tylko wtedy, gdy spełnione są wszystkie trzy z następujących warunków:

- Środowisko uruchomieniowe wykrywa źle sformułowaną sekwencję UTF-16 lub sekwencję UTF-16, której nie można przekonwertować na kodowanie docelowe.
- Określono niestandardową <xref:System.Text.EncoderFallback>.
- Niestandardowy <xref:System.Text.EncoderFallback> próbuje zastąpić nową niesformatowaną lub nieprzekonwertowaną sekwencję UTF-16.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="recommended-action"></a>Zalecana akcja

Większość deweloperów nie musi podejmować wszelkie działania.

Jeśli aplikacja używa niestandardowej klasy <xref:System.Text.EncoderFallback> i <xref:System.Text.EncoderFallbackBuffer>, upewnij się, że implementacja <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> wypełnia bufor rezerwowy przy użyciu poprawnie sformułowanych danych UTF-16, które są bezpośrednio konwertowane na kodowanie docelowe, gdy metoda <xref:System.Text.EncoderFallbackBuffer.Fallback%2A> jest wywoływana po raz pierwszy przez środowiska uruchomieniowego.

#### <a name="category"></a>Kategoria

CoreFx

#### <a name="affected-apis"></a>Narażone interfejsy API

- <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>
- <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Text.EncoderFallbackBuffer.Fallback`
- `M:System.Text.EncoderFallbackBuffer.GetNextChar`

-->
