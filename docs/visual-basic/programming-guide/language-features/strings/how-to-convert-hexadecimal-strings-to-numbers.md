---
title: 'Instrukcje: Konwertowanie ciągów szestnastkowych na numery (Visual Basic)'
ms.date: 01/31/2018
helpviewer_keywords:
- numbers [Visual Basic], hexadecimals
- hexadecimals [Visual Basic], decimals
- examples [Visual Basic], string conversion
- decimals [Visual Basic], hexadecimals
- string conversion [Visual Basic], hexadecimal to numbers
ms.assetid: 76675807-eadb-4c08-bd50-e6c6ff4b8ced
ms.openlocfilehash: ddb7b39f7a47234c003ca16e1d7ea013e113c108
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62054045"
---
# <a name="how-to-convert-hexadecimal-strings-to-numbers-visual-basic"></a>Instrukcje: Konwertowanie ciągów szestnastkowych na numery (Visual Basic)

Ten przykład konwertuje ciąg szesnastkowy do liczby całkowitej przy użyciu <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> metody.

## <a name="to-convert-a-hexadecimal-string-to-a-number"></a>Aby przekonwertować ciągu szesnastkowego na liczbę

- Użyj <xref:System.Convert.ToInt32(System.String,System.Int32)> metodę, aby przekonwertować numer wyrażone w base-16 na liczbę całkowitą.

  Pierwszy argument <xref:System.Convert.ToInt32(System.String,System.Int32)> metody jest ciąg do przekonwertowania. Drugi argument opisuje jakie podstawowa, liczba jest będzie wyrażana; szesnastkowa to podstawa 16.

  [!code-vb[VbVbalrStrings#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#62)]

- Należy zwrócić uwagę na to, że ciąg szesnastkowy ma następujące ograniczenia:

  - Nie może zawierać `&h` prefiks.
  - Nie może zawierać `_` separator cyfr.

  Jeśli prefiks lub separator cyfr jest obecna, wywołanie <xref:System.Convert.ToInt32(System.String,System.Int32)> metoda zgłasza wyjątek <xref:System.FormatException>.

## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType>
