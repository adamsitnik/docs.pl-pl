---
title: 'Instrukcje: Zapisywanie tekstu do plików w języku Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], writing to
- text, writing to files
- writing to files [Visual Basic]
- examples [Visual Basic], text files
ms.assetid: 304956eb-530d-4df7-b48f-9b4d1f2581a0
ms.openlocfilehash: 7f9702469afbe9fdaa9bf727f5f70459ce884d6e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623279"
---
# <a name="how-to-write-text-to-files-in-visual-basic"></a>Instrukcje: Zapisywanie tekstu do plików w języku Visual Basic
<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> Metoda może służyć do zapisywanie tekstu do plików. Jeśli określony plik nie istnieje, zostanie utworzony.  
  
## <a name="procedure"></a>Procedura  
  
#### <a name="to-write-text-to-a-file"></a>Aby wpisać tekst w pliku  
  
- Użyj `WriteAllText` metodę, aby wpisać tekst do pliku, określając pliku i tekst do wyświetlenia. Ten przykład zapisuje linię `"This is new text."` pliku o nazwie `test.txt`, dodając tekst na wszelki istniejący tekst w pliku.  
  
     [!code-vb[VbFileIOWrite#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#3)]  
  
#### <a name="to-write-a-series-of-strings-to-a-file"></a>Do zapisu serii ciągów w pliku  
  
- W pętli poprzez kolekcji ciągów. Użyj `WriteAllText` metodę, aby wpisać tekst w pliku, określając pliku docelowego i parametry, które mają zostać dodane i ustawienie `append` do `True`.  
  
     Ten przykład Przepisuje nazwy plików w `Documents and Settings` do katalogu `FileList.txt`, wstawianie karetki zwracają między nimi w celu zwiększenia czytelności.  
  
     [!code-vb[VbFileIOWrite#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#4)]  
  
## <a name="robust-programming"></a>Niezawodne programowanie  
 Następujące warunki mogą spowodować wyjątek:  
  
- Ścieżka nie jest prawidłowa dla jednego z następujących przyczyn: jest to ciąg o zerowej długości, zawiera tylko znak odstępu, zawiera nieprawidłowe znaki lub jest ścieżką do urządzenia (rozpoczyna się od \\ \\.\\) (<xref:System.ArgumentException>).  
  
- Ścieżka jest nieprawidłowa, ponieważ jest on `Nothing` (<xref:System.ArgumentNullException>).  
  
- `File` Wskazuje ścieżkę, która nie istnieje (<xref:System.IO.FileNotFoundException> lub <xref:System.IO.DirectoryNotFoundException>).  
  
- Plik jest używany przez inny proces lub wystąpi błąd We/Wy (<xref:System.IO.IOException>).  
  
- Ścieżka przekracza maksymalną długość zdefiniowaną przez system (<xref:System.IO.PathTooLongException>).  
  
- Nazwa pliku lub katalogu w ścieżce zawiera dwukropek (:) lub jest w nieprawidłowym formacie (<xref:System.NotSupportedException>).  
  
- Użytkownik nie ma wystarczających uprawnień do wyświetlania ścieżki (<xref:System.Security.SecurityException>).  
  
- Dysk jest pełny i wywołanie `WriteAllText` zakończy się niepowodzeniem (<xref:System.IO.IOException>).  
  
 Jeśli używasz w kontekście częściowego zaufania, kod może zgłosić wyjątek ze względu na niewystarczające uprawnienia. Aby uzyskać więcej informacji, zobacz [podstawy zabezpieczeń dostępu kodu](../../../../framework/misc/code-access-security-basics.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- [Instrukcje: Odczyt z plików tekstowych](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files.md)
