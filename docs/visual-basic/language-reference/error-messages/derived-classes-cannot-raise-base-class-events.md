---
title: Klasy pochodne nie mogą wywoływać zdarzeń klasy bazowej
ms.date: 07/20/2015
f1_keywords:
- vbc30029
- bc30029
helpviewer_keywords:
- BC30029
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
ms.openlocfilehash: 030c9c2ffa97572298b23f05c23e3af0df7387b0
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/29/2019
ms.locfileid: "64913160"
---
# <a name="derived-classes-cannot-raise-base-class-events"></a>Klasy pochodne nie mogą wywoływać zdarzeń klasy bazowej
Zdarzenie może zostać wywołane jedynie z deklaracji miejsca, w którym jest zdeklarowana. W związku z tym klasy nie mogą wywoływać zdarzeń z żadną inną klasę, nawet jeśli jest on z którego pochodzi.  
  
 **Identyfikator błędu:** BC30029  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Przenieś `Event` instrukcji lub `RaiseEvent` instrukcji, dzięki czemu są one w tej samej klasie.  
  
## <a name="see-also"></a>Zobacz także

- [Event, instrukcja](../../../visual-basic/language-reference/statements/event-statement.md)
- [RaiseEvent, instrukcja](../../../visual-basic/language-reference/statements/raiseevent-statement.md)
