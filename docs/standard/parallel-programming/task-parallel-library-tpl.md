---
title: Biblioteka zadań równoległych (TPL)
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET, concurrency in
- .NET, parallel programming in
- Parallel Programming
ms.assetid: b8f99f43-9104-45fd-9bff-385a20488a23
ms.openlocfilehash: 487fe48462803ac19318f450f2576989f196a9be
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73139956"
---
# <a name="task-parallel-library-tpl"></a>Biblioteka zadań równoległych (TPL)
Biblioteka zadań równoległych (TPL) to zestaw typów publicznych i interfejsów API w przestrzeni nazw <xref:System.Threading?displayProperty=nameWithType> i <xref:System.Threading.Tasks?displayProperty=nameWithType>. Zadaniem biblioteki TPL jest zwiększenie produktywności deweloperów przez uproszczenie procesu dodawania równoległości i współbieżności do aplikacji. Biblioteka TPL skaluje stopień współbieżności dynamicznie, aby jak najefektywniej wykorzystać wszystkie dostępne procesory. Ponadto TPL obsługuje partycjonowanie pracy, planowanie wątków w <xref:System.Threading.ThreadPool>, pomoc techniczna dotycząca anulowania, zarządzanie stanami i inne szczegóły niskiego poziomu. Za pomocą TPL można zmaksymalizować wydajność kodu przy jednoczesnym skoncentrowaniu się na pracy, którą program ma wykonać.  
  
 Począwszy od .NET Framework 4, TPL jest preferowanym sposobem pisania kodu wielowątkowego i równoległego. Jednak nie cały kod nadaje się do przetwarzania równoległego. Na przykład jeśli pętla wykonuje tylko niewielką ilość pracy w każdej iteracji lub nie działa dla wielu iteracji, obciążenie związane z przetwarzaniem równoległym może powodować wolniejsze działanie kodu. Ponadto przetwarzanie równoległe, jak każdy kod wielowątkowy, dodaje złożoności do wykonywania programu. Chociaż TPL upraszcza scenariusze wielowątkowe, zalecamy przynajmniej podstawowe zrozumienie pojęcia wątkowości, na przykład blokad, zakleszczeń i sytuacje wyścigu, aby skutecznie korzystać z TPL.  
  
## <a name="related-topics"></a>Tematy pokrewne  
  
|Tytuł|Opis|  
|-|-|  
|[Równoległość danych](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)|Opisuje sposób tworzenia równoległych `for` i pętli `foreach` (`For` i `For Each` w Visual Basic).|  
|[Programowanie asynchroniczne oparte na zadaniach](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)|Opisuje sposób tworzenia i uruchamiania zadań niejawnie przy użyciu <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType> lub jawnie przy użyciu obiektów <xref:System.Threading.Tasks.Task> bezpośrednio.|  
|[Przepływ danych](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)|Opisuje, jak używać składników przepływu danych w bibliotece przepływu danych TPL w celu obsługi wielu operacji, które muszą się komunikować ze sobą, lub w celu przetwarzania danych, gdy tylko staną się dostępne.|  
|[Korzystanie z modelu TPL z innymi wzorcami asynchronicznymi](../../../docs/standard/parallel-programming/using-tpl-with-other-asynchronous-patterns.md)|Opisuje sposób używania TPL z innymi wzorami asynchronicznymi w .NET|  
|[Potencjalne pułapki związane z równoległością danych i zadań](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md)|Opisuje kilka typowych pułapek oraz sposoby unikania ich.|  
|[Równoległe LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)|Opisuje sposób osiągnięcia równoległości danych za pomocą zapytań LINQ.|  
|[Programowanie równoległe](../../../docs/standard/parallel-programming/index.md)|Węzeł najwyższego poziomu dla równoległego programowania .NET.|  
  
## <a name="see-also"></a>Zobacz także

- [Przykłady programowania równoległego przy użyciu .NET Framework](https://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)
