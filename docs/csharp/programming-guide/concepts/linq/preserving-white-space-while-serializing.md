---
title: Zachowywanie białych znaków podczas Serializing3
ms.date: 07/20/2015
ms.assetid: 0c4f8b98-483b-4cf8-86be-fa146eef90dc
ms.openlocfilehash: 6d357d40c13a66a152b3c8bb5f61e3a3374c4055
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2019
ms.locfileid: "66484076"
---
# <a name="preserving-white-space-while-serializing"></a>Zachowywanie białych znaków podczas serializowania
W tym temacie opisano sposób kontrolowania biały znak podczas serializowania drzewa XML.  
  
 Typowym scenariuszem jest Odczytaj dane XML z wcięciami, utworzyć drzewa XML w pamięci bez wszystkie węzły tekstowe białe miejsca (to znaczy nie zachowania biały), wykonywanie operacji na pliku XML, a następnie zapisz plik XML, z wcięciem. Po użytkownik serializacji XML za pomocą formatowania, tylko istotne biały znak w drzewie XML są zachowywane. Jest to domyślne zachowanie dla [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].  
  
 Inny typowy scenariusz polega na odczytywanie i modyfikację XML, który już został celowo z wcięciami. Nie można zmienić to wcięcie w dowolny sposób. Aby to zrobić w [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], gdy obciążenia lub nemohla analyzovat kód XML i Wyłącz formatowanie podczas serializacji XML jest zachowany biały znak.  
  
## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a>Biały metod, które serializowanie drzew XML  
 Następujące metody w klasie <xref:System.Xml.Linq.XElement> i <xref:System.Xml.Linq.XDocument> klasy serializacji drzewa XML. Może wykonywać serializację drzewa XML w pliku <xref:System.IO.TextReader>, lub <xref:System.Xml.XmlReader>. `ToString` Metoda serializuje do ciągu.  
  
- <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType>  
  
- [XElement.ToString()](xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType)
  
- [XDocument.ToString()](xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=nameWithType)
  
 Jeśli metoda nie przyjmuje <xref:System.Xml.Linq.SaveOptions> jako argument, a następnie metoda sformatuje (wcięcie) serializacji XML. W takim przypadku wszystkie nieważny biały znak w drzewie XML jest odrzucany.  
  
 Jeśli metoda <xref:System.Xml.Linq.SaveOptions> jako argument, a następnie można określić metody nie formatu (wcięcie) serializacji XML. W takim przypadku wszystkie biały znak w drzewie XML są zachowywane.  
