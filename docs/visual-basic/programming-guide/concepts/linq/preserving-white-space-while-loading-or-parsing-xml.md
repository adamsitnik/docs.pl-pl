---
title: Zachowywanie białych znaków podczas ładowania lub analizowania XML2
ms.date: 07/20/2015
ms.assetid: ef6518e0-2c8d-462c-8b92-a16e9dc737ad
ms.openlocfilehash: 7febbf1ea27d3e73df8b91869befcd0b29a07c6e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64666139"
---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>Zachowywanie białych znaków podczas ładowania lub analizowania kodu XML
W tym temacie opisano sposób kontrolowania zachowania biały znak [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].  
  
 Typowym scenariuszem jest Odczytaj dane XML z wcięciami, utworzyć drzewa XML w pamięci bez wszystkie węzły tekstowe białe miejsca (to znaczy nie zachowania biały), wykonywanie operacji na pliku XML, a następnie zapisz plik XML, z wcięciem. Po użytkownik serializacji XML za pomocą formatowania, tylko istotne biały znak w drzewie XML są zachowywane. Jest to domyślne zachowanie dla [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].  
  
 Inny typowy scenariusz polega na odczytywanie i modyfikację XML, który już został celowo z wcięciami. Nie można zmienić to wcięcie w dowolny sposób. Aby to zrobić w [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], gdy obciążenia lub nemohla analyzovat kód XML i Wyłącz formatowanie podczas serializacji XML jest zachowany biały znak.  
  
 W tym temacie opisano metody służące do wypełniania drzew XML zachowania biały znak. Aby dowiedzieć się, jak kontrolowanie biały znak podczas serializowania drzew XML, zobacz [zachowania biały znak podczas serializowania](../../../../visual-basic/programming-guide/concepts/linq/preserving-white-space-while-serializing.md).  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>Zachowanie metody służące do wypełniania drzew XML  
 Następujące metody w klasie <xref:System.Xml.Linq.XElement> i <xref:System.Xml.Linq.XDocument> klasy wypełnianie drzewa XML. Możesz wypełnić drzewa XML z pliku, <xref:System.IO.TextReader>, <xref:System.Xml.XmlReader>, lub ciągiem:  
  
- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>  
  
 Jeśli metoda nie przyjmuje <xref:System.Xml.Linq.LoadOptions> jako argument, metoda nie zachowa nieważny biały znak.  
  
 W większości przypadków, gdy ta metoda przyjmuje <xref:System.Xml.Linq.LoadOptions> jako argument, można opcjonalnie zachować nieważny biały znak jako węzły tekstowe w drzewie XML. Jednakże jeśli metoda Trwa ładowanie XML z <xref:System.Xml.XmlReader>, a następnie <xref:System.Xml.XmlReader> Określa, czy biały znak zostanie zachowany, czy nie. Ustawienie <xref:System.Xml.Linq.LoadOptions.PreserveWhitespace> odniesie żadnego skutku.  
  
 Za pomocą tych metod, jeśli biały znak są zachowywane, nieważny biały znak jest wstawiany do drzewa XML jako <xref:System.Xml.Linq.XText> węzłów. Jeśli biały znak nie są zachowywane, nie są wstawiane węzły tekstowe.  
  
 Można utworzyć drzewa XML przy użyciu <xref:System.Xml.XmlWriter>. Węzły, które są zapisywane w <xref:System.Xml.XmlWriter> są wypełnione w drzewie. Jednak w przypadku tworzenia drzewa XML przy użyciu tej metody, wszystkie węzły są zachowanych, niezależnie od tego, czy węzeł jest biały znak, czy nie, oraz czy biały istotne lub nie.  
  
## <a name="see-also"></a>Zobacz także

- [Analizowanie kodu XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
