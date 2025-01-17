---
title: 'Instrukcje: dodawanie do lub usuwanie z kolekcji kontrolek w czasie wykonywania'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- run time [Windows Forms], removing controls
- controls [Windows Forms], adding using collections
- controls collections
- collections [Windows Forms], adding items
- run time [Windows Forms], adding controls
- controls [Windows Forms], removing using collections
ms.assetid: 771bf895-3d5f-469b-a324-3528f343657e
ms.openlocfilehash: 87ad4c957ac5b99438684d398a0c5ad7d126c406
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925044"
---
# <a name="how-to-add-to-or-remove-from-a-collection-of-controls-at-run-time"></a>Instrukcje: dodawanie do lub usuwanie z kolekcji kontrolek w czasie wykonywania
Typowe zadania związane z tworzeniem aplikacji to dodawanie kontrolek do i usuwanie kontrolek z dowolnych kontrolek kontenera w <xref:System.Windows.Forms.Panel> formularzach (takich jak lub <xref:System.Windows.Forms.GroupBox> kontrolka, a nawet do samego formularza). W czasie projektowania formanty mogą być przeciągane bezpośrednio do panelu lub pola grupy. W czasie wykonywania te kontrolki utrzymują `Controls` kolekcję, która śledzi umieszczanie na nich formantów.  
  
> [!NOTE]
> Poniższy przykład kodu ma zastosowanie do każdej kontrolki, która zachowuje kolekcję kontrolek.  
  
### <a name="to-add-a-control-to-a-collection-programmatically"></a>Aby programowo dodać kontrolkę do kolekcji  
  
1. Utwórz wystąpienie kontrolki, która ma zostać dodana.  
  
2. Ustaw właściwości nowej kontrolki.  
  
3. Dodaj kontrolkę do `Controls` kolekcji kontrolki nadrzędnej.  
  
     Poniższy przykład kodu pokazuje, jak utworzyć wystąpienie <xref:System.Windows.Forms.Button> kontrolki. Wymaga formularza z <xref:System.Windows.Forms.Panel> kontrolką i że metoda obsługi zdarzeń dla `NewPanelButton_Click`tworzonego przycisku już istnieje.  
  
    ```vb  
    Public NewPanelButton As New Button()  
  
    Public Sub AddNewControl()  
       ' The Add method will accept as a parameter any object that derives  
       ' from the Control class. In this case, it is a Button control.  
       Panel1.Controls.Add(NewPanelButton)  
       ' The event handler indicated for the Click event in the code   
       ' below is used as an example. Substite the appropriate event  
       ' handler for your application.  
       AddHandler NewPanelButton.Click, AddressOf NewPanelButton_Click  
    End Sub  
    ```  
  
    ```csharp  
    public Button newPanelButton = new Button();  
  
    public void addNewControl()  
    {   
       // The Add method will accept as a parameter any object that derives  
       // from the Control class. In this case, it is a Button control.  
       panel1.Controls.Add(newPanelButton);  
       // The event handler indicated for the Click event in the code   
       // below is used as an example. Substitute the appropriate event  
       // handler for your application.  
       this.newPanelButton.Click += new System.EventHandler(this. NewPanelButton_Click);  
    }  
    ```  
  
### <a name="to-remove-controls-from-a-collection-programmatically"></a>Aby programowo usunąć kontrolki z kolekcji  
  
1. Usuń procedurę obsługi zdarzeń ze zdarzenia. W Visual Basic, użyj słowa kluczowego [RemoveHandler instrukcji](../../../visual-basic/language-reference/statements/removehandler-statement.md) ; w C#programie Użyj [operatora-=](../../../csharp/language-reference/operators/subtraction-operator.md).  
  
2. Użyj metody, aby usunąć żądany formant z `Controls` kolekcji panelu. `Remove`  
  
3. Wywołaj <xref:System.Windows.Forms.Control.Dispose%2A> metodę, aby zwolnić wszystkie zasoby używane przez formant.  
  
    ```vb  
    Public Sub RemoveControl()  
    ' NOTE: The code below uses the instance of   
    ' the button (NewPanelButton) from the previous example.  
       If Panel1.Controls.Contains(NewPanelButton) Then  
          RemoveHandler NewPanelButton.Click, AddressOf _   
             NewPanelButton_Click  
          Panel1.Controls.Remove(NewPanelButton)  
          NewPanelButton.Dispose()  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void removeControl(object sender, System.EventArgs e)  
    {  
    // NOTE: The code below uses the instance of   
    // the button (newPanelButton) from the previous example.  
       if(panel1.Controls.Contains(newPanelButton))  
       {  
          this.newPanelButton.Click -= new System.EventHandler(this.   
             NewPanelButton_Click);  
          panel1.Controls.Remove(newPanelButton);  
          newPanelButton.Dispose();  
       }  
    }  
    ```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.Panel>
- [Panel, kontrolka](panel-control-windows-forms.md)
