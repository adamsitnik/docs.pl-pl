---
title: 'Poradnik: Tworzenie pliku dokumentacji XML przy użyciu modelu CodeDOM'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CodeDOM, generating XML documentation
- XML documentation, creating using CodeDOM
- Code Document Object Model, generating XML documentation
ms.assetid: e3b80484-36b9-41dd-9d21-a2f9a36381dc
ms.openlocfilehash: cdd1f173274b6bd33c4a67ed8eb0974c4c8e8e70
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73130189"
---
# <a name="how-to-create-an-xml-documentation-file-using-codedom"></a>Poradnik: Tworzenie pliku dokumentacji XML przy użyciu modelu CodeDOM
CodeDOM można użyć do utworzenia kodu, który generuje dokumentację XML. Proces obejmuje tworzenie wykresu CodeDOM, który zawiera komentarze dokumentacji XML, generowanie kodu i kompilowanie wygenerowanego kodu z opcją kompilatora, która tworzy dane wyjściowe dokumentacji XML.  
  
### <a name="to-create-a-codedom-graph-that-contains-xml-documentation-comments"></a>Aby utworzyć wykres CodeDOM zawierający komentarze dokumentacji XML  
  
1. Utwórz <xref:System.CodeDom.CodeCompileUnit> zawierający wykres CodeDOM dla przykładowej aplikacji.  
  
2. Użyj konstruktora <xref:System.CodeDom.CodeCommentStatement.%23ctor%2A> z parametrem `docComment` ustawionym na `true`, aby utworzyć elementy komentarza i tekst dokumentacji XML.  
  
     [!code-csharp[CodeDomHelloWorldSample#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#4)]
     [!code-vb[CodeDomHelloWorldSample#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#4)]  
  
### <a name="to-generate-the-code-from-the-codecompileunit"></a>Aby wygenerować kod z CodeCompileUnit  
  
1. Użyj metody <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A>, aby wygenerować kod i utworzyć plik źródłowy do skompilowania.  
  
     [!code-csharp[CodeDomHelloWorldSample#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#5)]
     [!code-vb[CodeDomHelloWorldSample#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#5)]  
  
### <a name="to-compile-the-code-and-generate-the-documentation-file"></a>Aby skompilować kod i wygenerować plik dokumentacji  
  
1. Dodaj opcję kompilatora **/doc** do właściwości <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> obiektu <xref:System.CodeDom.Compiler.CompilerParameters> i przekaż obiekt do metody <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A>, aby utworzyć plik dokumentacji XML podczas kompilowania kodu.  
  
     [!code-csharp[CodeDomHelloWorldSample#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#6)]
     [!code-vb[CodeDomHelloWorldSample#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#6)]  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kodu tworzy wykres CodeDOM z komentarzami dokumentacji, generuje plik kodu z Grafu i kompiluje plik i tworzy skojarzony plik dokumentacji XML.  
  
 [!code-csharp[CodeDomHelloWorldSample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#1)]
 [!code-vb[CodeDomHelloWorldSample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#1)]  
  
 W przykładzie kodu jest tworzona następująca dokumentacja XML w pliku HelloWorldDoc. XML.  
  
```xml  
<?xml version="1.0" ?>   
<doc>  
  <assembly>  
    <name>HelloWorld</name>   
  </assembly>  
  <members>  
    <member name="T:Samples.Class1">  
      <summary>  
        Create a Hello World application.   
        <seealso cref="M:Samples.Class1.Main" />   
      </summary>  
    </member>  
    <member name="M:Samples.Class1.Main">  
      <summary>  
        Main method for HelloWorld application.   
        <para>Add a new paragraph to the description.</para>   
      </summary>  
    </member>  
  </members>  
</doc>  
```  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
  
- Ten przykład kodu wymaga pomyślnego wykonania zestawu uprawnień `FullTrust`.  
  
## <a name="see-also"></a>Zobacz także

- [Dokumentowanie kodu za pomocą XML](../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
- [Komentarze dokumentacji XML](../../csharp/programming-guide/xmldoc/index.md)
- [Dokumentacja XML](/cpp/ide/xml-documentation-visual-cpp)
