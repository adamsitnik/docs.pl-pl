---
title: Wykorzystywanie wzorca asynchronicznego opartego na zadaniach
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: 033cf871-ae24-433d-8939-7a3793e547bf
ms.openlocfilehash: f80e6ae520ab03c0f5f4edc30c0b7102193ee6c5
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73139818"
---
# <a name="consuming-the-task-based-asynchronous-pattern"></a>Wykorzystywanie wzorca asynchronicznego opartego na zadaniach

Korzystając ze wzorca asynchronicznego opartego na zadaniach (TAP) do pracy z operacjami asynchronicznymi, można użyć wywołań zwrotnych, aby osiągnąć oczekiwanie bez blokowania.  W przypadku zadań jest to realizowane za poorednictwem metod, takich jak <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType>. Obsługa asynchroniczna oparta na języku ukrywa wywołania zwrotne przez umożliwienie wykonywania operacji asynchronicznych w ramach normalnego przepływu sterowania, a kod wygenerowany przez kompilator zapewnia tę samą obsługę na poziomie interfejsu API.

## <a name="suspending-execution-with-await"></a>Wstrzymywanie wykonywania za pomocą oczekiwania
 Począwszy od .NET Framework 4,5, można użyć słowa kluczowego [await](../../csharp/language-reference/operators/await.md) w C# i [operatora await](../../visual-basic/language-reference/operators/await-operator.md) w Visual Basic, aby asynchronicznie oczekiwać na <xref:System.Threading.Tasks.Task> i <xref:System.Threading.Tasks.Task%601> obiektów. Po oczekiwaniu na <xref:System.Threading.Tasks.Task>wyrażenie `await` jest typu `void`. Po oczekiwaniu na <xref:System.Threading.Tasks.Task%601>wyrażenie `await` jest typu `TResult`. Wyrażenie `await` musi wystąpić wewnątrz treści metody asynchronicznej. Aby uzyskać więcej informacji C# na temat obsługi języka Visual Basic w .NET Framework 4,5, zobacz specyfikacje C# języka i Visual Basic.

 W obszarze okładek funkcja await instaluje wywołanie zwrotne dla zadania przy użyciu kontynuacji.  To wywołanie zwrotne wznawia metodę asynchroniczną w punkcie zawieszenia. Po wznowieniu metody asynchronicznej, jeśli oczekiwana operacja zakończyła się pomyślnie i była <xref:System.Threading.Tasks.Task%601>, zwracany jest `TResult`.  Jeśli <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601>, których oczekiwano, zakończyło się w stanie <xref:System.Threading.Tasks.TaskStatus.Canceled>, zostanie zgłoszony wyjątek <xref:System.OperationCanceledException>.  Jeśli <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601>, których oczekiwano, zakończyło się w stanie <xref:System.Threading.Tasks.TaskStatus.Faulted>, zgłaszany jest wyjątek, który spowodował błąd. `Task` może wystąpić błąd w wyniku wielu wyjątków, ale propagowany jest tylko jeden z tych wyjątków. Jednak Właściwość <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> zwraca wyjątek <xref:System.AggregateException>, który zawiera wszystkie błędy.

 Jeśli kontekst synchronizacji (<xref:System.Threading.SynchronizationContext> Object) jest skojarzony z wątkiem wykonującym metodę asynchroniczną w chwili zawieszenia (na przykład jeśli właściwość <xref:System.Threading.SynchronizationContext.Current%2A?displayProperty=nameWithType> nie jest `null`), Metoda asynchroniczna zostanie wznowiona na tym samym kontekst synchronizacji przy użyciu metody <xref:System.Threading.SynchronizationContext.Post%2A> kontekstu. W przeciwnym razie opiera się na harmonogramie zadań (<xref:System.Threading.Tasks.TaskScheduler> Object), który był aktualny w chwili zawieszenia. Zazwyczaj jest to domyślny harmonogram zadań (<xref:System.Threading.Tasks.TaskScheduler.Default%2A?displayProperty=nameWithType>), który jest przeznaczony dla puli wątków. Ten harmonogram zadań określa, czy oczekiwana operacja asynchroniczna powinna zostać wznowiona, gdy została zakończona, lub czy należy zaplanować wznowienie. Domyślny harmonogram zwykle pozwala na kontynuację działania w wątku, w którym Zakończono operację oczekiwania.

 Gdy wywoływana jest Metoda asynchroniczna, synchronicznie wykonuje treść funkcji do momentu, gdy pierwsze wyrażenie await oczekuje na wystąpienie oczekujące, które nie zostało jeszcze ukończone, a następnie wywołanie wraca do obiektu wywołującego. Jeśli Metoda asynchroniczna nie zwraca `void`, zwracany jest obiekt <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601> reprezentujący bieżące obliczenie. W nieunieważnionej metodzie asynchronicznej, jeśli wystąpiła instrukcja return lub zostanie osiągnięty koniec treści metody, zadanie zostanie wykonane w <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> stanie końcowym. Jeśli nieobsługiwany wyjątek powoduje, że kontrolka opuszcza treść metody asynchronicznej, zadanie kończy się w stanie <xref:System.Threading.Tasks.TaskStatus.Faulted>. Jeśli ten wyjątek jest <xref:System.OperationCanceledException>, zadanie zakończyło się w stanie <xref:System.Threading.Tasks.TaskStatus.Canceled>. W ten sposób wynik lub wyjątek jest ostatecznie publikowany.

 Istnieje kilka ważnych różnic między tym zachowaniem.  Ze względu na wydajność, jeśli zadanie zostało już zakończone przez czas oczekiwania na zadanie, kontrola nie zostanie osiągnięta, a funkcja nadal będzie wykonywana.  Ponadto powrót do oryginalnego kontekstu nie zawsze jest pożądanym zachowaniem i można go zmienić. opisano to szczegółowo w następnej sekcji.

### <a name="configuring-suspension-and-resumption-with-yield-and-configureawait"></a>Konfigurowanie zawieszenia i wznawiania przy użyciu programu Yield i ConfigureAwait
 Kilka metod zapewnia większą kontrolę nad wykonywaniem metody asynchronicznej. Na przykład można użyć metody <xref:System.Threading.Tasks.Task.Yield%2A?displayProperty=nameWithType>, aby wprowadzić punkt Yield do metody asynchronicznej:

```csharp
public class Task : …
{
    public static YieldAwaitable Yield();
    …
}
```

 Jest to równoważne asynchronicznemu księgowaniu lub planowaniu z powrotem do bieżącego kontekstu.

```csharp
Task.Run(async delegate
{
    for(int i=0; i<1000000; i++)
    {
        await Task.Yield(); // fork the continuation into a separate work item
        ...
    }
});
```

 Można również użyć metody <xref:System.Threading.Tasks.Task.ConfigureAwait%2A?displayProperty=nameWithType>, aby lepiej kontrolować zawieszanie i wznawianie w metodzie asynchronicznej.  Jak wspomniano wcześniej, domyślnie bieżący kontekst jest przechwytywany w momencie zawieszenia asynchronicznej metody i ten przechwycony kontekst jest używany do wywołania kontynuacji metody asynchronicznej po wznowieniu.  W wielu przypadkach jest to dokładne zachowanie.  W innych przypadkach nie można uważać na kontekst kontynuacji i można osiągnąć lepszą wydajność, unikając takich ogłoszeń z powrotem do oryginalnego kontekstu.  Aby włączyć tę funkcję, użyj metody <xref:System.Threading.Tasks.Task.ConfigureAwait%2A?displayProperty=nameWithType>, aby poinformować, że Operacja await nie przechwytuje i wznowić w kontekście, ale aby kontynuować wykonywanie wszędzie tam, gdzie operacja asynchroniczna została zakończona:

```csharp
await someTask.ConfigureAwait(continueOnCapturedContext:false);
```

## <a name="canceling-an-asynchronous-operation"></a>Anulowanie operacji asynchronicznej
 Począwszy od .NET Framework 4, naciśnij pozycję metody, które obsługują anulowanie, podaj co najmniej jedno Przeciążenie, które akceptuje token anulowania (<xref:System.Threading.CancellationToken> Object).

 Token anulowania jest tworzony za pomocą źródła tokenu anulowania (<xref:System.Threading.CancellationTokenSource> Object).  Właściwość <xref:System.Threading.CancellationTokenSource.Token%2A> źródła zwraca token anulowania, który zostanie zasygnalizowane, gdy wywoływana jest metoda <xref:System.Threading.CancellationTokenSource.Cancel%2A> źródła.  Na przykład jeśli chcesz pobrać pojedynczą stronę sieci Web i chcesz mieć możliwość anulowania operacji, utworzysz obiekt <xref:System.Threading.CancellationTokenSource>, Przekaż swój token do metody TAP, a następnie Wywołaj metodę <xref:System.Threading.CancellationTokenSource.Cancel%2A> źródła, gdy wszystko będzie gotowe do anulowania operacji :

```csharp
var cts = new CancellationTokenSource();
string result = await DownloadStringAsync(url, cts.Token);
… // at some point later, potentially on another thread
cts.Cancel();
```

 Aby anulować wiele wywołań asynchronicznych, można przekazać ten sam token do wszystkich wywołań:

```csharp
var cts = new CancellationTokenSource();
    IList<string> results = await Task.WhenAll(from url in urls select DownloadStringAsync(url, cts.Token));
    // at some point later, potentially on another thread
    …
    cts.Cancel();
```

 Lub można przekazać ten sam token do selektywnego podzbioru operacji:

```csharp
var cts = new CancellationTokenSource();
    byte [] data = await DownloadDataAsync(url, cts.Token);
    await SaveToDiskAsync(outputPath, data, CancellationToken.None);
    … // at some point later, potentially on another thread
    cts.Cancel();
```

 Żądania anulowania mogą być inicjowane z dowolnego wątku.

 Można przekazać wartość <xref:System.Threading.CancellationToken.None%2A?displayProperty=nameWithType> do dowolnej metody, która akceptuje token anulowania, aby wskazać, że anulowanie nigdy nie będzie wymagane.  Powoduje to, że właściwość <xref:System.Threading.CancellationToken.CanBeCanceled%2A?displayProperty=nameWithType> zwraca `false`, a wywołana metoda może odpowiednio zoptymalizować.  W celach testowych można także przekazać wcześniej anulowany token anulowania, którego wystąpienie jest tworzone przy użyciu konstruktora, który akceptuje wartość logiczną, aby wskazać, czy token powinien zostać uruchomiony w stanie już anulowane lub niemożliwego do anulowania.

 To podejście do anulowania ma kilka zalet:

- Można przekazać ten sam token anulowania do dowolnej liczby operacji asynchronicznych i synchronicznych.

- To samo żądanie anulowania może być rozmnożenia dowolną liczbą odbiorników.

- Deweloper asynchronicznego interfejsu API ma pełną kontrolę nad tym, czy można żądać anulowania i kiedy może on obowiązywać.

- Kod korzystający z interfejsu API może selektywnie określić wywołania asynchroniczne, do których będą propagowane żądania anulowania.

## <a name="monitoring-progress"></a>Postęp monitorowania
 Niektóre metody asynchroniczne uwidaczniają postęp przez interfejs postępu przesłany do metody asynchronicznej.  Rozważmy na przykład funkcję, która asynchronicznie Pobiera ciąg tekstowy, i w sposób podnosi aktualizacje postępu, które obejmują procent pobierania, który został dotąd zakończony.  Taka metoda może być używana w aplikacji Windows Presentation Foundation (WPF) w następujący sposób:

```csharp
private async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.IsEnabled = false;
    try
    {
        txtResult.Text = await DownloadStringAsync(txtUrl.Text,
            new Progress<int>(p => pbDownloadProgress.Value = p));
    }
    finally { btnDownload.IsEnabled = true; }
}
```

<a name="combinators"></a>
## <a name="using-the-built-in-task-based-combinators"></a>Używanie wbudowanych kombinatorów opartych na zadaniach
 Przestrzeń nazw <xref:System.Threading.Tasks> zawiera kilka metod tworzenia i pracy z zadaniami.

### <a name="taskrun"></a>Zadanie. Run
 Klasa <xref:System.Threading.Tasks.Task> zawiera kilka metod <xref:System.Threading.Tasks.Task.Run%2A>, które umożliwiają łatwe odciążanie pracy jako <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601> do puli wątków, na przykład:

```csharp
public async void button1_Click(object sender, EventArgs e)
{
    textBox1.Text = await Task.Run(() =>
    {
        // … do compute-bound work here
        return answer;
    });
}
```

 Niektóre z tych metod <xref:System.Threading.Tasks.Task.Run%2A>, takich jak Przeciążenie <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=nameWithType>, istnieją jako skróty dla metody <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType>.  Inne przeciążenia, takie jak <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=nameWithType>, umożliwiają użycie oczekiwania w ramach odciążonej pracy, na przykład:

```csharp
public async void button1_Click(object sender, EventArgs e)
{
    pictureBox1.Image = await Task.Run(async() =>
    {
        using(Bitmap bmp1 = await DownloadFirstImageAsync())
        using(Bitmap bmp2 = await DownloadSecondImageAsync())
        return Mashup(bmp1, bmp2);
    });
}
```

 Takie przeciążenia są logicznie równoważne z użyciem metody <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> w połączeniu z metodą rozszerzenia <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> w bibliotece zadań równoległych.

### <a name="taskfromresult"></a>Task. FromResult
 Użyj metody <xref:System.Threading.Tasks.Task.FromResult%2A> w scenariuszach, w których dane mogą być już dostępne i wystarczy zwrócić z metody zwracającej zadania do <xref:System.Threading.Tasks.Task%601>:

```csharp
public Task<int> GetValueAsync(string key)
{
    int cachedValue;
    return TryGetCachedValue(out cachedValue) ?
        Task.FromResult(cachedValue) :
        GetValueAsyncInternal();
}

private async Task<int> GetValueAsyncInternal(string key)
{
    …
}
```

### <a name="taskwhenall"></a>Task.WhenAll
 Użyj metody <xref:System.Threading.Tasks.Task.WhenAll%2A>, aby asynchronicznie oczekiwać na wiele operacji asynchronicznych, które są reprezentowane jako zadania.  Metoda ma wiele przeciążeń, które obsługują zestaw zadań nieogólnych lub niejednorodnego zestawu zadań ogólnych (na przykład asynchronicznie czeka na wiele operacji zwracających wartość void lub asynchronicznie czeka na wiele metod zwracających wartości, gdzie Każda wartość może mieć inny typ i umożliwia obsługę jednolitego zestawu zadań ogólnych (takich jak asynchroniczne oczekiwanie na wiele metod zwracających `TResult`).

 Załóżmy, że chcesz wysyłać wiadomości e-mail do kilku klientów. Możesz nakładać się na wysyłanie komunikatów, aby nie czekać na ukończenie jednego komunikatu przed wysłaniem następnego. Możesz również dowiedzieć się, kiedy operacje wysyłania zostały zakończone i czy wystąpiły jakieś błędy:

```csharp
IEnumerable<Task> asyncOps = from addr in addrs select SendMailAsync(addr);
await Task.WhenAll(asyncOps);
```

 Ten kod nie obsługuje jawnie wyjątków, które mogą wystąpić, ale umożliwia propagowanie wyjątków z `await` w wyniku zadania z <xref:System.Threading.Tasks.Task.WhenAll%2A>.  Aby obsłużyć wyjątki, można użyć kodu takiego jak:

```csharp
IEnumerable<Task> asyncOps = from addr in addrs select SendMailAsync(addr);
try
{
    await Task.WhenAll(asyncOps);
}
catch(Exception exc)
{
    ...
}
```

 W takim przypadku, jeśli jakakolwiek operacja asynchroniczna nie powiedzie się, wszystkie wyjątki zostaną skonsolidowane w <xref:System.AggregateException> wyjątek, który jest przechowywany w <xref:System.Threading.Tasks.Task>, który jest zwracany z metody <xref:System.Threading.Tasks.Task.WhenAll%2A>.  Jednak tylko jeden z tych wyjątków jest propagowany przez słowo kluczowe `await`.  Jeśli chcesz przejrzeć wszystkie wyjątki, możesz ponownie napisać poprzedni kod w następujący sposób:

```csharp
Task [] asyncOps = (from addr in addrs select SendMailAsync(addr)).ToArray();
try
{
    await Task.WhenAll(asyncOps);
}
catch(Exception exc)
{
    foreach(Task faulted in asyncOps.Where(t => t.IsFaulted))
    {
        … // work with faulted and faulted.Exception
    }
}
```

 Rozważmy przykład pobierania wielu plików z sieci Web asynchronicznie.  W takim przypadku wszystkie operacje asynchroniczne mają jednorodne typy wyników i łatwo jest uzyskać dostęp do wyników:

```csharp
string [] pages = await Task.WhenAll(
    from url in urls select DownloadStringAsync(url));
```

 Można użyć tych samych technik obsługi wyjątków, które zostały omówione w poprzednim scenariuszu zwracającym wartość pustą:

```csharp
Task [] asyncOps =
    (from url in urls select DownloadStringAsync(url)).ToArray();
try
{
    string [] pages = await Task.WhenAll(asyncOps);
    ...
}
catch(Exception exc)
{
    foreach(Task<string> faulted in asyncOps.Where(t => t.IsFaulted))
    {
        … // work with faulted and faulted.Exception
    }
}
```

### <a name="taskwhenany"></a>Task.WhenAny
 Za pomocą metody <xref:System.Threading.Tasks.Task.WhenAny%2A> można asynchronicznie czekać, aż tylko jedna z wielu operacji asynchronicznych jest reprezentowana jako zadania do wykonania.  Ta metoda służy cztery główne przypadki użycia:

- Nadmiarowość: wielokrotne wykonywanie operacji i wybieranie tej, która kończy się pierwszym (na przykład kontaktowanie się z wieloma usługami sieci Web notowań giełdowych, które spowodują wygenerowanie pojedynczego wyniku i wybranie tego, który zakończy najszybszy).

- Przeplot: uruchamianie wielu operacji i oczekiwanie na ukończenie wszystkich, ale przetwarzanie ich w miarę ich ukończenia.

- Ograniczanie przepustowości: Zezwalanie na wykonywanie dodatkowych operacji w miarę ich kończenia.  Jest to rozszerzenie scenariusza z przeplotem.

- Wczesna bailout: na przykład operacja reprezentowana przez zadanie T1 może być pogrupowana w <xref:System.Threading.Tasks.Task.WhenAny%2A> zadania z innym zadaniem T2 i można oczekiwać na zadanie <xref:System.Threading.Tasks.Task.WhenAny%2A>. Zadanie T2 może reprezentować limit czasu lub anulowanie lub inny sygnał, który powoduje ukończenie zadania <xref:System.Threading.Tasks.Task.WhenAny%2A> przed zakończeniem T1.

#### <a name="redundancy"></a>Nadmiarowości
 Rozważ przypadek, w którym chcesz podjąć decyzję o tym, czy kupić magazyn.  Istnieje kilka zaufanych usług sieci Web, które są zaufane, ale w zależności od dziennego obciążenia każda usługa może zakończyć się wolno w różnym czasie.  Za pomocą metody <xref:System.Threading.Tasks.Task.WhenAny%2A> można odbierać powiadomienia po zakończeniu dowolnej operacji:

```csharp
var recommendations = new List<Task<bool>>()
{
    GetBuyRecommendation1Async(symbol),
    GetBuyRecommendation2Async(symbol),
    GetBuyRecommendation3Async(symbol)
};
Task<bool> recommendation = await Task.WhenAny(recommendations);
if (await recommendation) BuyStock(symbol);
```

 W przeciwieństwie do <xref:System.Threading.Tasks.Task.WhenAll%2A>, która zwraca nieopakowane wyniki wszystkich zadań, które zakończyły się pomyślnie, <xref:System.Threading.Tasks.Task.WhenAny%2A> zwraca zadanie, które zostało zakończone. Jeśli zadanie nie powiedzie się, ważne jest, aby wiedzieć, że zakończyło się niepowodzeniem, a jeśli zadanie zakończyło się pomyślnie, ważne jest, aby wiedzieć, z którym zadaniem jest skojarzona wartość zwracana.  W związku z tym należy uzyskać dostęp do wyniku zwracanego zadania lub w dalszej części tego oczekiwania, jak pokazano w tym przykładzie.

 Tak jak w przypadku <xref:System.Threading.Tasks.Task.WhenAll%2A>należy mieć możliwość uwzględnienia wyjątków.  Ponieważ otrzymujesz zadanie zakończone z powrotem, możesz oczekiwać, że zwrócone zadanie ma błędy propagowane i `try/catch` je odpowiednio; na przykład:

```csharp
Task<bool> [] recommendations = …;
while(recommendations.Count > 0)
{
    Task<bool> recommendation = await Task.WhenAny(recommendations);
    try
    {
        if (await recommendation) BuyStock(symbol);
        break;
    }
    catch(WebException exc)
    {
        recommendations.Remove(recommendation);
    }
}
```

 Ponadto nawet jeśli pierwsze zadanie zostało zakończone pomyślnie, kolejne zadania mogą zakończyć się niepowodzeniem.  W tym momencie masz kilka opcji związanych z wyjątkami: możesz poczekać na zakończenie wszystkich uruchomionych zadań, w tym przypadku można użyć metody <xref:System.Threading.Tasks.Task.WhenAll%2A> lub można zdecydować, że wszystkie wyjątki są ważne i muszą być rejestrowane.  W tym celu można użyć kontynuacji do otrzymywania powiadomień, gdy zadania są wykonywane asynchronicznie:

```csharp
foreach(Task recommendation in recommendations)
{
    var ignored = recommendation.ContinueWith(
        t => { if (t.IsFaulted) Log(t.Exception); });
}
```

 lub:

```csharp
foreach(Task recommendation in recommendations)
{
    var ignored = recommendation.ContinueWith(
        t => Log(t.Exception), TaskContinuationOptions.OnlyOnFaulted);
}
```

 lub nawet:

```csharp
private static async void LogCompletionIfFailed(IEnumerable<Task> tasks)
{
    foreach(var task in tasks)
    {
        try { await task; }
        catch(Exception exc) { Log(exc); }
    }
}
…
LogCompletionIfFailed(recommendations);
```

 Na koniec można anulować wszystkie pozostałe operacje:

```csharp
var cts = new CancellationTokenSource();
var recommendations = new List<Task<bool>>()
{
    GetBuyRecommendation1Async(symbol, cts.Token),
    GetBuyRecommendation2Async(symbol, cts.Token),
    GetBuyRecommendation3Async(symbol, cts.Token)
};

Task<bool> recommendation = await Task.WhenAny(recommendations);
cts.Cancel();
if (await recommendation) BuyStock(symbol);
```

#### <a name="interleaving"></a>Przeplatanie
 Rozważ przypadek, w którym pobierasz obrazy z sieci Web i przetwarzasz każdy obraz (na przykład dodając obraz do kontrolki interfejsu użytkownika).  Należy wykonać przetwarzanie sekwencyjne w wątku interfejsu użytkownika, ale chcesz pobrać obrazy jako współbieżnie, jak to możliwe. Ponadto nie chcesz, aby do interfejsu użytkownika były dodawane obrazy, dopóki nie zostaną pobrane — chcesz je dodać po ich zakończeniu:

```csharp
List<Task<Bitmap>> imageTasks =
    (from imageUrl in urls select GetBitmapAsync(imageUrl)).ToList();
while(imageTasks.Count > 0)
{
    try
    {
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);
        imageTasks.Remove(imageTask);

        Bitmap image = await imageTask;
        panel.AddImage(image);
    }
    catch{}
}
```

 Można również zastosować przeplot do scenariusza, który obejmuje przetwarzanie obliczeniowe na <xref:System.Threading.ThreadPool> pobranych obrazów; na przykład:

```csharp
List<Task<Bitmap>> imageTasks =
    (from imageUrl in urls select GetBitmapAsync(imageUrl)
         .ContinueWith(t => ConvertImage(t.Result)).ToList();
while(imageTasks.Count > 0)
{
    try
    {
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);
        imageTasks.Remove(imageTask);

        Bitmap image = await imageTask;
        panel.AddImage(image);
    }
    catch{}
}
```

#### <a name="throttling"></a>Dławienie
 Rozważmy przykład przeplotu, z tą różnicą, że użytkownik pobiera wiele obrazów, które muszą być ograniczone. na przykład potrzebna jest tylko określona liczba pobrań jednocześnie. Aby to osiągnąć, można uruchomić podzestaw operacji asynchronicznych.  Po zakończeniu operacji można uruchomić dodatkowe operacje, aby wykonać ich miejsce:

```csharp
const int CONCURRENCY_LEVEL = 15;
Uri [] urls = …;
int nextIndex = 0;
var imageTasks = new List<Task<Bitmap>>();
while(nextIndex < CONCURRENCY_LEVEL && nextIndex < urls.Length)
{
    imageTasks.Add(GetBitmapAsync(urls[nextIndex]));
    nextIndex++;
}

while(imageTasks.Count > 0)
{
    try
    {
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);
        imageTasks.Remove(imageTask);

        Bitmap image = await imageTask;
        panel.AddImage(image);
    }
    catch(Exception exc) { Log(exc); }

    if (nextIndex < urls.Length)
    {
        imageTasks.Add(GetBitmapAsync(urls[nextIndex]));
        nextIndex++;
    }
}
```

#### <a name="early-bailout"></a>Wczesna bailout
 Należy wziąć pod uwagę, że oczekujesz, że operacja zostanie ukończona asynchronicznie, gdy jednocześnie odpowie na żądanie anulowania użytkownika (na przykład użytkownik kliknął przycisk Anuluj). Poniższy kod ilustruje ten scenariusz:

```csharp
private CancellationTokenSource m_cts;

public void btnCancel_Click(object sender, EventArgs e)
{
    if (m_cts != null) m_cts.Cancel();
}

public async void btnRun_Click(object sender, EventArgs e)
{
    m_cts = new CancellationTokenSource();
    btnRun.Enabled = false;
    try
    {
        Task<Bitmap> imageDownload = GetBitmapAsync(txtUrl.Text);
        await UntilCompletionOrCancellation(imageDownload, m_cts.Token);
        if (imageDownload.IsCompleted)
        {
            Bitmap image = await imageDownload;
            panel.AddImage(image);
        }
        else imageDownload.ContinueWith(t => Log(t));
    }
    finally { btnRun.Enabled = true; }
}

private static async Task UntilCompletionOrCancellation(
    Task asyncOp, CancellationToken ct)
{
    var tcs = new TaskCompletionSource<bool>();
    using(ct.Register(() => tcs.TrySetResult(true)))
        await Task.WhenAny(asyncOp, tcs.Task);
    return asyncOp;
}
```

 Ta implementacja umożliwia ponowne włączenie interfejsu użytkownika natychmiast po podjęciu decyzji o rezygnacji, ale nie anulowania podstawowych operacji asynchronicznych.  Kolejną alternatywą jest anulowanie operacji oczekujących w przypadku podjęcia decyzji o rezygnacji, ale nie ponowne nawiązanie interfejsu użytkownika do momentu zakończenia operacji, prawdopodobnie z powodu wcześniejszego zakończenia z powodu żądania anulowania:

```csharp
private CancellationTokenSource m_cts;

public async void btnRun_Click(object sender, EventArgs e)
{
    m_cts = new CancellationTokenSource();

    btnRun.Enabled = false;
    try
    {
        Task<Bitmap> imageDownload = GetBitmapAsync(txtUrl.Text, m_cts.Token);
        await UntilCompletionOrCancellation(imageDownload, m_cts.Token);
        Bitmap image = await imageDownload;
        panel.AddImage(image);
    }
    catch(OperationCanceledException) {}
    finally { btnRun.Enabled = true; }
}
```

 Inny przykład wczesnej bailout obejmuje użycie metody <xref:System.Threading.Tasks.Task.WhenAny%2A> w połączeniu z metodą <xref:System.Threading.Tasks.Task.Delay%2A>, zgodnie z opisem w następnej sekcji.

### <a name="taskdelay"></a>Task.Delay
 Za pomocą metody <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> można wprowadzać pauzy do wykonania metody asynchronicznej.  Jest to przydatne w przypadku wielu rodzajów funkcjonalności, w tym tworzenia pętli sondowania i opóźnieniu obsługi danych wejściowych użytkownika przez określony czas.  Metoda <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> może być również przydatna w połączeniu z <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> do implementowania limitów czasu dla oczekiwania.

 Jeśli zadanie, które jest częścią większej liczby operacji asynchronicznej (na przykład usługa sieci Web ASP.NET) trwa zbyt długo, ogólna operacja może pogorszyć się, zwłaszcza jeśli nie zostanie ukończona.  Z tego powodu ważne jest, aby mieć możliwość przekroczenia limitu czasu podczas oczekiwania na operację asynchroniczną.  Metody synchroniczne <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Task.WaitAll%2A?displayProperty=nameWithType>i <xref:System.Threading.Tasks.Task.WaitAny%2A?displayProperty=nameWithType> akceptują wartości limitu czasu, ale odpowiadające im <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType>/<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> i wymienione wcześniej <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>/metody <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> nie.  Zamiast tego można użyć kombinacji <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> i <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> w celu zaimplementowania limitu czasu.

 Na przykład w aplikacji interfejsu użytkownika Załóżmy, że chcesz pobrać obraz i wyłączyć interfejs użytkownika podczas pobierania obrazu. Jeśli jednak pobieranie trwa zbyt długo, należy ponownie włączyć interfejs użytkownika i odrzucić pobieranie:

```csharp
public async void btnDownload_Click(object sender, EventArgs e)
{
    btnDownload.Enabled = false;
    try
    {
        Task<Bitmap> download = GetBitmapAsync(url);
        if (download == await Task.WhenAny(download, Task.Delay(3000)))
        {
            Bitmap bmp = await download;
            pictureBox.Image = bmp;
            status.Text = "Downloaded";
        }
        else
        {
            pictureBox.Image = null;
            status.Text = "Timed out";
            var ignored = download.ContinueWith(
                t => Trace("Task finally completed"));
        }
    }
    finally { btnDownload.Enabled = true; }
}
```

 To samo dotyczy wielu pobrań, ponieważ <xref:System.Threading.Tasks.Task.WhenAll%2A> zwraca zadanie:

```csharp
public async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.Enabled = false;
    try
    {
        Task<Bitmap[]> downloads =
            Task.WhenAll(from url in urls select GetBitmapAsync(url));
        if (downloads == await Task.WhenAny(downloads, Task.Delay(3000)))
        {
            foreach(var bmp in downloads) panel.AddImage(bmp);
            status.Text = "Downloaded";
        }
        else
        {
            status.Text = "Timed out";
            downloads.ContinueWith(t => Log(t));
        }
    }
    finally { btnDownload.Enabled = true; }
}
```

## <a name="building-task-based-combinators"></a>Tworzenie kombinatorów opartych na zadaniach
 Ponieważ zadanie jest w stanie całkowicie reprezentować operację asynchroniczną i zapewnić funkcje synchroniczne i asynchroniczne do dołączania do operacji, pobierając wyniki i tak dalej, można utworzyć przydatne biblioteki kombinatorów, które tworzą zadania w Kompiluj większe wzorce.  Zgodnie z opisem w poprzedniej sekcji .NET Framework zawiera kilka wbudowanych kombinatorów, ale można również utworzyć własne. Poniższe sekcje zawierają kilka przykładów potencjalnych metod i typów Combinator.

### <a name="retryonfault"></a>RetryOnFault
 W wielu sytuacjach można ponowić próbę wykonania operacji, jeśli poprzednia próba zakończy się niepowodzeniem.  W przypadku kodu synchronicznego można utworzyć metodę pomocnika, taką jak `RetryOnFault`, w poniższym przykładzie, aby to zrobić:

```csharp
public static T RetryOnFault<T>(
    Func<T> function, int maxTries)
{
    for(int i=0; i<maxTries; i++)
    {
        try { return function(); }
        catch { if (i == maxTries-1) throw; }
    }
    return default(T);
}
```

 Można skompilować prawie identyczną metodę pomocnika dla operacji asynchronicznych, które są implementowane za pomocą polecenia TAP i w ten sposób zwracają zadania:

```csharp
public static async Task<T> RetryOnFault<T>(
    Func<Task<T>> function, int maxTries)
{
    for(int i=0; i<maxTries; i++)
    {
        try { return await function().ConfigureAwait(false); }
        catch { if (i == maxTries-1) throw; }
    }
    return default(T);
}
```

 Następnie można użyć tego Combinator do zakodowania ponownych prób w logice aplikacji; na przykład:

```csharp
// Download the URL, trying up to three times in case of failure
string pageContents = await RetryOnFault(
    () => DownloadStringAsync(url), 3);
```

 Można również rozszerzyć funkcję `RetryOnFault`. Na przykład funkcja może zaakceptować kolejną `Func<Task>`, która zostanie wywołana między ponownymi próbami, aby określić, kiedy należy wykonać operację ponownie; na przykład:

```csharp
public static async Task<T> RetryOnFault<T>(
    Func<Task<T>> function, int maxTries, Func<Task> retryWhen)
{
    for(int i=0; i<maxTries; i++)
    {
        try { return await function().ConfigureAwait(false); }
        catch { if (i == maxTries-1) throw; }
        await retryWhen().ConfigureAwait(false);
    }
    return default(T);
}
```

 Następnie można użyć funkcji w następujący sposób, aby poczekać na sekundę przed ponowieniem próby wykonania operacji:

```csharp
// Download the URL, trying up to three times in case of failure,
// and delaying for a second between retries
string pageContents = await RetryOnFault(
    () => DownloadStringAsync(url), 3, () => Task.Delay(1000));
```

### <a name="needonlyone"></a>NeedOnlyOne
 Czasami możesz skorzystać z nadmiarowości, aby poprawić opóźnienia operacji i szanse na sukces.  Należy wziąć pod uwagę wiele usług sieci Web, które zapewniają notowanie giełdowe, ale w różnych porach dnia każda usługa może zapewnić różne poziomy jakości i czasu odpowiedzi.  Aby obsłużyć te wahania, możesz wydać żądania do wszystkich usług sieci Web i zaraz po otrzymaniu odpowiedzi z jednej z nich anulować pozostałe żądania.  Można zaimplementować funkcję pomocnika, aby ułatwić implementowanie tego wspólnego wzorca uruchamiania wielu operacji, oczekiwanie na dowolny, a następnie anulowanie reszty. W poniższym przykładzie funkcja `NeedOnlyOne` ilustruje ten scenariusz:

```csharp
public static async Task<T> NeedOnlyOne(
    params Func<CancellationToken,Task<T>> [] functions)
{
    var cts = new CancellationTokenSource();
    var tasks = (from function in functions
                 select function(cts.Token)).ToArray();
    var completed = await Task.WhenAny(tasks).ConfigureAwait(false);
    cts.Cancel();
    foreach(var task in tasks)
    {
        var ignored = task.ContinueWith(
            t => Log(t), TaskContinuationOptions.OnlyOnFaulted);
    }
    return completed;
}
```

 Następnie można użyć tej funkcji w następujący sposób:

```csharp
double currentPrice = await NeedOnlyOne(
    ct => GetCurrentPriceFromServer1Async("msft", ct),
    ct => GetCurrentPriceFromServer2Async("msft", ct),
    ct => GetCurrentPriceFromServer3Async("msft", ct));
```

### <a name="interleaved-operations"></a>Operacje z przeplotem
 Istnieje potencjalny problem z wydajnością przy użyciu metody <xref:System.Threading.Tasks.Task.WhenAny%2A> do obsługi scenariusza z przeplotem podczas pracy z bardzo dużymi zestawami zadań. Każde wywołanie <xref:System.Threading.Tasks.Task.WhenAny%2A> powoduje, że kontynuacja jest rejestrowana przy każdym zadaniu. W przypadku N liczba zadań w wyniku operacji z przeplotem zostanie (N<sup>2</sup>) kontynuowane. Jeśli pracujesz z dużym zestawem zadań, możesz użyć Combinator (`Interleaved` w poniższym przykładzie), aby rozwiązać problem z wydajnością:

```csharp
static IEnumerable<Task<T>> Interleaved<T>(IEnumerable<Task<T>> tasks)
{
    var inputTasks = tasks.ToList();
    var sources = (from _ in Enumerable.Range(0, inputTasks.Count)
                   select new TaskCompletionSource<T>()).ToList();
    int nextTaskIndex = -1;
    foreach (var inputTask in inputTasks)
    {
        inputTask.ContinueWith(completed =>
        {
            var source = sources[Interlocked.Increment(ref nextTaskIndex)];
            if (completed.IsFaulted)
                source.TrySetException(completed.Exception.InnerExceptions);
            else if (completed.IsCanceled)
                source.TrySetCanceled();
            else
                source.TrySetResult(completed.Result);
        }, CancellationToken.None,
           TaskContinuationOptions.ExecuteSynchronously,
           TaskScheduler.Default);
    }
    return from source in sources
           select source.Task;
}
```

 Następnie można użyć Combinator, aby przetwarzać wyniki zadań po ich zakończeniu. na przykład:

```csharp
IEnumerable<Task<int>> tasks = ...;
foreach(var task in Interleaved(tasks))
{
    int result = await task;
    …
}
```

### <a name="whenallorfirstexception"></a>WhenAllOrFirstException
 W niektórych scenariuszach punktowania/zbierania możesz oczekiwać na wszystkie zadania w zestawie, chyba że wystąpił błąd jednego z nich, w takim przypadku chcesz przerwać oczekiwanie od razu po wystąpieniu wyjątku.  Można to zrobić za pomocą metody Combinator, takiej jak `WhenAllOrFirstException` w poniższym przykładzie:

```csharp
public static Task<T[]> WhenAllOrFirstException<T>(IEnumerable<Task<T>> tasks)
{
    var inputs = tasks.ToList();
    var ce = new CountdownEvent(inputs.Count);
    var tcs = new TaskCompletionSource<T[]>();

    Action<Task> onCompleted = (Task completed) =>
    {
        if (completed.IsFaulted)
            tcs.TrySetException(completed.Exception.InnerExceptions);
        if (ce.Signal() && !tcs.Task.IsCompleted)
            tcs.TrySetResult(inputs.Select(t => t.Result).ToArray());
    };

    foreach (var t in inputs) t.ContinueWith(onCompleted);
    return tcs.Task;
}
```

## <a name="building-task-based-data-structures"></a>Tworzenie struktur danych opartych na zadaniach
 Oprócz możliwości kompilowania niestandardowych kombinatorów opartych na zadaniach, mających strukturę danych w <xref:System.Threading.Tasks.Task> i <xref:System.Threading.Tasks.Task%601>, która reprezentuje zarówno wyniki operacji asynchronicznej, jak i konieczna synchronizacja do dołączenia, sprawia, że jest to bardzo zaawansowany typ które umożliwiają tworzenie niestandardowych struktur danych, które mają być używane w scenariuszach asynchronicznych.

### <a name="asynccache"></a>AsyncCache
 Jednym z ważnych aspektów zadania jest to, że może on zostać przekazany do wielu odbiorców, wszyscy z nich mogą go oczekiwać, zarejestrować kontynuację, uzyskać wynik lub wyjątki (w przypadku <xref:System.Threading.Tasks.Task%601>) i tak dalej.  Dzięki temu <xref:System.Threading.Tasks.Task> i <xref:System.Threading.Tasks.Task%601> idealnie dopasowane do użycia w asynchronicznej infrastrukturze buforowania.  Oto przykład małej, ale zaawansowanej asynchronicznej pamięci podręcznej utworzonej na podstawie <xref:System.Threading.Tasks.Task%601>:

```csharp
public class AsyncCache<TKey, TValue>
{
    private readonly Func<TKey, Task<TValue>> _valueFactory;
    private readonly ConcurrentDictionary<TKey, Lazy<Task<TValue>>> _map;

    public AsyncCache(Func<TKey, Task<TValue>> valueFactory)
    {
        if (valueFactory == null) throw new ArgumentNullException("loader");
        _valueFactory = valueFactory;
        _map = new ConcurrentDictionary<TKey, Lazy<Task<TValue>>>();
    }

    public Task<TValue> this[TKey key]
    {
        get
        {
            if (key == null) throw new ArgumentNullException("key");
            return _map.GetOrAdd(key, toAdd =>
                new Lazy<Task<TValue>>(() => _valueFactory(toAdd))).Value;
        }
    }
}
```

 [AsyncCache\<TKey, TValue >](https://devblogs.microsoft.com/pfxteam/parallelextensionsextras-tour-12-asynccache/) Klasa akceptuje jako delegata do jego konstruktora funkcję, która pobiera `TKey` i zwraca <xref:System.Threading.Tasks.Task%601>.  Wszystkie poprzednio używane wartości z pamięci podręcznej są przechowywane w słowniku wewnętrznym, a `AsyncCache` zapewnia generowanie tylko jednego zadania na klucz, nawet jeśli dostęp do pamięci podręcznej odbywa się współbieżnie.

 Na przykład można utworzyć pamięć podręczną dla pobranych stron sieci Web:

```csharp
private AsyncCache<string,string> m_webPages =
    new AsyncCache<string,string>(DownloadStringAsync);
```

 Tej pamięci podręcznej można następnie użyć w metodach asynchronicznych zawsze, gdy potrzebna jest zawartość strony sieci Web. Klasa `AsyncCache` zapewnia pobieranie możliwie najmniejszej liczby stron i buforowanie wyników.

```csharp
private async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.IsEnabled = false;
    try
    {
        txtContents.Text = await m_webPages["https://www.microsoft.com"];
    }
    finally { btnDownload.IsEnabled = true; }
}
```

### <a name="asyncproducerconsumercollection"></a>AsyncProducerConsumerCollection
 Można również użyć zadań do kompilowania struktur danych do koordynowania działań asynchronicznych.  Rozważmy jeden z klasycznych wzorców projektów równoległych: producent/konsument.  W tym wzorcu producenci generują dane, które są używane przez konsumentów, a producenci i konsumenci mogą działać równolegle. Na przykład Odbiorca przetwarza element 1, który został wcześniej wygenerowany przez producenta, który teraz produkuje element 2.  W przypadku wzorca producent/odbiorca niezmiennie potrzeba pewnej struktury danych do przechowywania pracy utworzonej przez producentów, aby konsumenci mogli otrzymywać powiadomienia o nowych danych i znajdować je, jeśli są dostępne.

 Oto prosta struktura danych oparta na zadaniach, które umożliwiają stosowanie metod asynchronicznych jako producentów i konsumentów:

```csharp
public class AsyncProducerConsumerCollection<T>
{
    private readonly Queue<T> m_collection = new Queue<T>();
    private readonly Queue<TaskCompletionSource<T>> m_waiting =
        new Queue<TaskCompletionSource<T>>();

    public void Add(T item)
    {
        TaskCompletionSource<T> tcs = null;
        lock (m_collection)
        {
            if (m_waiting.Count > 0) tcs = m_waiting.Dequeue();
            else m_collection.Enqueue(item);
        }
        if (tcs != null) tcs.TrySetResult(item);
    }

    public Task<T> Take()
    {
        lock (m_collection)
        {
            if (m_collection.Count > 0)
            {
                return Task.FromResult(m_collection.Dequeue());
            }
            else
            {
                var tcs = new TaskCompletionSource<T>();
                m_waiting.Enqueue(tcs);
                return tcs.Task;
            }
        }
    }
}
```

 Dzięki tej strukturze danych można napisać kod, taki jak następujące:

```csharp
private static AsyncProducerConsumerCollection<int> m_data = …;
…
private static async Task ConsumerAsync()
{
    while(true)
    {
        int nextItem = await m_data.Take();
        ProcessNextItem(nextItem);
    }
}
…
private static void Produce(int data)
{
    m_data.Add(data);
}
```

Przestrzeń nazw <xref:System.Threading.Tasks.Dataflow> zawiera typ <xref:System.Threading.Tasks.Dataflow.BufferBlock%601>, którego można użyć w podobny sposób, ale bez konieczności kompilowania niestandardowego typu kolekcji:

```csharp
private static BufferBlock<int> m_data = …;
…
private static async Task ConsumerAsync()
{
    while(true)
    {
        int nextItem = await m_data.ReceiveAsync();
        ProcessNextItem(nextItem);
    }
}
…
private static void Produce(int data)
{
    m_data.Post(data);
}
```

> [!NOTE]
> Przestrzeń nazw <xref:System.Threading.Tasks.Dataflow> jest dostępna w .NET Framework 4,5 za pomocą narzędzia **NuGet**. Aby zainstalować zestaw, który zawiera <xref:System.Threading.Tasks.Dataflow> przestrzeni nazw, Otwórz projekt w programie Visual Studio, wybierz polecenie **Zarządzaj pakietami NuGet** z menu Projekt i Wyszukaj w trybie online pakiet Microsoft. TPL. przepływu danych.

## <a name="see-also"></a>Zobacz także

- [Wzorzec asynchroniczny oparty na zadaniach (TAP)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)
- [Implementowanie wzorca asynchronicznego opartego na zadaniach](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)
- [Współdziałanie z innymi wzorcami asynchronicznymi i typami](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)
