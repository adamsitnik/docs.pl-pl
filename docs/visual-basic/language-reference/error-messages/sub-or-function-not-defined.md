---
title: Procedura lub funkcja nie jest zdefiniowana
ms.date: 07/20/2015
f1_keywords:
- vbrID35
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
ms.openlocfilehash: 3a56d5596c79900bb5818a6ed7f8736859b5ea15
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593199"
---
# <a name="sub-or-function-not-defined-visual-basic"></a>Procedura lub funkcja nie jest zdefiniowana
A `Sub` lub `Function` muszą być zdefiniowane w celu wywołana. Możliwe przyczyny tego błędu:  
  
- Błąd w pisowni nazwy procedury.  
  
- Podjęcie próby wywołać procedurę z innego projektu bez jawnie dodać odwołanie do tego projektu w **odwołania** okno dialogowe.  
  
- Określenie procedury, która jest niewidoczna dla procedury wywołującej.  
  
- Deklarowanie procedury biblioteki dołączanej (dynamicznie DLL) Windows lub dla komputerów Macintosh zasobów kod procedury, która nie jest określony zasób biblioteki lub kodu.  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
1. Upewnij się, że poprawna nazwa procedury.  
  
2. Znajdowanie nazwy do projektu zawierającego procedury, aby wywołać w **odwołania** okno dialogowe. Jeśli nie zostanie wyświetlony, kliknij przycisk **Przeglądaj** przycisk, aby ją wyszukać. Zaznacz pole wyboru po lewej stronie nazwy projektu, a następnie kliknij przycisk **OK**.  
  
3. Sprawdź nazwę procedury.  
  
## <a name="see-also"></a>Zobacz także

- [Typy błędów](../../../visual-basic/programming-guide/language-features/error-types.md)
- [Zarządzanie odwołaniami w projekcie](/visualstudio/ide/managing-references-in-a-project)
- [Sub, instrukcja](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Function, instrukcja](../../../visual-basic/language-reference/statements/function-statement.md)
