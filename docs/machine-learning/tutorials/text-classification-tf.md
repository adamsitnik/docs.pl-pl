---
title: 'Samouczek: analizowanie tonacji przeglądów filmów przy użyciu wstępnie przeszkolonego modelu TensorFlow'
description: W tym samouczku przedstawiono sposób użycia wstępnie przeszkolonego modelu TensorFlow do klasyfikowania tonacji w komentarzach w witrynie sieci Web. Tonacji klasyfikator binarny jest aplikacją C# konsolową opracowaną przy użyciu programu Visual Studio.
ms.date: 09/30/2019
ms.topic: tutorial
ms.custom: mvc
ms.author: nakersha
author: natke
ms.openlocfilehash: 417abb5052df95c8496d97894d3e11d2956d7a1a
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72774395"
---
# <a name="tutorial-analyze-sentiment-of-movie-reviews-using-a-pre-trained-tensorflow-model-in-mlnet"></a>Samouczek: analizowanie tonacji przeglądów filmów przy użyciu wstępnie przeszkolonego modelu TensorFlow w ML.NET

W tym samouczku przedstawiono sposób użycia wstępnie przeszkolonego modelu TensorFlow do klasyfikowania tonacji w komentarzach w witrynie sieci Web. Tonacji klasyfikator binarny jest aplikacją C# konsolową opracowaną przy użyciu programu Visual Studio.

Model TensorFlow używany w tym samouczku został przeszkolony przy użyciu recenzji filmów z bazy danych IMDB. Po zakończeniu opracowywania aplikacji będzie można dostarczyć tekst z recenzji filmu, a aplikacja poinformuje użytkownika o tym, czy przegląd ma pozytywne czy negatywne tonacji.

Z tego samouczka dowiesz się, jak wykonywać następujące czynności:
> [!div class="checklist"]
>
> * Załaduj wstępnie szkolony model TensorFlow
> * Przekształć tekst komentarza witryny internetowej w funkcje odpowiednie dla modelu
> * Tworzenie prognoz przy użyciu modelu

Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TextClassificationTF) .

## <a name="prerequisites"></a>Wymagania wstępne

* [Program Visual Studio 2017 w wersji 15,6 lub nowszej](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) z zainstalowanym obciążeniem "Programowanie dla wielu platform w środowisku .NET Core".

## <a name="setup"></a>Konfiguracja

### <a name="create-the-application"></a>Tworzenie aplikacji

1. Utwórz **aplikację konsolową .NET Core** o nazwie "TextClassificationTF".

2. Utwórz katalog o nazwie *dane* w projekcie, aby zapisać pliki zestawu danych.

3. Zainstaluj **pakiet NuGet Microsoft.ml**:

    W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**. Wybierz pozycję "nuget.org" jako źródło pakietu, a następnie wybierz kartę **Przeglądaj** . wyszukaj pozycję **Microsoft.ml**, wybierz pakiet, a następnie wybierz przycisk **Instaluj** . Kontynuuj instalację, zgadzając się z postanowieniami licencyjnymi dotyczącymi wybranego pakietu. Powtórz te kroki dla **Microsoft. ml. TensorFlow**.

### <a name="add-the-tensorflow-model-to-the-project"></a>Dodawanie modelu TensorFlow do projektu

> [!NOTE]
> Model tego samouczka pochodzi z repozytorium w witrynie GitHub [/machinelearning-TestData](https://github.com/dotnet/machinelearning-testdata/tree/master/Microsoft.ML.TensorFlow.TestModels/sentiment_model) . Model jest w formacie TensorFlow SavedModel.

1. Pobierz [plik zip sentiment_model](https://github.com/dotnet/samples/blob/master/machine-learning/models/textclassificationtf/sentiment_model.zip?raw=true)i rozpakuj.

    Plik zip zawiera:

    * `saved_model.pb`: sam model TensorFlow. Model przyjmuje stałą długość (w rozmiarze 600) tablicę funkcji reprezentujących tekst w ciągu przeglądu IMDB i wyprowadza dwa prawdopodobieństwa, które są sumowane do 1: prawdopodobieństwo, że przegląd danych wejściowych ma pozytywne tonacji, i prawdopodobieństwo, że przegląd danych wejściowych ma ujemna tonacji.
    * `imdb_word_index.csv`: mapowanie poszczególnych wyrazów na wartość całkowitą. Mapowanie jest używane do generowania funkcji wejściowych dla modelu TensorFlow.

2. Skopiuj zawartość wewnętrznego katalogu `sentiment_model` do katalogu `sentiment_model` projektu *TextClassificationTF* . Ten katalog zawiera model i dodatkowe pliki pomocnicze, które są odpowiednie dla tego samouczka, jak pokazano na poniższej ilustracji:

   ![zawartość katalogu sentiment_model](./media/text-classification-tf/sentiment-model-files.png)

3. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy każdy plik w katalogu `sentiment_model` i podkatalogu, a następnie wybierz polecenie **Właściwości**. W obszarze **Zaawansowane**Zmień wartość opcji **Kopiuj do katalogu wyjściowego** na Kopiuj, **jeśli nowszy**.

### <a name="add-using-statements-and-global-variables"></a>Dodaj instrukcje using i zmienne globalne

1. Dodaj następujące dodatkowe instrukcje `using` na początku pliku *program.cs* :

   [!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/TextClassificationTF/Program.cs#AddUsings "Add necessary usings")]

1. Utwórz dwie zmienne globalne bezpośrednio nad metodą `Main`, aby przechowywać ścieżkę do zapisanego pliku modelu i długość wektora funkcji.

   [!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/TextClassificationTF/Program.cs#DeclareGlobalVariables "Declare global variables")]

    * `_modelPath` jest ścieżką do pliku nauczonego modelu.
    * `FeatureLength` jest długością tablicy funkcji liczb całkowitych, która oczekuje model.

### <a name="model-the-data"></a>Modelowanie danych

Przeglądy filmów są bezpłatne tekstu. Aplikacja konwertuje tekst na format wejściowy oczekiwany przez model w wielu odrębnych etapach.

Pierwszym jest podział tekstu na oddzielne słowa i użycie podanego pliku mapowania do mapowania każdego wyrazu na kodowanie całkowite. Wynikiem tej transformacji jest tablica o zmiennej długości całkowitej o długości odpowiadającej liczbie wyrazów w zdaniu.

|Właściwość| Wartość|Typ|
|-------------|-----------------------|------|
|ReviewText|Ta folia jest naprawdę dobra|string|
|VariableLengthFeatures|14, 22, 9, 66, 78,... |int []|

Rozmiar tablicy funkcji o zmiennej długości jest zmieniany na stałą długość wynoszącą 600. Jest to długość oczekiwana przez model TensorFlow.

|Właściwość| Wartość|Typ|
|-------------|-----------------------|------|
|ReviewText|Ta folia jest naprawdę dobra|string|
|VariableLengthFeatures|14, 22, 9, 66, 78,... |int []|
|Funkcje|14, 22, 9, 66, 78,... |int [600]|

1. Utwórz klasę danych wejściowych po metodzie `Main`:

    [!code-csharp[MovieReviewClass](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#MovieReviewClass "Declare movie review type")]

    Klasa danych wejściowych `MovieReview` ma `string` do komentarzy użytkowników (`ReviewText`).

1. Utwórz klasę dla funkcji o zmiennej długości, po metodzie `Main`:

    [!code-csharp[VariableLengthFeatures](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#VariableLengthFeatures "Declare variable length features type")]

    Właściwość `VariableLengthFeatures` ma atrybut [vectortype](xref:Microsoft.ML.Data.VectorTypeAttribute.%23ctor%2A) służący do wyznaczania go jako wektor.  Wszystkie elementy wektorowe muszą być tego samego typu. W przypadku zestawów danych z dużą liczbą kolumn ładowanie wielu kolumn jako jednego wektora zmniejsza liczbę danych przekazywanych w przypadku zastosowania transformacji danych.

    Ta klasa jest używana w akcji `ResizeFeatures`. Nazwy jego właściwości (w tym przypadku tylko jeden) są używane do wskazania kolumn w widoku danych, które mogą być używane jako _dane wejściowe_ niestandardowej akcji mapowania.

1. Utwórz klasę dla funkcji o stałej długości po metodzie `Main`:

    [!code-csharp[FixedLengthFeatures](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#FixedLengthFeatures)]

    Ta klasa jest używana w akcji `ResizeFeatures`. Nazwy jego właściwości (w tym przypadku tylko jeden) są używane do wskazania kolumn w widoku danych, które mogą być używane jako _dane wyjściowe_ niestandardowej akcji mapowania.

    Należy zauważyć, że nazwa właściwości `Features` jest określana przez model TensorFlow. Nie można zmienić tej nazwy właściwości.

1. Utwórz klasę dla przewidywania po metodzie `Main`:

    [!code-csharp[Prediction](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#Prediction "Declare prediction class")]

    `MovieReviewSentimentPrediction` jest klasą przewidywania używaną po przekształceniu modelu. `MovieReviewSentimentPrediction` ma jedną `float` tablicę (`Prediction`) i atrybut `VectorType`.

### <a name="create-the-mlcontext-lookup-dictionary-and-action-to-resize-features"></a>Tworzenie MLContext, słownika wyszukiwania i akcji w celu zmiany rozmiaru funkcji

[Klasa MLContext](xref:Microsoft.ML.MLContext) jest punktem początkowym dla wszystkich operacji ml.NET. Inicjowanie `mlContext` tworzy nowe środowisko ML.NET, które może być współużytkowane przez obiekty przepływu pracy tworzenia modelu. Jest to podobne, pojęciowo, aby `DBContext` w Entity Framework.

1. Zastąp wiersz `Console.WriteLine("Hello World!")` w metodzie `Main` następującym kodem, aby zadeklarować i zainicjować zmienną mlContext:

   [!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreateMLContext "Create the ML Context")]

1. Utwórz słownik służący do kodowania wyrazów jako liczby całkowite przy użyciu metody [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%2A) do ładowania danych mapowania z pliku, jak pokazano w poniższej tabeli:

    |Word     |Indeks    |
    |---------|---------|
    |bezpiecznego     |  362    |
    |Możesz     |  181    |
    |odpowiednich    |  355    |
    |efekty  |  302    |
    |całkiem  |  547    |

    Dodaj poniższy kod, aby utworzyć mapę wyszukiwania:

    [!code-csharp[CreateLookupMap](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreateLookupMap)]

1. Dodaj `Action`, aby zmienić rozmiar tablicy tablica liczb całkowitych wyrazów o zmiennej długości do tablicy o stałym rozmiarze, z następnymi wierszami kodu:

   [!code-csharp[ResizeFeatures](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#ResizeFeatures)]

## <a name="load-the-pre-trained-tensorflow-model"></a>Załaduj wstępnie szkolony model TensorFlow

1. Dodaj kod, aby załadować model TensorFlow:

    [!code-csharp[LoadTensorFlowModel](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#LoadTensorFlowModel)]

    Po załadowaniu modelu można wyodrębnić jego schemat wejściowy i wyjściowy. Schematy są wyświetlane tylko dla zainteresowania i tylko do celów szkoleniowych. Ten kod nie jest potrzebny do działania końcowej aplikacji:

    [!code-csharp[GetModelSchema](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#GetModelSchema)]

    Schemat wejściowy jest tablicą o stałej długości w postaci słów szyfrowanych liczbą całkowitą. Schemat danych wyjściowych jest tablicą zmiennoprzecinkową prawdopodobieństwa wskazującą, czy tonacji przeglądu jest ujemna, czy dodatnia. Te wartości są sumowane do 1, ponieważ prawdopodobieństwo wystąpienia pozytywnego jest uzupełnieniem prawdopodobieństwa, że tonacji jest ujemna.

## <a name="create-the-mlnet-pipeline"></a>Tworzenie potoku ML.NET

1. Utwórz potok i Podziel tekst wejściowy na słowa przy użyciu transformacji [TokenizeIntoWords](xref:Microsoft.ML.TextCatalog.TokenizeIntoWords%2A) , aby podzielić tekst na wyrazy jako następny wiersz kodu:

   [!code-csharp[TokenizeIntoWords](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#TokenizeIntoWords)]

   Transformacja [TokenizeIntoWords](xref:Microsoft.ML.TextCatalog.TokenizeIntoWords%2A) używa spacji do analizowania tekstu/ciągu w słowach. Tworzy nową kolumnę i dzieli każdy ciąg wejściowy na wektor podciągów w oparciu o separator zdefiniowany przez użytkownika.

1. Mapuj słowa na ich kodowanie całkowite przy użyciu tabeli odnośników zadeklarowanej powyżej:

    [!code-csharp[MapValue](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#MapValue)]

1. Zmień rozmiar kodowania Integer o zmiennej długości na stałą długość określoną przez model:

    [!code-csharp[CustomMapping](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CustomMapping)]

1. Klasyfikuj dane wejściowe za pomocą załadowanego modelu TensorFlow:

    [!code-csharp[ScoreTensorFlowModel](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#ScoreTensorFlowModel)]

    Dane wyjściowe modelu TensorFlow są nazywane `Prediction/Softmax`. Należy pamiętać, że nazwa `Prediction/Softmax` jest określana przez model TensorFlow. Nie można zmienić tej nazwy.

1. Utwórz nową kolumnę przewidywania danych wyjściowych:

    [!code-csharp[SnippetCopyColumns](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#SnippetCopyColumns)]

    Należy skopiować kolumnę `Prediction/Softmax` na jedną z nazwą, która może być używana jako właściwość w C# klasie: `Prediction`. Znak `/` nie jest dozwolony w nazwie C# właściwości.

## <a name="create-the-mlnet-model-from-the-pipeline"></a>Tworzenie modelu ML.NET z potoku

1. Dodaj kod, aby utworzyć model z potoku:

    [!code-csharp[SnippetCreateModel](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#SnippetCreateModel)]

    Model ML.NET jest tworzony na podstawie łańcucha szacowania w potoku przez wywołanie metody `Fit`. W takim przypadku nie dopasowujemy żadnych danych w celu utworzenia modelu, ponieważ model TensorFlow został już wcześniej przeszkolony. Dostarczamy pusty obiekt widoku danych w celu spełnienia wymagań metody `Fit`.

## <a name="use-the-model-to-make-a-prediction"></a>Tworzenie prognoz przy użyciu modelu

1. Dodaj metodę `PredictSentiment` poniżej metody `Main`:

    ```csharp
    public static void PredictSentiment(MLContext mlContext, ITransformer model)
    {

    }
    ```

1. Dodaj następujący kod, aby utworzyć `PredictionEngine` jako pierwszy wiersz w `PredictSentiment()` metodzie:

    [!code-csharp[CreatePredictionEngine](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreatePredictionEngine)]

    [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) jest WYGODNYm interfejsem API, który umożliwia prognozowanie jednego wystąpienia danych. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) nie jest bezpieczny wątkowo. Jest to możliwe do użycia w środowiskach wielowątkowych lub prototypowych. Aby zwiększyć wydajność i bezpieczeństwo wątków w środowiskach produkcyjnych, Użyj usługi `PredictionEnginePool`, która tworzy [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) obiektów do użycia w całej aplikacji. Zapoznaj się z tym przewodnikiem dotyczącym [korzystania z `PredictionEnginePool` w ASP.NET Core Web API](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application).

    > [!NOTE]
    > rozszerzenie usługi `PredictionEnginePool` jest obecnie w wersji zapoznawczej.

1. Dodaj komentarz, aby przetestować prognozę przeszkolonego modelu w metodzie `Predict()`, tworząc wystąpienie `MovieReview`:

    [!code-csharp[CreateTestData](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreateTestData)]

1. Przekaż dane komentarzy testowych do `Prediction Engine` przez dodanie następnych wierszy kodu w metodzie `PredictSentiment()`:

    [!code-csharp[Predict](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#Predict)]

1. Funkcja [przewidywania ()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) wykonuje prognozowanie w jednym wierszu danych:

    |Właściwość| Wartość|Typ|
    |-------------|-----------------------|------|
    |Przewidując|[0,5459937, 0,454006255]|float []|

1. Wyświetl prognozowanie tonacji przy użyciu następującego kodu:

    [!code-csharp[DisplayPredictions](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#DisplayPredictions)]

1. Dodaj wywołanie do `PredictSentiment` na końcu metody `Main`:

    [!code-csharp[CallPredictSentiment](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CallPredictSentiment)]

## <a name="results"></a>Wyniki

Kompiluj i uruchamiaj aplikację.

Wyniki powinny wyglądać podobnie do poniższego. Podczas przetwarzania wyświetlane są komunikaty. Mogą pojawić się ostrzeżenia lub przetwarzanie komunikatów. Te komunikaty zostały usunięte z następujących wyników dla przejrzystości.

```console
Number of classes: 2
Is sentiment/review positive ? Yes
```

Nabycia! Pomyślnie skompilowano model uczenia maszynowego do klasyfikowania i przewidywania komunikatów tonacji przez ponowne użycie wstępnie nauczonego modelu `TensorFlow` w ML.NET.

Kod źródłowy dla tego samouczka można znaleźć w repozytorium [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TextClassificationTF) .

W tym samouczku przedstawiono sposób wykonywania tych instrukcji:
> [!div class="checklist"]
>
> * Załaduj wstępnie szkolony model TensorFlow
> * Przekształć tekst komentarza witryny internetowej w funkcje odpowiednie dla modelu
> * Tworzenie prognoz przy użyciu modelu
