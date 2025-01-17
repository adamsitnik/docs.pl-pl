---
title: OpenFileDialog — Informacje o składniku (Formularze systemu Windows)
ms.date: 03/30/2017
f1_keywords:
- OpenFileDialog
helpviewer_keywords:
- OpenFileDialog component [Windows Forms], about OpenFileDialog
- Open File dialog box [Windows Forms], displaying in Windows Forms
ms.assetid: cd717300-46b6-4f82-8207-b218fa7fa407
ms.openlocfilehash: 24327ded50ac927642e2687b40b1f10de9bdf41e
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211700"
---
# <a name="openfiledialog-component-overview-windows-forms"></a>OpenFileDialog — Informacje o składniku (Formularze systemu Windows)

Formularze Windows <xref:System.Windows.Forms.OpenFileDialog> składnik to wstępnie skonfigurowane okno dialogowe. Jest to ta sama **Otwórz plik** okno dialogowe ujawnione przez system operacyjny Windows. Dziedziczy <xref:System.Windows.Forms.CommonDialog> klasy.

## <a name="use-this-component"></a>Użyj tego składnika

Na użytek ten składnik w swojej aplikacji z systemem Windows jako proste rozwiązanie Wybieranie pliku audytów Konfigurowanie własnego okno dialogowe. Opierając się na standardowych okien dialogowych Windows, możesz tworzyć aplikacje, w których podstawowych funkcji jest natychmiast dobrze znanym użytkownikom. Należy jednak pamiętać, że w przypadku przy użyciu <xref:System.Windows.Forms.OpenFileDialog> składnik, należy napisać własną logiką otwarcia pliku.

Użyj <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> metodę, aby wyświetlić okno dialogowe w czasie wykonywania. Możesz umożliwić użytkownikom wybór wielokrotny pliki można otworzyć za pomocą <xref:System.Windows.Forms.OpenFileDialog.Multiselect%2A> właściwości. Ponadto można użyć <xref:System.Windows.Forms.OpenFileDialog.ShowReadOnly%2A> właściwości w celu określenia, jeśli pole wyboru tylko do odczytu, pojawi się w oknie dialogowym. <xref:System.Windows.Forms.OpenFileDialog.ReadOnlyChecked%2A> Właściwość wskazuje, czy zaznaczono pole wyboru tylko do odczytu. Na koniec <xref:System.Windows.Forms.FileDialog.Filter%2A> właściwość ustawia bieżący ciągu nazwy pliku filtru, który określa opcje, które są wyświetlane w polu "Typy plików" w oknie dialogowym.

Gdy zostanie dodany do formularza, <xref:System.Windows.Forms.OpenFileDialog> składnika, który pojawia się na pasku w dolnej części projektanta Windows Forms w programie Visual Studio.

## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.OpenFileDialog>
- [OpenFileDialog, składnik](openfiledialog-component-windows-forms.md)
