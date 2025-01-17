---
title: 'Instrukcje: zapisywanie plików za pomocą kontrolki RichTextBox formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- saving files
- RTF files [Windows Forms], saving in RichTextBox control
- examples [Windows Forms], text boxes
- saving files [Windows Forms], RichTextBox control
- files [Windows Forms], saving with RichTextBox control
- RichTextBox control [Windows Forms], saving files
- .rtf files [Windows Forms], saving in RichTextBox control
- text files [Windows Forms], saving from RichTextBox control
ms.assetid: 4a58ec19-84d1-4383-9110-298c06adcfca
ms.openlocfilehash: c5d88e4942d96ee12e8b9f40156090c874386668
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046266"
---
# <a name="how-to-save-files-with-the-windows-forms-richtextbox-control"></a>Instrukcje: zapisywanie plików za pomocą kontrolki RichTextBox formularzy systemu Windows

Formant Windows Forms <xref:System.Windows.Forms.RichTextBox> może zapisywać informacje wyświetlane w jednym z kilku formatów:

- Zwykły tekst

- Zwykły tekst Unicode

- Format tekstu sformatowanego (RTF)

- RTF z miejscami zamiast obiektów OLE

- Zwykły tekst z reprezentacją tekstową obiektów OLE

Aby zapisać plik, wywołaj <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> metodę. Możesz również użyć metody **SaveFile** , aby zapisać dane w strumieniu. Aby uzyskać więcej informacji, zobacz <xref:System.Windows.Forms.RichTextBox.SaveFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>.

### <a name="to-save-the-contents-of-the-control-to-a-file"></a>Aby zapisać zawartość kontrolki do pliku

1. Określ ścieżkę pliku, który ma zostać zapisany.

    Aby to zrobić w aplikacji w świecie rzeczywistym, zazwyczaj używany jest <xref:System.Windows.Forms.SaveFileDialog> składnik. Aby zapoznać się z omówieniem, zobacz [Omówienie składnika SaveFileDialog](savefiledialog-component-overview-windows-forms.md).

2. Wywołaj <xref:System.Windows.Forms.RichTextBox> metodę kontrolki, określając plik do zapisania i opcjonalnie typ pliku. <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> W przypadku wywołania metody z nazwą pliku jako jedynego argumentu, plik zostanie zapisany w formacie RTF. Aby określić inny typ pliku, wywołaj metodę z wartością <xref:System.Windows.Forms.RichTextBoxStreamType> wyliczenia jako jej drugi argument.

    W poniższym przykładzie ścieżką ustawioną dla lokalizacji pliku tekstu sformatowanego jest folder **Moje dokumenty** . Ta lokalizacja jest używana, ponieważ można założyć, że większość komputerów z systemem operacyjnym Windows będzie zawierać ten folder. Wybranie tej lokalizacji pozwala również użytkownikom z minimalnymi poziomami dostępu do systemu w celu bezpiecznego uruchomienia aplikacji. W poniższym przykładzie założono, że formularz <xref:System.Windows.Forms.RichTextBox> z kontrolką został już dodany.

    ```vb
    Public Sub SaveFile()
       ' You should replace the bold file name in the
       ' sample below with a file name of your own choosing.
       RichTextBox1.SaveFile(System.Environment.GetFolderPath _
       (System.Environment.SpecialFolder.Personal) _
       & "\Testdoc.rtf", _
          RichTextBoxStreamType.RichNoOleObjs)
    End Sub
    ```

    ```csharp
    public void SaveFile()
    {
       // You should replace the bold file name in the
       // sample below with a file name of your own choosing.
       // Note the escape character used (@) when specifying the path.
       richTextBox1.SaveFile(System.Environment.GetFolderPath
       (System.Environment.SpecialFolder.Personal)
       + @"\Testdoc.rtf",
          RichTextBoxStreamType.RichNoOleObjs);
    }
    ```

    ```cpp
    public:
       void SaveFile()
       {
          // You should replace the bold file name in the
          // sample below with a file name of your own choosing.
          richTextBox1->SaveFile(String::Concat
             (System::Environment::GetFolderPath
             (System::Environment::SpecialFolder::Personal),
             "\\Testdoc.rtf"), RichTextBoxStreamType::RichNoOleObjs);
       }
    ```

    > [!IMPORTANT]
    > Ten przykład tworzy nowy plik, jeśli plik jeszcze nie istnieje. Jeśli aplikacja musi utworzyć plik, aplikacja musi mieć dostęp do tego folderu. Uprawnienia są ustawiane przy użyciu list kontroli dostępu. Jeśli plik już istnieje, aplikacja musi mieć tylko uprawnienia do zapisu, które ma mniejsze uprawnienia. Jeśli to możliwe, bezpieczniejsze jest tworzenie pliku podczas wdrażania i udzielanie dostępu do odczytu tylko do jednego pliku, a nie tworzenie dostępu do folderu. Ponadto bardziej bezpieczne jest zapisanie danych do folderów użytkowników niż folder główny lub folder Program Files.

## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.RichTextBox.SaveFile%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox, kontrolka](richtextbox-control-windows-forms.md)
- [Kontrolki do użycia w formularzach Windows Forms](controls-to-use-on-windows-forms.md)
