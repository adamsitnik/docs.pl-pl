---
title: Like — Operator (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Like
- vb.Like
helpviewer_keywords:
- similar to
- pattern matching
- Like operator [Visual Basic]
- '? symbol, wildcard character'
- string comparison [Visual Basic], Like operator
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- symbols, wildcard
- wildcards, Like operator
- strings [Visual Basic], matching
- string comparison [Visual Basic], sorting data
- data [Visual Basic], sorting
- text [Visual Basic], comparing
- operators [Visual Basic], pattern-matching
- data [Visual Basic], string comparisons
- string comparison [Visual Basic], Like operators
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
ms.openlocfilehash: 795ecc2e80d57af29ccd50c50d2dd209c6425e40
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701134"
---
# <a name="like-operator-visual-basic"></a>Like — Operator (Visual Basic)
Porównuje ciąg ze wzorcem.  

> [!IMPORTANT]
> Operator `Like` nie jest obecnie obsługiwany w projektach .NET Core i .NET Standard.

## <a name="syntax"></a>Składnia  
  
```vb  
result = string Like pattern  
```  
  
## <a name="parts"></a>Części  
 `result`  
 Wymagany. Dowolna zmienna `Boolean`. Wynik jest wartością `Boolean` wskazującą, czy `string` spełnia `pattern`.  
  
 `string`  
 Wymagany. Dowolne wyrażenie `String`.  
  
 `pattern`  
 Wymagany. Dowolne wyrażenie `String` zgodne z konwencjami dopasowania wzorca opisanymi w "uwagi".  
  
## <a name="remarks"></a>Uwagi  
 Jeśli wartość w `string` spełnia wzorzec zawarty w `pattern`, `result` jest `True`. Jeśli ciąg nie spełnia wzorca, `result` jest `False`. Jeśli oba `string` i `pattern` są pustymi ciągami, wynik jest `True`.  
  
## <a name="comparison-method"></a>Metoda porównania  
 Zachowanie operatora `Like` zależy od [instrukcji Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md). Domyślną metodą porównywania ciągów dla każdego pliku źródłowego jest `Option Compare Binary`.  
  
## <a name="pattern-options"></a>Opcje wzorca  
 Wbudowane dopasowania wzorców zapewniają uniwersalne narzędzie do porównywania ciągów. Funkcje dopasowania wzorców umożliwiają dopasowanie każdego znaku w `string` względem określonego znaku, symbolu wieloznacznego, listy znaków lub zakresu znaków. W poniższej tabeli przedstawiono znaki dozwolone w `pattern` i ich dopasowanie.  
  
|Znaki w `pattern`|Dopasowania w `string`|  
|-----------------------------|-------------------------|  
|`?`|Dowolny pojedynczy znak|  
|`*`|Zero lub więcej znaków|  
|`#`|Dowolna pojedyncza cyfra (0 – 9)|  
|`[charlist]`|Dowolny pojedynczy znak w `charlist`|  
|`[!charlist]`|Dowolny pojedynczy znak nie w `charlist`|  
  
## <a name="character-lists"></a>Listy znaków  
 Grupa zawierająca jeden lub więcej znaków (`charlist`) ujęta w nawiasy kwadratowe (`[ ]`) może być używana do dopasowania dowolnego pojedynczego znaku w `string` i może zawierać prawie dowolny kod znaków, w tym cyfry.  
  
 Wykrzyknik (`!`) na początku `charlist` oznacza, że jest to dopasowanie, jeśli dowolny znak z wyjątkiem znaków w `charlist` zostanie znaleziony w `string`. Gdy używany jest nawiasy klamrowe, wykrzyknik dopasowuje się do samego siebie.  
  
## <a name="special-characters"></a>Znaki specjalne  
 Aby dopasować znaki specjalne do lewego nawiasu (`[`), znaku zapytania (`?`), znaku numeru (`#`) i gwiazdki (`*`), umieść je w nawiasach. Nie można użyć prawego nawiasu (`]`) w grupie, aby dopasować się do siebie, ale można go użyć poza grupą jako pojedynczym znakiem.  
  
 Sekwencja znaków `[]` jest traktowana jako ciąg o zerowej długości (`""`). Jednak nie może być częścią listy znaków ujętej w nawiasy klamrowe. Jeśli chcesz sprawdzić, czy pozycja w `string` zawiera jedną z grup znaków lub nie ma żadnego znaku, możesz użyć dwa razy `Like`. Aby zapoznać się z przykładem, zobacz [jak: dopasowywanie ciągu do wzorca](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md).  
  
## <a name="character-ranges"></a>Zakresy znaków  
 Używając łącznika (`–`), aby oddzielić dolną i górną granicę zakresu, `charlist` może określić zakres znaków. Na przykład, `[A–Z]` powoduje dopasowanie, jeśli pozycja znaku w `string` zawiera dowolny znak z zakresu `A` – `Z`, a `[!H–L]` powoduje dopasowanie, Jeśli odpowiednia pozycja znaku zawiera dowolny znak poza zakres `H` – `L`.  
  
 Po określeniu zakresu znaków muszą one znajdować się w rosnącej kolejności sortowania, czyli od najniższego do najwyższego. W tym celu `[A–Z]` jest prawidłowym wzorcem, ale `[Z–A]` nie jest.  
  
### <a name="multiple-character-ranges"></a>Wiele zakresów znaków  
 Aby określić wiele zakresów dla tej samej pozycji znaku, umieść je w tych samych nawiasach bez ograniczników. Na przykład `[A–CX–Z]` powoduje dopasowanie, jeśli pozycja znaku w `string` zawiera dowolny znak w zakresie `A` – `C` lub zakres `X` – `Z`.  
  
### <a name="usage-of-the-hyphen"></a>Użycie łącznika  
 Łącznik (`–`) może pojawić się na początku (po wykrzykniku, jeśli istnieje) lub na końcu `charlist`, aby dopasować sam siebie. W każdej innej lokalizacji łącznik identyfikuje zakres znaków, które są rozdzielane znakami po obu stronach łącznika.  
  
## <a name="collating-sequence"></a>Kolejność sortowania  
 Znaczenie określonego zakresu zależy od kolejności znaków w czasie wykonywania określony przez `Option Compare` i ustawienia regionalne systemu, w którym uruchomiono kod. W przypadku `Option Compare Binary` zakres `[A–E]` pasuje do `A`, `B`, `C`, `D` i `E`. W przypadku `Option Compare Text` `[A–E]` dopasowuje `A`, `a`, `À`, `à`, `B`, `b`, `C`, `c`, 0, 1, 2 i 3. Zakres nie pasuje do `Ê` lub `ê`, ponieważ znaki akcentowane są sortowane po nieakcentowane znaki w kolejności sortowania.  
  
## <a name="digraph-characters"></a>Znaki odgrafu  
 W niektórych językach istnieją znaki alfabetyczne, które reprezentują dwa oddzielne znaki. Na przykład w kilku językach użyto znaku `æ`, aby reprezentować znaki `a` i `e`, gdy pojawiają się razem. Operator `Like` rozpoznaje, że pojedynczy znak dwugrafu i dwa poszczególne znaki są równoważne.  
  
 Gdy język, który używa znaku oddzielenia jest określony w ustawieniach regionalnych systemu, wystąpienie pojedynczego znaku w `pattern` lub `string` dopasowuje równoważną dwuznakową sekwencję w innym ciągu. Podobnie, znak podgrafu w `pattern` ujęty w nawiasy kwadratowe (na liście lub w zakresie) jest zgodny z równoważną dwuznakową sekwencją w `string`.  
  
## <a name="overloading"></a>Przeciążenie  
 Operator `Like` może być *przeciążony*, co oznacza, że Klasa lub struktura może przedefiniować jej zachowanie, gdy operand ma typ tej klasy lub struktury. Jeśli Twój kod używa tego operatora dla takiej klasy lub struktury, pamiętaj o tym, aby zrozumieć jego ponownie zdefiniowane zachowanie. Aby uzyskać więcej informacji, zobacz [procedury operatorów](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Przykład  
 W tym przykładzie używa operatora `Like` do porównywania ciągów z różnymi wzorcami. Wyniki przejdą do zmiennej `Boolean` wskazującej, czy każdy ciąg spełnia wzorzec.  
  
 [!code-vb[VbVbalrOperators#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.Strings.InStr%2A>
- <xref:Microsoft.VisualBasic.Strings.StrComp%2A>
- [Operatory porównania](../../../visual-basic/language-reference/operators/comparison-operators.md)
- [Pierwszeństwo operatorów w Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [Operatory według funkcji](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Option Compare, instrukcja](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [Operatory i wyrażenia](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [Instrukcje: dopasowywanie ciągu do wzorca](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)
