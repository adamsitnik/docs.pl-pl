---
title: Nazewnictwo parametrów
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
author: KrzysztofCwalina
ms.openlocfilehash: 0e5b33839372e303b96bd6b84949f9a82da2f689
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026314"
---
# <a name="naming-parameters"></a>Nazewnictwo parametrów
Poza oczywiste powodu czytelności warto postępuj zgodnie z wytycznymi dla nazw parametrów, ponieważ parametry są wyświetlane w dokumentacji i w projektancie, gdy zawierają narzędzi do projektowania wizualnego, funkcja Intellisense i przeglądania funkcji klasy.  
  
 **✓ DO** Użyj camelCasing w nazwach parametrów.  
  
 **✓ DO** Użyj nazwy opisowej parametrów.  
  
 **✓ CONSIDER** przy użyciu nazwy parametru znaczenie niż typ parametru.  
  
### <a name="naming-operator-overload-parameters"></a>Nazywanie parametrów przeciążenia operatora  
 **✓ DO** użyj `left` i `right` dla nazw parametrów przeciążenia operatora binarnego Jeśli znaczenia parametrów nie istnieje.  
  
 **✓ DO** użyj `value` dla Jednoargumentowy operator przeciążenia nazwy parametrów, jeśli żadnego znaczenia parametrów nie istnieje.  
  
 **✓ CONSIDER** łatwy do rozpoznania nazwy dla operatora przeciążenia parametrów, jeśli wykonanie tej tak dodaje wartość.  
  
 **X DO NOT** Użyj skrótów lub wskaźniki liczbowe dla operatora przeciążenia nazwy parametrów.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*  
  
 *Przedrukowano za uprawnienie Pearson edukacji, Inc. z [wytyczne dotyczące projektowania Framework: Konwencje, Idiomy i wzorców dla wielokrotnego użytku, do bibliotek .NET, wydanie 2](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina i Brad Abrams publikowane 22 Oct 2008 przez Addison Wesley Professional w ramach serii rozwoju Windows firmy Microsoft.*  
  
## <a name="see-also"></a>Zobacz także

- [Struktura — zalecenia dotyczące projektowania](../../../docs/standard/design-guidelines/index.md)
- [Wskazówki dotyczące nazewnictwa](../../../docs/standard/design-guidelines/naming-guidelines.md)
