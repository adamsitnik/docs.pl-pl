---
title: Działanie ThrottledParallelForEach
ms.date: 03/30/2017
ms.assetid: f2855b5f-e9a7-433d-96a4-40fc31025215
ms.openlocfilehash: 2694173e203fae9b620e9594d6d4a494bdedafef
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637760"
---
# <a name="throttled-parallel-foreach"></a>Działanie ThrottledParallelForEach

`ThrottleParallelForEach` Działanie jest podobne do <xref:System.Activities.Statements.ParallelForEach%601> działania z jednym wyjątkiem że umożliwia ustawienie współczynnika współbieżności Aby ograniczyć liczbę jednoczesnych gałęzi do wykonania. `ThrottleParallelForEach` Pochodzi od klasy działania <xref:System.Activities.NativeActivity>, ponieważ należy ją zaplanować inne działania (działania podrzędne), a ten jest dostępny tylko za pośrednictwem <xref:System.Activities.NativeActivityContext> klasy.

## <a name="projects"></a>Projekty

|**ProjectName**|**Opis**|**Pliki główne**|
|-|-|-|
|ThrottledParallelForEach|Zawiera `ThrottledParallelForEach` działanie i jego projektanta.|ThrottledParallelForEach.cs<br /><br /> `ThrottledParallelForEach` Definicji działania.|
|CodeTestClient|Przykładowa aplikacja kliencka, która umożliwia skonfigurowanie i uruchamia przepływ pracy o `ThrottledParallelForEach` przy użyciu kodu imperatywnego.|Program.cs<br /><br /> Definiuje i jest uruchamiane wystąpienie przykładowy przepływ pracy.|

## <a name="to-use-this-sample"></a>Aby użyć tego przykładu

1. Za pomocą programu Visual Studio 2010, otwórz plik ThrottledParallelForEach.sln.

2. Aby skompilować rozwiązanie, naciśnij klawisze CTRL + SHIFT + B.

3. Aby uruchomić rozwiązanie, naciśnij klawisz F5.

> [!IMPORTANT]
> Przykłady może już być zainstalowany na tym komputerze. Przed kontynuowaniem sprawdź, czy są dostępne dla następującego katalogu (ustawienie domyślne).
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Jeśli ten katalog nie istnieje, przejdź do strony [Windows Communication Foundation (WCF) i przykłady Windows Workflow Foundation (WF) dla platformy .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) do pobierania wszystkich Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykładów. W tym przykładzie znajduje się w następującym katalogu.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\ThrottledParallelForEach`
