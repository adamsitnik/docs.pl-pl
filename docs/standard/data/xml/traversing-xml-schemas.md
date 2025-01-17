---
title: Przechodzenie schematów XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: cce69574-5861-4a30-b730-2e18d915d8ee
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6040a7aa8f3244ea0ce2e66042537bc45c347b05
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037853"
---
# <a name="traversing-xml-schemas"></a>Przechodzenie schematów XML

Przechodzenie przez schemat XML za pomocą interfejsu API modelu obiektów schematu (SOM) zapewnia dostęp do elementów, atrybutów i typów przechowywanych w modelu SOM. Przechodzenie schematu XML załadowanego do modelu SOM jest również pierwszym krokiem w edycji schematu XML przy użyciu interfejsu API modelu SOM.

## <a name="traversing-an-xml-schema"></a>Przechodzenie schematu XML

Następujące właściwości <xref:System.Xml.Schema.XmlSchema> klasy zapewniają dostęp do kolekcji wszystkich elementów globalnych dodanych do schematu XML.

|Właściwość|Typ obiektu przechowywany w kolekcji lub tablicy|
|--------------|---------------------------------------------------|
|<xref:System.Xml.Schema.XmlSchema.Elements%2A>|<xref:System.Xml.Schema.XmlSchemaElement>|
|<xref:System.Xml.Schema.XmlSchema.Attributes%2A>|<xref:System.Xml.Schema.XmlSchemaAttribute>|
|<xref:System.Xml.Schema.XmlSchema.AttributeGroups%2A>|<xref:System.Xml.Schema.XmlSchemaAttributeGroup>|
|<xref:System.Xml.Schema.XmlSchema.Groups%2A>|<xref:System.Xml.Schema.XmlSchemaGroup>|
|<xref:System.Xml.Schema.XmlSchema.Includes%2A>|<xref:System.Xml.Schema.XmlSchemaExternal>, <xref:System.Xml.Schema.XmlSchemaInclude>, <xref:System.Xml.Schema.XmlSchemaImport>lub<xref:System.Xml.Schema.XmlSchemaRedefine>|
|<xref:System.Xml.Schema.XmlSchema.Items%2A>|<xref:System.Xml.Schema.XmlSchemaObject>(zapewnia dostęp do wszystkich elementów poziomu globalnego, atrybutów i typów).|
|<xref:System.Xml.Schema.XmlSchema.Notations%2A>|<xref:System.Xml.Schema.XmlSchemaNotation>|
|<xref:System.Xml.Schema.XmlSchema.SchemaTypes%2A>|<xref:System.Xml.Schema.XmlSchemaType>, <xref:System.Xml.Schema.XmlSchemaSimpleType>, <xref:System.Xml.Schema.XmlSchemaComplexType>|
|<xref:System.Xml.Schema.XmlSchema.UnhandledAttributes%2A>|<xref:System.Xml.XmlAttribute>(zapewnia dostęp do atrybutów, które nie należą do przestrzeni nazw schematu)|

> [!NOTE]
> Wszystkie właściwości wymienione w powyższej tabeli, z wyjątkiem <xref:System.Xml.Schema.XmlSchema.Items%2A> właściwości, są właściwościami po schemacie kompilacja-sprawdzonych (PSCI), które nie są dostępne, dopóki schemat nie zostanie skompilowany. <xref:System.Xml.Schema.XmlSchema.Items%2A> Właściwość jest właściwością prekompilowania schematu, której można użyć przed skompilowaniem schematu w celu uzyskania dostępu do wszystkich elementów poziomu globalnego, atrybutów i typów oraz edytowania ich.
>
> <xref:System.Xml.Schema.XmlSchema.UnhandledAttributes%2A> Właściwość zapewnia dostęp do wszystkich atrybutów, które nie należą do przestrzeni nazw schematu. Te atrybuty nie są przetwarzane przez procesor schematu.

Poniższy przykład kodu demonstruje przechodzenie przez schemat klienta utworzony w temacie [Tworzenie schematów XML](../../../../docs/standard/data/xml/building-xml-schemas.md) . Przykład kodu demonstruje przechodzenie schematu przy użyciu kolekcji opisanych powyżej i zapisuje wszystkie elementy i atrybuty w schemacie do konsoli programu.

Przykład przechodzi przez schemat klienta w poniższych krokach.

1. Dodaje schemat klienta do nowego <xref:System.Xml.Schema.XmlSchemaSet> obiektu, a następnie kompiluje go. Wszystkie ostrzeżenia i błędy walidacji schematu napotkane podczas odczytywania lub kompilowania schematu <xref:System.Xml.Schema.ValidationEventHandler> są obsługiwane przez delegata.

2. Pobiera skompilowany <xref:System.Xml.Schema.XmlSchema> obiekt <xref:System.Xml.Schema.XmlSchemaSet> z obiektu przez iterację <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> we właściwości. Ze względu na to, że schemat jest skompilowany, dostępne są właściwości po schemacie kompilacja-sprawdzonych (PSCI).

3. Wykonuje iterację na <xref:System.Xml.Schema.XmlSchemaElement> każdym <xref:System.Xml.Schema.XmlSchemaObjectTable.Values%2A> z kolekcji kolekcji <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> po schemacie, tworząc nazwę każdego elementu w konsoli.

4. Pobiera typ `Customer` złożony elementu <xref:System.Xml.Schema.XmlSchemaComplexType> przy użyciu klasy.

5. Jeśli typ złożony ma jakiekolwiek atrybuty, pobiera <xref:System.Collections.IDictionaryEnumerator> <xref:System.Xml.Schema.XmlSchemaAttribute> i zapisuje jego nazwę w konsoli programu.

6. Pobiera cząstkę sekwencji typu złożonego przy użyciu <xref:System.Xml.Schema.XmlSchemaSequence> klasy.

7. Iteruje każde <xref:System.Xml.Schema.XmlSchemaElement> <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A?displayProperty=nameWithType> w kolekcji, pisząc nazwę każdego elementu podrzędnego w konsoli.

Poniżej znajduje się kompletny przykład kodu.

[!code-cpp[XmlSchemaTraverseExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaTraverseExample/CPP/XmlSchemaTraverseExample.cpp#1)]
[!code-csharp[XmlSchemaTraverseExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaTraverseExample/CS/XmlSchemaTraverseExample.cs#1)]
[!code-vb[XmlSchemaTraverseExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaTraverseExample/VB/XmlSchemaTraverseExample.vb#1)]

Właściwość może być <xref:System.Xml.Schema.XmlSchemaSimpleType> lub<xref:System.Xml.Schema.XmlSchemaComplexType> jeśli jest typem prostym zdefiniowanym przez użytkownika lub typu złożonego. <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A?displayProperty=nameWithType> Może to być <xref:System.Xml.Schema.XmlSchemaDatatype> również, jeśli jest to jeden z wbudowanych typów danych zdefiniowanych w rekomendacji schematu W3C XML. W <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A> schemacie `Customer` klienta <xref:System.Xml.Schema.XmlSchemaComplexType> elementjest`LastName` , a elementy <xref:System.Xml.Schema.XmlSchemaSimpleType>i. `FirstName`

Przykład kodu w temacie [Building schematy XML](../../../../docs/standard/data/xml/building-xml-schemas.md) użył <xref:System.Xml.Schema.XmlSchemaComplexType.Attributes%2A?displayProperty=nameWithType> kolekcji, aby dodać atrybut `CustomerId` do `Customer` elementu. Jest to właściwość kompilacji poprzedzającej schemat. Odpowiednia właściwość po schemacie kompilacja-sprawdzonych jest <xref:System.Xml.Schema.XmlSchemaComplexType.AttributeUses%2A?displayProperty=nameWithType> kolekcją, która zawiera wszystkie atrybuty typu złożonego, łącznie z tymi, które są dziedziczone za pomocą typu pochodnego.

## <a name="see-also"></a>Zobacz także

- [Model SOM (XML Schema Object Model) ― omówienie](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)
- [Odczytywanie i zapisywanie schematów XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)
- [Tworzenie schematów XML](../../../../docs/standard/data/xml/building-xml-schemas.md)
- [Edytowanie schematów XML](../../../../docs/standard/data/xml/editing-xml-schemas.md)
- [Uwzględnianie lub importowanie schematów XML](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)
- [Klasa XmlSchemaSet na potrzeby kompilacji schematu](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)
- [Zestaw informacji po kompilacji schematu](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)
