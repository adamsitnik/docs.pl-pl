---
title: 'Instrukcje: wyszukiwanie elementu głównego (XPath-LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 72c3aed5-9522-4454-a876-2070aad13f2e
ms.openlocfilehash: d8ac28b698b0c61a4d9e3beea61ff8a8e1074b88
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/15/2019
ms.locfileid: "72320584"
---
# <a name="how-to-find-the-root-element-xpath-linq-to-xml-visual-basic"></a>Instrukcje: wyszukiwanie elementu głównego (XPath-LINQ to XML) (Visual Basic)
W tym temacie pokazano, jak uzyskać element główny z wyrażeniem XPath i [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].  
  
 Wyrażenie XPath:  
  
 `/PurchaseOrders`  
  
## <a name="example"></a>Przykład  
 Ten przykład umożliwia znalezienie elementu głównego.  
  
 W tym przykładzie zastosowano następujący dokument XML: [przykładowy plik XML: wiele zamówień zakupu (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
```vb  
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")  
  
' LINQ to XML query  
Dim el1 As XElement = po.Root  
  
' XPath expression  
Dim el2 As XElement = po.XPathSelectElement("/PurchaseOrders")  
  
If el1 Is el2 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(el1.Name)  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```console  
Results are identical  
PurchaseOrders  
```  
  
## <a name="see-also"></a>Zobacz także

- [LINQ to XML dla użytkowników XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
