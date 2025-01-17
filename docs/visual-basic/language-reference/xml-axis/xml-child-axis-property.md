---
title: Właściwości osi elementu podrzędnego XML (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyChildAxis
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 89a59d00-985e-4f5c-b59f-29b47bad11cb
ms.openlocfilehash: 88d0b1f315bc1bb9dc474604d222a8ebcc1e40aa
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582238"
---
# <a name="xml-child-axis-property-visual-basic"></a>Właściwości osi elementu podrzędnego XML (Visual Basic)
Zapewnia dostęp do elementów podrzędnych jednego z następujących: obiektu <xref:System.Xml.Linq.XElement>, obiektu <xref:System.Xml.Linq.XDocument>, kolekcji obiektów <xref:System.Xml.Linq.XElement> lub kolekcji obiektów <xref:System.Xml.Linq.XDocument>.  
  
## <a name="syntax"></a>Składnia  
  
```vb  
object.<child>  
```  
  
## <a name="parts"></a>Części  
  
|Termin|Definicja|  
|---|---|  
|`object`|Wymagany. Obiekt <xref:System.Xml.Linq.XElement>, obiekt <xref:System.Xml.Linq.XDocument>, kolekcja obiektów <xref:System.Xml.Linq.XElement> lub kolekcja obiektów <xref:System.Xml.Linq.XDocument>.|  
|. <|Wymagany. Wskazuje początek właściwości osi podrzędnej.|  
|`child`|Wymagany. Nazwa węzłów podrzędnych do uzyskania dostępu do formularza [`prefix:]name`.<br /><br /> -    `Prefix` — opcjonalne. Prefiks przestrzeni nazw XML dla węzła podrzędnego. Musi to być globalna przestrzeń nazw XML zdefiniowana za pomocą instrukcji `Imports`.<br />-    `Name` — wymagane. Nazwa lokalnego węzła podrzędnego. Zobacz [nazwy zadeklarowanych elementów i atrybutów XML](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|  
|>|Wymagany. Oznacza koniec właściwości osi podrzędnej.|  
  
## <a name="return-value"></a>Wartość zwracana  
 Kolekcja obiektów <xref:System.Xml.Linq.XElement>.  
  
## <a name="remarks"></a>Uwagi  
 Można użyć właściwości osi elementu podrzędnego XML, aby uzyskać dostęp do węzłów podrzędnych według nazwy z obiektu <xref:System.Xml.Linq.XElement> lub <xref:System.Xml.Linq.XDocument> lub z kolekcji obiektów <xref:System.Xml.Linq.XElement> lub <xref:System.Xml.Linq.XDocument>. Użyj właściwości `Value` XML, aby uzyskać dostęp do wartości pierwszego węzła podrzędnego w zwróconej kolekcji. Aby uzyskać więcej informacji, zobacz [Właściwość wartości XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
 Kompilator Visual Basic konwertuje właściwości osi podrzędnej na wywołania metody <xref:System.Xml.Linq.XContainer.Elements%2A>.  
  
## <a name="xml-namespaces"></a>Przestrzenie nazw XML  
 Nazwa we właściwości osi podrzędnej może używać tylko prefiksów przestrzeni nazw XML zadeklarowanych globalnie z instrukcją `Imports`. Nie może używać prefiksów przestrzeni nazw XML zadeklarowanych lokalnie w literałach elementu XML. Aby uzyskać więcej informacji, zobacz [Imports — Instrukcja (przestrzeń nazw XML)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje, jak uzyskać dostęp do węzłów podrzędnych o nazwie `phone` z obiektu `contact`.  
  
 [!code-vb[VbXMLSamples#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#17)]  
  
 Ten kod wyświetla następujący tekst:  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje, jak uzyskać dostęp do węzłów podrzędnych o nazwie `phone` z kolekcji zwróconej przez właściwość oś podrzędną `contact` obiektu `contacts`.  
  
 [!code-vb[VbXMLSamples#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#18)]  
  
 Ten kod wyświetla następujący tekst:  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>Przykład  
 Poniższy przykład deklaruje `ns` jako prefiks przestrzeni nazw XML. Następnie używa prefiksu przestrzeni nazw, aby utworzyć literał XML i uzyskać dostęp do pierwszego węzła podrzędnego przy użyciu kwalifikowanej nazwy `ns:name`.  
  
 [!code-vb[VbXMLSamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples8.vb#19)]  
  
 Ten kod wyświetla następujący tekst:  
  
 `Patrick Hines`  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.Linq.XElement>
- [Właściwości osi XML](../../../visual-basic/language-reference/xml-axis/index.md)
- [Literały XML](../../../visual-basic/language-reference/xml-literals/index.md)
- [Tworzenie kodu XML w Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Nazwy deklarowanych elementów i atrybutów XML](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
