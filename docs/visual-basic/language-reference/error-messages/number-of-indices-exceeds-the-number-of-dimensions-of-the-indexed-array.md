---
title: Liczba indeksów przekracza liczbę wymiarów tablicy indeksowanej
ms.date: 07/20/2015
f1_keywords:
- bc30106
- vbc30106
helpviewer_keywords:
- BC30106
ms.assetid: 2c5363e1-62c2-4f5a-b675-c7337aeb363d
ms.openlocfilehash: 76cf0a997e9ad36ab4b5dfdc7c4bc29c57d309eb
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665691"
---
# <a name="number-of-indices-exceeds-the-number-of-dimensions-of-the-indexed-array"></a>Liczba indeksów przekracza liczbę wymiarów tablicy indeksowanej
Liczba indeksów, które umożliwiają dostęp do elementu tablicy musi być dokładnie taki sam jak rangę tablicy, czyli liczbę wymiarów zadeklarowany dla niego.  
  
 **Identyfikator błędu:** BC30106  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Usuń indeksy dolne z odwołaniem do tablicy, aż łączna liczba indeksów dolnych jest równa rangę tablicy. Na przykład:  
  
    ```vb  
    Dim gameBoard(3, 3) As String  
  
    ' Incorrect code. The array has two dimensions.  
    gameBoard(1, 1, 1) = "X"  
    gameBoard(2, 1, 1) = "O"  
  
    ' Correct code.  
    gameBoard(0, 0) = "X"  
    gameBoard(1, 0) = "O"  
    ```  
  
## <a name="see-also"></a>Zobacz także

- [Tablice](../../../visual-basic/programming-guide/language-features/arrays/index.md)
