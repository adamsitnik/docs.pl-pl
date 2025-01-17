---
title: 'Porady: korzystanie ze zdarzeń w aplikacjach formularzy sieci Web'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [.NET Framework], Web Forms
- Web Forms controls, and events
- event handlers [.NET Framework], Web Forms
- events [.NET Framework], consuming
- Web Forms, event handling
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
ms.openlocfilehash: 1f95fd0dcc12f2d4e47ee07e1e6bb15d91000f0f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73124786"
---
# <a name="how-to-consume-events-in-a-web-forms-application"></a>Porady: korzystanie ze zdarzeń w aplikacjach formularzy sieci Web
Typowy scenariusz w aplikacjach formularzy sieci Web ASP.NET to wypełnienie strony sieci Web z kontrolkami, a następnie wykonanie konkretnej akcji na podstawie tego, która kontrolka klika użytkownika. Na przykład formant <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> wywołuje zdarzenie, gdy użytkownik kliknie go na stronie sieci Web. Dzięki obsłudze zdarzenia, aplikacja może wykonać odpowiednią logikę aplikacji dla tego przycisku.  
  
### <a name="to-handle-a-button-click-event-on-a-webpage"></a>Aby obsługiwać przycisk Kliknij zdarzenie na stronie sieci Web  
  
1. Utwórz stronę formularzy sieci Web ASP.NET (Web), która ma kontrolkę <xref:System.Web.UI.WebControls.Button> z wartością `OnClick` ustawioną na nazwę metody, która zostanie zdefiniowana w następnym kroku.  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. Zdefiniuj procedurę obsługi zdarzeń, która pasuje do sygnatury delegata zdarzenia <xref:System.Web.UI.WebControls.Button.Click> i ma nazwę zdefiniowaną dla `OnClick` wartości.  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     Zdarzenie <xref:System.Web.UI.WebControls.Button.Click> używa klasy <xref:System.EventHandler> dla typu delegata oraz klasy <xref:System.EventArgs> dla danych zdarzenia. Struktura strony ASP.NET automatycznie generuje kod, który tworzy wystąpienie <xref:System.EventHandler> i dodaje to wystąpienie delegata do zdarzenia <xref:System.Web.UI.WebControls.Button.Click> wystąpienia <xref:System.Web.UI.WebControls.Button>.  
  
3. W metodzie obsługi zdarzeń zdefiniowanej w kroku 2 Dodaj kod, aby wykonać wszelkie akcje, które są wymagane w przypadku wystąpienia zdarzenia.  
  
## <a name="see-also"></a>Zobacz także

- [Zdarzenia](../../../docs/standard/events/index.md)
