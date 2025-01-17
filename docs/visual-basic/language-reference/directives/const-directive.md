---
title: '#Const — dyrektywa (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.#Const
- '#vb.Const'
- '#Const'
helpviewer_keywords:
- '#Const directive'
- conditional compilation [Visual Basic], directives
- Const directive (#Const)
- Visual Basic compiler, compiler directives
- constants [Visual Basic], Const directive
- constants [Visual Basic], declaring
- Const statement [Visual Basic], directive (#Const)
- 'declaring constants [Visual Basic], #const directive'
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
ms.openlocfilehash: 031f35df24fd52aeeafcb7b4c0208806d7fc5fc4
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72774753"
---
# <a name="const-directive"></a>#Const — dyrektywa
Definiuje warunkowe stałe kompilatora dla Visual Basic.  
  
## <a name="syntax"></a>Składnia  
  
```vb  
#Const constname = expression  
```  
  
## <a name="parts"></a>Części  
 `constname`  
 Wymagany. Nazwa zdefiniowanej stałej.  
  
 `expression`  
 Wymagany. Literał, inna warunkowa stała kompilatora lub dowolna kombinacja, która zawiera wszystkie lub wszystkie operatory arytmetyczne lub logiczne z wyjątkiem `Is`.  
  
## <a name="remarks"></a>Uwagi  
 Warunkowe stałe kompilatora są zawsze prywatne dla pliku, w którym się znajdują. Nie można tworzyć publicznych stałych kompilatora przy użyciu dyrektywy `#Const`; można je utworzyć tylko w interfejsie użytkownika lub za pomocą opcji kompilatora `/define`.  
  
 W `expression` można używać tylko warunkowych stałych kompilatora i literałów. Użycie stałej standardowej zdefiniowanej za pomocą `Const` powoduje wystąpienie błędu. Odwrotnie, można użyć stałych zdefiniowanych za pomocą słowa kluczowego `#Const` tylko dla kompilacji warunkowej. Stałe mogą być również niezdefiniowane, w takim przypadku mają wartość `Nothing`.  
  
## <a name="example"></a>Przykład  
 Ten przykład używa dyrektywy `#Const`.  
  
 [!code-vb[VbVbalrConditionalComp#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>Zobacz także

- [-Definiuj (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
- [#If...Then...#Else, dyrektywy](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [Const, instrukcja](../../../visual-basic/language-reference/statements/const-statement.md)
- [Kompilacja warunkowa](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [If...Then...Else, instrukcja](../../../visual-basic/language-reference/statements/if-then-else-statement.md)
