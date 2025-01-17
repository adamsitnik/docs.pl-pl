---
title: Przestrzenie C# nazw — Przewodnik programowania
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, namespaces
- namespaces [C#]
ms.assetid: b1c4ab46-3fad-4ffa-9deb-dd50a2d8c65a
ms.openlocfilehash: cf5a7f239cf7d3cd3a6e39f31d16adb830646afc
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039492"
---
# <a name="namespaces-c-programming-guide"></a>Przestrzenie nazw (Przewodnik programowania w języku C#)

Przestrzenie nazw są intensywnie używane w C# programowaniu na dwa sposoby. Najpierw .NET Framework używa przestrzeni nazw do organizowania jej wielu klas w następujący sposób:  
  
 [!code-csharp[csProgGuide#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#22)]  
  
`System`jest przestrzenią nazw `Console` i jest klasą w tej przestrzeni nazw. Można `using` użyć słowa kluczowego, tak aby pełna nazwa nie była wymagana, jak w poniższym przykładzie:  
  
 [!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]  
  
 [!code-csharp[csProgGuide#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#25)]  
  
Aby uzyskać więcej informacji, zobacz [dyrektywa using](../../language-reference/keywords/using-directive.md).  
  
Po drugie, zadeklarowanie własnych przestrzeni nazw może pomóc w kontroli zakresu nazw klas i metod w większych projektach programistycznych. Użyj słowa kluczowego [Namespace](../../language-reference/keywords/namespace.md) , aby zadeklarować przestrzeń nazw, jak w poniższym przykładzie:  
  
 [!code-csharp[csProgGuideNamespaces#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#6)]

Nazwa przestrzeni nazw musi być prawidłową C# [nazwą identyfikatora](../inside-a-program/identifier-names.md).

## <a name="namespaces-overview"></a>Przegląd przestrzeni nazw  

Przestrzenie nazw mają następujące właściwości:  
  
- Organizują one duże projekty kodu.  
- Są one rozdzielane za pomocą `.` operatora.  
- `using` Dyrektywa eliminuje konieczność określenia nazwy przestrzeni nazw dla każdej klasy.  
- Przestrzeń nazw jest przestrzenią nazw "root" `global::System` : zawsze odwołuje się do przestrzeni nazw platformy .NET <xref:System>. `global`  

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [przestrzenie nazw](~/_csharplang/spec/namespaces.md) [ C# specyfikacji języka](~/_csharplang/spec/introduction.md).
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Używanie przestrzeni nazw](using-namespaces.md)
- [Instrukcje: Korzystanie z przestrzeni nazw my](how-to-use-the-my-namespace.md)
- [Nazwy identyfikatorów](../inside-a-program/identifier-names.md)
- [using, dyrektywa](../../language-reference/keywords/using-directive.md)
- [:: operator](../../language-reference/operators/namespace-alias-qualifier.md)
