---
title: 'Instrukcje: dodawanie i usuwanie elementów za pomocą kontrolki DomainUpDown'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- DomainUpDown control [Windows Forms], removing items from
- spin button control [Windows Forms], removing items
ms.assetid: e70f5cbc-b497-41a9-975a-344c00e56ed2
ms.openlocfilehash: f56bc2b7b7b8a783ac298b220c83281f38da29da
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662349"
---
# <a name="how-to-remove-items-from-windows-forms-domainupdown-controls"></a>Instrukcje: dodawanie i usuwanie elementów za pomocą kontrolki DomainUpDown
Możesz usunąć elementy z formularzy Windows <xref:System.Windows.Forms.DomainUpDown> kontroli przez wywołanie metody <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A> lub <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A> metody <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection> klasy. <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A> Metoda usuwa określony element, podczas gdy <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A> metoda usuwa element według ich pozycji.  
  
### <a name="to-remove-an-item"></a>Aby usunąć element  
  
- Użyj <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A> metody <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection> klasy, aby usunąć element według nazwy.  
  
    ```vb  
    DomainUpDown1.Items.Remove("noodles")  
    ```  
  
    ```csharp  
    domainUpDown1.Items.Remove("noodles");  
    ```  
  
    ```cpp  
    domainUpDown1->Items->Remove("noodles");  
    ```  
  
     —lub—  
  
- Użyj <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A> metodę, aby usunąć element według ich pozycji.  
  
    ```vb  
    ' Removes the first item in the list.  
    DomainUpDown1.Items.RemoveAt(0)  
    ```  
  
    ```csharp  
    // Removes the first item in the list.  
    domainUpDown1.Items.RemoveAt(0);  
    ```  
  
    ```cpp  
    // Removes the first item in the list.  
    domainUpDown1->Items->RemoveAt(0);  
    ```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.DomainUpDown>
- <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A?displayProperty=nameWithType>
- [DomainUpDown, kontrolka](domainupdown-control-windows-forms.md)
- [DomainUpDown, kontrolka — omówienie](domainupdown-control-overview-windows-forms.md)
