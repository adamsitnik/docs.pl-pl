---
title: 'Instrukcje: Kopiowanie katalogów'
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directory copying
- I/O [.NET Framework], copying directories
- subdirectory copying
- copying directories
- directories [.NET Framework], copying
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2a7fa901d887701e0fa41a0887b363adec07dba2
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644681"
---
# <a name="how-to-copy-directories"></a>Instrukcje: Kopiowanie katalogów
W tym temacie pokazano, jak używać klas we/wy synchronicznie skopiować zawartość katalogu do innej lokalizacji. 

Na przykład kopiowanie plików asynchronicznego Zobacz [asynchroniczne We/Wy pliku](../../../docs/standard/io/asynchronous-file-i-o.md). 

W tym przykładzie kopiuje podkatalogi, ustawiając `copySubDirs` z `DirectoryCopy` metody `true`. `DirectoryCopy` Rekursywnie metoda kopiuje podkatalogi poprzez wywołanie sam w poszczególnych podkatalogach, dopóki nie będą wyświetlane nie do skopiowania.  
  
## <a name="example"></a>Przykład  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.IO.FileInfo>
- <xref:System.IO.DirectoryInfo>
- <xref:System.IO.FileStream>
- [We/Wy plików i strumieni](../../../docs/standard/io/index.md)
- [Typowe zadania we/wy](../../../docs/standard/io/common-i-o-tasks.md)
- [Asynchroniczne We/Wy pliku](../../../docs/standard/io/asynchronous-file-i-o.md)
