---
title: TextFieldParser nie obsługuje tokenami komentarzy, które zawierają odstęp
ms.date: 07/20/2015
f1_keywords:
- vbrTextFieldParser_WhitespaceInToken
ms.assetid: 55107656-270e-4bbb-841a-478904df8e07
ms.openlocfilehash: af0f09bb7a8afc3b6e63cfab1a7176ba26cf20a6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64660897"
---
# <a name="textfieldparser-does-not-support-comment-tokens-that-contain-white-space"></a>TextFieldParser nie obsługuje tokenami komentarzy, które zawierają odstęp
Podano tokenu komentarz, który zawiera biały znak. `TextFieldParser` Nie obsługuje tokenami komentarzy, zawierające biały znak, chyba że biały występuje na początku tokenu. Biały znak pojawiają się na początku token jest ignorowany.  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Należy podać token prawidłowy komentarz.  
  
## <a name="see-also"></a>Zobacz także

- [Właściwość TextFieldParser.CommentTokens](xref:Microsoft.VisualBasic.FileIO.TextFieldParser.CommentTokens%2A)
- [Analizowanie plików tekstowych za pomocą obiektu TextFieldParser](../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)
- [TextFieldParser, obiekt](../../visual-basic/language-reference/objects/textfieldparser-object.md)
