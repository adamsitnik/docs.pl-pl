---
title: Obsługa białych znaków i istotnych białych znaków podczas ładowania modelu DOM
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1d9bbb14320b84a6d417c5c28026b169092de219
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61799336"
---
# <a name="white-space-and-significant-white-space-handling-when-loading-the-dom"></a>Obsługa białych znaków i istotnych białych znaków podczas ładowania modelu DOM
Podczas ładowania dokumentu, można ustawić opcję zachowania biały znak i utworzyć **XmlWhitespace** węzłów w drzewie dokumentu. Aby utworzyć węzły odstępu, ustaw **PreserveWhitespace** właściwości na wartość true. Jeśli ustawiono właściwość **false**biały znak węzły nie są tworzone, co jest ustawieniem domyślnym. Węzły znaczące spacje są zawsze zachowywane, a **XmlSignificantWhitespace** węzły są zawsze tworzone w pamięci w celu przedstawienia tych danych, niezależnie od ustawienia **PreserveWhitespace** Flaga.  
  
 Jeśli dokument jest ładowany z czytnika, następnie ustawienie **PreserveWhitespace** flagą właściwości **XmlDocument** klasa ma wpływ na tworzenie **XmlWhitespace** węzłów tylko wtedy, gdy **WhitespaceHandling** właściwość **klasy XmlTextReader** nie jest ustawiony na **elementu WhitespaceHandling.None**. Jest to wartość z **WhitespaceHandling** właściwości czytnika, który ma pierwszeństwo przed ustawieniem tej flagi na **XmlDocument**. Aby uzyskać więcej informacji na temat **XmlSignificantWhitespace**, zobacz <xref:System.Xml.XmlSignificantWhitespace>.  
  
## <a name="see-also"></a>Zobacz także

- [Model DOM (XML Document Object Model)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
