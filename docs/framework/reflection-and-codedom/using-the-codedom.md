---
title: Używanie modelu CodeDOM
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- code compilers
- Code Document Object Model
- Code Document Object Model, graphs
- types, CodeDOM
- namespaces [.NET Framework], CodeDOM
- templated code generation
- dynamically representing source code
- source code models
- CodeDOM
- graphing with CodeDOM
- dynamic compilation
- code generators
- CodeDOM, graphs
ms.assetid: 0444ddf3-c3f6-44ed-a999-f710d9c3e0cf
ms.openlocfilehash: c4cab79976acae236de5a8eaad5a42cdba7d04f9
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73130010"
---
# <a name="using-the-codedom"></a>Używanie modelu CodeDOM
CodeDOM zawiera typy reprezentujące wiele typowych typów elementów kodu źródłowego. Można zaprojektować program, który kompiluje model kodu źródłowego za pomocą elementów CodeDOM do złożenia grafu obiektów. Ten Graf obiektu może być renderowany jako kod źródłowy przy użyciu generatora kodu CodeDOM dla obsługiwanego języka programowania. CodeDOM można także użyć do kompilowania kodu źródłowego do zestawu binarnego.  
  
 Niektóre typowe zastosowania dla CodeDOM:  
  
- Generowanie kodu z szablonami: generowanie kodu dla ASP.NET, proxy klienta usług sieci Web XML, kreatorów kodu, projektantów lub innych mechanizmów emitujących kod.  
  
- Kompilacja dynamiczna: obsługa kompilacji kodu w jednym lub wielu językach.  
  
## <a name="building-a-codedom-graph"></a>Kompilowanie wykresu CodeDOM  
 Przestrzeń nazw <xref:System.CodeDom> zawiera klasy służące do reprezentowania logicznej struktury kodu źródłowego, niezależnie od składni języka.  
  
### <a name="the-structure-of-a-codedom-graph"></a>Struktura wykresu CodeDOM  
 Struktura wykresu CodeDOM jest taka sama jak drzewo kontenerów. Najwyższego lub głównego kontenera każdy nadawać wykres CodeDOM jest <xref:System.CodeDom.CodeCompileUnit>. Każdy element modelu kodu źródłowego musi być połączony z wykresem przez właściwość <xref:System.CodeDom.CodeObject> w grafie.  
  
### <a name="building-a-source-code-model-for-a-sample-hello-world-program"></a>Kompilowanie modelu kodu źródłowego dla przykładowego programu Hello world  
 Poniższy przewodnik przedstawia przykład sposobu tworzenia wykresu obiektu CodeDOM, który reprezentuje kod dla prostej aplikacji Hello world. Aby uzyskać pełny kod źródłowy tego przykładu kodu, zapoznaj się z tematem <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType>.  
  
#### <a name="creating-a-compile-unit"></a>Tworzenie jednostki kompilacji  
 CodeDOM definiuje obiekt o nazwie <xref:System.CodeDom.CodeCompileUnit>, który może odwoływać się do wykresu obiektu CodeDOM, który modeluje kod źródłowy do skompilowania. **CodeCompileUnit** ma właściwości do przechowywania odwołań do atrybutów, przestrzeni nazw i zestawów.  
  
 Dostawcy CodeDom, które pochodzą z klasy <xref:System.CodeDom.Compiler.CodeDomProvider>, zawierają metody, które przetwarzają Graf obiektów, do których odwołuje się **CodeCompileUnit**.  
  
 Aby utworzyć Graf obiektu dla prostej aplikacji, należy złożyć model kodu źródłowego i odwołać się do niego z **CodeCompileUnit**.  
  
 Można utworzyć nową jednostkę kompilacji z składnią zademonstrowaną w tym przykładzie:  
  
 [!code-cpp[CodeDomExample#12](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#12)]
 [!code-csharp[CodeDomExample#12](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#12)]
 [!code-vb[CodeDomExample#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#12)]  
  
 <xref:System.CodeDom.CodeSnippetCompileUnit> może zawierać sekcję kodu źródłowego, która znajduje się już w języku docelowym, ale nie może być renderowana w innym języku.  
  
#### <a name="defining-a-namespace"></a>Definiowanie przestrzeni nazw  
 Aby zdefiniować przestrzeń nazw, Utwórz <xref:System.CodeDom.CodeNamespace> i przypisz jej nazwę przy użyciu odpowiedniego konstruktora lub ustawiając jej właściwość **name** .  
  
 [!code-cpp[CodeDomExample#13](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#13)]
 [!code-csharp[CodeDomExample#13](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#13)]
 [!code-vb[CodeDomExample#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#13)]  
  
#### <a name="importing-a-namespace"></a>Importowanie przestrzeni nazw  
 Aby dodać dyrektywę import przestrzeni nazw do przestrzeni nazw, Dodaj <xref:System.CodeDom.CodeNamespaceImport>, która wskazuje przestrzeń nazw do zaimportowania do kolekcji **CodeNamespace. Imports** .  
  
 Poniższy kod dodaje import dla przestrzeni nazw **system** do kolekcji **Imports** **CodeNamespace** o nazwie `samples`:  
  
 [!code-cpp[CodeDomExample#14](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#14)]
 [!code-csharp[CodeDomExample#14](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#14)]
 [!code-vb[CodeDomExample#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#14)]  
  
#### <a name="linking-code-elements-into-the-object-graph"></a>Łączenie elementów kodu do grafu obiektów  
 Wszystkie elementy kodu, które tworzą wykres CodeDOM, muszą być połączone z <xref:System.CodeDom.CodeCompileUnit>, który jest elementem głównym drzewa przez serię odwołań do elementów bezpośrednio przywoływanych ze wszystkich właściwości obiektu głównego grafu. Ustaw obiekt na właściwość obiektu kontenera, aby ustanowić odwołanie z obiektu kontenera.  
  
 Poniższa instrukcja dodaje `samples` **CodeNamespace** do właściwości kolekcji **przestrzeni nazw** głównego **CodeCompileUnit**.  
  
 [!code-cpp[CodeDomExample#15](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#15)]
 [!code-csharp[CodeDomExample#15](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#15)]
 [!code-vb[CodeDomExample#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#15)]  
  
#### <a name="defining-a-type"></a>Definiowanie typu  
 Aby zadeklarować klasę, strukturę, interfejs lub Wyliczenie przy użyciu CodeDOM, Utwórz nowy <xref:System.CodeDom.CodeTypeDeclaration>i przypisz mu nazwę. Poniższy przykład ilustruje to przy użyciu przeciążenia konstruktora, aby ustawić właściwość **name** :  
  
 [!code-cpp[CodeDomExample#16](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#16)]
 [!code-csharp[CodeDomExample#16](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#16)]
 [!code-vb[CodeDomExample#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#16)]  
  
 Aby dodać typ do przestrzeni nazw, Dodaj <xref:System.CodeDom.CodeTypeDeclaration>, który reprezentuje typ, który ma zostać dodany do przestrzeni nazw do kolekcji **typów** **CodeNamespace**.  
  
 W poniższym przykładzie pokazano, jak dodać klasę o nazwie `class1` do **CodeNamespace** o nazwie `samples`:  
  
 [!code-cpp[CodeDomExample#17](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#17)]
 [!code-csharp[CodeDomExample#17](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#17)]
 [!code-vb[CodeDomExample#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#17)]  
  
#### <a name="adding-class-members-to-a-class"></a>Dodawanie elementów członkowskich klasy do klasy  
 Przestrzeń nazw <xref:System.CodeDom> zawiera różne elementy, których można użyć do reprezentowania elementów członkowskich klasy. Każdy element członkowski klasy można dodać do kolekcji **Members** <xref:System.CodeDom.CodeTypeDeclaration>.  
  
#### <a name="defining-a-code-entry-point-method-for-an-executable"></a>Definiowanie metody punktu wejścia kodu dla pliku wykonywalnego  
 Jeśli tworzysz kod dla programu wykonywalnego, konieczne jest wskazanie punktu wejścia programu, tworząc <xref:System.CodeDom.CodeEntryPointMethod> reprezentujący metodę, która ma zostać rozpoczęta.  
  
 Poniższy przykład ilustruje sposób definiowania metody punktu wejścia, która zawiera <xref:System.CodeDom.CodeMethodInvokeExpression>, która wywołuje **System. Console. WriteLine** , aby wydrukować "Hello World!":  
  
 [!code-cpp[CodeDomExample#18](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#18)]
 [!code-csharp[CodeDomExample#18](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#18)]
 [!code-vb[CodeDomExample#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#18)]  
  
 Poniższa instrukcja dodaje metodę punktu wejścia o nazwie `Start` do kolekcji **członkowie** `class1`:  
  
 [!code-cpp[CodeDomExample#19](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#19)]
 [!code-csharp[CodeDomExample#19](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#19)]
 [!code-vb[CodeDomExample#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#19)]  
  
 Teraz <xref:System.CodeDom.CodeCompileUnit> o nazwie `compileUnit` zawiera wykres CodeDOM dla prostego programu Hello world. Aby uzyskać informacje na temat generowania i kompilowania kodu z wykresu CodeDOM, zobacz [generowanie kodu źródłowego i kompilowanie programu z wykresu CodeDOM](generating-and-compiling-source-code-from-a-codedom-graph.md).  
  
### <a name="more-information-on-building-a-codedom-graph"></a>Więcej informacji na temat tworzenia wykresu CodeDOM  
 CodeDOM obsługuje wiele typowych typów elementów kodu znalezionych w językach programowania, które obsługują środowisko uruchomieniowe języka wspólnego. CodeDOM nie został zaprojektowany tak, aby zapewnić elementy reprezentujące wszystkie możliwe funkcje języka programowania. Kod, którego nie można łatwo przedstawić, za pomocą elementów CodeDOM można hermetyzować w <xref:System.CodeDom.CodeSnippetExpression>, <xref:System.CodeDom.CodeSnippetStatement>, <xref:System.CodeDom.CodeSnippetTypeMember>lub <xref:System.CodeDom.CodeSnippetCompileUnit>. Fragmenty kodu nie mogą jednak być tłumaczone na inne języki automatycznie przez CodeDOM.  
  
 Aby uzyskać dokumentację dla każdego z typów CodeDOM, zobacz dokumentację referencyjną <xref:System.CodeDom> przestrzeni nazw.  
  
 Aby uzyskać szybki wykres w celu zlokalizowania elementu CodeDOM, który reprezentuje określony typ elementu kodu, zobacz [Krótki przewodnik CodeDOM](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100)).
