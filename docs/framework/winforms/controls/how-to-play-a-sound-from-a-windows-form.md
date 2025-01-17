---
title: 'Instrukcje: odtwarzanie dźwięku za pomocą formularza systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- playing sounds [Windows Forms], Windows Forms
- sounds [Windows Forms], playing
- sounds
- My.Computer.Audio object [Windows Forms], playing sounds
- examples [Windows Forms], sounds
ms.assetid: 3d3350b7-1ebd-4e05-a738-48ca1160a19d
ms.openlocfilehash: 68a68f05b847877641132e540995f6b14bb6e065
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015800"
---
# <a name="how-to-play-a-sound-from-a-windows-form"></a>Instrukcje: odtwarzanie dźwięku za pomocą formularza systemu Windows
Ten przykład odtwarza dźwięk w danej ścieżce w czasie wykonywania.

## <a name="example"></a>Przykład

```vb
Sub PlaySimpleSound()
    My.Computer.Audio.Play("c:\Windows\Media\chimes.wav")
End Sub
```

```csharp
private void playSimpleSound()
{
    SoundPlayer simpleSound = new SoundPlayer(@"c:\Windows\Media\chimes.wav");
    simpleSound.Play();
}
```

## <a name="compiling-the-code"></a>Kompilowanie kodu
 Ten przykład wymaga:

- Zastąp nazwę `"c:\Windows\Media\chimes.wav"` pliku prawidłową nazwą pliku.

- (C#) Odwołanie do <xref:System.Media?displayProperty=nameWithType> przestrzeni nazw.

## <a name="robust-programming"></a>Niezawodne programowanie
 Operacje na plikach powinny być ujęte w obrębie odpowiednich bloków obsługi wyjątków strukturalnych.

 Następujące warunki mogą spowodować wyjątek:

- Nazwa ścieżki jest źle sformułowana. Na przykład zawiera niedozwolone znaki lub jest tylko białym znakiem (<xref:System.ArgumentException> Klasa).

- Ścieżka jest tylko do odczytu (<xref:System.IO.IOException> Klasa).

- Nazwa ścieżki to `null` (<xref:System.ArgumentNullException> Klasa).

- Nazwa ścieżki jest za długa (<xref:System.IO.PathTooLongException> Klasa).

- Ścieżka jest nieprawidłowa (<xref:System.IO.DirectoryNotFoundException> Klasa).

- Ścieżka ma tylko dwukropek, ":" (<xref:System.NotSupportedException> Klasa).

## <a name="net-framework-security"></a>Zabezpieczenia.NET Framework
 Nie należy podejmować decyzji dotyczących zawartości pliku na podstawie rozszerzenia nazwy pliku. Na przykład plik `Form1.vb` nie może być plikiem źródłowym Visual Basic. Sprawdź wszystkie dane wejściowe, zanim użyjesz danych w aplikacji.

## <a name="see-also"></a>Zobacz także

- <xref:System.Media.SoundPlayer>
- [Instrukcje: Asynchroniczne ładowanie dźwięku w formularzu systemu Windows](how-to-load-a-sound-asynchronously-within-a-windows-form.md)
