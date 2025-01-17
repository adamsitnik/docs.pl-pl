---
title: Przegląd formularzy systemu Windows i niezarządzanych aplikacji
ms.date: 03/30/2017
helpviewer_keywords:
- COM [Windows Forms]
- Windows Forms, unmanaged
- COM interop
- ActiveX controls [Windows Forms], about ActiveX controls
- Windows Forms, interop
ms.assetid: 0a26d99d-8135-4895-8760-c9a2b5f67f14
ms.openlocfilehash: 02f3224a8069fd091833bb09744389592c769818
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592504"
---
# <a name="windows-forms-and-unmanaged-applications-overview"></a>Przegląd formularzy systemu Windows i niezarządzanych aplikacji
Aplikacje Windows Forms i formanty może współpracować z niezarządzanych aplikacji za pomocą niektóre zastrzeżenia. Poniżej opisano scenariusze i konfiguracje obsługujące aplikacje i formanty Windows Forms oraz te, które nie obsługują.  
  
## <a name="windows-forms-controls-and-activex-applications"></a>Windows Forms, formanty i aplikacji ActiveX  
 Z wyjątkiem programu Microsoft Internet Explorer i Microsoft Foundation Classes (MFC) kontrolek formularzy Windows Forms nie są obsługiwane w aplikacji, które mają hosta formantów ActiveX. Inne aplikacje i narzędzia programistyczne, które są zdolne do hostowania kontrolki ActiveX, w tym kontenerów testów ActiveX z wersji programu Visual Studio, które są starsze niż program Visual Studio .NET 2003 nie są obsługiwane hosty dla kontrolek formularzy Windows Forms.  
  
 Te ograniczenia mają zastosowanie również do korzystania z kontrolek Windows Forms za pomocą Component Object Model COM interop. Korzystanie z kontrolki Windows Forms za pomocą wywołalne opakowanie COM (CCW) jest obsługiwana tylko w programie Internet Explorer. Aby uzyskać więcej informacji na temat współdziałania z modelem COM Zobacz  
  
 [Usługa międzyoperacyjna modelu COM](../../../visual-basic/programming-guide/com-interop/index.md).  
  
 W poniższej tabeli przedstawiono dostępne ActiveX hostingu obsługę kontrolek formularzy Windows Forms.  
  
|Wersja Windows Forms|Pomoc techniczna|  
|---------------------------|-------------|  
|.NET framework w wersji 1.0|Internet Explorer 5.01 i nowsze wersje|  
|.NET framework w wersji 1.1 lub nowszy|Internet Explorer 5.01 i nowsze wersje<br /><br /> Microsoft Foundation Classes (MFC) 7.0 lub nowszy|  
  
## <a name="hosting-windows-forms-components-as-activex-controls"></a>Hostowanie składniki formularzy Windows jako kontrolki ActiveX  
 W .NET Framework 1.1 Obsługa zostało rozszerzone, aby MFC w wersji 7.0 i nowszych wersjach. Ta obsługa obejmuje dowolnego kontenera, który jest w pełni zgodna z MFC 7.0 i nowszych kontener formantu ActiveX.  
  
 Rejestracja kontrolek Windows Forms jako formantów ActiveX nie jest obsługiwana. Ponadto podczas wywoływania `com.ms.win32.Ole32.CoCreateInstance` metoda dla kontrolek formularzy Windows Forms nie jest obsługiwana. Tylko zarządzane Aktywacja kontrolek formularzy Windows Forms jest obsługiwane. Po utworzeniu kontrolki Windows Forms, można go umieścić w aplikacji MFC, podobnie jak w przypadku formantu ActiveX.  
  
 Aby użyć kontrolek formularzy Windows Forms w niezarządzanej aplikacji, możesz hostować przy użyciu niezarządzanego CLR hostowania interfejsów API środowiska CLR lub korzystanie z funkcji międzyoperacyjności języka C++. Korzystanie z funkcji międzyoperacyjności języka C++ jest zalecanym rozwiązaniem.  
  
## <a name="windows-forms-in-com-client-applications"></a>Formularzy Windows w aplikacje klienckie modelu COM  
 Po otwarciu formularza Windows od aplikacji klienckiej COM, takich jak Visual Basic 6.0 lub aplikacja MFC formularza może zachowywać się niestabilnie. Na przykład po naciśnięciu klawisza TAB fokus nie zmienia się z jednego formantu do innego formantu. Po naciśnięciu klawisza ENTER podczas przycisku polecenia ma fokus, przycisk firmy <xref:System.Windows.Forms.Control.Click> zdarzenie jest zgłaszane w nie. Może również wystąpić nieoczekiwane zachowanie dla naciśnięć klawiszy lub działania myszy.  
  
 Dzieje się tak, ponieważ Niezarządzana aplikacja nie implementuje obsługę pętli komunikatów, która formularze Windows wymaga, aby działać poprawnie. Pętli komunikatów udostępniany przez aplikację klienta COM jest różni się od pętli komunikatów Windows Forms.  
  
 Komunikat aplikacji pętli to pętla wewnętrzny programu, które pobierają wiadomości z kolejki komunikatów wątku, tłumaczy je, a następnie wysyła je do aplikacji, które mają być obsługiwane. Pętli komunikatów dla formularza Windows nie ma taką samą architekturę co pętli komunikatów, które zapewniają starszych aplikacji, takich jak aplikacje Visual Basic 6.0 i aplikacjach MFC. Wiadomości okna, które są wysyłane do pętli komunikatów mogą być traktowane inaczej niż w formularzu Windows oczekuje. W związku z tym mogą wystąpić nieoczekiwane zachowanie. Niektóre kombinacje klawiszy mogą nie działać, niektóre działania myszy może nie działać lub niektóre zdarzenia nie mogą zostać podjęte, zgodnie z oczekiwaniami.  
  
## <a name="resolving-interoperability-issues"></a>Rozwiązywanie problemów ze współdziałaniem  
 Można rozwiązać te problemy przez wyświetlanie formularza w pętli komunikatów .NET Framework, która została utworzona przy użyciu <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> metody.  
  
 Aby dzieło formularza Windows poprawnie z modelu COM aplikacji klienckiej, należy uruchom go na pętli komunikatów Windows Forms. Aby to zrobić, użyj jednej z następujących metod:  
  
- Użyj <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metodę w celu wyświetlenia formularza Windows. Aby uzyskać więcej informacji, zobacz [jak: Obsługa międzyoperacyjności modelu COM za pomocą wyświetlania formularza Windows, za pomocą metody ShowDialog](com-interop-by-displaying-a-windows-form-shadow.md).  
  
- Wyświetlania każdego formularza Windows w nowym wątku. Aby uzyskać więcej informacji, zobacz [jak: Obsługa międzyoperacyjności modelu COM za pomocą wyświetlania każdego formularza Windows w jego własnym wątku](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md).  
  
## <a name="see-also"></a>Zobacz także

- [Formularze Windows Forms i niezarządzane aplikacje](windows-forms-and-unmanaged-applications.md)
- [Usługa międzyoperacyjna modelu COM](../../../visual-basic/programming-guide/com-interop/index.md)
- [Współdziałanie COM w aplikacjach .NET Framework](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)
- [Przykłady współdziałania COM](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/cxcz83xf(v=vs.90))
- [Aximp.exe (importer kontrolki ActiveX formularzy Windows Forms)](../../tools/aximp-exe-windows-forms-activex-control-importer.md)
- [Udostępnianie składników .NET Framework modelowi COM](../../interop/exposing-dotnet-components-to-com.md)
- [Pakowanie zestawu dla modelu COM](../../interop/packaging-an-assembly-for-com.md)
- [Rejestrowanie zestawów do użycia z modelem COM](../../interop/registering-assemblies-with-com.md)
- [Instrukcje: Obsługa międzyoperacyjności modelu COM za pomocą wyświetlania formularza Windows, za pomocą ShowDialog — metoda](com-interop-by-displaying-a-windows-form-shadow.md)
- [Instrukcje: Obsługa międzyoperacyjności modelu COM za pomocą wyświetlania każdego formularza Windows w jego własnym wątku](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)
