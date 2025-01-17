---
title: 'Instrukcje: Znajdź elementy podrzędne na podstawie pozycji (XPath-LINQ to XML) (C#)'
ms.date: 07/20/2015
ms.assetid: e35bb269-ec86-4c96-8321-12491a0eb2c3
ms.openlocfilehash: 1adbbb6dd074ffcb39269a800024e444cf8791d1
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253757"
---
# <a name="how-to-find-child-elements-based-on-position-xpath-linq-to-xml-c"></a>Instrukcje: Znajdź elementy podrzędne na podstawie pozycji (XPath-LINQ to XML) (C#)
Czasami chcesz znaleźć elementy na podstawie ich położenia. Może być konieczne znalezienie drugiego elementu lub znalezienie trzeciej przez piąty element.  
  
 Wyrażenie XPath:  
  
 `Test[position() >= 2 and position() <= 4]`  
  
 Istnieją dwa podejścia do pisania tego [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] zapytania w sposób opóźniony. Można użyć <xref:System.Linq.Enumerable.Skip%2A> operatorów i <xref:System.Linq.Enumerable.Take%2A> lub użyć <xref:System.Linq.Enumerable.Where%2A> przeciążenia, które przyjmuje indeks. <xref:System.Linq.Enumerable.Where%2A> Używając przeciążenia, należy użyć wyrażenia lambda, które przyjmuje dwa argumenty. W poniższym przykładzie przedstawiono obie metody wyboru na podstawie pozycji.  
  
## <a name="example"></a>Przykład  
 Ten przykład wyszukuje sekundę za pomocą czwartego `Test` elementu. Wynik jest kolekcją elementów.  
  
 W tym przykładzie zastosowano następujący dokument XML: [Przykładowy plik XML: Konfiguracja testu (LINQ to XML)](./sample-xml-file-test-configuration-linq-to-xml.md).  
  
```csharp  
XElement testCfg = XElement.Load("TestConfig.xml");  
  
// LINQ to XML query  
IEnumerable<XElement> list1 =  
    testCfg  
    .Elements("Test")  
    .Skip(1)  
    .Take(3);  
  
// LINQ to XML query  
IEnumerable<XElement> list2 =  
    testCfg  
    .Elements("Test")  
    .Where((el, idx) => idx >= 1 && idx <= 3);  
  
// XPath expression  
IEnumerable<XElement> list3 =  
  testCfg.XPathSelectElements("Test[position() >= 2 and position() <= 4]");  
  
if (list1.Count() == list2.Count() &&  
    list1.Count() == list3.Count() &&  
    list1.Intersect(list2).Count() == list1.Count() &&  
    list1.Intersect(list3).Count() == list1.Count())  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```output  
Results are identical  
<Test TestId="0002" TestType="CMD">  
  <Name>Find succeeding characters</Name>  
  <CommandLine>Examp2.EXE</CommandLine>  
  <Input>abc</Input>  
  <Output>def</Output>  
</Test>  
<Test TestId="0003" TestType="GUI">  
  <Name>Convert multiple numbers to strings</Name>  
  <CommandLine>Examp2.EXE /Verbose</CommandLine>  
  <Input>123</Input>  
  <Output>One Two Three</Output>  
</Test>  
<Test TestId="0004" TestType="GUI">  
  <Name>Find correlated key</Name>  
  <CommandLine>Examp3.EXE</CommandLine>  
  <Input>a1</Input>  
  <Output>b1</Output>  
</Test>  
```  
