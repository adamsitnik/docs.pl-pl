---
title: C#Delegaty — Przewodnik po przykładzie C# języka
description: Dowiedz się, późne powiązania z C# delegatów
ms.date: 08/10/2016
ms.assetid: 3cc27357-3ac2-43a1-aad0-86a77b88f884
ms.openlocfilehash: 35a1e212b50e77eb43271a657c8abb21eb6cfb4a
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/15/2019
ms.locfileid: "65634636"
---
# <a name="delegates"></a>Delegaty

A ***typ delegowany*** reprezentuje odwołania do metod z określonego parametru listy i typ zwracany. Delegatów można umożliwić traktować metod jako jednostki, które mogą być przypisane do zmiennych i przekazywane jako parametry. Delegaty są podobne do koncepcji wskaźników funkcji, w przeciwieństwie do innych języków, ale w przeciwieństwie do wskaźników funkcji, obiekty delegowane są zorientowane obiektowo i bezpieczny typowo.

Poniższy przykład deklaruje i wykorzystuje typ delegata, o nazwie `Function`.

[!code-csharp[DelegateExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L3-L37)]

Wystąpienie `Function` typ delegata można odwoływać się do dowolnej metody, która przyjmuje `double` argument i zwraca `double` wartość. `Apply` Metodę stosuje się daną funkcję do elementów `double[]`, zwracanie `double[]` z wynikami. W `Main` metody `Apply` służy do trzech różnych funkcji w celu stosowania `double[]`.

Delegat może odwoływać się statycznej metody (takie jak `Square` lub `Math.Sin` w poprzednim przykładzie) lub metodą wystąpienia (takie jak `m.Multiply` w poprzednim przykładzie). Delegat, który odwołuje się do metody wystąpienia odwołuje się konkretny obiekt, a gdy wywoływana jest metoda wystąpienia, za pośrednictwem delegata, staje się ten obiekt `this` w wywołaniu.

Delegatów można także tworzyć, używając funkcji anonimowych, które są "wbudowane metody", które są tworzone na bieżąco. Funkcje anonimowe można zobaczyć zmienne lokalne otaczającym metody. Zatem w powyższym przykładzie mnożnik mogą być zapisywane łatwiej bez korzystania z klasy mnożnik:

[!code-csharp[LambdaExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L44-L44)]

Interesujące i przydatne własności delegata jest, nie wiedzieć, i nie interesuje klasy, metody, która odwołuje się do; wszystko, co dla Ciebie ważne jest, do którego istnieje odwołanie metoda ma te same parametry oraz zwracany typ jak delegat.

>[!div class="step-by-step"]
>[Poprzednie](enums.md)
>[dalej](attributes.md)
