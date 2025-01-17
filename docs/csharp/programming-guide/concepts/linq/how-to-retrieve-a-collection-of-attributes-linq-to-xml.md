---
title: 'Instrukcje: Pobieranie kolekcji atrybutów (LINQ to XML) (C#)'
ms.date: 07/20/2015
ms.assetid: a49ee7a3-b2c2-4d49-9b5c-b7c6c41f4f13
ms.openlocfilehash: b1721de5ac396faab010dab691bfd88991bad638
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253437"
---
# <a name="how-to-retrieve-a-collection-of-attributes-linq-to-xml-c"></a>Instrukcje: Pobieranie kolekcji atrybutów (LINQ to XML) (C#)
W <xref:System.Xml.Linq.XElement.Attributes%2A> tym temacie przedstawiono metodę. Ta metoda pobiera atrybuty elementu.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje, jak wykonać iterację kolekcji atrybutów elementu.  
  
```csharp  
XElement val = new XElement("Value",  
    new XAttribute("ID", "1243"),  
    new XAttribute("Type", "int"),  
    new XAttribute("ConvertableTo", "double"),  
    "100");  
IEnumerable<XAttribute> listOfAttributes =  
    from att in val.Attributes()  
    select att;  
foreach (XAttribute a in listOfAttributes)  
    Console.WriteLine(a);  
```  
  
 Ten kod generuje następujące dane wyjściowe:  
  
```output  
ID="1243"  
Type="int"  
ConvertableTo="double"  
```  
  
## <a name="see-also"></a>Zobacz także

- [Osie LINQ to XML (C#)](./linq-to-xml-axes-overview.md)
