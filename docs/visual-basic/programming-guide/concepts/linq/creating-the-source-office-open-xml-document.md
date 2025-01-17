---
title: Tworzenie źródłowego dokumentu Office Open XML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 61ccd6fb-0c47-4075-afdf-5b5021330f21
ms.openlocfilehash: 75030f3d1c2940cc84f81b85dca921497137439f
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2019
ms.locfileid: "71352946"
---
# <a name="creating-the-source-office-open-xml-document-visual-basic"></a>Tworzenie źródłowego dokumentu Office Open XML (Visual Basic)
W tym temacie przedstawiono sposób tworzenia dokumentu Office Open XML WordprocessingML, który jest używany przez inne przykłady w tym samouczku. Jeśli wykonasz te instrukcje, dane wyjściowe będą zgodne z danymi wyjściowymi podanymi w każdym przykładzie.  
  
 Jednak przykłady w tym samouczku będą działały z dowolnym prawidłowym dokumentem WordprocessingML.  
  
 Aby utworzyć dokument, który jest wykorzystywany przez ten samouczek, musisz mieć zainstalowany Microsoft Office 2007 lub nowszy lub mieć Microsoft Office 2003 z pakietem zgodności Microsoft Office dla formatów plików programów Word, Excel i PowerPoint 2007.  
  
## <a name="creating-the-wordprocessingml-document"></a>Tworzenie dokumentu WordprocessingML  
  
#### <a name="to-create-the-wordprocessingml-document"></a>Aby utworzyć dokument WordprocessingML  
  
1. Utwórz nowy dokument programu Microsoft Word.  
  
2. Wklej następujący tekst do nowego dokumentu:  
  
    ```text  
    Parsing WordprocessingML with LINQ to XML  
  
    The following example prints to the console.  
  
    Imports System  
  
    Class Program  
        Public Shared  Sub Main(ByVal args() As String)  
            Console.WriteLine("Hello World")  
        End Sub  
    End Class  
  
    This example produces the following output:  
  
    Hello World  
    ```  
  
3. Sformatuj pierwszy wiersz za pomocą stylu "Nagłówek 1".  
  
4. Wybierz wiersze, które zawierają kod Visual Basic. Pierwszy wiersz rozpoczyna się od słowa kluczowego `Imports`. Ostatnim wierszem jest "End Class". Sformatuj linie przy użyciu czcionki Courier. Sformatuj je przy użyciu nowego stylu i nazwij nowy styl "Code".  
  
5. Na koniec zaznacz cały wiersz zawierający dane wyjściowe i sformatuj go przy użyciu stylu `Code`.  
  
6. Zapisz dokument i nadaj mu nazwę SampleDoc. docx.  
  
    > [!NOTE]
    > Jeśli używasz programu Microsoft Word 2003, wybierz pozycję **dokument programu Word 2007** na liście rozwijanej **Zapisz jako typ** .  
  
## <a name="see-also"></a>Zobacz także

- [Samouczek: Manipulowanie zawartością w dokumencie WordprocessingML (Visual Basic) ](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
