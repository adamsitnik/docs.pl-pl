---
ms.openlocfilehash: e613f0c52c77efebf250f5935d5cbfc29bc09a6b
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802539"
---
### <a name="wpf-printing-stack-update"></a>Aktualizację stosu drukowanie WPF

|   |   |
|---|---|
|Szczegóły|Za pomocą drukowanie interfejsów API firmy WPF <xref:System.Printing.PrintQueue?displayProperty=name> teraz wywołania interfejsu API pakietu dokument Drukuj okna na rzecz teraz przestarzałe API drukowanie plików XPS. Zmiana została wprowadzona przy użyciu użytkowanie pamiętać; Użytkownicy ani deweloperzy nie powinny zostać wyświetlone wszelkie zmiany w zachowanie lub użycie interfejsu API. Nowy stos drukowania jest domyślnie włączona, podczas uruchamiania w systemie Windows 10 Creators Update. Stary stosu drukowania będą nadal działać tak jak wcześniej w starszych wersjach Windows.|
|Sugestia|Aby użyć starego stosu w aktualizacji systemu Windows 10 dla twórców, ustaw <code>UseXpsOMPrinting</code> wartości REG_DWORD <code>HKEY_CURRENT_USER\Software\Microsoft\.NETFramework\Windows Presentation Foundation\Printing</code> klucza rejestru w celu <code>1</code>.|
|Scope|Krawędź|
|Wersja|4.7|
|Typ|Środowisko uruchomieniowe|

