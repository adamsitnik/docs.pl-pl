---
title: Sprawdzanie poprawności złożoności haseł (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- String data type [Visual Basic], validation
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
ms.openlocfilehash: ff0ac933be917b5604966240ff1fbd331a34ba77
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64663626"
---
# <a name="walkthrough-validating-that-passwords-are-complex-visual-basic"></a>Przewodnik: Sprawdzanie poprawności hasła złożoności (Visual Basic)
Ta metoda sprawdza, czy niektóre cechy silnego hasła i aktualizuje jako parametr ciągu przy użyciu informacji o tym, które sprawdza, czy hasła nie powiodło się.  
  
 Hasła mogą być wykorzystywane w bezpieczny system do autoryzacji użytkownika. Jednak musi być trudne dla nieautoryzowanych użytkowników w celu odgadnięcia hasła. Osoby atakujące mogą wykorzystać *atak słownikowy* program, który wykonuje iterację przez wszystkie wyrazy w słowniku (lub słowniki wielu w różnych językach) i sprawdza, czy dowolny wyraz działać jako hasło tego użytkownika. Szybko można złamać słabe hasła, takie jak "Yankees" lub "Mustang". Silniejszych haseł, takich jak "? Użytkownik "L1N3vaFiNdMeyeP@sSWerd!", są znacznie mniej prawdopodobne złamać. System chronionych hasłem należy upewnić się, że użytkownicy wybierać silne hasła.  
  
 Silne hasło jest złożony (zawierającego kombinację wielkie litery, małe litery, cyfry i znaki specjalne) i nie jest wyrazem. W tym przykładzie pokazano, jak sprawdzić, co do złożoności.  
  
## <a name="example"></a>Przykład  
  
### <a name="code"></a>Kod  
 [!code-vb[VbVbcnRegEx#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#1)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Wywołaj tę metodę, przekazując ciąg, który zawiera to hasło.  
  
 Ten przykład wymaga:  
  
- Dostęp do elementów członkowskich <xref:System.Text.RegularExpressions> przestrzeni nazw. Dodaj `Imports` instrukcji, jeśli użytkownik są nie pełni kwalifikujących się nazwy elementów członkowskich w kodzie. Aby uzyskać więcej informacji, zobacz [Importy — instrukcja (.NET Namespace i Type)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
## <a name="security"></a>Zabezpieczenia  
 Jeśli przenosisz hasła przez sieć, należy użyć metody bezpiecznego przesyłania danych. Aby uzyskać więcej informacji, zobacz [zabezpieczenia aplikacji sieci Web platformy ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/330a99hc(v=vs.100)).
  
 Można zwiększyć dokładność `ValidatePassword` funkcja poprzez dodanie dodatkowej złożoności kontroli:  
  
- Porównaj hasło i jego podciągów przed nazwę użytkownika, identyfikator użytkownika i słownika zdefiniowanego przez aplikację. Ponadto należy traktować podobnych znaków jako równoważne podczas przeprowadzania porównania. Na przykład zaliczenie litery "l" i "e" odpowiednikiem cyfry "1" i "3".  
  
- Jeśli ma tylko jedną wielką literę, upewnij się, że nie jest pierwszym znakiem hasła.  
  
- Upewnij się, że ostatnich dwóch znaków hasła są znaki.  
  
- Nie zezwalaj na hasła, w których wszystkie symbole są wprowadzane z klawiatury w górnym wierszu.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Text.RegularExpressions.Regex>
- [Zabezpieczenia aplikacji sieci Web platformy ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/330a99hc(v=vs.100))
