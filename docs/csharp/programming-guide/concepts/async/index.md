---
title: Programowanie asynchroniczne wC#
description: Omówienie C# obsługi programowania asynchronicznego przy użyciu asynchronicznych, oczekujących, zadań i zadań<T>
ms.date: 03/18/2019
ms.openlocfilehash: 4ed48a2e74dde5ae0f24ebd680ace133e05e15d4
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/30/2019
ms.locfileid: "70167893"
---
# <a name="asynchronous-programming-with-async-and-await"></a>Programowanie asynchroniczne z Async i await

Model programowania asynchronicznego zadania (TAP) zawiera streszczenie w porównaniu z kodem asynchronicznym. Napiszesz kod jako sekwencję instrukcji, tak jak zawsze. Można odczytać ten kod, tak jakby każda instrukcja została zakończona przed rozpoczęciem następnego. Kompilator wykonuje szereg transformacji, ponieważ niektóre z tych instrukcji mogą zacząć pracę i zwrócić <xref:System.Threading.Tasks.Task> , która reprezentuje bieżącą pracę.

Jest to cel tej składni: Włącz kod, który odczytuje się jak sekwencja instrukcji, ale wykonuje się w znacznie bardziej skomplikowanej kolejności na podstawie zewnętrznej alokacji zasobów i po zakończeniu zadań. Jest to analogiczne do sposobu, w jaki ludzie udostępniają instrukcje dotyczące procesów zawierających zadania asynchroniczne. W tym artykule przedstawiono przykład instrukcji służących do nawiązywania śniadania, aby zobaczyć, `async` jak słowa kluczowe i `await` ułatwiają powód dla kodu, który zawiera szereg instrukcji asynchronicznych. Napiszesz instrukcje podobne do poniższej listy, aby wyjaśnić, jak utworzyć śniadanie:

1. Wlać filiżankę kawy.
1. Podgrzewaj panoramę, a następnie przefrj dwie jaja.
1. Narybka trzy wycinki Bacon.
1. Wyskakujące dwa elementy chleba.
1. Dodaj masło i dżem do wyskakującego powiadomienia.
1. Wlać szklany sok pomarańczowy.

W przypadku korzystania z funkcji gotowania należy wykonać te instrukcje asynchronicznie. Zaczniesz rozgrzewać panoramy dla jaj, a następnie uruchomić Bacon. Należy umieścić chleb w wyskakującym, a następnie rozpocząć jaja. W każdym kroku procesu należy uruchomić zadanie, a następnie zwrócić uwagę na zadania, które są gotowe do Twojej uwagi.

Śniadanie gotowania jest dobrym przykładem asynchronicznej pracy, która nie jest równoległa. Jedna osoba (lub wątek) może obsłużyć wszystkie te zadania. W przypadku kontynuowania nieprzerwanego śniadania jedna osoba może napełnić proces, rozpoczynając następne zadanie przed pierwszym zakończeniem. Postęp gotowania niezależnie od tego, czy ktoś ją ogląda. Gdy tylko zaczniesz rozgrzewać kadrowanie dla jaj, możesz zacząć Frying Bacon. Po rozpoczęciu Bacon można umieścić chleb w wyskakującym pasku.

Dla algorytmu równoległego potrzebna jest wiele Cooka (lub wątków). Jedna z nich spowoduje, że jaja, jeden z Bacon i tak dalej. Każdy z nich będzie koncentrować się tylko na jednym zadaniu. Każdy Cooka (lub wątek) zostałby zablokowany synchronicznie, oczekując na Bacon w celu przerzucenia lub wyskakującego okienka. 

Teraz Rozważ te same instrukcje, które zostały C# wpisane jako instrukcje:

[!code-csharp[SynchronousBreakfast](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-starter/Program.cs#Main)]

Komputery nie interpretują tych instrukcji w taki sam sposób jak ludzie. Komputer będzie blokować każdą instrukcję do momentu zakończenia pracy przed przejściem do następnej instrukcji. Spowoduje to utworzenie niespełniającego śniadania. Późniejsze zadania nie zostaną uruchomione do momentu ukończenia wcześniejszych zadań. Utworzenie śniadania może zająć dużo czasu, a niektóre elementy byłyby na zimno przed rozpoczęciem. 

Jeśli chcesz, aby komputer wykonywał powyższe instrukcje asynchronicznie, musisz napisać kod asynchroniczny.

Te zagadnienia są ważne w przypadku programów, które można napisać dzisiaj. Podczas pisania programów klienckich, interfejs użytkownika ma reagować na dane wejściowe użytkownika. Twoja aplikacja nie powinna sprawiać, że telefon jest zamrożony podczas pobierania danych z sieci Web. W przypadku pisania programów serwerowych nie ma możliwości blokowania wątków. Te wątki mogą obsługiwać inne żądania. Użycie kodu synchronicznego, gdy istnieje asynchroniczna alternatywa, powoduje, że skalowanie w poziomie jest tańsze. Płacisz za te zablokowane wątki.

Pomyślne aplikacje Modern wymagają kodu asynchronicznego. Bez obsługi języka, pisania asynchronicznie wymaganego kodu wywołania zwrotne, zdarzenia ukończenia lub inne oznacza, że zasłania pierwotny cel kodu. Zaletą kodu synchronicznego jest łatwość zrozumienia. Akcje krok po kroku ułatwiają skanowanie i zrozumienie. Tradycyjne modele asynchroniczne zmuszają do skoncentrowania się na asynchronicznym charakterze kodu, a nie na podstawowych działaniach kodu.

## <a name="dont-block-await-instead"></a>Nie blokuj, await zamiast

Powyższy kod demonstruje niewłaściwe rozwiązanie: konstruowanie kodu synchronicznego do wykonywania operacji asynchronicznych. Zgodnie z zapisaniem ten kod blokuje wątek wykonujący go przez wykonywanie innych czynności. Nie zostanie ona przerwana, gdy jakieś zadania są w toku. Po wprowadzeniu chleba na wyskakującym pasku jest to możliwe. Dowiesz się, jak wszyscy rozmawiają z Twoim zdjęte. 

Zacznijmy od zaktualizowania tego kodu, aby wątek nie zablokuje wykonywania zadań. `await` Słowo kluczowe zapewnia nieblokujący sposób uruchamiania zadania, a następnie kontynuuje wykonywanie po zakończeniu zadania. Prosta, asynchroniczna wersja kodu naśniadania będzie wyglądać następująco:

[!code-csharp[SimpleAsyncBreakfast](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-V2/Program.cs#Main)]

Ten kod nie jest blokowany, gdy jaja lub Bacon są gotowania. W tym kodzie nie zostaną uruchomione żadne inne zadania. Nadal wyskakujące powiadomienie na wyskakującym pasku i stare je do momentu pop. Ale co najmniej, wystarczy odpowiedzieć na każdą z nich. W restauracji, w której znajduje się wiele zamówień, Cooka może rozpocząć kolejną śniadanie, podczas gdy pierwszy jest gotowania.

Teraz wątek pracujący nad śniadaniem nie jest blokowany podczas oczekiwania na zadanie uruchomione, które jeszcze się nie zakończyło. W przypadku niektórych aplikacji ta zmiana jest wymagana. Aplikacja GUI nadal reaguje na użytkownika za pomocą tylko tej zmiany. Jednak w tym scenariuszu potrzebujesz więcej informacji. Nie chcesz, aby poszczególne zadania składników były wykonywane sekwencyjnie. Przed zaczekaniem na ukończenie poprzedniego zadania lepiej uruchomić wszystkie zadania składników.

## <a name="start-tasks-concurrently"></a>Uruchom zadania współbieżnie

W wielu scenariuszach należy od razu zacząć uruchamiać kilka niezależnych zadań. Następnie, po zakończeniu każdego zadania, można kontynuować wykonywanie innych gotowych zadań. W przypadku korzystania z analogu śniadaniowego wiesz, jak szybko uzyskać śniadanie. Wszystko to jest również wykonywane blisko tego samego czasu. Uzyskasz gorącą śniadanie.

<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> I powiązane typy są klasami, których można użyć, aby przyczynić się do zadań, które są w toku. Dzięki temu można napisać kod, który jest bardziej zbliżony do sposobu, w jaki faktycznie tworzysz śniadanie. W tym samym czasie można rozpocząć gotowanie jaj, Bacon i wyskakujących powiadomień. Ponieważ każda z nich wymaga działania, należy zwrócić uwagę na to zadanie, zadbać o następną akcję, a następnie oczekiwać na coś innego, co wymaga uwagi.

Uruchamiasz zadanie i przytrzymasz do <xref:System.Threading.Tasks.Task> obiektu, który reprezentuje pracę. Każde zadanie `await` zostanie wyświetlone przed rozpoczęciem pracy z jego wynikiem.

Wprowadźmy te zmiany w kodzie śniadania. Pierwszym krokiem jest przechowywanie zadań do operacji po ich uruchomieniu, a nie ich oczekiwanie:

```csharp
Coffee cup = PourCoffee();
Console.WriteLine("coffee is ready");
Task<Egg> eggTask = FryEggs(2);
Egg eggs = await eggTask;
Console.WriteLine("eggs are ready");
Task<Bacon> baconTask = FryBacon(3);
Bacon bacon = await baconTask;
Console.WriteLine("bacon is ready");
Task<Toast> toastTask = ToastBread(2);
Toast toast = await toastTask;
ApplyButter(toast);
ApplyJam(toast);
Console.WriteLine("toast is ready");
Juice oj = PourOJ();
Console.WriteLine("oj is ready");

Console.WriteLine("Breakfast is ready!");
```

Następnie można przenieść `await` instrukcje dotyczące Bacon i jaj do końca metody przed objęciem śniadania:

```csharp
Coffee cup = PourCoffee();
Console.WriteLine("coffee is ready");
Task<Egg> eggTask = FryEggs(2);
Task<Bacon> baconTask = FryBacon(3);
Task<Toast> toastTask = ToastBread(2);
Toast toast = await toastTask;
ApplyButter(toast);
ApplyJam(toast);
Console.WriteLine("toast is ready");
Juice oj = PourOJ();
Console.WriteLine("oj is ready");

Egg eggs = await eggTask;
Console.WriteLine("eggs are ready");
Bacon bacon = await baconTask;
Console.WriteLine("bacon is ready");

Console.WriteLine("Breakfast is ready!");
```

Poprzedni kod działa lepiej. Wszystkie zadania asynchroniczne są uruchamiane jednocześnie. Każde zadanie zostanie zaczekane tylko wtedy, gdy są potrzebne wyniki. Poprzedni kod może być podobny do kodu w aplikacji sieci Web, która wysyła żądania różnych mikrousług, a następnie łączy wyniki w jedną stronę. Wszystkie żądania zostaną wprowadzone natychmiast, następnie `await` wszystkie te zadania i tworzą stronę sieci Web.

## <a name="composition-with-tasks"></a>Kompozycja z zadaniami

 Wszystko jest gotowe do śniadania w tym samym czasie, z wyjątkiem wyskakującego powiadomienia. Wyskakujące powiadomienia są kompozycją operacji asynchronicznej (wyskakujące chleb) i synchronicznymi operacjami (dodaniem masła i zakleszczeniem). Aktualizacja tego kodu ilustruje ważną koncepcję:

> [!IMPORTANT]
> Kompozycja operacji asynchronicznej, po której następuje synchroniczna operacja, jest operacją asynchroniczną. Podano inny sposób, jeśli jakakolwiek część operacji jest asynchroniczna, cała operacja jest asynchroniczna.

Powyższy kod wskazuje, że można użyć <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601> obiektów do przechowywania uruchomionych zadań. `await` Każde zadanie przed użyciem jego wyniku. Następnym krokiem jest utworzenie metod, które reprezentują kombinację innych zadań. Przed objęciem śniadania, należy oczekiwać, że zadanie reprezentuje wyskakujące chleb przed dodaniem masła i dżemu. Można przedstawić, że pracujesz z poniższym kodem:

[!code-csharp[ComposeToastTask](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-V3/Program.cs#ComposeToastTask)]

Poprzednia metoda ma `async` modyfikator w podpisie. Sygnalizuje kompilatorowi, że ta metoda zawiera `await` instrukcję; zawiera operacje asynchroniczne. Ta metoda przedstawia zadanie, które wyskakujące chleb, a następnie dodaje masło i dżem. Ta metoda zwraca <xref:System.Threading.Tasks.Task%601> , który reprezentuje skład tych trzech operacji. Główny blok kodu jest teraz:

[!code-csharp[StartConcurrentTasks](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-V3/Program.cs#Main)]

Poprzednia zmiana ilustruje ważną technikę pracy z kodem asynchronicznym. Tworzysz zadania, oddzielając operacje do nowej metody, która zwraca zadanie. Możesz określić, kiedy ma oczekiwać to zadanie. Można uruchamiać inne zadania współbieżnie.

## <a name="await-tasks-efficiently"></a>Efektywne zadania oczekujące

Serie `await` instrukcji na końcu powyższego kodu można ulepszyć przy użyciu metod `Task` klasy. Jeden z tych interfejsów API <xref:System.Threading.Tasks.Task.WhenAll%2A>to, które <xref:System.Threading.Tasks.Task> zwraca, gdy wszystkie zadania na liście argumentów zostały ukończone, jak pokazano w poniższym kodzie:

```csharp
await Task.WhenAll(eggTask, baconTask, toastTask);
Console.WriteLine("eggs are ready");
Console.WriteLine("bacon is ready");
Console.WriteLine("toast is ready");
Console.WriteLine("Breakfast is ready!");
```

Kolejną opcją jest użycie <xref:System.Threading.Tasks.Task.WhenAny%2A>, która `Task<Task>` zwraca zakończenie, gdy którykolwiek z jego argumentów zakończy działanie. Możesz oczekiwać na zwrócone zadanie, wiedząc, że już zostało zakończone. Poniższy kod pokazuje, jak można użyć <xref:System.Threading.Tasks.Task.WhenAny%2A> do oczekiwania na zakończenie pierwszego zadania, a następnie przetworzyć jego wynik. Po przetworzeniu wyniku z zadania zakończonego zadanie zostało usunięte z listy zadań przesłanych do `WhenAny`.

[!code-csharp[AwaitAnyTask](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-final/Program.cs#AwaitAnyTask)]

Po wprowadzeniu wszystkich zmian końcowa wersja `Main` wygląda podobnie do następującego kodu:

[!code-csharp[Final](~/samples/snippets/csharp/tour-of-async/AsyncBreakfast-final/Program.cs#Main)]

Ten ostatni kod jest asynchroniczny. Dokładniej odzwierciedla to, w jaki sposób osoba może zacooka śniadanie. Porównaj poprzedni kod z pierwszym przykładowym kodem w tym artykule. Podstawowe działania są nadal jasne przed odczytaniem kodu. Można odczytać ten kod w taki sam sposób, jak w przypadku uzyskania śniadania na początku tego artykułu. Funkcje języka dla i `async` `await` zapewniają tłumaczenie dla każdej osoby, która wykonuje te instrukcje: Rozpocznij zadania w miarę możliwości i nie blokuj oczekiwania na ukończenie zadań.
