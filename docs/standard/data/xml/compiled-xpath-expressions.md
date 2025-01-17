---
title: Skompilowane wyrażenia XPath
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: e25dd95f-b64c-4d8b-a3a4-379e1aa0ad55
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fb6e3677d79f3131432c3daebeee4d166b5450b2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916662"
---
# <a name="compiled-xpath-expressions"></a>Skompilowane wyrażenia XPath
<xref:System.Xml.XPath.XPathExpression> <xref:System.Xml.XPath.XPathExpression.Compile%2A> <xref:System.Xml.XPath.XPathNavigator> <xref:System.Xml.XPath.XPathNavigator.Compile%2A> Obiekt reprezentuje skompilowane zapytanie XPath zwrócone z metody statycznej klasy lub metody klasy. <xref:System.Xml.XPath.XPathExpression>  
  
## <a name="the-xpathexpression-class"></a>Klasa XPathExpression  
 Skompilowane zapytanie XPath reprezentowane przez <xref:System.Xml.XPath.XPathExpression> obiekt jest przydatne, jeśli ta sama kwerenda XPath jest używana więcej niż raz.  
  
 Na przykład w <xref:System.Xml.XPath.XPathNavigator.Select%2A> przypadku wywołania metody wiele razy zamiast używać ciągu reprezentującego zapytanie XPath za każdym razem <xref:System.Xml.XPath.XPathExpression.Compile%2A> Użyj metody <xref:System.Xml.XPath.XPathExpression> klasy lub <xref:System.Xml.XPath.XPathNavigator.Compile%2A> metody <xref:System.Xml.XPath.XPathNavigator> klasy do kompilowania i buforowanie zapytania XPath w <xref:System.Xml.XPath.XPathExpression> obiekcie w celu ponownego użycia i zwiększenia wydajności.  
  
 Po skompilowaniu <xref:System.Xml.XPath.XPathExpression> obiekt może być używany jako dane wejściowe dla następujących <xref:System.Xml.XPath.XPathNavigator> metod klasy w zależności od typu zwracanego z kwerendy XPath.  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.XPath.XPathNavigator.Matches%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 W poniższej tabeli opisano każdy z typów zwracanych przez konsorcjum W3C XPath, ich Microsoft .NET Framework equivalencies i metody <xref:System.Xml.XPath.XPathExpression> , z których może korzystać obiekt na podstawie zwracanego typu.  
  
|Typ zwracany XPath W3C|Typ odpowiedni .NET Framework|Opis|Metody|  
|---------------------------|------------------------------------|-----------------|-------------|  
|`Node set`|<xref:System.Xml.XPath.XPathNodeIterator>|Nieuporządkowana kolekcja węzłów bez duplikatów utworzonych w kolejności dokumentu.|<xref:System.Xml.XPath.XPathNavigator.Select%2A> lub <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
|`Boolean`|<xref:System.Boolean>|Wartość `true` lub `false` .|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>oraz<br /><br /> <xref:System.Xml.XPath.XPathNavigator.Matches%2A>|  
|`Number`|<xref:System.Double>|Liczba zmiennoprzecinkowa.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
|`String`|<xref:System.String>|Sekwencja znaków UCS.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
  
> [!NOTE]
> <xref:System.Xml.XPath.XPathNavigator.Matches%2A> Metoda akceptuje wyrażenie XPath jako parametr. <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> Metoda<xref:System.Xml.XPath.XPathNavigator> zwraca obiekt, a nie jeden z typów zwracanych w formacie XPath.  
  
### <a name="the-returntype-property"></a>Właściwość ReturnType  
 Po skompilowaniu zapytania XPath do <xref:System.Xml.XPath.XPathExpression> obiektu można <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> użyć właściwości <xref:System.Xml.XPath.XPathExpression> obiektu, aby określić, co zwraca zapytanie XPath.  
  
 Właściwość zwraca jedną z następujących <xref:System.Xml.XPath.XPathResultType> wartości wyliczenia reprezentujących typy zwracane W3C XPath. <xref:System.Xml.XPath.XPathExpression.ReturnType%2A>  
  
- <xref:System.Xml.XPath.XPathResultType.Any>  
  
- <xref:System.Xml.XPath.XPathResultType.Boolean>  
  
- <xref:System.Xml.XPath.XPathResultType.Error>  
  
- <xref:System.Xml.XPath.XPathResultType.Navigator>  
  
- <xref:System.Xml.XPath.XPathResultType.NodeSet>  
  
- <xref:System.Xml.XPath.XPathResultType.Number>  
  
- <xref:System.Xml.XPath.XPathResultType.String>  
  
 Poniższy przykład używa <xref:System.Xml.XPath.XPathExpression> obiektu do zwrócenia numeru i zestawu węzłów `books.xml` z pliku. Właściwość każdego <xref:System.Xml.XPath.XPathExpression> obiektu, <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> a także wyniki z i <xref:System.Xml.XPath.XPathNavigator.Select%2A> metody są zapisywane w konsoli programu. <xref:System.Xml.XPath.XPathExpression.ReturnType%2A>  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Returns a number.  
Dim query1 As XPathExpression = navigator.Compile("bookstore/book/price/text()*10")  
Console.WriteLine(query1.ReturnType)  
  
Dim number As Double = CType(navigator.Evaluate(query1), Double)  
Console.WriteLine(number)  
  
' Returns a node set.  
Dim query2 As XPathExpression = navigator.Compile("bookstore/book/price")  
Console.WriteLine(query2.ReturnType)  
  
Dim nodes As XPathNodeIterator = navigator.Select(query2)  
nodes.MoveNext()  
Console.WriteLine(nodes.Current.Value)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Returns a number.  
XPathExpression query1 = navigator.Compile("bookstore/book/price/text()*10");  
Console.WriteLine(query1.ReturnType);  
  
Double number = (Double)navigator.Evaluate(query1);  
Console.WriteLine(number);  
  
// Returns a node set.  
XPathExpression query2 = navigator.Compile("bookstore/book/price");  
Console.WriteLine(query2.ReturnType);  
  
XPathNodeIterator nodes = navigator.Select(query2);  
nodes.MoveNext();  
Console.WriteLine(nodes.Current.Value);  
```  
  
 Przykład pobiera `books.xml` plik jako dane wejściowe.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="higher-performance-xpath-expressions"></a>Wyrażenia XPath o wyższej wydajności  
 Aby uzyskać lepszą wydajność, użyj najbardziej określonego wyrażenia XPath możliwego w zapytaniach. Na przykład `book` , jeśli węzeł jest węzłem `bookstore` podrzędnym węzła, a `bookstore` węzeł jest elementem najwyższego poziomu w dokumencie XML, użycie wyrażenia `/bookstore/book` XPath jest szybsze niż używanie `//book`. Wyrażenie `//book` XPath skanuje każdy węzeł w drzewie XML, aby zidentyfikować pasujące węzły.  
  
 Ponadto przy użyciu metody nawigacji zestawu węzłów dostarczonej przez <xref:System.Xml.XPath.XPathNavigator> klasę mogą spowodować zwiększenie wydajności na podstawie metod wyboru dostarczonych <xref:System.Xml.XPath.XPathNavigator> przez klasę w przypadkach, gdy kryteria wyboru są proste. Na przykład, jeśli trzeba wybrać pierwszy element podrzędny bieżącego węzła, można użyć <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A> metody, aby `child::*[1]` użyć wyrażenia XPath i <xref:System.Xml.XPath.XPathNavigator.Select%2A> metody.  
  
 Aby uzyskać więcej informacji o metodach nawigacji zestawu węzłów <xref:System.Xml.XPath.XPathNavigator> klasy, zobacz Nawigowanie po [węźle przy użyciu elementu XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [Przetwarzanie danych XML przy użyciu modelu danych XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [Wybieranie danych XML przy użyciu klasy XPathNavigator](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [Obliczanie wyrażeń XPath przy użyciu klasy XPathNavigator](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [Dopasowywanie węzłów przy użyciu klasy XPathNavigator](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)
- [Typy węzłów rozpoznawanych w zapytaniach XPath](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [Zapytania XPath i przestrzenie nazw](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
