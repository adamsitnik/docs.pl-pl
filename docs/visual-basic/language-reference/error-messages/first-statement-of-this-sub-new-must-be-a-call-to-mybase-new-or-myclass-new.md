---
title: Pierwsza instrukcja tego elementu „Sub New” musi być wywołaniem do „MyBase.New” lub „MyClass.New” (Nie jest dostępny żaden konstruktor bez parametrów)
ms.date: 07/20/2015
f1_keywords:
- bc30148
- vbc30148
helpviewer_keywords:
- BC30148
ms.assetid: 4426e8fc-cb39-4eb8-ba95-503cd32fcc89
ms.openlocfilehash: 160e4d512a1533b3c89a1af50b47600ca6df51c2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592057"
---
# <a name="first-statement-of-this-sub-new-must-be-a-call-to-mybasenew-or-myclassnew-no-accessible-constructor-without-parameters"></a>Pierwsza instrukcja tego elementu „Sub New” musi być wywołaniem do „MyBase.New” lub „MyClass.New” (Nie jest dostępny żaden konstruktor bez parametrów)
Pierwsza instrukcja tego elementu "Sub New" musi być wywołaniem elementu "MyBase.New" lub "MyClass.New", ponieważ klasy bazowej\<basename > "z"\<derivedname > "nie ma dostępnego elementu"Sub New", który można wywołać bez argumentów.  
  
 W klasie pochodnej, co konstruktor musi wywołać konstruktora klasy bazowej (`MyBase.New`). Jeśli klasa bazowa ma konstruktora bez parametrów, który jest dostępny dla klasy pochodnej `MyBase.New` zostaje wywołana automatycznie. W przeciwnym razie konstruktora klasy bazowej, musi zostać wywołana z parametrami, a nie można tego zrobić automatycznie. W takim przypadku pierwsza instrukcja każdej konstruktora klasy pochodnej musi wywołania sparametryzowanego konstruktora dla klasy bazowej lub wywołanie innego konstruktora w klasie pochodnej, która sprawia, że wywołanie konstruktora klasy podstawowej.  
  
 **Identyfikator błędu:** BC30148  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Wywołać `MyBase.New` dostarczanie wymagane parametry lub wywołanie konstruktora elementu równorzędnego, który sprawia, że takie wywołania.  
  
     Na przykład, jeśli klasa bazowa ma Konstruktor, który jest zadeklarowany jako `Public Sub New(ByVal index as Integer)`, pierwsza instrukcja w pochodnej konstruktora klasy może być `MyBase.New(100)`.  
  
## <a name="see-also"></a>Zobacz także

- [Podstawowe informacje o dziedziczeniu](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
