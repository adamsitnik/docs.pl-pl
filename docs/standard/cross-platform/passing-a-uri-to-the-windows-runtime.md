---
title: Przekazywanie adresu URI do środowiska wykonawczego systemu Windows
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Runtime, .NET Framework support for
- Windows Runtime, passing a URI to
ms.assetid: 3eb5ce6f-f304-4f87-8e81-0f25092f5ad4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c489ec893ea335c8fafc904cf2a12162580ec266
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025439"
---
# <a name="passing-a-uri-to-the-windows-runtime"></a>Przekazywanie adresu URI do środowiska wykonawczego systemu Windows
Metod środowiska wykonawczego Windows akceptuje tylko bezwzględne identyfikatorów URI. Jeśli przekażesz względny identyfikator URI do metody środowiska wykonawczego Windows, <xref:System.ArgumentException> wyjątku. Oto Dlaczego: Gdy używasz środowiska wykonawczego Windows w kodzie .NET Framework <xref:Windows.Foundation.Uri?displayProperty=nameWithType> klasa jest wyświetlany jako <xref:System.Uri?displayProperty=nameWithType> w technologii Intellisense. <xref:System.Uri?displayProperty=nameWithType> Klasa umożliwia względne identyfikatory URI, ale <xref:Windows.Foundation.Uri?displayProperty=nameWithType> klasy nie jest. Dotyczy to również metody, które należy udostępnić w składnikach środowiska wykonawczego Windows. Jeśli składnik udostępnia metodę, która przyjmuje identyfikator URI, podpis w kodzie zawiera <xref:System.Uri?displayProperty=nameWithType>. Jednak użytkownikom składnika podpis zawiera <xref:Windows.Foundation.Uri?displayProperty=nameWithType>. Identyfikator URI, który jest przekazywany do składnika musi być bezwzględnym identyfikatorem URI.  
  
W tym temacie pokazano, jak wykrywać bezwzględny identyfikator URI i jak go utworzyć przy odwoływaniu się do zasobu w pakiecie aplikacji.  
  
## <a name="detecting-and-using-an-absolute-uri"></a>Wykrywanie i używanie bezwzględnego identyfikatora URI  
Użyj <xref:System.Uri.IsAbsoluteUri%2A?displayProperty=nameWithType> właściwości, aby upewnić się, że identyfikator URI jest bezwzględny, przed przekazaniem go do środowiska wykonawczego Windows. Używanie tej właściwości jest bardziej efektywne niż wychwytywanie i obsługa <xref:System.ArgumentException> wyjątku.  
  
## <a name="using-an-absolute-uri-for-a-resource-in-the-app-package"></a>Za pomocą bezwzględny identyfikator URI zasobu w pakiecie aplikacji  
Jeśli chcesz określić identyfikator URI zasobu, który zawiera pakiet aplikacji, możesz użyć `ms-appx` lub `ms-appx-web` schemat, aby utworzyć bezwzględny identyfikator URI.  
  
Poniższy przykład pokazuje, jak ustawić <xref:Windows.UI.Xaml.Controls.WebView.Source%2A> właściwość <xref:Windows.UI.Xaml.Controls.WebView> kontroli i <xref:Windows.UI.Xaml.Controls.Image.Source%2A> właściwość <xref:Windows.UI.Xaml.Controls.Image> formantu do zasobów, które są zawarte w folderze o nazwie stron przy użyciu XAML i kodu.  
  
[!code-xaml[System.URIToWindowsURI#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml#1)]  
[!code-csharp[System.URIToWindowsURI#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml.cs#2)]
[!code-vb[System.URIToWindowsURI#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.uritowindowsuri/vb/mainpage.xaml.vb#2)]  
  
Aby uzyskać więcej informacji na temat tych schematów, zobacz [schematy identyfikatorów URI](/windows/uwp/app-resources/uri-schemes) w Centrum deweloperów Windows.  
  
## <a name="see-also"></a>Zobacz także

- [Obsługa programu .NET Framework dla aplikacji ze Sklepu Windows i środowiska wykonawczego systemu Windows](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
