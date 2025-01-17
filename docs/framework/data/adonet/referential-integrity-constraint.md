---
title: ograniczenie integralności referencyjnej
ms.date: 03/30/2017
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
ms.openlocfilehash: ad35df7bcca62ffdbc3842b0817b22c5482a3d4d
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738370"
---
# <a name="referential-integrity-constraint"></a>ograniczenie integralności referencyjnej
*Ograniczenie integralności referencyjnej* w Entity Data Model (EDM) jest podobne do ograniczenia integralności referencyjnej w relacyjnej bazie danych. W taki sam sposób, w jaki kolumna (lub kolumny) z tabeli bazy danych może odwoływać się do klucza podstawowego innej tabeli, [Właściwość](property.md) (lub właściwości) [typu jednostki](entity-type.md) może odwoływać się do [klucza jednostki](entity-key.md) innego typu jednostki. Typ obiektu, do którego istnieje odwołanie, nazywa się *głównym końcem* ograniczenia. Typ jednostki, który odwołuje się do głównego końca, nazywa się *końcem zależnym* od ograniczenia.  
  
 Ograniczenie integralności referencyjnej jest zdefiniowane w ramach [skojarzenia](association-type.md) między dwoma typami jednostek. Definicja ograniczenia integralności referencyjnej określa następujące informacje:  
  
- Główny koniec ograniczenia. (Typ jednostki, do której odwołuje się koniec zależny).  
  
- Klucz jednostki końca podmiotu zabezpieczeń.  
  
- Zależne zakończenie ograniczenia. (Typ jednostki, który ma właściwość lub właściwości odwołujące się do klucza jednostki końcowego końca).  
  
- Właściwość odwołania lub właściwości elementu End zależnego.  
  
 Ograniczenia więzów integralności w modelu EDM mają na celu zapewnienie, że poprawne skojarzenia zawsze istnieją. Aby uzyskać więcej informacji, zobacz [Właściwość klucza obcego](foreign-key-property.md).  
  
## <a name="example"></a>Przykład  
 Na poniższym diagramie przedstawiono model koncepcyjny z dwoma skojarzeniami: `WrittenBy` i `PublishedBy`. Typ jednostki `Book` ma właściwość `PublisherId`, która odwołuje się do klucza jednostki `Publisher` typu jednostki podczas definiowania ograniczenia integralności referencyjnej na skojarzeniu `PublishedBy`.  
  
 ![RefConstraintModel](./media/referential-integrity-constraint/reference-constraint-model.gif "Przykład modelu ograniczeń referencyjnych")  
  
 [ADO.NET Entity Framework](./ef/index.md) używa języka specyficznego dla domeny (DSL) zwanego językiem definicji schematu koncepcyjnego ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) do definiowania modeli koncepcyjnych. Poniższy CSDL definiuje ograniczenie integralności referencyjnej na skojarzeniu `PublishedBy` pokazanym w powyższym modelu koncepcyjnym.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a>Zobacz także

- [Kluczowe założenia modelu danych jednostki](entity-data-model-key-concepts.md)
- [Model danych jednostki](entity-data-model.md)
