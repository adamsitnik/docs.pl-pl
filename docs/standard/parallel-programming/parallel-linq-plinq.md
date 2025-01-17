---
title: Równoległe LINQ (PLINQ)
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ, overview
ms.assetid: 3d4d0cd3-bde4-490b-99e7-f4e41be96455
ms.openlocfilehash: 1ea880c6403a5fc8b26ba67fe21dfce79c4683db
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140038"
---
# <a name="parallel-linq-plinq"></a>Równoległe LINQ (PLINQ)
Równoległe LINQ (PLINQ) to równoległa implementacja LINQ to Objects. PLINQ implementuje pełny zestaw standardowych operatorów zapytań LINQ jako metody rozszerzenia dla przestrzeni nazw <xref:System.Linq> i ma dodatkowe operatory dla operacji równoległych. PLINQ łączy prostotę i czytelność składni LINQ z możliwością programowania równoległego. Podobnie jak kod, który jest przeznaczony dla biblioteki równoległej zadania, PLINQ zapytania skalowanie w poziomie współbieżności w oparciu o możliwości komputera hosta.  
  
 W wielu scenariuszach PLINQ może znacząco zwiększyć szybkość zapytań LINQ to Objects przy użyciu wszystkich dostępnych rdzeni na komputerze hosta wydajniejszie. Ta zwiększona wydajność zapewnia wysoką wydajność przetwarzania na komputerze stacjonarnym.  
  
## <a name="in-this-section"></a>W tej sekcji  
 [Wprowadzenie do PLINQ](../../../docs/standard/parallel-programming/introduction-to-plinq.md)  
  
 [Ogólne informacje o przyspieszeniach w PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)  
  
 [Zachowywanie kolejności w PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)  
  
 [Opcje scalania w PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)  
  
 [Instrukcje: tworzenie i wykonywanie prostego zapytania PLINQ](../../../docs/standard/parallel-programming/how-to-create-and-execute-a-simple-plinq-query.md)  
  
 [Instrukcje: sterowanie szeregowaniem w zapytaniu PLINQ](../../../docs/standard/parallel-programming/how-to-control-ordering-in-a-plinq-query.md)  
  
 [Instrukcje: łączenie równoległych i sekwencyjnych zapytań LINQ](../../../docs/standard/parallel-programming/how-to-combine-parallel-and-sequential-linq-queries.md)  
  
 [Instrukcje: obsługa wyjątków w zapytaniu PLINQ](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)  
  
 [Instrukcje: anulowanie zapytania PLINQ](../../../docs/standard/parallel-programming/how-to-cancel-a-plinq-query.md)  
  
 [Instrukcje: pisanie niestandardowej funkcji agregowania w PLINQ](../../../docs/standard/parallel-programming/how-to-write-a-custom-plinq-aggregate-function.md)  
  
 [Instrukcje: określanie trybu wykonywania w PLINQ](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)  
  
 [Instrukcje: określanie opcji scalania w PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)  
  
 [Instrukcje: iteracja katalogów plików przy użyciu technologii PLINQ](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)  
  
 [Instrukcje: mierzenie wydajności zapytań PLINQ](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)  
  
 [Próbka danych PLINQ](../../../docs/standard/parallel-programming/plinq-data-sample.md)  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Linq.ParallelEnumerable>
- [Programowanie równoległe](../../../docs/standard/parallel-programming/index.md)
- [Language-Integrated Query (LINQ) —C#](../../csharp/programming-guide/concepts/linq/index.md)  
- [Zapytanie zintegrowane z językiem (LINQ) — Visual Basic](../../visual-basic/programming-guide/concepts/linq/index.md)  
