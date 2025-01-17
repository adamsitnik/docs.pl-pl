---
title: 'Instrukcje: tworzenie i ustawienie niestandardowego modułu renderowania dla kontrolki ToolStrip w formularzach systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStrip control [Windows Forms], custom rendering
- toolbars [Windows Forms], rendering
- examples [Windows Forms], toolbars
- ToolStrip control [Windows Forms], rendering
ms.assetid: 88a804ba-679f-4ba3-938a-0dc396199c5b
ms.openlocfilehash: c354ace3a7d3ce43f549dd1295a85fbee004eb22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929738"
---
# <a name="how-to-create-and-set-a-custom-renderer-for-the-toolstrip-control-in-windows-forms"></a>Instrukcje: tworzenie i ustawienie niestandardowego modułu renderowania dla kontrolki ToolStrip w formularzach systemu Windows
<xref:System.Windows.Forms.ToolStrip>kontrolki zapewniają łatwą obsługę motywów i stylów. Możesz uzyskać całkowicie niestandardowy wygląd i zachowanie (wygląd i działanie), ustawiając <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> Właściwość <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType> lub właściwość na niestandardowy moduł renderujący.  
  
 Można przypisać moduły <xref:System.Windows.Forms.ToolStrip>renderowania do poszczególnych osób <xref:System.Windows.Forms.ContextMenuStrip>, <xref:System.Windows.Forms.MenuStrip>, <xref:System.Windows.Forms.ToolStripManager.Renderer%2A> lub <xref:System.Windows.Forms.StatusStrip> kontrolki, lub użyć właściwości, aby wpływać na wszystkie obiekty przez ustawienie <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=nameWithType> właściwości na <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode?displayProperty=nameWithType>.  
  
> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>zwraca <xref:System.Windows.Forms.ToolStripRenderMode.Custom> tylko wtedy, gdy <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> wartość nie `null`jest.  
  
### <a name="to-create-a-custom-renderer"></a>Aby utworzyć niestandardowy moduł renderujący  
  
1. <xref:System.Windows.Forms.ToolStripRenderer> Rozwiń klasę.  
  
2. Zaimplementuj żądane renderowanie niestandardowe przez zastępowanie właściwych *w...* elementy członkowskie  
  
    ```vb  
    Public Class RedTextRenderer  
        Inherits System.Windows.Forms.ToolStripRenderer  
        Protected Overrides Sub OnRenderItemText(ByVal e As _  
            ToolStripItemTextRenderEventArgs)   
            e.TextColor = Color.Red  
            e.TextFont = New Font("Helvetica", 7, FontStyle.Bold)  
            MyBase.OnRenderItemText(e)  
        End Sub  
    End Class  
    ```  
  
    ```csharp  
    public class RedTextRenderer : _  
        System.Windows.Forms.ToolStripRenderer  
    {  
        protected override void _  
            OnRenderItemText(ToolStripItemTextRenderEventArgs e)  
        {  
            e.TextColor = Color.Red;  
            e.TextFont = new Font("Helvetica", 7, FontStyle.Bold);  
           base.OnRenderItemText(e);  
        }  
    }  
    ```  
  
### <a name="to-set-the-custom-renderer-to-be-the-current-renderer"></a>Aby ustawić moduł renderowania niestandardowego jako bieżący moduł renderowania  
  
1. Aby ustawić niestandardowy moduł renderujący dla <xref:System.Windows.Forms.ToolStrip>jednego, <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=nameWithType> ustaw właściwość na niestandardowy moduł renderowania.  
  
    ```vb  
    toolStrip1.Renderer = New RedTextRenderer()  
    ```  
  
    ```csharp  
    toolStrip1.Renderer = new RedTextRenderer();  
    ```  
  
2. Lub w celu ustawienia modułu renderowania niestandardowego dla <xref:System.Windows.Forms.ToolStrip> wszystkich klas zawartych w aplikacji: Ustaw właściwość na moduł renderowania niestandardowego i <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> ustaw właściwość na <xref:System.Windows.Forms.ToolStripRenderMode.ManagerRenderMode>. <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=nameWithType>  
  
    ```vb  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode  
    ToolStripManager.Renderer = New RedTextRenderer()  
    ```  
  
    ```csharp  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode;  
    ToolStripManager.Renderer = new RedTextRenderer();  
    ```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.ToolStripManager.Renderer%2A>
- <xref:System.Windows.Forms.ToolStripRenderer>
- <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>
- [ToolStrip, kontrolka — omówienie](toolstrip-control-overview-windows-forms.md)
- [ToolStrip, kontrolka — architektura](toolstrip-control-architecture.md)
- [ToolStrip — podsumowanie informacji o technologii](toolstrip-technology-summary.md)
