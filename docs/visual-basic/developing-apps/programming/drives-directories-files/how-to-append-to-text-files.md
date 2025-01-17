---
title: 'Instrukcje: Łączenie się plikami tekstowymi w Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [Visual Basic], appending to files
- I/O [Visual Basic], My.Computer.FileSystem.WriteAllText method
- I/O [Visual Basic], WriteAllText method
ms.assetid: bbbd7fb5-f169-41a9-b53f-520ea9613913
ms.openlocfilehash: e855293ac3636049520a85abdf685091d437bb60
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64628906"
---
# <a name="how-to-append-to-text-files-in-visual-basic"></a>Instrukcje: Łączenie się plikami tekstowymi w Visual Basic
<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> Metoda może służyć do dołączenia do pliku tekstowego, określając, który `append` parametr ma wartość `True`.  
  
### <a name="to-append-to-a-text-file"></a>Aby dołączyć do pliku tekstowego  
  
- Użyj `WriteAllText` metody, określając pliku docelowego i ciąg do dołączenia i ustawienie `append` parametr `True`.  
  
     Ten przykład Przepisuje ciąg `"This is a test string."` pliku o nazwie `Testfile.txt`.  
  
     [!code-vb[VbFileIOWrite#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#6)]  
  
## <a name="robust-programming"></a>Niezawodne programowanie  
 Następujące warunki mogą spowodować wyjątek:  
  
- Ścieżka nie jest prawidłowa dla jednego z następujących przyczyn: jest to ciąg o zerowej długości, zawiera tylko znak odstępu, zawiera nieprawidłowe znaki lub jest ścieżką do urządzenia (rozpoczyna się od \\ \\.\\) (<xref:System.ArgumentException>).  
  
- Ścieżka jest nieprawidłowa, ponieważ jest on `Nothing` (<xref:System.ArgumentNullException>).  
  
- `File` Wskazuje ścieżkę, która nie istnieje (<xref:System.IO.FileNotFoundException> lub <xref:System.IO.DirectoryNotFoundException>).  
  
- Plik jest używany przez inny proces lub wystąpi błąd We/Wy (<xref:System.IO.IOException>).  
  
- Ścieżka przekracza maksymalną długość zdefiniowaną przez system (<xref:System.IO.PathTooLongException>).  
  
- Nazwa pliku lub katalogu w ścieżce zawiera dwukropek (:) lub jest w nieprawidłowym formacie (<xref:System.NotSupportedException>).  
  
- Użytkownik nie ma wystarczających uprawnień do wyświetlania ścieżki (<xref:System.Security.SecurityException>).  
  
## <a name="see-also"></a>Zobacz także

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- [Zapisywanie w plikach](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)
