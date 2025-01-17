---
title: 'Instrukcje: pobieranie wartości atrybutu (LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 5f4b3790-c83f-4eb3-a889-e3587edf3ca1
ms.openlocfilehash: 6f9a5936c962111eb75a05f5e3704f7132618143
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/15/2019
ms.locfileid: "72320475"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-visual-basic"></a>Instrukcje: pobieranie wartości atrybutu (LINQ to XML) (Visual Basic)
W tym temacie pokazano, jak uzyskać wartość atrybutów. Istnieją dwa podstawowe sposoby: można rzutować <xref:System.Xml.Linq.XAttribute> na żądany typ; operator jawnej konwersji konwertuje zawartość elementu lub atrybutu do określonego typu. Alternatywnie można użyć właściwości <xref:System.Xml.Linq.XAttribute.Value%2A>. Jednak Rzutowanie jest ogólnie lepszym rozwiązaniem. Jeśli rzutowany atrybut na typ dopuszczający wartość null, kod jest łatwiejszy do zapisu podczas pobierania wartości atrybutu, który może lub nie istnieje. Przykłady tej techniki można znaleźć w temacie [How to: pobieranie wartości elementu (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md).  
  
## <a name="example"></a>Przykład  
 W Visual Basic można użyć właściwości Integrated Attribute, aby pobrać wartość atrybutu.  
  
```vb  
Dim root As XElement = <Root Attr="abcde"/>  
Console.WriteLine(root)  
Dim str As String = root.@Attr  
Console.WriteLine(str)  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```xml  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>Przykład  
 W Visual Basic można użyć właściwości Integrated Attribute, aby ustawić wartość atrybutu. Ponadto w przypadku użycia właściwości Integrated Attribute do ustawienia wartości atrybutu, który nie istnieje, atrybut zostanie utworzony.  
  
```vb  
Dim root As XElement = <Root Att1="content"/>  
root.@Att1 = "new content"  
root.@Att2 = "new attribute"  
Console.WriteLine(root)  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```xml  
<Root Att1="new content" Att2="new attribute" />  
```  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje, jak pobrać wartość atrybutu, gdzie atrybut znajduje się w przestrzeni nazw. Aby uzyskać więcej informacji, zobacz temat [przestrzenie nazw — omówienie (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root aw:Attr="abcde"/>  
        Dim str As String = root.@aw:Attr  
        Console.WriteLine(str)  
    End Sub  
End Module  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```console  
abcde  
```  
  
## <a name="see-also"></a>Zobacz także

- [Osie LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
