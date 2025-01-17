---
title: Edytowanie schematów XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: fa09c8e5-c2b9-49d2-bb0d-40330cd13e4d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bd40677b3b21a4ee1b237656ea2814badbbcd593
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040768"
---
# <a name="editing-xml-schemas"></a>Edytowanie schematów XML

Edytowanie schematu XML jest jedną z najważniejszych funkcji modelu obiektów schematu (SOM). Wszystkie właściwości kompilacji przed schematem modelu SOM mogą służyć do zmiany istniejących wartości w schemacie XML. Schemat XML można następnie ponownie skompilować, aby odzwierciedlić zmiany.

Pierwszym krokiem podczas edytowania schematu załadowanego do modelu SOM jest przechodzenie przez schemat. Przed podjęciem próby edycji schematu należy zapoznać się z przechodzeniem schematu przy użyciu interfejsu API modelu SOM. Należy również zapoznać się z właściwościami prekompilowania i po schemacie kompilacji sprawdzonych (PSCI).

## <a name="editing-an-xml-schema"></a>Edytowanie schematu XML

W tej sekcji przedstawiono dwa przykłady kodu, z których każda edytuje schemat klienta utworzony w temacie [Tworzenie schematów XML](../../../../docs/standard/data/xml/building-xml-schemas.md) . Pierwszy przykład kodu dodaje `PhoneNumber` nowy element `Customer` do elementu, a drugi przykład kodu dodaje nowy `Title` atrybut do `FirstName` elementu. Pierwszy przykład używa również kolekcji po schemacie kompilacji <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> jako metody przechodzenia przez schemat klienta, podczas gdy drugi przykład kodu używa kolekcji przedprodukcyjnej kompilacji. <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType>

### <a name="phonenumber-element-example"></a>Przykład elementu nr telefonu

Ten pierwszy przykład kodu dodaje nowy `PhoneNumber` element `Customer` do elementu schematu klienta. Przykładowy kod edytuje schemat klienta w poniższych krokach.

1. Dodaje schemat klienta do nowego <xref:System.Xml.Schema.XmlSchemaSet> obiektu, a następnie kompiluje go. Wszystkie ostrzeżenia i błędy walidacji schematu napotkane podczas odczytywania lub kompilowania schematu <xref:System.Xml.Schema.ValidationEventHandler> są obsługiwane przez delegata.

2. Pobiera skompilowany <xref:System.Xml.Schema.XmlSchema> obiekt <xref:System.Xml.Schema.XmlSchemaSet> z obiektu przez iterację <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> we właściwości. Ze względu na to, że schemat jest skompilowany, dostępne są właściwości po schemacie kompilacja-sprawdzonych (PSCI).

3. `xs:string` <xref:System.Xml.Schema.XmlSchemaSimpleType> <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction> <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction.Facets%2A> Tworzy element przy użyciu klasy,ograniczenietypuprostegoprzyużyciuklasi,dodajezestawregułwzorcówdowłaściwościograniczeniaidodaje<xref:System.Xml.Schema.XmlSchemaElement> `PhoneNumber` ograniczenie do <xref:System.Xml.Schema.XmlSchemaSimpleType.Content%2A> właściwości typu prostego i typu prostego <xref:System.Xml.Schema.XmlSchemaElement.SchemaType%2A> do `PhoneNumber` elementu.

4. Wykonuje iterację na <xref:System.Xml.Schema.XmlSchemaElement> każdym <xref:System.Xml.Schema.XmlSchemaObjectTable.Values%2A> z kolekcji kolekcji po schemacie kompilacji <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> .

5. `"Customer"` `Customer` <xref:System.Xml.Schema.XmlSchemaComplexType> Jeśli element jest, pobiera typ złożony elementu przy użyciu <xref:System.Xml.Schema.XmlSchemaSequence> klasy i cząstki sekwencji typu złożonego przy użyciu klasy. <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A>

6. Dodaje nowy `PhoneNumber` element do sekwencji zawierającej istniejące `FirstName` elementy i `LastName` przy użyciu kolekcji przedprodukcyjnej kompilacja <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A> sekwencji.

7. Na koniec przetwarza <xref:System.Xml.Schema.XmlSchema> i kompiluje zmodyfikowany obiekt <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> przy użyciu metod <xref:System.Xml.Schema.XmlSchemaSet> i <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> klasy i zapisuje je w konsoli programu.

Poniżej znajduje się kompletny przykład kodu.

[!code-cpp[XmlSchemaEditExample1#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample1/CPP/XmlSchemaEditExample1.cpp#1)]
[!code-csharp[XmlSchemaEditExample1#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample1/CS/XmlSchemaEditExample1.cs#1)]
[!code-vb[XmlSchemaEditExample1#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample1/VB/XmlSchemaEditExample1.vb#1)]

Poniżej przedstawiono zmodyfikowany schemat klienta utworzony w temacie [Tworzenie schematów XML](../../../../docs/standard/data/xml/building-xml-schemas.md) .

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Customer">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="FirstName" type="xs:string" />
        <xs:element name="LastName" type="tns:LastNameType" />
        <xs:element name="PhoneNumber">           <xs:simpleType>             <xs:restriction base="xs:string">               <xs:pattern value="\d{3}-\d{3}-\d(4)" />             </xs:restriction>           </xs:simpleType>         </xs:element>
      </xs:sequence>
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /
>
    </xs:complexType>
  </xs:element>
  <xs:simpleType name="LastNameType">
    <xs:restriction base="xs:string">
      <xs:maxLength value="20" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

### <a name="title-attribute-example"></a>Przykład atrybutu tytułu

Ten drugi przykład kodu dodaje nowy `Title` atrybut `FirstName` do elementu schematu klienta. W pierwszym przykładzie kodu, typ `FirstName` elementu to. `xs:string` `FirstName` Aby element miał atrybut wraz z zawartością ciągu, jego typ musi być zmieniony na typ złożony z prostym modelem zawartości o rozszerzeniu zawartości.

Przykładowy kod edytuje schemat klienta w poniższych krokach.

1. Dodaje schemat klienta do nowego <xref:System.Xml.Schema.XmlSchemaSet> obiektu, a następnie kompiluje go. Wszystkie ostrzeżenia i błędy walidacji schematu napotkane podczas odczytywania lub kompilowania schematu <xref:System.Xml.Schema.ValidationEventHandler> są obsługiwane przez delegata.

2. Pobiera skompilowany <xref:System.Xml.Schema.XmlSchema> obiekt <xref:System.Xml.Schema.XmlSchemaSet> z obiektu przez iterację <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> we właściwości. Ze względu na to, że schemat jest skompilowany, dostępne są właściwości po schemacie kompilacja-sprawdzonych (PSCI).

3. Tworzy nowy typ złożony dla `FirstName` elementu <xref:System.Xml.Schema.XmlSchemaComplexType> przy użyciu klasy.

4. Tworzy nowe proste rozszerzenie zawartości z typem `xs:string`podstawowym, <xref:System.Xml.Schema.XmlSchemaSimpleContent> korzystając z klas i <xref:System.Xml.Schema.XmlSchemaSimpleContentExtension> .

5. Tworzy nowy `Title` atrybut <xref:System.Xml.Schema.XmlSchemaAttribute> przy <xref:System.Xml.Schema.XmlSchemaAttribute.SchemaTypeName%2A> użyciu`xs:string` klasy, z i dodaje atrybut do prostego rozszerzenia zawartości.

6. Ustawia model zawartości prostej zawartości na proste rozszerzenie zawartości oraz model zawartości typu złożonego na zawartość prostą.

7. Dodaje nowy typ złożony do kolekcji pre-Schema-compilation <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> .

8. Wykonuje iterację dla <xref:System.Xml.Schema.XmlSchemaObject> każdego w kolekcji przedprodukcyjnej kompilacji <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> .

> [!NOTE]
> Ponieważ element nie jest elementem globalnym w schemacie, nie jest dostępny <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> w kolekcjach ani <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType>. `FirstName` Przykładowy kod lokalizuje `FirstName` element przez pierwsze lokalizowanie `Customer` elementu.
>
> Pierwszy przykładowy kod przechodzą przez schemat przy użyciu kolekcji po schemacie kompilacji <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> . W tym przykładzie kolekcja pre-Schema-compilation <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> jest używana do przechodzenia przez schemat. Chociaż obie kolekcje zapewniają dostęp do elementów globalnych w schemacie, Iterowanie przez <xref:System.Xml.Schema.XmlSchema.Items%2A> kolekcję jest bardziej czasochłonne, ponieważ należy wykonać iterację wszystkich elementów globalnych w schemacie i nie ma żadnych właściwości PSCI. Kolekcje PSCI (<xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType>, <xref:System.Xml.Schema.XmlSchema.Attributes%2A?displayProperty=nameWithType>, <xref:System.Xml.Schema.XmlSchema.SchemaTypes%2A?displayProperty=nameWithType>, itd.) zapewniają bezpośredni dostęp do swoich elementów globalnych, atrybutów i typów oraz ich właściwości PSCI.

1. `"Customer"` <xref:System.Xml.Schema.XmlSchemaSequence> <xref:System.Xml.Schema.XmlSchemaComplexType> Jeśli jest elementem, którego <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> jest, pobiera typ `Customer` złożony elementu przy użyciu klasy i cząstki sekwencji typu złożonego przy użyciu klasy. <xref:System.Xml.Schema.XmlSchemaObject>

2. Wykonuje iterację dla <xref:System.Xml.Schema.XmlSchemaParticle> każdego w kolekcji przedprodukcyjnej kompilacji <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A?displayProperty=nameWithType> .

3. <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> `"FirstName"` <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> Jeśli jest elementem, to jest, `FirstName` ustawia `FirstName` element na nowy typ złożony. <xref:System.Xml.Schema.XmlSchemaParticle>

4. Na koniec przetwarza <xref:System.Xml.Schema.XmlSchema> i kompiluje zmodyfikowany obiekt <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> przy użyciu metod <xref:System.Xml.Schema.XmlSchemaSet> i <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> klasy i zapisuje je w konsoli programu.

Poniżej znajduje się kompletny przykład kodu.

[!code-cpp[XmlSchemaEditExample2#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample2/CPP/XmlSchemaEditExample2.cpp#1)]
[!code-csharp[XmlSchemaEditExample2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample2/CS/XmlSchemaEditExample2.cs#1)]
[!code-vb[XmlSchemaEditExample2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample2/VB/XmlSchemaEditExample2.vb#1)]

Poniżej przedstawiono zmodyfikowany schemat klienta utworzony w temacie [Tworzenie schematów XML](../../../../docs/standard/data/xml/building-xml-schemas.md) .

```xml
<?xml version="1.0" encoding=" utf-8"?>
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Customer">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="FirstName" type="tns:FirstNameComplexType" />
        <xs:element name="LastName" type="tns:LastNameType" />
      </xs:sequence>
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /
>
    </xs:complexType>
  </xs:element>
  <xs:simpleType name="LastNameType">
    <xs:restriction base="xs:string">
      <xs:maxLength value="20" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="FirstNameComplexType">     <xs:simpleContent>       <xs:extension base="xs:string">         <xs:attribute name="Title" type="xs:string" />       </xs:extension>     </xs:simpleContent>   </xs:complexType>
</xs:schema>
```

## <a name="see-also"></a>Zobacz także

- [Model SOM (XML Schema Object Model) ― omówienie](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)
- [Odczytywanie i zapisywanie schematów XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)
- [Tworzenie schematów XML](../../../../docs/standard/data/xml/building-xml-schemas.md)
- [Przechodzenie schematów XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)
- [Uwzględnianie lub importowanie schematów XML](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)
- [Klasa XmlSchemaSet na potrzeby kompilacji schematu](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)
- [Zestaw informacji po kompilacji schematu](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)
