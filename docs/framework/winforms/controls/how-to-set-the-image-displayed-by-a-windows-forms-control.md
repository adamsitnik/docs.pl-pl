---
title: 'Instrukcje: ustawianie obrazu wyświetlanego przez kontrolkę formularzy systemu Windows'
ms.date: 08/20/2019
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Button control [Windows Forms], images
- Windows Forms controls, images
- controls [Windows Forms], images
- images [Windows Forms], Windows Forms controls
- examples [Windows Forms], controls
ms.assetid: 9445af8f-4f62-48b0-a3f6-068058964b9f
ms.openlocfilehash: b1b1dbbb50c3b19cf8d8a7d7030d0bc168afb6a7
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666188"
---
# <a name="how-to-set-the-image-displayed-by-a-windows-forms-control"></a>Instrukcje: Ustawianie obrazu wyświetlanego przez kontrolkę Windows Forms

Kilka kontrolek Windows Forms może wyświetlać obrazy. Te obrazy mogą być ikonami, które wyjaśniają przeznaczenie kontrolki, na przykład ikona dyskietki na przycisku oznaczającego polecenie Zapisz. Alternatywnie, ikony mogą być obrazami tła, aby nadać formantowi wygląd i zachowanie.

## <a name="programmatic"></a>Program

Ustaw kontrolkę `Image` lub `BackgroundImage` właściwość na obiekt typu <xref:System.Drawing.Image>. Ogólnie rzecz biorąc, zostanie załadowany obraz z pliku za pomocą <xref:System.Drawing.Image.FromFile%2A> metody.

W poniższym przykładzie kodu ścieżka ustawiona dla lokalizacji obrazu jest folderem **Moje obrazy** . Większość komputerów z systemem operacyjnym Windows zawiera ten katalog. Dzięki temu użytkownicy mający minimalne poziomy dostępu do systemu mogą bezpiecznie uruchamiać aplikację. Poniższy przykład kodu wymaga, aby formularz z <xref:System.Windows.Forms.PictureBox> dodaną kontrolką został już dodany.

```vb
' Replace the image named below with your own icon.
PictureBox1.Image = Image.FromFile _
   (System.Environment.GetFolderPath _
   (System.Environment.SpecialFolder.MyPictures) _
   & "\Image.gif")
```

```csharp
// Replace the image named below with your own icon.
// Note the escape character used (@) when specifying the path.
pictureBox1.Image = Image.FromFile
   (System.Environment.GetFolderPath
   (System.Environment.SpecialFolder.MyPictures)
   + @"\Image.gif");
```

```cpp
// Replace the image named below with your own icon.
pictureBox1->Image = Image::FromFile(String::Concat
   (System::Environment::GetFolderPath
   (System::Environment::SpecialFolder::MyPictures),
   "\\Image.gif"));
```

## <a name="designer"></a>Projektant

1. W oknie **Właściwości** programu Visual Studio zaznacz właściwość **obraz** lub **BackgroundImage** kontrolki, a następnie wybierz wielokropek (![przycisk wielokropka w programie Visual Studio](./media/visual-studio-ellipsis-button.png)), aby wyświetlić **zaznaczenie** Okno dialogowe zasobów.

2. Wybierz obraz, który chcesz wyświetlić.

## <a name="see-also"></a>Zobacz także

- <xref:System.Drawing.Image.FromFile%2A>
- <xref:System.Drawing.Image>
- <xref:System.Windows.Forms.Control.BackgroundImage%2A>
