---
title: Zasady wnioskowania typów węzłów schematu i struktury
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: d74ce896-717d-4871-8fd9-b070e2f53cb0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6c68cd98b496143e6b964383f8fa0c3af5d2c87d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939641"
---
# <a name="rules-for-inferring-schema-node-types-and-structure"></a>Zasady wnioskowania typów węzłów schematu i struktury
W tym temacie opisano sposób, w jaki proces wnioskowania schematu tłumaczy typy węzłów w dokumencie XML na strukturę języka definicji schematu XML (XSD).  
  
## <a name="element-inference-rules"></a>Reguły wnioskowania elementów  
 W tej sekcji opisano reguły wnioskowania dotyczące deklaracji elementów. Istnieją osiem struktur deklaracji elementów, które zostaną wywnioskowane:  
  
1. Element typu prostego  
  
2. Pusty element  
  
3. Pusty element z atrybutami  
  
4. Element z atrybutami i prostą zawartością  
  
5. Element z sekwencją elementów podrzędnych  
  
6. Element z sekwencją elementów podrzędnych i atrybutów  
  
7. Element z sekwencją opcji elementów podrzędnych  
  
8. Element z sekwencją opcji elementów podrzędnych i atrybutów  
  
> [!NOTE]
> Wszystkie `complexType` deklaracje są wywnioskowane jako typy anonimowe. Jedynym wywnioskowanym elementem globalnym jest element główny; wszystkie inne elementy są lokalne.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
### <a name="simple-typed-element"></a>Prosty typ elementu  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Pogrubiony element pokazuje schemat wywnioskowany dla elementu typu prostego.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>text</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="root" type="xs:string" />`<br /><br /> `</xs:schema>`|  
  
### <a name="empty-element"></a>Pusty element  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Pogrubiony element pokazuje schemat wywnioskowany dla pustego elementu.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<empty/>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="empty" />`<br /><br /> `</xs:schema>`|  
  
### <a name="empty-element-with-attributes"></a>Pusty element z atrybutami  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Elementy pogrubione pokazują schemat wywnioskowany dla pustego elementu z atrybutami.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<empty attribute1="text"/>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="empty">`<br /><br /> `<xs:complexType>`<br /><br /> `<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `</xs:complexType>`<br /><br /> `</xs:element>`<br /><br /> `</xs:schema>`|  
  
### <a name="element-with-attributes-and-simple-content"></a>Element z atrybutami i prostą zawartością  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Elementy pogrubione pokazują schemat wywnioskowany dla elementu z atrybutami i prostą zawartością.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">value</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="root">`<br /><br /> `<xs:complexType>`<br /><br /> `<xs:simpleContent>`<br /><br /> `<xs:extension base="xs:string">`<br /><br /> `<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `</xs:extension>`<br /><br /> `</xs:simpleContent>`<br /><br /> `</xs:complexType>`<br /><br /> `</xs:element>`<br /><br /> `</xs:schema>`|  
  
### <a name="element-with-a-sequence-of-child-elements"></a>Element z sekwencją elementów podrzędnych  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Elementy pogrubione pokazują schemat wywnioskowany dla elementu z sekwencją elementów podrzędnych.  
  
> [!NOTE]
> Nawet jeśli element ma tylko jeden element podrzędny, jest nadal traktowany jako sekwencja.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>`<br /><br /> `<subElement/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="root">`<br /><br /> `<xs:complexType>`<br /><br /> `<xs:sequence>`<br /><br /> `<xs:element name="subElement" />`<br /><br /> `</xs:sequence>`<br /><br /> `</xs:complexType>`<br /><br /> `</xs:element>`<br /><br /> `</xs:schema>`|  
  
### <a name="element-with-a-sequence-of-child-elements-and-attributes"></a>Element z sekwencją elementów podrzędnych i atrybutów  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Elementy pogrubione pokazują schemat wywnioskowany dla elementu z sekwencją elementów podrzędnych i atrybutów.  
  
> [!NOTE]
> Nawet jeśli element ma tylko jeden element podrzędny, jest nadal traktowany jako sekwencja.  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="root">`<br /><br /> `<xs:complexType>`<br /><br /> `<xs:sequence>`<br /><br /> `<xs:element name="subElement1" />`<br /><br /> `<xs:element name="subElement2" />`<br /><br /> `</xs:sequence>`<br /><br /> `<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `</xs:complexType>`<br /><br /> `</xs:element>`<br /><br /> `</xs:schema>`|  
  
### <a name="element-with-a-sequence-and-choices-of-child-elements"></a>Element z sekwencją i wyborami elementów podrzędnych  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Elementy pogrubione pokazują schemat wywnioskowany dla elementu z sekwencją i wyborem elementów podrzędnych.  
  
> [!NOTE]
> Atrybut elementu jest ustawiony na `"unbounded"` w wywnioskowanym schemacie. `xs:choice` `maxOccurs`  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `<subElement1/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="root">`<br /><br /> `<xs:complexType>`<br /><br /> `<xs:sequence>`<br /><br /> `<xs:choice maxOccurs="unbounded">`<br /><br /> `<xs:element name="subElement1" />`<br /><br /> `<xs:element name="subElement2" />`<br /><br /> `</xs:choice>`<br /><br /> `</xs:sequence>`<br /><br /> `</xs:complexType>`<br /><br /> `</xs:element>`<br /><br /> `</xs:schema>`|  
  
### <a name="element-with-a-sequence-and-choice-of-child-elements-and-attributes"></a>Element z sekwencją i wyborem elementów podrzędnych i atrybutów  
 W poniższej tabeli przedstawiono dane wejściowe XML do <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> metody i Wygenerowano schemat XML. Elementy pogrubione pokazują schemat wywnioskowany dla elementu z sekwencją i wyborem elementów podrzędnych i atrybutów.  
  
> [!NOTE]
> Atrybut elementu jest ustawiony na `"unbounded"` w wywnioskowanym schemacie. `xs:choice` `maxOccurs`  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schemat|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `<subElement1/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> `<xs:element name="root">`<br /><br /> `<xs:complexType>`<br /><br /> `<xs:sequence>`<br /><br /> `<xs:choice maxOccurs="unbounded">`<br /><br /> `<xs:element name="subElement1" />`<br /><br /> `<xs:element name="subElement2" />`<br /><br /> `</xs:choice>`<br /><br /> `</xs:sequence>`<br /><br /> `<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `</xs:complexType>`<br /><br /> `</xs:element>`<br /><br /> `</xs:schema>`|  
  
### <a name="attribute-processing"></a>Przetwarzanie atrybutów  
 Za każdym razem, gdy w węźle zostanie napotkany nowy atrybut, jest on dodawany do wywnioskowanej definicji węzła przy `use="required"`użyciu. Przy następnym znalezieniu tego samego węzła w wystąpieniu proces wnioskowania będzie porównywał atrybuty bieżącego wystąpienia z tymi, które zostały już wywnioskowane. Jeśli w wystąpieniu brakuje niektórych z już wywnioskowanych elementów, `use="optional"` jest ono dodawane do definicji atrybutu. Nowe atrybuty są dodawane do istniejących deklaracji z `use="optional"`.  
  
### <a name="occurrence-constraints"></a>Ograniczenia wystąpień  
 Podczas procesu `minOccurs` wnioskowania o schemacie są generowane `maxOccurs` atrybuty i dla wywnioskowanych składników schematu, z wartościami `"0"` lub `"1"` i `"1"` lub `"unbounded"`. `"1"` Wartości i `"0"` `minOccurs="1"` `MinOccurs="0"` są używane tylko wtedy, gdy wartości i `"1"` nie mogą sprawdzić poprawności dokumentu XML (na przykład jeśli nie opisują dokładnie elementu, jest używany). `"unbounded"`  
  
### <a name="mixed-content"></a>Zawartość mieszana  
 Jeśli element zawiera zawartość mieszaną (na przykład tekst przeplatany z elementami), `mixed="true"` atrybut jest generowany dla niedozwolonej definicji typu złożonego.  
  
## <a name="other-node-type-inference-rules"></a>Inne reguły wnioskowania typu węzła  
 W poniższej tabeli opisano reguły wnioskowania dotyczące przetwarzania instrukcji, komentarza, odwołania do jednostki, CDATA, typu dokumentu i węzłów przestrzeni nazw.  
  
|Typ węzła|{1&gt;Translacja&lt;1}|  
|---------------|-----------------|  
|Przetwarzanie instrukcji|Ignorowane.|  
|Komentarz|Ignorowane.|  
|Odwołanie do jednostki|<xref:System.Xml.Schema.XmlSchemaInference> Klasa nie obsługuje odwołań do jednostek. Jeśli dokument XML zawiera odwołania do jednostek, należy użyć czytnika rozszerzającego jednostki. Na przykład można przekazać obiekt <xref:System.Xml.XmlTextReader> <xref:System.Xml.XmlTextReader.EntityHandling%2A> z właściwością ustawioną <xref:System.Xml.EntityHandling.ExpandEntities> jako parametr. Jeśli są napotkane odwołania do jednostek, a czytnik nie rozszerza jednostek, zgłaszany jest wyjątek.|  
|CDATA|Wszystkie `<![CDATA[ … ]]` sekcje dokumentu XML zostaną wywnioskowane jako `xs:string`.|  
|Typ dokumentu|Ignorowane.|  
|Namespaces|Ignorowane.|  
  
 Aby uzyskać więcej informacji na temat procesu wnioskowania schematu, zobacz [wnioskowanie schematów z dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.Schema.XmlSchemaInference>
- [Model SOM (XML Schema Object Model)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)
- [Wnioskowanie schematu XML](../../../../docs/standard/data/xml/inferring-an-xml-schema.md)
- [Wnioskowanie schematów na podstawie dokumentów XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)
- [Zasady wnioskowania typów prostych](../../../../docs/standard/data/xml/rules-for-inferring-simple-types.md)
