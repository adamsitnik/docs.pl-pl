---
title: Zły tryb pliku
ms.date: 07/20/2015
f1_keywords:
- vbrID54
ms.assetid: 74891e96-884b-4c8d-872d-cd11ae272372
ms.openlocfilehash: 9a59faf1b6f845858e36efcabdf0758e41ad75dc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619746"
---
# <a name="bad-file-mode"></a>Zły tryb pliku
Instrukcje używane w manipulowanie zawartością pliku musi być zgodna z trybem, w którym plik został otwarty. Możliwe przyczyny:  
  
- A `FilePutObject` lub `FileGetObject` instrukcja Określa kolejny plik.  
  
- A `Print` instrukcja Określa plik, który został otwarty w trybie dostępu innych niż `Output` lub `Append`.  
  
- `Input` Instrukcja Określa plik, który został otwarty inny niż tryb dostępu `Input`  
  
- Próba zapisu do plików tylko do odczytu.  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Upewnij się, że `FilePutObject` i `FileGetObject` odnoszą się tylko do plików otwartych do `Random` lub `Binary` dostępu.  
  
- Upewnij się, że `Print` Określa plik, który został otwarty albo `Output` lub `Append` tryb dostępu. W przeciwnym razie użyj innej instrukcji, aby umieścić dane w pliku, lub ponownie otworzyć plik w odpowiedni tryb.  
  
- Upewnij się, że `Input` Określa plik, który został otwarty `Input`. W przeciwnym razie użyj innej instrukcji, aby umieścić dane w pliku lub ponownie otworzyć plik w odpowiedni tryb.  
  
- Jeśli piszesz w pliku tylko do odczytu, Zmień stan odczytu/zapisu pliku lub nie należy próbować zapisanie w nim.  
  
- Użyj funkcji dostępnych w `My.Computer.FileSystem` obiektu.  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.FileSystem>
- [Rozwiązywanie problemów: Odczytywanie z oraz zapisywanie w plikach tekstowych](../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
