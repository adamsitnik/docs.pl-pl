---
title: Używanie obsługi wyjątków filtrowanych przez użytkownika
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- user-filtered exceptions
- exceptions, user-filtered
ms.assetid: aa80d155-060d-41b4-a636-1ceb424afee8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 228bae8db833abfa3c8c906d57e2177cde644548
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945460"
---
# <a name="using-user-filtered-exception-handlers"></a>Używanie obsługi wyjątków filtrowanych przez użytkownika

Obecnie usługa Visual Basic obsługuje wyjątki filtrowane przez użytkownika. Programy obsługi wyjątków filtrowanych przez użytkownika przechwytywać i obsługiwać wyjątki, na podstawie wymagań zdefiniowanych dla wyjątku. Użyj tych procedur obsługi **Catch** instrukcję, określając **podczas** — słowo kluczowe.  
  
 Ta technika jest przydatna, gdy obiekt określony wyjątek odpowiada wiele błędów. W tym przypadku obiekt ma zazwyczaj właściwość, która zawiera kod błędu skojarzony z błędem. Właściwości kodu błędu w wyrażeniu służy do wybierania tylko określony błąd mają być obsługiwane w tym **Catch** klauzuli.  
  
 W poniższym przykładzie w języku Visual Basic pokazano **Catch/gdy** instrukcji.  
  
```vb
Try  
    'Try statements.  
    Catch When Err = VBErr_ClassLoadException
    'Catch statements.
End Try  
```  
  
 Wyrażenie klauzuli filtrowanych przez użytkownika nie ma ograniczeń w dowolny sposób. Jeśli wystąpi wyjątek podczas wykonywania wyrażenia filtrowanych przez użytkownika, ten wyjątek jest odrzucana i wyrażenie filtru jest uznawany za zostały ocenione na wartość false. W takim wypadku środowisko uruchomieniowe języka wspólnego kontynuuje wyszukiwanie obsługi dla bieżącego wyjątku.  
  
## <a name="combining-the-specific-exception-and-the-user-filtered-clauses"></a>Łączenie określonego wyjątku i klauzule filtrowanych przez użytkownika  
 Instrukcja catch może zawierać zarówno określony wyjątek, jak i klauzule filtrowanych przez użytkownika. Środowisko uruchomieniowe sprawdza określony wyjątek, najpierw. Jeśli określony wyjątek zakończy się powodzeniem, środowisko uruchomieniowe wykonuje filtr użytkownika. Filtr ogólny może zawierać odwołanie do zmiennej zadeklarowanej w filtrze klasy. Należy zauważyć kolejność klauzul dwóch filtru nie można cofnąć.  
  
 W poniższym przykładzie w języku Visual Basic przedstawia określony wyjątek `ClassLoadException` w **Catch** instrukcji, a także przy użyciu klauzuli filtrowanych przez użytkownika **podczas** — słowo kluczowe.  
  
```vb
Try  
    'Try statements.
    Catch cle As ClassLoadException When cle.IsRecoverable()  
    'Catch statements.
End Try  
```  

## <a name="see-also"></a>Zobacz także

- [Wyjątki](index.md)
