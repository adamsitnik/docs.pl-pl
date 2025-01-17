---
title: Jak korzystać z interfejsu API zautomatyzowanej ML.NET ML
description: Interfejs API zautomatyzowanej sieci ML.NET automatyzuje proces tworzenia modelu i generuje model gotowy do wdrożenia. Informacje na temat opcji, których można użyć do konfigurowania automatycznych zadań uczenia maszynowego.
ms.date: 04/24/2019
ms.custom: mvc,how-to
ms.openlocfilehash: bb1cd66e7341f2ada57d533d8b2dcbb48f08f726
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72774549"
---
# <a name="how-to-use-the-mlnet-automated-machine-learning-api"></a>Jak korzystać z interfejsu API automatycznego uczenia maszynowego ML.NET

Automatyczne Uczenie maszynowe (AutoML) automatyzuje proces stosowania uczenia maszynowego do danych. Mając zestaw danych, można uruchomić **eksperyment** AutoML, aby wykonać iterację różnych danych featurizations, algorytmów uczenia maszynowego i parametrów do wybierania najlepszego modelu.

> [!NOTE]
> Ten temat odnosi się do zautomatyzowanego interfejsu API uczenia maszynowego dla usługi ML.NET, który jest obecnie w wersji zapoznawczej. Materiał może ulec zmianie.

## <a name="load-data"></a>Ładowanie danych

Automatyczne Uczenie maszynowe obsługuje ładowanie zestawu danych do [IDataView](xref:Microsoft.ML.IDataView). Dane mogą mieć postać plików z wartościami rozdzielanymi tabulatorami (TSV) i plików z wartościami rozdzielanymi przecinkami (CSV).

Przykład:

```csharp
using Microsoft.ML;
using Microsoft.ML.AutoML;
    // ...
    MLContext mlContext = new MLContext();
    IDataView trainDataView = mlContext.Data.LoadFromTextFile<SentimentIssue>("my-data-file.csv", hasHeader: true);
```

## <a name="select-the-machine-learning-task-type"></a>Wybierz typ zadania uczenia maszynowego
Przed utworzeniem eksperymentu należy określić rodzaj problemu z uczeniem maszynowym, który ma zostać rozwiązany. Automatyczne Uczenie maszynowe obsługuje następujące zadania w ML:

* Klasyfikacja binarna
* Klasyfikacja wieloklasowa
* Ubytk

## <a name="create-experiment-settings"></a>Utwórz ustawienia eksperymentu

Utwórz ustawienia eksperymentu dla typu zadania o określonej ML:

* Klasyfikacja binarna

  ```csharp
  var experimentSettings = new BinaryExperimentSettings();
  ```

* Klasyfikacja wieloklasowa

  ```csharp
  var experimentSettings = new MulticlassExperimentSettings();
  ```

* Ubytk

  ```csharp
  var experimentSettings = new RegressionExperimentSettings();
  ```

## <a name="configure-experiment-settings"></a>Konfigurowanie ustawień eksperymentu

Eksperymenty są wysoce konfigurowalne. Zobacz dokumentację [interfejsu API AutoML](https://docs.microsoft.com/dotnet/api/?view=automl-dotnet) , aby uzyskać pełną listę ustawień konfiguracji.

Oto kilka przykładów:

1. Określ maksymalny czas działania eksperymentu.

    ```csharp
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    ```

1. Użyj tokenu anulowania, aby anulować eksperyment przed zaplanowaniem jego zakończenia.

    ```csharp
    experimentSettings.CancellationToken = cts.Token;

    // Cancel experiment after the user presses any key
    CancelExperimentAfterAnyKeyPress(cts);
    ```

1. Określ inną metrykę optymalizacji.

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.OptimizingMetric = RegressionMetric.MeanSquaredError;
    ```

1. Ustawienie `CacheDirectory` jest wskaźnikiem do katalogu, w którym zostaną zapisane wszystkie modele przeszkolone podczas zadania AutoML. Jeśli `CacheDirectory` ma wartość null, modele będą przechowywane w pamięci zamiast zapisywać na dysku.

    ```csharp
    experimentSettings.CacheDirectory = null;
    ```

1. Poinstruuj zautomatyzowany ML, aby nie używać niektórych instruktorów.

    Domyślna lista instruktorów do optymalizacji są zbadane według poszczególnych zadań. Tę listę można modyfikować dla każdego eksperymentu. Na przykład, instruktorzy, którzy działają wolno w zestawie danych, można usunąć z listy. Aby zoptymalizować na jednym konkretnym wywołaniu Trainer `experimentSettings.Trainers.Clear()`, Dodaj Trainer, którego chcesz użyć.

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.Trainers.Remove(RegressionTrainer.LbfgsPoissonRegression);
    experimentSettings.Trainers.Remove(RegressionTrainer.OnlineGradientDescent);
    ```

Listę obsługiwanych zadań instruktorów na ML można znaleźć w odpowiadającym jej poniższym łączu:

* [Obsługiwane algorytmy klasyfikacji binarnej](xref:Microsoft.ML.AutoML.BinaryClassificationTrainer)
* [Obsługiwane algorytmy klasyfikacji wieloklasowej](xref:Microsoft.ML.AutoML.MulticlassClassificationTrainer)
* [Obsługiwane algorytmy regresji](xref:Microsoft.ML.AutoML.RegressionTrainer)

## <a name="optimizing-metric"></a>Optymalizowanie metryki

Metryka optymalizacji, jak pokazano w powyższym przykładzie, określa metrykę do zoptymalizowania podczas uczenia modelu. Metryka optymalizacji, którą można wybrać, zależy od wybranego typu zadania. Poniżej znajduje się lista dostępnych metryk.

|[Klasyfikacja binarna](xref:Microsoft.ML.AutoML.BinaryClassificationMetric) | [Klasyfikacja wieloklasowa](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric) |[Ubytk](xref:Microsoft.ML.AutoML.RegressionMetric)
|-- |-- |--
|Odpowiedni| LogLoss | RSquared
|AreaUnderPrecisionRecallCurve | LogLossReduction | MeanAbsoluteError
|AreaUnderRocCurve | MacroAccuracy | MeanSquaredError
|F1Score | Mikrodokładność | RootMeanSquaredError
|NegativePrecision | TopKAccuracy
|NegativeRecall |
|PositivePrecision
|PositiveRecall

## <a name="data-pre-processing-and-featurization"></a>Wstępne przetwarzanie i cechowania danych

> [!NOTE]
> W kolumnie funkcji obsługiwane są tylko typy <xref:System.Boolean>, <xref:System.Single> i <xref:System.String>.

Przetwarzanie wstępne danych odbywa się domyślnie, a następujące kroki są wykonywane automatycznie:

1. Funkcje upuszczania bez użytecznych informacji

    Porzuć funkcje bez użytecznych informacji dotyczących szkoleń i zestawów walidacji. Obejmują one funkcje, w których brakuje wszystkich wartości, takich same jak wszystkie wiersze, lub z bardzo dużą kardynalnością (np. skrótami, identyfikatorami lub identyfikatorami GUID).

1. Brak wskazania wartości i nie należy ich przypisywaniu

    Wypełnij brakujące komórki wartości wartością domyślną dla typu danych. Dołącz funkcje wskaźnika z taką samą liczbą gniazd jak w przypadku kolumny wejściowej. Wartość w funkcjach dołączanych wskaźników jest `1`, jeśli brakuje wartości w kolumnie wejściowej i `0` w przeciwnym razie.

1. Generuj dodatkowe funkcje

    Dla funkcji tekstowych: Funkcje zbioru dla programu Word przy użyciu unigrams i Tri-Character-Grams.

    W przypadku funkcji kategorii: jednostronicowe kodowanie dla funkcji niskiej kardynalności i jednostronicowe kodowanie dla wysokich funkcji kategorii.

1. Przekształcenia i kodowania

    Funkcje tekstowe z bardzo kilkoma unikatowymi wartościami przekształconymi na funkcje kategorii. W zależności od kardynalności funkcji kategorii należy wykonać jedno-gorąca lub jednostronicowe kodowanie skrótu.

## <a name="exit-criteria"></a>Kryteria wyjścia

Zdefiniuj kryteria, aby ukończyć zadanie:

1. Zakończ po upływie czasu `MaxExperimentTimeInSeconds` w ustawieniach eksperymentu możesz określić, jak długo w sekundach ma być nadal wykonywane zadanie.

1. Wyjście z tokenu anulowania — można użyć tokenu anulowania, który umożliwia anulowanie zadania przed jego zaplanowaniem.

    ```csharp
    var cts = new CancellationTokenSource();
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    experimentSettings.CancellationToken = cts.Token;
    ```

## <a name="create-an-experiment"></a>Tworzenie eksperymentu

Po skonfigurowaniu ustawień eksperymentu możesz przystąpić do tworzenia eksperymentu.

```csharp
RegressionExperiment experiment = mlContext.Auto().CreateRegressionExperiment(experimentSettings);
```

## <a name="run-the-experiment"></a>Uruchamianie eksperymentu

Uruchamianie eksperymentu wyzwala wstępne przetwarzanie danych, wybór algorytmu uczenia i dostrajanie parametrów. AutoML będzie kontynuował generowanie kombinacji cechowania, algorytmów uczenia i parametrów do momentu osiągnięcia `MaxExperimentTimeInSeconds` lub przerwania eksperymentu.

```csharp
ExperimentResult<RegressionMetrics> experimentResult = experiment
    .Execute(trainingDataView, LabelColumnName, progressHandler: progressHandler);
```

Zapoznaj się z innymi przeciążeniami `Execute()`, jeśli chcesz przekazać dane walidacji, informacje o kolumnie wskazujące cel kolumny lub prefeaturizers.

## <a name="training-modes"></a>Tryby szkoleniowe

### <a name="training-dataset"></a>Zestaw danych szkoleniowych

AutoML zapewnia przeciążoną metodę wykonywania eksperymentu, która umożliwia dostarczanie danych szkoleniowych. Wewnętrznie, zautomatyzowanej ML dzieli dane na pociąg-Validate Splits.

```csharp
experiment.Execute(trainDataView);
```

### <a name="custom-validation-dataset"></a>Niestandardowy zestaw danych walidacji

Użyj niestandardowego zestawu danych walidacji, jeśli podział losowy nie jest akceptowalny, jak zwykle jest to przypadek z danymi szeregów czasowych. Możesz określić własny zestaw danych walidacji. Model zostanie oceniony względem określonego zestawu danych walidacji, a nie do co najmniej jednego losowo ustawionego typu danych.

```csharp
experiment.Execute(trainDataView, validationDataView);
```

## <a name="explore-model-metrics"></a>Eksplorowanie metryk modelu

Po każdej iteracji eksperymentu ML są przechowywane metryki dotyczące tego zadania.

Można na przykład uzyskać dostęp do metryk walidacji z najlepszego przebiegu:

```csharp
RegressionMetrics metrics = experimentResult.BestRun.ValidationMetrics;
Console.WriteLine($"R-Squared: {metrics.RSquared:0.##}");
Console.WriteLine($"Root Mean Squared Error: {metrics.RootMeanSquaredError:0.##}");
```

Poniżej znajdują się wszystkie dostępne metryki na ML zadania:

* [Metryki klasyfikacji binarnej](xref:Microsoft.ML.AutoML.BinaryClassificationMetric)
* [Metryki klasyfikacji wieloklasowej](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric)
* [Metryki regresji](xref:Microsoft.ML.AutoML.RegressionMetric)

## <a name="see-also"></a>Zobacz także

Aby uzyskać pełne przykłady kodu i więcej informacji, odwiedź repozytorium [dotnet/machinelearning-Samples](https://github.com/dotnet/machinelearning-samples/tree/master#automate-mlnet-models-generation-preview-state) w witrynie GitHub.
