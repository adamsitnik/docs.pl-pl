---
title: 'Instrukcje: dodawanie i usuwanie kart za pomocą kontrolki TabControl formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tabs [Windows Forms], removing from pages
- TabPage control
- TabControl control [Windows Forms], adding and removing tabs
- tabs [Windows Forms], adding to pages
- tab pages
ms.assetid: 66d4dfca-41e8-44e3-9c80-fb7ac4cb1619
ms.openlocfilehash: 938f1210eaa3479822e752327123737a3286fe9a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64624056"
---
# <a name="how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol"></a>Instrukcje: dodawanie i usuwanie kart za pomocą kontrolki TabControl formularzy systemu Windows
Domyślnie <xref:System.Windows.Forms.TabControl> kontrolka zawiera dwa <xref:System.Windows.Forms.TabPage> kontrolki. Możesz uzyskać dostęp tych kartach za pośrednictwem <xref:System.Windows.Forms.TabControl.TabPages%2A> właściwości.  
  
### <a name="to-add-a-tab-programmatically"></a>Aby programowo dodać kartę  
  
- Użyj <xref:System.Windows.Forms.TabControl.TabPageCollection.Add%2A> metody <xref:System.Windows.Forms.TabControl.TabPages%2A> właściwości.  
  
    ```vb  
    Dim myTabPage As New TabPage()  
    myTabPage.Text = "TabPage" & (TabControl1.TabPages.Count + 1)  
    TabControl1.TabPages.Add(myTabPage)  
    ```  
  
    ```csharp  
    string title = "TabPage " + (tabControl1.TabCount + 1).ToString();  
    TabPage myTabPage = new TabPage(title);  
    tabControl1.TabPages.Add(myTabPage);  
    ```  
  
    ```cpp  
    String^ title = String::Concat("TabPage ",  
       (tabControl1->TabCount + 1).ToString());  
    TabPage^ myTabPage = gcnew TabPage(title);  
    tabControl1->TabPages->Add(myTabPage);  
    ```  
  
### <a name="to-remove-a-tab-programmatically"></a>Aby usunąć kartę programowe  
  
- Aby usunąć wybrane karty, użyj <xref:System.Windows.Forms.TabControl.TabPageCollection.Remove%2A> metody <xref:System.Windows.Forms.TabControl.TabPages%2A> właściwości.  
  
     —lub—  
  
- Aby usunąć wszystkie karty, użyj <xref:System.Windows.Forms.TabControl.TabPageCollection.Clear%2A> metody <xref:System.Windows.Forms.TabControl.TabPages%2A> właściwości.  
  
    ```vb  
    ' Removes the selected tab:  
    TabControl1.TabPages.Remove(TabControl1.SelectedTab)  
    ' Removes all the tabs:  
    TabControl1.TabPages.Clear()  
    ```  
  
    ```csharp  
    // Removes the selected tab:  
    tabControl1.TabPages.Remove(tabControl1.SelectedTab);  
    // Removes all the tabs:  
    tabControl1.TabPages.Clear();  
    ```  
  
    ```cpp  
    // Removes the selected tab:  
    tabControl1->TabPages->Remove(tabControl1->SelectedTab);  
    // Removes all the tabs:  
    tabControl1->TabPages->Clear();  
    ```  
  
## <a name="see-also"></a>Zobacz także

- [TabControl, kontrolka — omówienie](tabcontrol-control-overview-windows-forms.md)
- [Instrukcje: Dodawanie kontrolki do karty](how-to-add-a-control-to-a-tab-page.md)
- [Instrukcje: Wyłączanie kart](how-to-disable-tab-pages.md)
- [Instrukcje: Zmienianie wyglądu kontrolki TabControl formularzy Windows Forms](how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)
