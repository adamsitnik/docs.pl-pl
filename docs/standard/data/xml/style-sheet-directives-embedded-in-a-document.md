---
title: Dyrektywy dotyczące arkusza stylów osadzone w dokumencie
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: d79fb295-ebc7-438d-ba1b-05be7d534834
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 65987c5e29d593758b21259d6367202c882df2de
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026942"
---
# <a name="style-sheet-directives-embedded-in-a-document"></a>Dyrektywy dotyczące arkusza stylów osadzone w dokumencie

Od czasu do czasu istniejących XML zawiera dyrektywy arkusz stylów z `<?xml:stylesheet?>`. Program Microsoft Internet Explorer akceptuje to jako alternatywa `<?xml-stylesheet?>` składni. Gdy dane XML zawierają `<?xml:stylesheet?>` dyrektywy, jak pokazano w poniższym danych próby załadowania tych danych do XML Document Object Model (DOM) zgłasza wyjątek.

```xml
<?xml version="1.0" ?>
<?xml:stylesheet type="text/xsl" href="test2.xsl"?>
<root>
    <test>Node 1</test>
    <test>Node 2</test>
</root>
```

Dzieje się tak dlatego `<?xml:stylesheet?>` jest uznawany za nieprawidłową **ProcessingInstruction** do modelu DOM. Wszelkie **ProcessingInstruction**, zgodnie z przestrzeni nazw w specyfikacji XML może zawierać tylko nazwy nie dwukropka (NCNames), w przeciwieństwie kwalifikowanej nazwy (QNames).

Od 6 sekcji przestrzeni nazw w specyfikacji XML, mających wpływ **obciążenia** i **działanie metody LoadXml** metody są zgodne ze specyfikacją jest to, że w dokumencie:

- Wszystkie typy elementu i nazwach atrybutów zawiera zero lub dwukropka.

- Nie nazwy jednostek, ProcessingInstruction elementów docelowych lub nazw w notacji zawierają wszystkie dwukropki.

Za pomocą `<?xml:stylesheet?>` zawierające dwukropek, możesz teraz naruszają reguły w drugim punktor.

Zgodnie z World Wide Web Consortium (W3C) [kojarzenie arkusze stylów, za pomocą XML dokumenty, wersja 1.0 zalecenie](https://www.w3.org/TR/xml-stylesheet/), jest instrukcja przetwarzania, aby skojarzyć arkusz stylów XSLT z dokumentu XML `<?xml-stylesheet?>`, za pomocą kreska, zastępując z dwukropkiem.

## <a name="see-also"></a>Zobacz także

- [Model DOM (XML Document Object Model)](xml-document-object-model-dom.md)
