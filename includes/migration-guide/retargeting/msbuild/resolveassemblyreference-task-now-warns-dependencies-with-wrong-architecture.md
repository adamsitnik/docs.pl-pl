---
ms.openlocfilehash: 39a329597ef28e002242103a247515d94761676a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62091699"
---
### <a name="resolveassemblyreference-task-now-warns-of-dependencies-with-the-wrong-architecture"></a>Wyświetli ostrzeżenie zależności z architekturą niewłaściwego resolveassemblyreference — zadanie

|   |   |
|---|---|
|Szczegóły|Zadanie emituje ostrzeżenie MSB3270, co oznacza, że odwołanie lub dowolną z jego zależności jest niezgodna Architektura aplikacji. Na przykład, dzieje się tak w przypadku aplikacji, którą skompilowano przy użyciu <code>AnyCPU</code> opcja powoduje dołączenie x86 odwołania. Taki scenariusz może spowodować błąd aplikacji w czasie wykonywania (w tym przypadku, gdy aplikacja jest wdrożona jako x64 procesu).|
|Sugestia|Istnieją dwa obszary wpływ:<ul><li>Ponowna kompilacja generuje ostrzeżenia, które nie pojawiły się po aplikacji został skompilowany w ramach poprzedniej wersji programu MSBuild. Jednak ponieważ ostrzeżenie identyfikuje możliwym źródłem błędów czasu wykonywania, powinien można zbadać i które zostały rozwiązane.</li><li>Jeśli ostrzeżenia są traktowane jako błędy, aplikacja zakończy się niepowodzeniem skompilować.</li></ul>|
|Zakres|Mały|
|Wersja|4.5.1|
|Typ|Przekierowanie|
