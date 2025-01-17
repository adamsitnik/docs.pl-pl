---
title: Zła nazwa lub numer pliku
ms.date: 07/20/2015
f1_keywords:
- vbrID52
ms.assetid: d0e96aea-7621-48f6-a78b-5d37d18aaa4e
ms.openlocfilehash: 7a16e951030731bdcbb48b5fbb1a0d1881d5e1ec
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619391"
---
# <a name="bad-file-name-or-number"></a>Zła nazwa lub numer pliku
Wystąpił błąd podczas próby uzyskania dostępu do określonego pliku. Wśród możliwych przyczyn tego błędu są:  
  
- Oświadczenie odnosi się do pliku przy użyciu nazwy pliku lub numeru, który nie został określony w `FileOpen` instrukcji lub która została określona w `FileOpen` instrukcji, jednak podano wartość następnie zamknięty.  
  
- Oświadczenie odnosi się do pliku z numerem, który znajduje się poza zakresem numerów plików.  
  
- Oświadczenie odnosi się do nazwy pliku lub numer, który jest nieprawidłowy.  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
1. Upewnij się, że nazwa pliku jest określona w `FileOpen` instrukcji. Należy pamiętać, że po wywołaniu `FileClose` instrukcji bez argumentów, może przypadkowo zamknięto wszystkie otwarte pliki.  
  
2. Jeśli Twój kod generuje algorithmically liczby plików, upewnij się, że cyfry są prawidłowe.  
  
3. Sprawdź nazwy pliku, aby upewnić się, że są one zgodne z konwencjami systemu operacyjnego.  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>
- [Visual Basic — konwencje nazewnictwa](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
