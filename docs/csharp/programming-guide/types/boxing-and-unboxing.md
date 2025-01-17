---
title: Pakowanie i rozpakowywanie — C# Przewodnik programistyczny
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- cs.boxing
helpviewer_keywords:
- C# language, boxing
- C# language, unboxing
- unboxing [C#]
- boxing [C#]
ms.assetid: 8da9bbf4-bce9-4b08-b2e5-f64c11c56514
ms.openlocfilehash: 849983bb9cce6c9e0f41247a898747300fd29435
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588536"
---
# <a name="boxing-and-unboxing-c-programming-guide"></a>Konwersja boxing i konwersja unboxing (Przewodnik programowania w języku C#)
Opakowanie to proces konwersji [typu wartości](../../language-reference/keywords/value-types.md) na typ `object` lub dowolny typ interfejsu implementowany przez ten typ wartości. Gdy środowisko CLR pola typu wartości, zawija wartość wewnątrz <xref:System.Object?displayProperty=nameWithType> wystąpienia i zapisuje je na stosie zarządzanym. Rozpakowywanie wyodrębnia typ wartości z obiektu. Opakowanie jest niejawne; Rozpakowywanie jest jawne. Pojęcie opakowania i rozpakowywanie opiera się na C# ujednoliconym widoku systemu typów, w którym wartość dowolnego typu może być traktowana jako obiekt.  
  
 W poniższym przykładzie zmienna `i` Integer jest *opakowana* i przypisana do obiektu. `o`  
  
 [!code-csharp[csProgGuideTypes#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#14)]  
  
 Obiekt `o` może być następnie nieopakowany i przypisany do zmiennej `i`całkowitej:  
  
 [!code-csharp[csProgGuideTypes#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#15)]  
  
 W poniższych przykładach pokazano, jak opakowanie jest używane C#w programie.  
  
 [!code-csharp[csProgGuideTypes#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#47)]  
  
## <a name="performance"></a>Wydajność  
 W odniesieniu do prostych przydziałów, opakowanie i rozpakowywanie są w sposób obliczeniowy kosztowny. Gdy typ wartości jest opakowany, nowy obiekt musi być przydzielony i skonstruowany. W mniejszym stopniu rzutowanie wymagane do rozpakowywania jest również kosztowne w praktyce. Aby uzyskać więcej informacji, zobacz [wydajność](../../../framework/performance/performance-tips.md).  
  
## <a name="boxing"></a>Boxing  
 Opakowanie jest używane do przechowywania typów wartości w stosie zebranych elementów bezużytecznych. Opakowanie jest niejawną konwersją [typu wartości](../../language-reference/keywords/value-types.md) na typ `object` lub dowolny typ interfejsu implementowany przez ten typ wartości. Opakowanie typu wartości przydziela wystąpienie obiektu na stercie i kopiuje wartość do nowego obiektu.  
  
 Rozważmy następującą deklarację zmiennej typu wartości:  
  
 [!code-csharp[csProgGuideTypes#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#17)]  
  
 Poniższa instrukcja niejawnie stosuje operację pakowania na zmiennej `i`:  
  
 [!code-csharp[csProgGuideTypes#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#18)]  
  
 Wynikiem tej instrukcji jest utworzenie odwołania `o`do obiektu na stosie, który odwołuje się do wartości typu `int`na stercie. Ta wartość jest kopią wartości typu wartości przypisanej do zmiennej `i`. Różnica między dwoma zmiennymi, `i` a `o`, jest zilustrowana na poniższej ilustracji konwersji pakującej:  
  
 ![Ilustracja przedstawiająca różnicę między zmiennymi i i o.](./media/boxing-and-unboxing/boxing-operation-i-o-variables.gif)    
  
 Istnieje również możliwość, że opakowanie zostało jawnie wykonane, jak w poniższym przykładzie, ale jawne opakowanie nigdy nie jest wymagane:  
  
 [!code-csharp[csProgGuideTypes#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#19)]  
  
## <a name="description"></a>Opis  
 Ten przykład konwertuje zmienną `i` całkowitą na obiekt `o` przy użyciu opakowania. Następnie wartość przechowywana w zmiennej `i` zostanie zmieniona z `123` na `456`. W przykładzie pokazano, że oryginalny typ wartości i obiekt opakowany używają oddzielnych lokalizacji pamięci, w związku z czym można przechowywać różne wartości.  
  
## <a name="example"></a>Przykład  
 [!code-csharp[csProgGuideTypes#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#16)]  
  
## <a name="unboxing"></a>Rozpakowywanie  
 Rozpakowywanie jest jawną konwersją z typu `object` na [Typ wartości](../../language-reference/keywords/value-types.md) lub z typu interfejsu do typu wartości, który implementuje interfejs. Odpakowywanie operacji składa się z:  
  
- Sprawdzanie wystąpienia obiektu, aby upewnić się, że jest to opakowana wartość danego typu wartości.  
  
- Kopiowanie wartości z wystąpienia do zmiennej typu wartości.  
  
 Następujące instrukcje przedstawiają operacje pakowania i rozpakowywania:  
  
 [!code-csharp[csProgGuideTypes#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#21)]  
  
 Na poniższej ilustracji przedstawiono wynik poprzednich instrukcji: 
  
 ![Ilustracja przedstawiająca konwersję rozpakowywanie.](./media/boxing-and-unboxing/unboxing-conversion-operation.gif)
  
 Aby rozpakowywanie typów wartości zakończyło się pomyślnie w czasie wykonywania, element, który jest rozpakowany, musi być odwołaniem do obiektu, który został wcześniej utworzony przez opakowanie wystąpienia tego typu wartości. Próba Unbox `null` <xref:System.NullReferenceException>powoduje. Próba Unbox odwołania do niezgodnego typu wartości powoduje wystąpienie <xref:System.InvalidCastException>.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład ilustruje przypadek nieprawidłowego rozpakowywania i wyniki `InvalidCastException`. Przy `try` użyciu `catch`i, komunikat o błędzie jest wyświetlany po wystąpieniu błędu.  
  
 [!code-csharp[csProgGuideTypes#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#20)]  
  
 Ten program wyprowadza:  
  
 `Specified cast is not valid. Error: Incorrect unboxing.`  
  
 W przypadku zmiany instrukcji:  
  
```csharp
int j = (short) o;  
```  
  
 na:  
  
```csharp
int j = (int) o;  
```  
  
 Konwersja zostanie wykonana i otrzymasz dane wyjściowe:  
  
 `Unboxing OK.`  
  
## <a name="c-language-specification"></a>Specyfikacja języka C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="related-sections"></a>Sekcje pokrewne  
 Informacje dodatkowe:  
  
- [Typy odwołań](../../language-reference/keywords/reference-types.md)  
  
- [Typy wartości](../../language-reference/keywords/value-types.md)  
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
