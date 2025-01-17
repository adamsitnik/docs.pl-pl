---
title: 'Instrukcje: tworzenie pola tekstowego hasła za pomocą kontrolki TextBox formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- TextBox control [Windows Forms], entering passwords
- password boxes [Windows Forms], creating
- PasswordChar property in text boxes
- passwords [Windows Forms], input mask
- passwords [Windows Forms], password text box
ms.assetid: d105d6b9-3d50-44cd-80d8-2c0e2f486727
ms.openlocfilehash: 56391777c75db288c33d1b2192355be0df50f7ee
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046120"
---
# <a name="how-to-create-a-password-text-box-with-the-windows-forms-textbox-control"></a>Instrukcje: tworzenie pola tekstowego hasła za pomocą kontrolki TextBox formularzy systemu Windows

Pole hasła to Windows Forms pole tekstowe, które wyświetla znaki zastępcze, gdy użytkownik wpisze ciąg.

### <a name="to-create-a-password-text-box"></a>Aby utworzyć pole tekstowe hasła

1. <xref:System.Windows.Forms.TextBox.PasswordChar%2A> Ustaw właściwość <xref:System.Windows.Forms.TextBox> kontrolki na określony znak.

    <xref:System.Windows.Forms.TextBox.PasswordChar%2A> Właściwość określa znak wyświetlany w polu tekstowym. Na przykład, jeśli chcesz, aby gwiazdki były wyświetlane w polu hasło, określ * dla <xref:System.Windows.Forms.TextBox.PasswordChar%2A> właściwości w okno właściwości. Następnie, niezależnie od tego, jaki znak jest wpisany przez użytkownika w polu tekstowym, zostanie wyświetlona gwiazdka.

2. Obowiązkowe <xref:System.Windows.Forms.TextBoxBase.MaxLength%2A> Ustaw właściwość. Właściwość określa liczbę znaków, które można wpisać w polu tekstowym. W przypadku przekroczenia maksymalnej długości system emituje sygnał dźwiękowy, a pole tekstowe nie akceptuje więcej znaków. Zwróć uwagę, że nie chcesz tego robić, ponieważ maksymalna długość hasła może być używana przez hakerów próbujących złamać hasło.

    Poniższy przykład kodu pokazuje, jak zainicjować pole tekstowe, które akceptuje ciąg o długości do 14 znaków i wyświetla gwiazdki zamiast ciągu. `InitializeMyControl` Procedura nie zostanie wykonana automatycznie; musi być wywoływana.

    > [!IMPORTANT]
    > <xref:System.Windows.Forms.TextBox.PasswordChar%2A> Użycie właściwości w polu tekstowym może pomóc w zapewnieniu, że inne osoby nie będą mogły określić hasła użytkownika, jeśli zaobserwują użytkownika. Ta miara zabezpieczeń nie obejmuje żadnego rodzaju magazynu ani przesyłania hasła, które może wystąpić z powodu logiki aplikacji. Ponieważ wprowadzony tekst nie jest w żaden sposób szyfrowany, należy go traktować tak jak wszystkie inne poufne dane. Mimo że nie jest on wyświetlany jako taki, hasło jest nadal traktowane jako ciąg tekstowy (chyba że zaimplementowano dodatkową miarę zabezpieczeń).

    ```vb
    Private Sub InitializeMyControl()
       ' Set to no text.
       TextBox1.Text = ""
       ' The password character is an asterisk.
       TextBox1.PasswordChar = "*"
       ' The control will allow no more than 14 characters.
       TextBox1.MaxLength = 14
    End Sub
    ```

    ```csharp
    private void InitializeMyControl()
    {
       // Set to no text.
       textBox1.Text = "";
       // The password character is an asterisk.
       textBox1.PasswordChar = '*';
       // The control will allow no more than 14 characters.
       textBox1.MaxLength = 14;
    }
    ```

    ```cpp
    private:
       void InitializeMyControl()
       {
          // Set to no text.
          textBox1->Text = "";
          // The password character is an asterisk.
          textBox1->PasswordChar = '*';
          // The control will allow no more than 14 characters.
          textBox1->MaxLength = 14;
       }
    ```

## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.TextBox>
- [TextBox, kontrolka — omówienie](textbox-control-overview-windows-forms.md)
- [Instrukcje: Kontrolowanie punktu wstawiania w kontrolce TextBox Windows Forms](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [Instrukcje: Tworzenie pola tekstowego tylko do odczytu](how-to-create-a-read-only-text-box-windows-forms.md)
- [Instrukcje: Umieszczanie cudzysłowu w ciągu](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [Instrukcje: Zaznacz tekst w kontrolce TextBox Windows Forms](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [Instrukcje: Wyświetl wiele wierszy w kontrolce TextBox Windows Forms](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox, kontrolka](textbox-control-windows-forms.md)
