---
title: Serializacja — .NET
ms.date: 09/02/2019
helpviewer_keywords:
- JSON serialization
- XML serialization, defined
- binary serialization
- serializing objects
- serialization
- objects, serializing
ms.assetid: 4d1111c0-9447-4231-a997-96a2b74b3453
ms.openlocfilehash: e6db24326c79ab6509b253c45c27f87a2aacd73c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053347"
---
# <a name="serialization-in-net"></a>Serializacja w .NET

Serializacja jest proces konwersji stan obiektu do formularza, które mogą być utrwalone lub transportowane. Uzupełnienie serializacji jest deserializacji, która konwertuje strumień na obiekt. Procesy te umożliwiają jednoczesne przechowywanie i przesyłanie danych.  
  
Platforma .NET oferuje następujące technologie serializacji:  
  
- [Serializacja binarna](binary-serialization.md) zachowuje wierność typu, co jest przydatne do zachowania stanu obiektu między różnymi wywołaniami aplikacji. Na przykład można udostępnić obiekt między różnymi aplikacjami, serializacji go do Schowka. Można serializować obiektu w strumieniu na dysku w pamięci, za pośrednictwem sieci i tak dalej. Komunikacja zdalna używa serializacji do przekazywania obiektów "według wartości" z jednego komputera lub domeny aplikacji do innej.  
  
- [Serializacji XML i SOAP](xml-and-soap-serialization.md) serializować tylko właściwości publiczne i pola i nie zachowuje wierności typów. Jest to przydatne, gdy chcesz zapewnić lub wykorzystać dane bez ograniczania aplikacji, która korzysta z danych. Ponieważ kod XML jest otwarty standard, jest atrakcyjny wybór udostępnianie danych w sieci Web. Podobnie protokołu SOAP jest otwarty standard, co pozwala na wybór atrakcyjny.  
  
- [Serializacja kodu JSON](system-text-json-overview.md) wykonuje serializacji tylko właściwości publicznych i nie zachowuje wierności typów. JSON to otwarty standard, który jest atrakcyjnym wyborem w przypadku udostępniania danych w sieci Web.

## <a name="reference"></a>Tematy pomocy

<xref:System.Runtime.Serialization>  
Zawiera klasy, które mogą być używane do serializacji i deserializacji obiektów.
  
<xref:System.Xml.Serialization>  
Zawiera klasy, których można użyć do wykonywania serializacji obiektów w dokumentach formatu XML lub strumieni.

<xref:System.Text.Json>  
Zawiera klasy, których można użyć do serializacji obiektów w dokumenty lub strumienie w formacie JSON.
