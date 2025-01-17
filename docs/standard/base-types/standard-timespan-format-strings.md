---
title: Standardowe ciągi formatujące TimeSpan
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- format specifiers, standard time interval
- format strings
- standard time interval format strings
- standard format strings, time intervals
- format specifiers, time intervals
- time intervals [.NET Framework], formatting
- time [.NET Framework], formatting
- formatting [.NET Framework], time
- standard TimeSpan format strings
- formatting [.NET Framework], time intervals
ms.assetid: 9f6c95eb-63ae-4dcc-9c32-f81985c75794
ms.openlocfilehash: 5284eb52d7b50307e51945fc0b4a9deb8818f2e2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73121696"
---
# <a name="standard-timespan-format-strings"></a>Standardowe ciągi formatujące TimeSpan
<a name="Top"></a>Standardowy ciąg formatujący <xref:System.TimeSpan> używa pojedynczego specyfikatora formatu do definiowania tekstowej reprezentacji wartości <xref:System.TimeSpan>, która wynika z operacji formatowania. Dowolny ciąg formatu, który zawiera więcej niż jeden znak, w tym znak odstępu, jest interpretowany jako ciąg niestandardowego formatu <xref:System.TimeSpan>. Aby uzyskać więcej informacji, zobacz [Niestandardowe ciągi formatujące TimeSpan](../../../docs/standard/base-types/custom-timespan-format-strings.md) .  
  
 Ciąg reprezentujący wartości <xref:System.TimeSpan> są generowane przez wywołania przeciążenia metody <xref:System.TimeSpan.ToString%2A?displayProperty=nameWithType>, a także metody obsługujące formatowanie złożone, takie jak <xref:System.String.Format%2A?displayProperty=nameWithType>. Aby uzyskać więcej informacji, zobacz [Typy formatowania](../../../docs/standard/base-types/formatting-types.md) i [formatowanie złożone](../../../docs/standard/base-types/composite-formatting.md). Poniższy przykład ilustruje użycie standardowych ciągów formatu w operacjach formatowania.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/formatexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/formatexample1.vb#2)]  
  
 Ciągi standardowego formatu <xref:System.TimeSpan> są również używane przez metody <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> i <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> do definiowania wymaganego formatu ciągów wejściowych na potrzeby analizowania operacji. (Analizowanie konwertuje ciąg reprezentujący wartość na tę wartość). Poniższy przykład ilustruje użycie standardowych ciągów formatu podczas analizowania operacji.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/parseexample1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/parseexample1.vb#3)]  
  
<a name="top"></a>Poniższa tabela zawiera listę specyfikatorów formatu standardowego interwału czasu.  
  
|Specyfikator formatu|Nazwa|Opis|Przykłady|  
|----------------------|----------|-----------------|--------------|  
|s|Stały format (niezmienny)|Ten specyfikator nie jest uwzględniany w kulturze. Formularz `[-][d'.']hh':'mm':'ss['.'fffffff]`.<br /><br /> (Ciągi formatu "t" i "T" dają te same wyniki).<br /><br /> Więcej informacji: [specyfikator formatu stałej ("c")](#Constant).|`TimeSpan.Zero`-> 00:00:00<br /><br /> `New TimeSpan(0, 0, 30, 0)`-> 00:30:00<br /><br /> `New TimeSpan(3, 17, 25, 30, 500)`-> 3.17:25:30.5000000|  
|„g”|Ogólny krótki format|Ten specyfikator wyprowadza tylko to, co jest potrzebne. Jest ona zależna od kultury i ma postać `[-][d':']h':'mm':'ss[.FFFFFFF]`.<br /><br /> Więcej informacji: [specyfikator formatu ogólnego ("g")](#GeneralShort).|`New TimeSpan(1, 3, 16, 50, 500)`-> 1:3: 16:50.5 (pl-US)<br /><br /> `New TimeSpan(1, 3, 16, 50, 500)`-> 1:3: 16:50, 5 (fr-FR)<br /><br /> `New TimeSpan(1, 3, 16, 50, 599)`-> 1:3: 16:50.599 (pl-US)<br /><br /> `New TimeSpan(1, 3, 16, 50, 599)`-> 1:3: 16:50599 (fr-FR)|  
|„G”|Format ogólnie długi|Ten specyfikator zawsze Wyprowadza dni i siedem cyfr. Jest ona zależna od kultury i ma postać `[-]d':'hh':'mm':'ss.fffffff`.<br /><br /> Więcej informacji: [specyfikator formatu ogólnego ("G")](#GeneralLong).|`New TimeSpan(18, 30, 0)`-> 0:18:30:00.0000000 (EN-US)<br /><br /> `New TimeSpan(18, 30, 0)`-> 0:18:30:00, 0000000 (fr-FR)|  
  
<a name="Constant"></a>   
## <a name="the-constant-c-format-specifier"></a>Specyfikator formatu stałej ("c")  
 Specyfikator formatu "c" zwraca reprezentację ciągu <xref:System.TimeSpan> wartości w następującej postaci:  
  
 [-] [*d*.] *hh*:*mm*:*SS*[. *fffffff*]  
  
 Elementy w nawiasach kwadratowych ([ i ]) są opcjonalne. Kropka (.) i dwukropek (:) są symbolami literału. W poniższej tabeli opisano pozostałe elementy.  
  
|Element|Opis|  
|-------------|-----------------|  
|*-*|Opcjonalny znak ujemny, który wskazuje ujemny przedział czasu.|  
|*Wykres*|Opcjonalna liczba dni bez zer wiodących.|  
|*formacie*|Liczba godzin z zakresu od "00" do "23".|  
|*–*|Liczba minut obejmująca wartość "00" do "59".|  
|*RR*|Liczba sekund określająca zakres od "0" do "59".|  
|*fffffff*|Opcjonalna część ułamkowa sekundy.  Jego wartość może być z zakresu od "0000001" (jeden takt lub 1 10-milionowego sekundy) do "9999999" (9 999 999 10-dziesięciomilionowych sekundy lub jeden drugi z więcej niż jeden takt).|  
  
 W przeciwieństwie do specyfikatorów formatu "g" i "G", specyfikator formatu "c" nie jest uwzględniany w kulturze. Generuje ciąg reprezentujący wartość <xref:System.TimeSpan>, która jest niezmienna i która jest wspólna dla wszystkich poprzednich wersji .NET Framework przed .NET Framework 4. "c" jest domyślnym ciągiem formatu <xref:System.TimeSpan>; Metoda <xref:System.TimeSpan.ToString?displayProperty=nameWithType> formatuje wartość przedziału czasu przy użyciu ciągu formatu "c".  
  
> [!NOTE]
> <xref:System.TimeSpan> obsługuje również ciągi formatu standardowego "t" i "T", które są identyczne w zachowaniu dla standardowego ciągu formatu "c".  
  
 Poniższy przykład tworzy wystąpienie dwóch <xref:System.TimeSpan> obiektów, używa ich do wykonywania operacji arytmetycznych i wyświetla wynik. W każdym przypadku używa formatowania złożonego, aby wyświetlić wartość <xref:System.TimeSpan> przy użyciu specyfikatora formatu "c".  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardc1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardc1.vb#1)]  
  
 [Wróć do tabeli](#Top)  
  
<a name="GeneralShort"></a>   
## <a name="the-general-short-g-format-specifier"></a>Specyfikator formatu ogólnego ("g")  
 Specyfikator formatu <xref:System.TimeSpan> "g" zwraca reprezentację ciągu <xref:System.TimeSpan> wartości w postaci kompaktowej przez uwzględnienie tylko tych elementów, które są niezbędne. Ma następującą postać:  
  
 [-] [*d*:] *h*:*mm*:*SS*[. *FFFFFFF*]  
  
 Elementy w nawiasach kwadratowych ([ i ]) są opcjonalne. Dwukropek (:) jest symbolem literału. W poniższej tabeli opisano pozostałe elementy.  
  
|Element|Opis|  
|-------------|-----------------|  
|*-*|Opcjonalny znak ujemny, który wskazuje ujemny przedział czasu.|  
|*Wykres*|Opcjonalna liczba dni bez zer wiodących.|  
|*c*|Liczba godzin z zakresu od "0" do "23" bez zer wiodących.|  
|*–*|Liczba minut obejmująca wartość "00" do "59".|  
|*RR*|Liczba sekund określająca zakres od "00" do "59"..|  
|*.*|Separator sekund ułamkowych. Jest ona równoważna z właściwością <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> określonej kultury bez zastąpień użytkownika.|  
|*FFFFFFF*|Ułamki sekund. Zostanie wyświetlona najmniejsza liczba cyfr.|  
  
 Podobnie jak specyfikator formatu "G", specyfikator formatu "g" jest lokalizowany. Separator ułamków sekund jest oparty na bieżącej kulturze lub właściwości <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> określonej kultury.  
  
 Poniższy przykład tworzy wystąpienie dwóch <xref:System.TimeSpan> obiektów, używa ich do wykonywania operacji arytmetycznych i wyświetla wynik. W każdym przypadku używa formatowania złożonego, aby wyświetlić wartość <xref:System.TimeSpan> przy użyciu specyfikatora formatu "g". Ponadto formatuje wartość <xref:System.TimeSpan> przy użyciu Konwencji formatowania bieżącej kultury systemu (w tym przypadku jest to angielski-Stany Zjednoczone lub EN-US) oraz kulturę Francuska-Francja (fr-FR).  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardshort1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardshort1.vb#4)]  
  
 [Wróć do tabeli](#Top)  
  
<a name="GeneralLong"></a>   
## <a name="the-general-long-g-format-specifier"></a>Specyfikator formatu ogólnego ("G")  
 Specyfikator formatu <xref:System.TimeSpan> "G" zwraca reprezentację ciągu <xref:System.TimeSpan> wartości w postaci długiej, która zawsze zawiera dni i ułamki sekund. Ciąg, który jest wynikiem specyfikatora formatu standardowego "G", ma następującą postać:  
  
 [-] *d*:*hh*:*mm*:*SS*. *fffffff*  
  
 Elementy w nawiasach kwadratowych ([ i ]) są opcjonalne. Dwukropek (:) jest symbolem literału. W poniższej tabeli opisano pozostałe elementy.  
  
|Element|Opis|  
|-------------|-----------------|  
|*-*|Opcjonalny znak ujemny, który wskazuje ujemny przedział czasu.|  
|*Wykres*|Liczba dni bez zer wiodących.|  
|*formacie*|Liczba godzin z zakresu od "00" do "23".|  
|*–*|Liczba minut obejmująca wartość "00" do "59".|  
|*RR*|Liczba sekund określająca zakres od "00" do "59".|  
|*.*|Separator sekund ułamkowych. Jest ona równoważna z właściwością <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> określonej kultury bez zastąpień użytkownika.|  
|*fffffff*|Ułamki sekund.|  
  
 Podobnie jak specyfikator formatu "G", specyfikator formatu "g" jest lokalizowany. Separator ułamków sekund jest oparty na bieżącej kulturze lub właściwości <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> określonej kultury.  
  
 Poniższy przykład tworzy wystąpienie dwóch <xref:System.TimeSpan> obiektów, używa ich do wykonywania operacji arytmetycznych i wyświetla wynik. W każdym przypadku używa formatowania złożonego, aby wyświetlić wartość <xref:System.TimeSpan> przy użyciu specyfikatora formatu "G". Ponadto formatuje wartość <xref:System.TimeSpan> przy użyciu Konwencji formatowania bieżącej kultury systemu (w tym przypadku jest to angielski-Stany Zjednoczone lub EN-US) oraz kulturę Francuska-Francja (fr-FR).  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardlong1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardlong1.vb#5)]  
  
 [Wróć do tabeli](#Top)  
  
## <a name="see-also"></a>Zobacz także

- [Formatowanie typów](../../../docs/standard/base-types/formatting-types.md)
- [Niestandardowe ciągi formatujące TimeSpan](../../../docs/standard/base-types/custom-timespan-format-strings.md)
- [Analizowanie ciągów](../../../docs/standard/base-types/parsing-strings.md)
