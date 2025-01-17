---
title: Rozpoznanie późnego wiązania; mogą wystąpić błędy podczas wykonywania
ms.date: 07/20/2015
f1_keywords:
- vbc42017
- BC42017
helpviewer_keywords:
- BC42017
ms.assetid: 45f552c8-57c6-44c0-97d3-e510119b257a
ms.openlocfilehash: 6b78dfed1d615ba865f136365eac1c9c131ed5a5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661952"
---
# <a name="late-bound-resolution-runtime-errors-could-occur"></a>Rozpoznanie późnego wiązania; mogą wystąpić błędy podczas wykonywania
Obiekt jest przypisany do zmiennej, zadeklarowanej będzie [Object — typ danych](../../../visual-basic/language-reference/data-types/object-data-type.md).  
  
 Kiedy Deklarujesz zmienną `Object`, kompilator musi wykonać *późnym wiązaniu*, co powoduje, że dodatkowe operacje w czasie wykonywania. Udostępnia ona również aplikację, aby potencjalne błędy czasu wykonywania. Na przykład, jeśli przypisujesz <xref:System.Windows.Forms.Form> do `Object` zmiennej, a następnie spróbuj uzyskać dostęp do <xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=nameWithType> właściwości, środowisko wykonawcze zgłasza <xref:System.MemberAccessException> ponieważ <xref:System.Windows.Forms.Form> klasy nie ujawnia `NameTable` właściwości.  
  
 Jeśli zadeklarujesz zmienną określonego typu, kompilator będzie mógł wykonać *wczesne powiązania* w czasie kompilacji. Skutkuje to lepszą wydajność i kontrolowany dostęp do elementów członkowskich z określonego typu i zwiększenia czytelności kodu.  
  
 Domyślnie ta wiadomość jest ostrzeżenie. Uzyskać informacje o ukrywaniu ostrzeżenia lub traktowanie ostrzeżeń jako błędy, zobacz [Konfigurowanie ostrzeżeń w języku Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Identyfikator błędu:** BC42017  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Jeśli to możliwe należy zadeklarować zmienną określonego typu.  
  
## <a name="see-also"></a>Zobacz także

- [Wczesne i późne powiązania](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
- [Deklaracja zmiennej obiektu](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
