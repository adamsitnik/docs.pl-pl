---
title: 'Instrukcje: Przekształć transmisję strumieniową dużychC#dokumentów XML ()'
ms.date: 07/20/2015
ms.assetid: 5f16d1f8-5370-4b55-b0c8-e497df163037
ms.openlocfilehash: 3ddafc0e053a5dc18d024588e9f71081c8d6da14
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593184"
---
# <a name="how-to-perform-streaming-transform-of-large-xml-documents-c"></a>Instrukcje: Przekształć transmisję strumieniową dużychC#dokumentów XML ()
Czasami konieczne jest przekształcenie dużych plików XML i zapisanie aplikacji w celu przewidzenia rozmiaru pamięci aplikacji. Jeśli spróbujesz wypełnić drzewo XML bardzo dużym plikiem XML, użycie pamięci będzie proporcjonalne do rozmiaru pliku (to jest zbyt duże). W związku z tym należy zamiast tego użyć techniki przesyłania strumieniowego.  
  
 Techniki przesyłania strumieniowego najlepiej zastosować w sytuacjach, gdy trzeba przetwarzać dokument źródłowy tylko raz i można przetwarzać elementy w kolejności dokumentu. Niektóre standardowe operatory zapytań, takie jak <xref:System.Linq.Enumerable.OrderBy%2A>, iteruje źródło, zbierają wszystkie dane, sortują je, a następnie zwracają pierwszy element w sekwencji. Należy pamiętać, że jeśli używasz operatora zapytania, który materializuje jego źródło przed uzyskaniem pierwszego elementu, nie będzie zachowana mała ilość pamięci dla aplikacji.  
  
 Nawet jeśli używasz techniki opisanej w [temacie How to: Strumieniowe fragmenty XML z dostępem do informacji nagłówkaC#(](./how-to-stream-xml-fragments-with-access-to-header-information.md)), jeśli próbujesz utworzyć drzewo XML zawierające przekształcony dokument, użycie pamięci będzie zbyt duże.  
  
 Istnieją dwa główne podejścia. Jednym z metod jest użycie odroczonych charakterystyk <xref:System.Xml.Linq.XStreamingElement>przetwarzania. Innym rozwiązaniem jest utworzenie <xref:System.Xml.XmlWriter>i użycie [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] funkcji <xref:System.Xml.XmlWriter>do zapisu elementów do. W tym temacie przedstawiono oba podejścia.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kompiluje się w przykładzie w [instrukcje: Strumieniowe fragmenty XML z dostępem do informacji nagłówkaC#(](./how-to-stream-xml-fragments-with-access-to-header-information.md)).  
  
 W tym przykładzie zastosowano opóźnione funkcje <xref:System.Xml.Linq.XStreamingElement> wykonywania w celu przesyłania strumieniowego danych wyjściowych. W tym przykładzie można przekształcić bardzo duży dokument przy zachowaniu małej ilości pamięci.  
  
 Należy zauważyć, że niestandardowa oś`StreamCustomerItem`() została zaprojektowana w taki sposób, aby oczekuje dokumentu `Customer` `Name`, `Item` , i elementów, i że te elementy będą ułożone jak w poniższym dokumencie source. XML. Jednak bardziej niezawodna implementacja zostanie przygotowana do analizy nieprawidłowego dokumentu.  
  
 Poniżej znajduje się dokument źródłowy source. XML:  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>   
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null)  
                        {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    XStreamingElement root = new XStreamingElement("Root",  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        )  
    );  
    root.Save("Test.xml");  
    Console.WriteLine(File.ReadAllText("Test.xml"));  
}  
```  
  
 Ten kod generuje następujące dane wyjściowe:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kompiluje się również na przykład w [temacie How to: Strumieniowe fragmenty XML z dostępem do informacji nagłówkaC#(](./how-to-stream-xml-fragments-with-access-to-header-information.md)).  
  
 Ten przykład używa funkcji [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] , aby pisać elementy <xref:System.Xml.XmlWriter>do. W tym przykładzie można przekształcić bardzo duży dokument przy zachowaniu małej ilości pamięci.  
  
 Należy zauważyć, że niestandardowa oś`StreamCustomerItem`() została zaprojektowana w taki sposób, aby oczekuje dokumentu `Customer` `Name`, `Item` , i elementów, i że te elementy będą ułożone jak w poniższym dokumencie source. XML. Bardziej niezawodna implementacja może jednak spowodować sprawdzenie poprawności dokumentu źródłowego przy użyciu XSD lub przygotowania do przeanalizowania nieprawidłowego dokumentu.  
  
 Ten przykład używa tego samego dokumentu źródłowego, source. XML, jak w poprzednim przykładzie w tym temacie. Generuje również dokładnie te same dane wyjściowe.  
  
 Użycie <xref:System.Xml.Linq.XStreamingElement> do przesyłania strumieniowego wyjściowego pliku XML jest preferowany przez <xref:System.Xml.XmlWriter>zapis do.  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null) {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    IEnumerable<XElement> srcTree =  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        );  
    XmlWriterSettings xws = new XmlWriterSettings();  
    xws.OmitXmlDeclaration = true;  
    xws.Indent = true;  
    using (XmlWriter xw = XmlWriter.Create("Output.xml", xws)) {  
        xw.WriteStartElement("Root");  
        foreach (XElement el in srcTree)  
            el.WriteTo(xw);  
        xw.WriteEndElement();  
    }  
  
    string str = File.ReadAllText("Output.xml");  
    Console.WriteLine(str);  
}  
```  
  
 Ten kod generuje następujące dane wyjściowe:  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  