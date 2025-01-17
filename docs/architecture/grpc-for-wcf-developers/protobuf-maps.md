---
title: Mapy protobuf dla słowników — gRPC dla deweloperów WCF
description: Dowiedz się, jak reprezentować za pomocą map protobuf. Typy słowników netto.
author: markrendle
ms.date: 09/09/2019
ms.openlocfilehash: aef6b0f378e7a63f362ec42642cae15b32d49a08
ms.sourcegitcommit: 337bdc5a463875daf2cc6883e5a2da97d56f5000
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/24/2019
ms.locfileid: "72846335"
---
# <a name="protobuf-maps-for-dictionaries"></a>Mapy Protobuf dla słowników

Ważne jest, aby reprezentować dowolne kolekcje nazwanych wartości w komunikatach. W programie .NET jest to często obsługiwane przy użyciu typów słowników. Protobuf jest odpowiednikiem typu `map<key_type, value_type>` na platformie .NET <xref:System.Collections.Generic.IDictionary%602>. W tej sekcji pokazano, jak zadeklarować `map` w protobuf i jak używać wygenerowanego kodu.

```protobuf
message StockPrices {
    map<string, double> prices = 1;
}
```

W wygenerowanym kodzie `map` pola używają klasy `Google.Protobuf.Collections.MapField<TKey, TValue>`, która implementuje standardowe interfejsy kolekcji .NET, w tym <xref:System.Collections.Generic.IDictionary%602>.

Nie można bezpośrednio powtarzać pól mapy w definicji komunikatu, ale można utworzyć zagnieżdżony komunikat zawierający mapę i użyć `repeated` na typ komunikatu, jak w poniższym przykładzie:

```protobuf
message Order {
    message Attributes {
        map<string, string> values = 1;
    }
    repeated Attributes attributes = 1;
}
```

## <a name="using-mapfield-properties-in-code"></a>Używanie właściwości MapField w kodzie

`MapField` właściwości generowane na podstawie `map` pól są tylko do odczytu i nie będą `null`. Aby ustawić właściwość mapy, użyj metody `Add(IDictionary<TKey,TValue> values)` na pustej właściwości `MapField`, aby skopiować wartości z dowolnego słownika platformy .NET.

```csharp
public Order CreateOrder(Dictionary<string, string> attributes)
{
    var order = new Order();
    order.Attributes.Add(attributes);
    return order;
}
```

## <a name="further-reading"></a>Dalsze odczytywanie

Aby uzyskać więcej informacji na temat protobuf, zobacz oficjalną [dokumentację protobuf](https://developers.google.com/protocol-buffers/docs/overview).

>[!div class="step-by-step"]
>[Poprzedni](protobuf-enums.md)
>[Następny](wcf-services-to-grpc-comparison.md)
