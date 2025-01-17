---
title: Przegląd osi LINQ to XML (C#)
ms.date: 07/20/2015
ms.assetid: 516792fb-461d-40a8-8a50-9993a51258fc
ms.openlocfilehash: b984232f03815ac78b792af2289f15eeb0578cd5
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2019
ms.locfileid: "73418201"
---
# <a name="linq-to-xml-axes-overview-c"></a>Przegląd osi LINQ to XML (C#)
Po utworzeniu drzewa XML lub załadowaniu dokumentu XML do drzewa XML można wykonać zapytania do niego, aby znaleźć elementy i atrybuty i pobrać ich wartości. Kolekcje są pobierane za pomocą *metod osi*, nazywanych również *osiami*. Niektóre osie są metodami klas <xref:System.Xml.Linq.XElement> i <xref:System.Xml.Linq.XDocument>, które zwracają <xref:System.Collections.Generic.IEnumerable%601> kolekcje. Niektóre osie są metodami rozszerzającymi w klasie <xref:System.Xml.Linq.Extensions>. Osie zaimplementowane jako metody rozszerzające działają na kolekcjach i zwracają kolekcje.  
  
 Zgodnie z opisem w temacie [XElement Class](./xelement-class-overview.md)— obiekt <xref:System.Xml.Linq.XElement> reprezentuje węzeł pojedynczego elementu. Zawartość elementu może być złożona (czasami nazywana zawartością strukturalną) lub może być elementem prostym. Prosty element może być pusty lub może zawierać wartość. Jeśli węzeł zawiera zawartość strukturalną, można użyć różnych metod osi do pobierania wyliczeń elementów podrzędnych. Najczęściej używane metody osi są <xref:System.Xml.Linq.XContainer.Elements%2A> i <xref:System.Xml.Linq.XContainer.Descendants%2A>.  
  
 Oprócz metod osi, które zwracają kolekcje, istnieją dwie metody, które są często używane w kwerendach [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]. Metoda <xref:System.Xml.Linq.XContainer.Element%2A> zwraca pojedynczy <xref:System.Xml.Linq.XElement>. Metoda <xref:System.Xml.Linq.XElement.Attribute%2A> zwraca pojedynczy <xref:System.Xml.Linq.XAttribute>.  
  
 W wielu celach [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] zapytania zapewniają najbardziej wydajny sposób badania drzewa, wyodrębniania danych z niego i przekształcania. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] zapytania działają na obiektach implementujących <xref:System.Collections.Generic.IEnumerable%601>, a [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] osi zwracają <xref:System.Collections.Generic.IEnumerable%601> kolekcji <xref:System.Xml.Linq.XElement> i <xref:System.Collections.Generic.IEnumerable%601> kolekcji <xref:System.Xml.Linq.XAttribute>. Te kolekcje są potrzebne do wykonywania zapytań.  
  
 Oprócz metod osi, które pobierają kolekcje elementów i atrybutów, istnieją metody osi, które umożliwiają iteracyjne przechodzenie między drzewa. Na przykład zamiast zajmowania się elementami i atrybutami można współpracować z węzłami drzewa. Węzły to bardziej szczegółowy poziom szczegółowości niż elementy i atrybuty. Podczas pracy z węzłami można analizować Komentarze XML, węzły tekstowe, instrukcje przetwarzania i nie tylko. Ta funkcja jest ważna, na przykład do osoby, która piszą Edytor tekstów i chce zapisywać dokumenty jako XML. Jednakże większość programistów XML dotyczy głównie elementów, atrybutów i ich wartości.  
  
## <a name="methods-for-retrieving-a-collection-of-elements"></a>Metody pobierania kolekcji elementów  
 Poniżej znajduje się podsumowanie metod klasy <xref:System.Xml.Linq.XElement> (lub jej klas podstawowych) wywoływanych na <xref:System.Xml.Linq.XElement> w celu zwrócenia kolekcji elementów.  
  
|Metoda|Opis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> nadrzędnych tego elementu. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów nadrzędnych, które mają określony <xref:System.Xml.Linq.XName>.|  
|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów podrzędnych tego elementu. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów podrzędnych, które mają określony <xref:System.Xml.Linq.XName>.|  
|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów podrzędnych tego elementu. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów podrzędnych, które mają określony <xref:System.Xml.Linq.XName>.|  
|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów, które są dostępne po elemencie. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów po tym elemencie, który ma określony <xref:System.Xml.Linq.XName>.|  
|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów, które są przed tym elementem. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów przed tym elementem, który ma określony <xref:System.Xml.Linq.XName>.|  
|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> tego elementu i jego elementów nadrzędnych. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów, które mają określony <xref:System.Xml.Linq.XName>.|  
|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> tego elementu i jego elementów podrzędnych. Przeciążenie zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement> elementów, które mają określony <xref:System.Xml.Linq.XName>.|  
  
## <a name="method-for-retrieving-a-single-element"></a>Metoda pobierania pojedynczego elementu  
 Poniższa metoda pobiera jeden element podrzędny z obiektu <xref:System.Xml.Linq.XElement>.  
  
|Metoda|Opis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=nameWithType>|Zwraca pierwszy obiekt podrzędny <xref:System.Xml.Linq.XElement>, który ma określony <xref:System.Xml.Linq.XName>.|  
  
## <a name="method-for-retrieving-a-collection-of-attributes"></a>Metoda pobierania kolekcji atrybutów  
 Poniższa metoda pobiera atrybuty z obiektu <xref:System.Xml.Linq.XElement>.  
  
|Metoda|Opis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|Zwraca <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XAttribute> wszystkich atrybutów.|  
  
## <a name="method-for-retrieving-a-single-attribute"></a>Metoda pobierania pojedynczego atrybutu  
 Poniższa metoda pobiera jeden atrybut z obiektu <xref:System.Xml.Linq.XElement>.  
  
|Metoda|Opis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType>|Zwraca <xref:System.Xml.Linq.XAttribute>, która ma określony <xref:System.Xml.Linq.XName>.|  
  
## <a name="see-also"></a>Zobacz także

- [Osie LINQ to XML (C#)](linq-to-xml-axes-overview.md)
