---
title: Atrybuty kontrolujące zakodowaną serializację SOAP
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: 2961d9abc6c32e78b5a61e8f2bbea5cfcf6677bd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61794943"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a>Atrybuty kontrolujące zakodowaną serializację SOAP

Dokument World Wide Web Consortium (W3C) o nazwie [proste obiektu dostępu protokołu (protokołu SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/) zawiera sekcję opcjonalną (sekcja 5), w tym artykule opisano, jak można zakodować parametry protokołu SOAP. Aby jest zgodny z sekcji 5 specyfikacji, należy użyć specjalnego zestawu atrybutów w <xref:System.Xml.Serialization> przestrzeni nazw. Zastosuj te atrybuty właściwe dla klas i składowych klas, a następnie użyj <xref:System.Xml.Serialization.XmlSerializer> do serializacji wystąpień klasy lub klas.

W poniższej tabeli przedstawiono atrybuty, których może być stosowana, i co robią. Aby uzyskać więcej informacji o korzystaniu z tych atrybutów do kontroli serializacji XML, zobacz [jak: Serializacja obiektu jako Stream XML kodowany w formacie protokołu SOAP](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md) i [jak: Zastąpienie serializacji XML protokołu SOAP zakodowane](how-to-override-encoded-soap-xml-serialization.md).

Aby uzyskać więcej informacji na temat atrybutów, zobacz [atrybuty](../../../docs/standard/attributes/index.md).

|Atrybut|Informacje zawarte w tym artykule dotyczą|Określa|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|Pole publiczne, właściwość, parametru lub wartości zwracanej.|Składowa klasy będzie serializowana jako atrybut XML.|
|<xref:System.Xml.Serialization.SoapElementAttribute>|Pole publiczne, właściwość, parametru lub wartości zwracanej.|Klasa będzie serializowana jako XML element.|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|Pole publicznej jest identyfikatorem wyliczenia.|Nazwa elementu element członkowski wyliczenia.|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|Właściwości publiczne i pola.|Właściwości lub pól mają być ignorowane, gdy klasa zawierająca jest serializowana.|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|Klasa pochodna publicznego deklaracje i metod publicznych w dokumentach sieci Web Services Description Language (WSDL).|Typ mają zostać uwzględnione podczas generowania schematów (do rozpoznany po serializacji).|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|Klasa publiczna deklaracji.|Klasa powinien zostać Zserializowany jako typ XML.|

## <a name="see-also"></a>Zobacz także

- [Serializacja XML i SOAP](xml-and-soap-serialization.md)
- [Instrukcje: Serializacja obiektu jako Stream XML kodowany w formacie protokołu SOAP](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [Instrukcje: Zastąp zakodowanego protokołu SOAP serializacji XML](how-to-override-encoded-soap-xml-serialization.md)
- [Atrybuty](../../../docs/standard/attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [Instrukcje: Serializacja obiektu](how-to-serialize-an-object.md)
- [Instrukcje: Deserializacji obiektu](how-to-deserialize-an-object.md)
