---
title: set — słowo kluczowe - C# odwołania
ms.custom: seodec18
ms.date: 03/10/2017
f1_keywords:
- set
- set_CSharpKeyword
helpviewer_keywords:
- set keyword [C#]
ms.assetid: 30d7e4e5-cc2e-4635-a597-14a724879619
ms.openlocfilehash: 0322f1bb94174dd3a0cdd2089c8626d25a80cc1c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61660752"
---
# <a name="set-c-reference"></a>set (odwołanie w C#)

`set` — Słowo kluczowe definiuje *akcesor* metoda we właściwości lub indeksatora, który przypisuje wartość do właściwości lub elementu indeksatora. Aby uzyskać więcej informacji i przykładów, zobacz [właściwości](../../programming-guide/classes-and-structs/properties.md), [implemented Properties](../../programming-guide/classes-and-structs/auto-implemented-properties.md), i [indeksatory](../../programming-guide/indexers/index.md).

W poniższym przykładzie zdefiniowano zarówno `get` i `set` akcesora dla właściwości o nazwie `Seconds`. Używa prywatnego pola o nazwie `_seconds` kopii wartości właściwości.

[!code-csharp[set#1](~/samples/snippets/csharp/language-reference/keywords/get/get-1.cs)]

Często `set` dostępu składa się z pojedynczej instrukcji, która przypisuje wartość, tak jak w poprzednim przykładzie. Począwszy od języka C# 7.0, można zaimplementować `set` dostępu jako element członkowski wyrażeniem. Poniższy przykład implementuje interfejsy `get` i `set` metod dostępu jako elementy członkowskie z wyrażeniem.

[!code-csharp[set#3](~/samples/snippets/csharp/language-reference/keywords/get/get-3.cs)]
  
Dla prostych sytuacjach, w których właściwość `get` i `set` Akcesory wykonać żadna inna operacja niż ustawienie lub odczytywania wartości pola prywatnego zapasowy, możesz korzystać z zalet Obsługa właściwości zaimplementowane automatycznie w kompilatorze języka C#. Poniższy przykład implementuje `Hours` jako automatycznie implementowanej właściwości. 

[!code-csharp[set#2](~/samples/snippets/csharp/language-reference/keywords/get/get-2.cs)]
  
## <a name="c-language-specification"></a>specyfikacja języka C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../../language-reference/index.md)
- [Przewodnik programowania w języku C#](../../programming-guide/index.md)
- [Słowa kluczowe języka C#](index.md)
- [Właściwości](../../programming-guide/classes-and-structs/properties.md)
