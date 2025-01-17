---
title: ColorDialog — Informacje o składniku (Formularze systemu Windows)
ms.date: 03/30/2017
f1_keywords:
- ColorDialog
helpviewer_keywords:
- color dialog box [Windows Forms], about color dialog box
- ColorDialog component [Windows Forms], about ColorDialog
ms.assetid: 6dbdd8f0-f697-4728-bb09-7ea156f6d800
ms.openlocfilehash: 284d42218fb4fbce873325b1e45c883d51eefab8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956341"
---
# <a name="colordialog-component-overview-windows-forms"></a>ColorDialog — Informacje o składniku (Formularze systemu Windows)
Formularze Windows <xref:System.Windows.Forms.ColorDialog> składnik to wstępnie skonfigurowane okno dialogowe, które pozwala użytkownikowi wybrać kolor z palety i dodać kolorów niestandardowych do tej palety. Jest to ten sam okno dialogowe, które pojawi się w innych aplikacji opartych na Windows do wybierania kolorów. Użyj go w ramach aplikacji opartych na Windows jako proste rozwiązanie audytów Konfigurowanie własnego okno dialogowe.  
  
 Kolor wybrany w oknie dialogowym są zwracane w <xref:System.Windows.Forms.ColorDialog.Color%2A> właściwości. Jeśli <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> właściwość jest ustawiona na `false`, przycisk "Definiowanie kolorów niestandardowych" jest wyłączona, a użytkownik jest ograniczone do wstępnie zdefiniowanych kolorów palety. Jeśli <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> właściwość jest ustawiona na `true`, użytkownik może wybrać kolory szarych. Aby wyświetlić okno dialogowe, należy wywołać jej <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> metody.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.ColorDialog>
- [ColorDialog, składnik](colordialog-component-windows-forms.md)
- [Kontrolki i składniki okien dialogowych](dialog-box-controls-and-components-windows-forms.md)
- [Instrukcje: Zmienianie wyglądu składnika ColorDialog formularzy Windows](how-to-change-the-appearance-of-the-windows-forms-colordialog-component.md)
