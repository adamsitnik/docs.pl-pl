---
title: Sprzęganie za pomocą kluczy złożonych (LINQ w C#)
description: Dowiedz się, jak sprzęgać za pomocą kluczy złożonych w składniku LINQ.
ms.date: 12/01/2016
ms.assetid: da70b54d-3213-45eb-8437-fbe75cbcf935
ms.openlocfilehash: 460a52da7e0c0a47b77d4c64e76641bae9da7cd6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61659881"
---
# <a name="join-by-using-composite-keys"></a>Sprzęganie za pomocą kluczy złożonych

Ten przykład przedstawia sposób wykonywania operacji łączenia, w których chcesz użyć więcej niż jednego klucza do zdefiniowania dopasowania. Jest to realizowane przy użyciu klucza złożonego. Można tworzyć złożonego klucza jako typu anonimowego lub nazwane wpisane wartościami, które chcesz porównać. Jeśli zmienna zapytania zostaną przekazane w granicach metody, należy użyć typu nazwanego, który zastępuje <xref:System.Object.Equals%2A> i <xref:System.Object.GetHashCode%2A> dla klucza. Nazwy właściwości i kolejność, w jakiej występują one muszą być identyczne w każdy klucz.

## <a name="example"></a>Przykład

Poniższy przykład pokazuje sposób użycia klucza złożonego do łączenia danych z trzech tabel:

```csharp
var query = from o in db.Orders
    from p in db.Products
    join d in db.OrderDetails
        on new {o.OrderID, p.ProductID} equals new {d.OrderID, d.ProductID} into details
        from d in details
        select new {o.OrderID, p.ProductID, d.UnitPrice};
```

Wnioskowanie o typie na klucze złożone zależy od nazwy właściwości kluczy i kolejności ich występowania. Jeśli właściwości w sekwencji źródłowej nie ma takie same nazwy, należy przypisać nowe nazwy w kluczach. Na przykład jeśli `Orders` tabeli i `OrderDetails` tabeli każdego używać różnych nazw kolumn, można utworzyć kluczy złożonych, przypisując identyczne nazwy typów anonimowych:

```csharp
join...on new {Name = o.CustomerName, ID = o.CustID} equals
    new {Name = d.CustName, ID = d.CustID }
```

Klucze złożone, które mogą być również używane w `group` klauzuli.

## <a name="see-also"></a>Zobacz także

- [Language Integrated Query (LINQ)](index.md)
- [join, klauzula](../language-reference/keywords/join-clause.md)
- [group, klauzula](../language-reference/keywords/group-clause.md)
