---
title: 'Instrukcje: Tworzenie formularzy nadrzędnych MDI'
ms.date: 03/30/2017
helpviewer_keywords:
- parent forms
- MDI [Windows Forms], creating forms
ms.assetid: 12c71221-2377-4bb6-b10b-7b4b300fd462
ms.openlocfilehash: 2aa4261d6354f744f000f36a87e70a39f5c004ea
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211396"
---
# <a name="how-to-create-mdi-parent-forms"></a>Instrukcje: Tworzenie formularzy nadrzędnych MDI

> [!IMPORTANT]
> W tym temacie używany <xref:System.Windows.Forms.MainMenu> formant, który został zastąpiony przez <xref:System.Windows.Forms.MenuStrip> kontroli. <xref:System.Windows.Forms.MainMenu> Kontrolki została zachowana na potrzeby zgodności z poprzednimi wersjami i użycia w przyszłości, jeśli wybierzesz. Informacje o tworzeniu MDI nadrzędnego formularza za pomocą <xref:System.Windows.Forms.MenuStrip>, zobacz [jak: Tworzenie List okien MDI za pomocą elementu MenuStrip](../controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md).

Podstawą aplikacji interfejsu wielu dokumentów (MDI) jest formularza nadrzędnego MDI. Jest to formularz, który zawiera oknami podrzędnymi MDI, które są podrzędne windows, w którym użytkownik wchodzi w interakcję z aplikacją MDI. Tworzenie formularza nadrzędnego MDI jest łatwe, zarówno w programie Windows Forms Designer, jak i programowo.

## <a name="create-an-mdi-parent-form-at-design-time"></a>Tworzenie formularza nadrzędnego MDI w czasie projektowania

1. Utwórz projekt aplikacji Windows w programie Visual Studio.

2. W **właściwości** oknie <xref:System.Windows.Forms.Form.IsMdiContainer%2A> właściwości **true**.

     Określa formularza jako kontenera okien podrzędnych MDI.

    > [!NOTE]
    > Podczas ustawiania właściwości w **właściwości** okna, można również ustawić `WindowState` właściwości **Maximized**, jeśli chcesz, ponieważ jest najprostszym manipulować oknami podrzędnymi MDI, gdy formularz nadrzędny jest zmaksymalizowany. Ponadto należy pamiętać, że krawędzi formularza nadrzędnego MDI przejmą kolorów systemu (zestaw w Panelu sterowania systemu Windows), zamiast kolor tyłu można ustawić za pomocą <xref:System.Windows.Forms.Control.BackColor%2A?displayProperty=nameWithType> właściwości.

3. Z **przybornika**, przeciągnij **MenuStrip** formantu do formularza. Utwórz element menu najwyższego poziomu za pomocą **tekstu** właściwością **& plik** ze wskazaniem elementów podmenu **& nowe** i **i Zamknij**. Również utworzyć menu najwyższego poziomu elementu o nazwie **& okna**.

     Pierwszym menu spowoduje to utworzenie i ukrywanie elementów menu w czasie wykonywania, i drugiego menu będzie śledzenie otwarte okna podrzędnego MDI. Na tym etapie utworzono nadrzędnego okna MDI.

4. Naciśnij klawisz **F5** do uruchomienia aplikacji. Aby uzyskać informacje dotyczące tworzenia elementu podrzędnego MDI systemu windows, które działają w ramach formularza nadrzędnego MDI, zobacz [jak: Tworzenie formularzy podrzędnych MDI](how-to-create-mdi-child-forms.md).

## <a name="see-also"></a>Zobacz także

- [Aplikacje interfejsu wielu dokumentów (MDI)](multiple-document-interface-mdi-applications.md)
- [Instrukcje: Tworzenie formularzy podrzędnych MDI](how-to-create-mdi-child-forms.md)
- [Instrukcje: Określanie elementu podrzędnego Active MDI](how-to-determine-the-active-mdi-child.md)
- [Instrukcje: Wysyłanie danych do Active MDI Child](how-to-send-data-to-the-active-mdi-child.md)
- [Instrukcje: Aranżowanie formularzy podrzędnych MDI](how-to-arrange-mdi-child-forms.md)
