---
title: 'Instrukcje: wiązanie z usługą sieci Web za pomocą kontrolki BindingSource formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Web services [Windows Forms], binding controls
- BindingSource component [Windows Forms], binding to a Web service
- examples [Windows Forms], BindingSource component
- controls [Windows Forms], binding to Web service
- BindingSource component [Windows Forms], examples
ms.assetid: ee261207-4573-4cb9-a8cb-5185037e0fba
ms.openlocfilehash: 94564ba2614e335da36828912e43fb9db7eca91b
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833996"
---
# <a name="how-to-bind-to-a-web-service-using-the-windows-forms-bindingsource"></a>Instrukcje: wiązanie z usługą sieci Web za pomocą kontrolki BindingSource formularzy systemu Windows
Jeśli chcesz powiązać kontrolkę formularza Windows wyniki uzyskane z wywołaniem usługi sieci Web XML, możesz użyć <xref:System.Windows.Forms.BindingSource> składnika. Ta procedura jest podobna do powiązania <xref:System.Windows.Forms.BindingSource> składnik do typu. Należy utworzyć serwer proxy po stronie klienta, który zawiera metody i typy udostępnianych przez usługę sieci Web. Możesz wygenerować, serwer proxy po stronie klienta z usługi sieci Web (.asmx), samego lub plik sieci Web Services Description Language (WSDL). Ponadto serwer proxy po stronie klienta, należy ujawnić pola złożone typy używane przez usługę sieci Web jako właściwości publiczne. Następnie Powiąż <xref:System.Windows.Forms.BindingSource> do jednego z typów ujawnione w sieci Web usługi serwera proxy.  
  
### <a name="to-create-and-bind-to-a-client-side-proxy"></a>Aby utworzyć i powiązać serwer proxy po stronie klienta  
  
1. Tworzenie formularza Windows w katalogu, co pozwala przy użyciu odpowiedniego obszaru nazw.  
  
2. Dodaj <xref:System.Windows.Forms.BindingSource> składnika do formularza.  
  
3. Otwórz wiersz polecenia programu Windows Software Development Kit (SDK) i przejdź do formularza znajdujący się w katalogu.  
  
4. Za pomocą narzędzia WSDL wprowadź `wsdl` adres URL .asmx lub pliku WSDL usługi sieci Web, a następnie przestrzeni nazw aplikacji i opcjonalnie język, w którym pracujesz.  
  
     Poniższy przykład kodu wykorzystuje usługę sieci Web, znajduje się w `http://webservices.eraserver.net/zipcoderesolver/zipcoderesolver.asmx`. Na przykład typ C# `wsdl http://webservices.eraserver.net.zipcoderesolver/zipcoderesolver.asmx /n:BindToWebService`, lub dla języka Visual Basic typu `wsdl http://webservices.eraserver.net.zipcoderesolver/zipcoderesolver.asmx /n:BindToWebService /language:VB`. Przekazanie ścieżki jako argument do języka WSDL narzędzie wygeneruje serwer proxy po stronie klienta w tym samym katalogu i przestrzeni nazw jako aplikację w wybranym języku. Jeśli używasz programu Visual Studio, należy dodać plik do projektu.  
  
5. Wybierz typ serwera proxy po stronie klienta, aby powiązać.  
  
     Zazwyczaj jest to typ zwracany przez metodę, oferowane przez usługę sieci Web. Pola wybranego typu muszą być widoczne jako właściwości publiczne dla powiązania celów.  
  
     [!code-cpp[System.Windows.Forms.DataConnectorWebService#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#4)]
     [!code-csharp[System.Windows.Forms.DataConnectorWebService#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.DataConnectorWebService#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#4)]  
  
6. Ustaw <xref:System.Windows.Forms.BindingSource.DataSource%2A> właściwość <xref:System.Windows.Forms.BindingSource> do typu, to znaczy ma zawarte w serwer proxy po stronie klienta dla usługi sieci Web.  
  
     [!code-cpp[System.Windows.Forms.DataConnectorWebService#2](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#2)]
     [!code-csharp[System.Windows.Forms.DataConnectorWebService#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.DataConnectorWebService#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#2)]  
  
### <a name="to-bind-controls-to-the-bindingsource-that-is-bound-to-a-web-service"></a>Aby powiązać formanty z BindingSource, który jest powiązany z usługą sieci Web  
  
- Powiązywanie kontrolek do <xref:System.Windows.Forms.BindingSource>, przekazując właściwość publiczna typu usługi sieci Web, która ma jako parametr.  
  
     [!code-cpp[System.Windows.Forms.DataConnectorWebService#3](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#3)]
     [!code-csharp[System.Windows.Forms.DataConnectorWebService#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.DataConnectorWebService#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#3)]  
  
## <a name="example"></a>Przykład  
 Poniższy przykład kodu pokazuje, jak powiązać <xref:System.Windows.Forms.BindingSource> składnik usługi sieci Web, a następnie powiązać pole tekstowe do <xref:System.Windows.Forms.BindingSource> składnika. Po kliknięciu przycisku, wywoływana jest metoda usługi sieci Web i wyniki pojawią się w `textbox1`.  
  
 [!code-cpp[System.Windows.Forms.DataConnectorWebService#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.DataConnectorWebService#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnectorWebService#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  
 Jest to kompletny przykład, który zawiera `Main` metoda i skróconą wersję kodu serwera proxy po stronie klienta.  
  
 Ten przykład wymaga:  
  
- Odwołania do zestawów systemu, System.Drawing, System.Web.Services, przestrzeń nazw System.Windows.Forms i System.Xml.  
  
## <a name="see-also"></a>Zobacz także

- [BindingSource, składnik](bindingsource-component.md)
- [Instrukcje: Powiązanie z typem formantu Windows Forms](how-to-bind-a-windows-forms-control-to-a-type.md)
