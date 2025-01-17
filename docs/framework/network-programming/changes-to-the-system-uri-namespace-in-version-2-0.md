---
title: Zmiany w przestrzeni nazw System.Uri w wersji 2.0
ms.date: 03/30/2017
ms.assetid: 35883fe9-2d09-4d8b-80ca-cf23a941e459
ms.openlocfilehash: 987010b8367069e8089df3f809d23f258bb68f2b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61642766"
---
# <a name="changes-to-the-systemuri-namespace-in-version-20"></a>Zmiany w przestrzeni nazw System.Uri w wersji 2.0

Wprowadzono kilka zmian <xref:System.Uri?displayProperty=nameWithType> klasy. Te zmiany stałej nieprawidłowe zachowanie, rozszerzone użyteczność i lepsze zabezpieczenia.

## <a name="obsolete-and-deprecated-members"></a>Elementy członkowskie przestarzała i przestarzałe

 Konstruktory:

- Wszystkie konstruktory, które mają `dontEscape` parametru.

 Metody:

- <xref:System.Uri.CheckSecurity%2A>

- <xref:System.Uri.Escape%2A>

- <xref:System.Uri.Canonicalize%2A>

- <xref:System.Uri.Parse%2A>

- <xref:System.Uri.IsReservedCharacter%2A>

- <xref:System.Uri.IsBadFileSystemCharacter%2A>

- <xref:System.Uri.IsExcludedCharacter%2A>

- <xref:System.Uri.EscapeString%2A>

## <a name="changes"></a>Zmiany

- Dla schematów identyfikator URI, które nie mają części kwerendy (plik, ftp i inne) "?" znak jest zawsze poprzedzone znakiem zmiany znaczenia i nie jest uważany za początku <xref:System.Uri.Query%2A> części.

- Niejawne pliku identyfikatorów URI (w postaci `c:\directory\file@name.txt`), znaku fragmentu ("#") jest zawsze poprzedzone znakiem zmiany znaczenia, chyba że wymagane są pełne unescaping lub <xref:System.Uri.LocalPath%2A> jest `true`.

- Obsługa hostname UNC została usunięta; przyjęto Specyfikacja IDN, reprezentujący międzynarodowych nazw hostów.

- <xref:System.Uri.LocalPath%2A> zawsze zwraca ciąg całkowicie o niezmienionym znaczeniu.

- <xref:System.Uri.ToString%2A> nie unescape o zmienionym znaczeniu '%', '?', lub znaku "#".

- <xref:System.Uri.Equals%2A> zawiera teraz <xref:System.Uri.Query%2A> wchodzi w skład w sprawdzanie równości.

- Operatory "=="i"! =" zastąpione i połączony z <xref:System.Uri.Equals%2A> metody.

- <xref:System.Uri.IsLoopback%2A> teraz tworzy spójne wyniki.

- Identyfikator URI "`file:///path`" nie jest już przetłumaczyć `file://path`.

- "#" teraz jest rozpoznawana jako terminatora nazwy hosta. Oznacza to, że `http://contoso.com#fragment` teraz jest konwertowany na `http://contoso.com/#fragment`.

- Błąd podczas łączenia podstawowy identyfikator URI z fragmentem został rozwiązany.

- Błąd w <xref:System.Uri.HostNameType%2A> został rozwiązany.

- Naprawiono usterkę podczas analizowania NNTP.

- Identyfikator URI w postaci HTTP:contoso.com teraz zgłasza wyjątek podczas analizowania.

- Struktura poprawnie przetwarza informacje o użytkowniku w identyfikatorze URI.

- Kompresja ścieżki identyfikatora URI jest stała, tak, aby uszkodzone URI nie może przechodzić przez system plików powyżej katalogu głównego.

## <a name="see-also"></a>Zobacz także

- <xref:System.Uri?displayProperty=nameWithType>
