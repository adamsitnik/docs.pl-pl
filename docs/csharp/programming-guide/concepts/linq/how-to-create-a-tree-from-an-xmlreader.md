---
title: 'Instrukcje: Tworzenie drzewa na podstawie elementu XmlReader (C#)'
ms.date: 07/20/2015
ms.assetid: 60951c9c-7087-406c-b5bb-c60e58609b21
ms.openlocfilehash: a0cff596e0a6d50aefab3645a99beec3277d05ec
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73418322"
---
# <a name="how-to-create-a-tree-from-an-xmlreader-c"></a>Instrukcje: Tworzenie drzewa na podstawie elementu XmlReader (C#)
W tym temacie pokazano, jak utworzyć drzewo XML bezpośrednio z <xref:System.Xml.XmlReader>. Aby utworzyć <xref:System.Xml.Linq.XElement> z <xref:System.Xml.XmlReader>, należy umieścić <xref:System.Xml.XmlReader> w węźle elementu. <xref:System.Xml.XmlReader> pominie Komentarze i instrukcje przetwarzania, ale jeśli <xref:System.Xml.XmlReader> jest umieszczony w węźle tekstowym, zostanie zgłoszony błąd. Aby uniknąć takich błędów, należy zawsze umieścić <xref:System.Xml.XmlReader> w elemencie przed utworzeniem drzewa XML z <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Przykład  
 Ten przykład używa następującego dokumentu XML: [przykładowy plik XML: Books (LINQ to XML)](./sample-xml-file-books-linq-to-xml.md).  
  
 Poniższy kod tworzy obiekt `T:System.Xml.XmlReader`, a następnie odczytuje węzły do momentu znalezienia węzła pierwszego elementu. Następnie ładuje obiekt <xref:System.Xml.Linq.XElement>.  
  
```csharp  
XmlReader r = XmlReader.Create("books.xml");  
while (r.NodeType != XmlNodeType.Element)  
    r.Read();  
XElement e = XElement.Load(r);  
Console.WriteLine(e);  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```xml  
<Catalog>  
   <Book id="bk101">  
      <Author>Garghentini, Davide</Author>  
      <Title>XML Developer's Guide</Title>  
      <Genre>Computer</Genre>  
      <Price>44.95</Price>  
      <PublishDate>2000-10-01</PublishDate>  
      <Description>An in-depth look at creating applications   
      with XML.</Description>  
   </Book>  
   <Book id="bk102">  
      <Author>Garcia, Debra</Author>  
      <Title>Midnight Rain</Title>  
      <Genre>Fantasy</Genre>  
      <Price>5.95</Price>  
      <PublishDate>2000-12-16</PublishDate>  
      <Description>A former architect battles corporate zombies,   
      an evil sorceress, and her own childhood to become queen   
      of the world.</Description>  
   </Book>  
</Catalog>  
```  
  
## <a name="see-also"></a>Zobacz także

- [Analizowanie pliku XMLC#()](how-to-parse-a-string.md)
