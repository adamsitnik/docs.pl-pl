---
title: Definiowanie zdarzeń w formantach formularzy systemu Windows
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [Windows Forms], defining within Windows Forms custom controls
- custom controls [Windows Forms], events using code
ms.assetid: d89f1096-8061-42e2-a855-a1f053f1940a
ms.openlocfilehash: 4235c8b3c513509023388112071e78cfd079ec6f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972344"
---
# <a name="defining-an-event-in-windows-forms-controls"></a>Definiowanie zdarzeń w formantach formularzy systemu Windows
Aby uzyskać szczegółowe informacje na temat definiowania zdarzenia niestandardowe, zobacz [zdarzenia](../../../standard/events/index.md). Jeśli zdefiniujesz zdarzenie, które nie ma żadnych skojarzonych danych, należy użyć typu podstawowego danych zdarzenia <xref:System.EventArgs>i użyj <xref:System.EventHandler> jako delegat wydarzenia. Celu pozostaje tylko zdefiniować element członkowski zdarzenia i chronioną `On` *EventName* metody, która wywołuje zdarzenia.  
  
 Poniższy kod fragment przedstawia sposób, w jaki `FlashTrackBar` formant niestandardowy definiuje niestandardowe zdarzenie `ValueChanged`. Aby uzyskać kompletny kod dla `FlashTrackBar` przykładowe, zobacz [jak: Utwórz formant programu Windows Forms pokazującej postęp](how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
```vb  
Option Explicit  
Option Strict  
  
Imports System  
Imports System.Windows.Forms  
Imports System.Drawing  
  
Public Class FlashTrackBar  
   Inherits Control  
  
   ' The event does not have any data, so EventHandler is adequate   
   ' as the event delegate.          
   ' Define the event member using the event keyword.  
   ' In this case, for efficiency, the event is defined   
   ' using the event property construct.  
   Public Event ValueChanged As EventHandler  
   ' The protected method that raises the ValueChanged   
   ' event when the value has actually   
   ' changed. Derived controls can override this method.    
   Protected Overridable Sub OnValueChanged(e As EventArgs)  
      RaiseEvent ValueChanged(Me, e)  
   End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Drawing;  
  
public class FlashTrackBar : Control {  
   // The event does not have any data, so EventHandler is adequate   
   // as the event delegate.  
   private EventHandler onValueChanged;  
   // Define the event member using the event keyword.  
   // In this case, for efficiency, the event is defined   
   // using the event property construct.  
   public event EventHandler ValueChanged {  
            add {  
                onValueChanged += value;  
            }  
            remove {  
                onValueChanged -= value;  
            }  
        }  
   // The protected method that raises the ValueChanged  
   // event when the value has actually   
   // changed. Derived controls can override this method.    
   protected virtual void OnValueChanged(EventArgs e) 
   {  
       ValueChanged?.Invoke(this, e);  
   }  
}  
```  
  
## <a name="see-also"></a>Zobacz także

- [Zdarzenia w kontrolkach formularzy Windows Forms](events-in-windows-forms-controls.md)
- [Zdarzenia](../../../standard/events/index.md)
