---
title: Niestandardowe partycjonery dla PLINQ i TPL
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, partitioners
ms.assetid: 96153688-9a01-47c4-8430-909cee9a2887
ms.openlocfilehash: 8caea6d8a97b8c0daf7c59718479ea2e12a52d78
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73141566"
---
# <a name="custom-partitioners-for-plinq-and-tpl"></a>Niestandardowe partycjonery dla PLINQ i TPL

Aby zrównoleglanie operację do źródła danych, jednym z najważniejszych kroków jest *partycjonowanie* źródła w wielu sekcjach, do których można uzyskać dostęp jednocześnie przez wiele wątków. PLINQ i Biblioteka zadań równoległych (TPL) zapewniają domyślne partycje, które działają w sposób przezroczysty podczas pisania kwerendy równoległej lub pętli <xref:System.Threading.Tasks.Parallel.ForEach%2A>. W przypadku bardziej zaawansowanych scenariuszy można podłączyć własną partycję.

## <a name="kinds-of-partitioning"></a>Rodzaje partycjonowania

Istnieje wiele sposobów partycjonowania źródła danych. W najbardziej wydajnych podejściach wiele wątków współdziała w celu przetworzenia oryginalnej sekwencji źródłowej, a nie fizycznego oddzielenia źródła na wiele podsekwencji. W przypadku tablic i innych indeksowanych źródeł, takich jak kolekcje <xref:System.Collections.IList>, w których długość jest znana z wyprzedzeniem, *partycjonowanie zakresu* jest Najprostszym rodzajem partycjonowania. Każdy wątek otrzymuje unikatowy indeks początkowy i końcowy, dzięki czemu może przetwarzać swój zakres źródła bez zastępowania lub przesłonięcia przez inny wątek. Jedyne obciążenie związane z partycjonowaniem zakresu jest początkową pracą tworzenia zakresów; po tym zakończeniu nie jest wymagana żadna dodatkowa synchronizacja. W związku z tym może zapewnić dobrą wydajność, o ile obciążenie jest podzielone równomiernie. Wadą partycjonowania zakresu jest to, że jeśli jeden wątek kończy się wczesnie, nie może pomóc innym wątkom zakończyć pracę.

W przypadku list połączonych lub innych kolekcji, których długość nie jest znana, można użyć *partycjonowania fragmentów*. W przypadku partycjonowania fragmentów każdy wątek lub zadanie w pętli równoległej lub zapytaniu zużywa pewną liczbę elementów źródłowych w jednym fragmencie, przetwarza je, a następnie wraca do pobrania dodatkowych elementów. Partycja gwarantuje, że wszystkie elementy są dystrybuowane i że nie ma duplikatów. Fragment może być dowolnym rozmiarem. Na przykład partycja, która jest przedstawiona w [instrukcje: implementowanie partycji dynamicznych](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md) tworzy fragmenty, które zawierają tylko jeden element. Tak długo, jak fragmenty nie są zbyt duże, ten rodzaj partycjonowania jest założenia równoważenia obciążenia, ponieważ przypisanie elementów do wątków nie jest wstępnie ustalone. Jednak program Partitioner ponosi obciążenie związane z synchronizacją za każdym razem, gdy wątek musi uzyskać kolejny fragment. Ilość synchronizacji ponoszonych w tych przypadkach jest odwrotnie proporcjonalna do rozmiaru fragmentów.

Ogólnie partycjonowanie zakresu jest szybsze, gdy czas wykonywania delegata jest mały do umiarkowany, a źródło ma dużą liczbę elementów, a całkowita praca każdej partycji jest w przybliżeniu równoważna. Partycjonowanie fragmentów jest zatem ogólnie szybsze w większości przypadków. W przypadku źródeł o niewielkiej liczbie elementów lub dłuższym czasie wykonywania dla delegata, wydajność partycjonowania fragmentu i zakresu jest równa.

Partycje TPL obsługują również dynamiczną liczbę partycji. Oznacza to, że mogą tworzyć partycje na bieżąco, na przykład gdy pętla <xref:System.Threading.Tasks.Parallel.ForEach%2A> duplikuje nowe zadanie. Ta funkcja umożliwia skalowanie ze sobą przy użyciu samej pętli. Dynamiczne partycje są również z równoważeniem obciążenia. Podczas tworzenia niestandardowej partycji należy obsługiwać partycjonowanie dynamiczne, aby można było go używać z pętli <xref:System.Threading.Tasks.Parallel.ForEach%2A>.

### <a name="configuring-load-balancing-partitioners-for-plinq"></a>Konfigurowanie partycji równoważenia obciążenia dla PLINQ

Niektóre przeciążenia metody <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=nameWithType> umożliwiają utworzenie partycji dla tablicy lub źródła <xref:System.Collections.IList> i określenie, czy należy podjąć próbę zrównoważenia obciążenia między wątki. Gdy partycja jest skonfigurowana do równoważenia obciążenia, używane jest partycjonowanie fragmentu, a elementy są przekazywane do każdej partycji w małych fragmentach w miarę ich żądania. Takie podejście pozwala upewnić się, że wszystkie partycje mają elementy do przetworzenia, dopóki cała pętla lub kwerenda nie zostanie ukończona. Dodatkowe Przeciążenie można wykorzystać w celu zapewnienia partycjonowania w ramach równoważenia obciążenia dowolnego źródła <xref:System.Collections.IEnumerable>.

Ogólnie rzecz biorąc, równoważenie obciążenia wymaga, aby partycje często żądały elementów z partycji. Z kolei partycja, która umożliwia partycjonowanie statycznej, może przypisywać elementy do każdego programu Partitioner wszystkie jednocześnie, używając partycjonowania zakresu lub fragmentu. Wymaga to mniejszego obciążenia niż Równoważenie obciążenia, ale może trwać dłużej, jeśli jeden wątek zostanie zakończony znacznie większym nakładem pracy niż inne. Domyślnie, gdy przeszedł element IList lub Array, PLINQ zawsze używa partycjonowania zakresu bez równoważenia obciążenia. Aby włączyć równoważenie obciążenia dla PLINQ, użyj metody `Partitioner.Create`, jak pokazano w poniższym przykładzie.

[!code-csharp[TPL_Partitioners#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#02)]
[!code-vb[TPL_Partitioners#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionsnippets_vb.vb#02)]

Najlepszym sposobem, aby określić, czy należy używać równoważenia obciążenia w danym scenariuszu, jest eksperymentowanie i pomiar, jak długo trwa wykonywanie operacji w ramach reprezentatywnych obciążeń i konfiguracji komputerów. Na przykład partycjonowanie statyczne może zapewnić znaczący przyspieszenie na komputerze z wieloma rdzeniami, który ma tylko kilka rdzeni, ale może to spowodować spowolnienie na komputerach mających stosunkowo wiele rdzeni.

Poniższa tabela zawiera listę dostępnych przeciążeń metody <xref:System.Collections.Concurrent.Partitioner.Create%2A>. Te partycje nie są ograniczone do użycia tylko z PLINQ lub <xref:System.Threading.Tasks.Task>. Mogą być również używane w przypadku dowolnej niestandardowej konstrukcji równoległej.

|Występują|Używa równoważenia obciążenia|
|--------------|-------------------------|
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|stałego|
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28%60%600%5B%5D%2CSystem.Boolean%29>|Gdy argument logiczny jest określony jako true|
|<xref:System.Collections.Concurrent.Partitioner.Create%60%601%28System.Collections.Generic.IList%7B%60%600%7D%2CSystem.Boolean%29>|Gdy argument logiczny jest określony jako true|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%29>|Ustawione|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int32%2CSystem.Int32%2CSystem.Int32%29>|Ustawione|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%29>|Ustawione|
|<xref:System.Collections.Concurrent.Partitioner.Create%28System.Int64%2CSystem.Int64%2CSystem.Int64%29>|Ustawione|

### <a name="configuring-static-range-partitioners-for-parallelforeach"></a>Konfigurowanie partycji zakresów statycznych dla elementu Parallel. ForEach

W pętli <xref:System.Threading.Tasks.Parallel.For%2A> treść pętli jest udostępniana metodzie jako delegat. Koszt wywołania tego delegata jest taki sam jak wywołanie metody wirtualnej. W niektórych scenariuszach treść pętli równoległej może być wystarczająco mała, że koszt wywołania delegata w każdej iteracji zostanie znaczący. W takich sytuacjach można użyć jednego z przeciążeń <xref:System.Collections.Concurrent.Partitioner.Create%2A>, aby utworzyć <xref:System.Collections.Generic.IEnumerable%601> partycji zakresu względem elementów źródłowych. Następnie można przekazać tę kolekcję zakresów do metody <xref:System.Threading.Tasks.Parallel.ForEach%2A>, której treść składa się z zwykłej pętli `for`owej. Zaletą tego podejścia jest to, że koszt wywołania delegata jest naliczany tylko raz dla każdego zakresu, a nie raz na element. Poniższy przykład demonstruje wzorzec podstawowy.

[!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
[!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]

Każdy wątek w pętli otrzymuje własne <xref:System.Tuple%602>, które zawierają początkową i końcową wartość indeksu w określonym zakresie. Wewnętrzna pętla `for` używa wartości `fromInclusive` i `toExclusive` do bezpośredniej pętli tablicy lub <xref:System.Collections.IList>.

Jeden z przeciążeń <xref:System.Collections.Concurrent.Partitioner.Create%2A> umożliwia określenie rozmiaru partycji i liczby partycji. Tego przeciążenia można używać w scenariuszach, w których prace na element są tak niskie, że nawet jedno wywołanie metody wirtualnej na element ma zauważalny wpływ na wydajność.

## <a name="custom-partitioners"></a>Niestandardowe partycje

W niektórych scenariuszach może być wartościowa, a nawet wymagane do zaimplementowania własnego programu Partitioner. Na przykład może istnieć niestandardowa Klasa kolekcji, która może być bardziej wydajna niż domyślna partycja, na podstawie wiedzy o wewnętrznej strukturze klasy. Możesz również utworzyć partycje zakresu o różnych rozmiarach na podstawie wiedzy o tym, jak długo będzie przetwarzać elementy w różnych lokalizacjach w kolekcji źródłowej.

Aby utworzyć podstawową partycję niestandardową, Utwórz klasę z <xref:System.Collections.Concurrent.Partitioner%601?displayProperty=nameWithType> i Zastąp metody wirtualne zgodnie z opisem w poniższej tabeli.

|||
|-|-|
|<xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>|Ta metoda jest wywoływana raz przez wątek główny i zwraca IList (IEnumerator (TSource)). Każdy wątek roboczy w pętli lub zapytaniu może wywoływać `GetEnumerator` na liście, aby pobrać <xref:System.Collections.Generic.IEnumerator%601> na oddzielnej partycji.|
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|Zwróć `true` w przypadku zaimplementowania <xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>, w przeciwnym razie, `false`.|
|<xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>|Jeśli <xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A> jest `true`, ta metoda może być wywoływana zamiast <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>.|

Jeśli wyniki muszą być sortowane lub wymagają dostępu indeksowanego do elementów, utwórz je od <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=nameWithType> i Zastąp metody wirtualne zgodnie z opisem w poniższej tabeli.

|||
|-|-|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetPartitions%2A>|Ta metoda jest wywoływana raz przez wątek główny i zwraca `IList(IEnumerator(TSource))`. Każdy wątek roboczy w pętli lub zapytaniu może wywoływać `GetEnumerator` na liście, aby pobrać <xref:System.Collections.Generic.IEnumerator%601> na oddzielnej partycji.|
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|Zwróć `true` w przypadku zaimplementowania <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>; w przeciwnym razie false.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetDynamicPartitions%2A>|Zazwyczaj to właśnie wywołuje <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A>|Jeśli <xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A> jest `true`, ta metoda może być wywoływana zamiast <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>.|

W poniższej tabeli znajdują się dodatkowe szczegółowe informacje o tym, jak trzy rodzaje partycji równoważenia obciążenia implementują klasę <xref:System.Collections.Concurrent.OrderablePartitioner%601>.

|Metoda/Właściwość|Elementy IList/Array bez równoważenia obciążenia|Elementy IList/Array z równoważeniem obciążenia|IEnumerable|
|----------------------|-------------------------------------------|----------------------------------------|-----------------|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>|Używa partycjonowania zakresu|Używa partycjonowania fragmentów zoptymalizowanego dla list dla partitionCount określonych|Używa partycjonowania fragmentów przez utworzenie statycznej liczby partycji.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A?displayProperty=nameWithType>|Zgłasza wyjątek nieobsługiwany|Używa partycjonowania fragmentów zoptymalizowanego pod kątem list i partycji dynamicznych|Używa partycjonowania fragmentów przez utworzenie dynamicznej liczby partycji.|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedInEachPartition%2A>|Zwraca `true`|Zwraca `true`|Zwraca `true`|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysOrderedAcrossPartitions%2A>|Zwraca `true`|Zwraca `false`|Zwraca `false`|
|<xref:System.Collections.Concurrent.OrderablePartitioner%601.KeysNormalized%2A>|Zwraca `true`|Zwraca `true`|Zwraca `true`|
|<xref:System.Collections.Concurrent.Partitioner%601.SupportsDynamicPartitions%2A>|Zwraca `false`|Zwraca `true`|Zwraca `true`|

### <a name="dynamic-partitions"></a>Partycje dynamiczne

Jeśli zamierzasz używać partycji w metodzie <xref:System.Threading.Tasks.Parallel.ForEach%2A>, musisz mieć możliwość zwrócenia dynamicznej liczby partycji. Oznacza to, że partycja może dostarczyć moduł wyliczający dla nowej partycji na żądanie w dowolnym momencie podczas wykonywania pętli. W zasadzie Każda pętla dodaje nowe zadanie równoległe, żąda nowej partycji dla tego zadania. Jeśli wymaga się, aby dane były możliwe do uporządkowania, należy utworzyć je od <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=nameWithType> tak, aby każdy element w każdej partycji miał przypisany unikatowy indeks.

Aby uzyskać więcej informacji, zobacz [temat jak: implementowanie partycji dynamicznych](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md).

### <a name="contract-for-partitioners"></a>Kontrakt dla partycji

Podczas implementowania niestandardowego programu Partitioner postępuj zgodnie z poniższymi wskazówkami, aby zapewnić poprawną interakcję z PLINQ i <xref:System.Threading.Tasks.Parallel.ForEach%2A> w TPL:

- Jeśli <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> jest wywoływana z argumentem równym zero lub mniejszym dla `partitionsCount`, throw <xref:System.ArgumentOutOfRangeException>. Mimo że PLINQ i TPL nigdy nie przekażą do `partitionCount` równej 0, jednak zalecamy ochronę przed możliwością.

- <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A> i <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A> powinny zawsze zwracać `partitionsCount` liczbę partycji. Jeśli program partitioner nie może utworzyć tylu partycji zgodnie z żądaniem, metoda powinna zwrócić pusty moduł wyliczający dla każdej z pozostałych partycji. W przeciwnym razie zarówno PLINQ, jak i TPL będą zgłaszać <xref:System.InvalidOperationException>.

- <xref:System.Collections.Concurrent.Partitioner%601.GetPartitions%2A>, <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderablePartitions%2A>, <xref:System.Collections.Concurrent.Partitioner%601.GetDynamicPartitions%2A>i <xref:System.Collections.Concurrent.OrderablePartitioner%601.GetOrderableDynamicPartitions%2A> nigdy nie powinny zwracać `null` (`Nothing` w Visual Basic). W takim przypadku PLINQ/TPL zgłosi <xref:System.InvalidOperationException>.

- Metody, które zwracają partycje, powinny zawsze zwracać partycje, które mogą w pełni i jednoznacznie wyliczyć źródło danych. Nie powinno być duplikowane w źródle danych ani elementy pominięte, chyba że jest to wymagane przez projekt partycji. Jeśli ta reguła nie zostanie zastosowana, kolejność danych wyjściowych może zostać zaszyfrowana.

- Następujące metody pobierające dane logiczne muszą zawsze prawidłowo zwracać następujące wartości, aby kolejność wyjściowa nie została zaszyfrowana:

  - `KeysOrderedInEachPartition`: Każda partycja zwraca elementy z rosnącymi indeksami kluczy.

  - `KeysOrderedAcrossPartitions`: dla wszystkich zwracanych partycji, indeksy kluczy na partycji *i* są wyższe niż indeksy kluczy na partycji *i*-1.

  - `KeysNormalized`: wszystkie indeksy kluczowych monotonicznie zwiększają się bez przerw, zaczynając od zera.

- Wszystkie indeksy muszą być unikatowe. Nie można duplikować indeksów. Jeśli ta reguła nie zostanie zastosowana, kolejność danych wyjściowych może zostać zaszyfrowana.

- Wszystkie indeksy muszą być nieujemne. Jeśli ta reguła nie zostanie zastosowana, PLINQ/TPL może zgłosić wyjątki.

## <a name="see-also"></a>Zobacz także

- [Programowanie równoległe](../../../docs/standard/parallel-programming/index.md)
- [Instrukcje: implementowanie partycji dynamicznych](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md)
- [Instrukcje: implementowanie partycjonera dla partycjonowania statycznego](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)
