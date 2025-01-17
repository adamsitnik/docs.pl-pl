---
title: Formularze systemu Windows — Omówienie
ms.date: 03/30/2017
helpviewer_keywords:
- smart clients
- Windows Forms, about Windows Forms
ms.assetid: 3a2b6284-c8d6-4e1c-8c69-0bed38f38cd4
ms.openlocfilehash: 71bf50bdcf058e94981dc5df4731b5d32dcc2069
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487206"
---
# <a name="windows-forms-overview"></a>Windows Forms — omówienie

Poniższy przegląd omawia zalety inteligentnych aplikacji klienckich, najważniejszych funkcji Windows Forms, programowania i jak Windows Forms można użyć do tworzenia inteligentnych klientów, którzy potrzeb współczesnych przedsiębiorstw i użytkowników końcowych.

## <a name="windows-forms-and-smart-client-apps"></a>Windows Forms i aplikacji klienckich inteligentne

 Za pomocą interfejsu Windows Forms, możesz tworzyć inteligentne klientów. *Blokada Smart klientów* atrakcyjnych wizualnie aplikacje, które są łatwe do wdrożenia i aktualizacji, można pracować, gdy są one połączone lub połączenia z Internetem i mogą uzyskiwać dostęp do zasobów na komputerze lokalnym w sposób bardziej bezpieczne niż tradycyjne Aplikacje z systemem Windows.

### <a name="build-rich-interactive-user-interfaces"></a>Tworzenie interfejsów użytkownika bogate, interaktywne

 Windows Forms to technologia inteligentne klienta dla programu .NET Framework, zbiór bibliotek zarządzanych, które upraszczają typowych zadań aplikacji, takich jak odczytywanie i zapisywanie w systemie plików. Gdy używasz środowiska programowania, takich jak Visual Studio, można utworzyć Windows Forms inteligentnych aplikacji klienckich wyświetlić informacje, żądać danych wejściowych od użytkowników oraz komunikować się ze zdalnymi komputerami za pośrednictwem sieci.

 W formularzach Windows *formularza* jest powierzchnią wizualną, na którym możesz wyświetlić informacje do użytkownika. Zazwyczaj tworzenie aplikacji Windows Forms przez dodawanie kontrolek do formularzy i tworzenie odpowiedzi na działania użytkownika, takich jak kliknięcia lub naciśnięcia klawiszy. A *kontroli* jest element interfejsu użytkownika dyskretnych, który wyświetla dane lub akceptuje dane wejściowe.

 Gdy użytkownik wykona coś do formularza lub jego formantów, akcja generuje zdarzenie. Aplikacja reaguje na zdarzenia przy użyciu kodu i przetwarza zdarzenia w momencie ich wystąpienia. Aby uzyskać więcej informacji, zobacz [tworzenie obsługi zdarzeń w formularzach Windows Forms](creating-event-handlers-in-windows-forms.md).

 Windows Forms zawiera szereg formantów, które można dodać do formularzy: formantów, które wyświetlają pola tekstowe, przyciski, pola listy rozwijanej, przyciski radiowe i nawet stron sieci Web. Aby uzyskać listę wszystkich kontrolek, można użyć w formularzu, zobacz [kontrolki do użycia w formularzach Windows Forms](./controls/controls-to-use-on-windows-forms.md). Jeśli formant nie spełnia Twoich potrzeb, formularze Windows obsługuje również tworzenie własnych niestandardowych kontrolek przy użyciu <xref:System.Windows.Forms.UserControl> klasy.

 Formularze Windows ma zaawansowanych kontrolek interfejsu użytkownika, które emulują funkcji wysokiej jakości aplikacji, takie jak Microsoft Office. Kiedy używasz <xref:System.Windows.Forms.ToolStrip> i <xref:System.Windows.Forms.MenuStrip> kontrolki, możesz utworzyć pasków narzędzi i menu, które zawierają tekst i obrazy, wyświetlić podmenu i hostują inne kontrolki, takie jak pola tekstowe i pola kombi.

 Za pomocą przeciągania i upuszczania **Windows Forms Designer** w programie Visual Studio, możesz łatwo tworzyć aplikacje Windows Forms. Po prostu zaznacz formanty z kursor i Dodaj miejsce w formularzu. Projektant udostępnia narzędzia, takie jak linii siatki i przyciągania uprości wyrównywanie formantów. Czy przy użyciu programu Visual Studio lub kompilacji w wierszu polecenia, można użyć <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel> i <xref:System.Windows.Forms.SplitContainer> służy do tworzenia zaawansowanych tworzą układów w krótszym czasie.

 Na koniec, jeśli musisz utworzyć własne niestandardowe elementy interfejsu użytkownika <xref:System.Drawing> przestrzeń nazw zawiera dużą liczbę klas do renderowania linii, okręgi i inne kształty bezpośrednio na formularzu.

> [!NOTE]
> Formanty formularzy Windows nie są przeznaczone do można zorganizować w różnych domenach aplikacji. Z tego powodu firma Microsoft obsługuje przekazywanie formantu Windows Forms w <xref:System.AppDomain> granic, mimo że <xref:System.Windows.Controls.Control> typ podstawowy elementu <xref:System.MarshalByRefObject> wydaje się w celu wskazania, że jest to możliwe. Aplikacje Windows Forms, mających wiele domen aplikacji są obsługiwane, tak długo, jak brak kontrolek Windows Forms są przekazywane poza granice domeny aplikacji.

#### <a name="create-forms-and-controls"></a>Tworzenie formularzy i kontrolek

Aby uzyskać szczegółowe informacje o sposobie używania tych funkcji zobacz następujące tematy Pomocy.

|Opis|Temat pomocy|
|-----------------|----------------|
|Za pomocą kontrolek na formularzach|[Instrukcje: Dodawanie formantów do formularzy Windows Forms](./controls/how-to-add-controls-to-windows-forms.md)|
|Za pomocą <xref:System.Windows.Forms.ToolStrip> kontroli|[Instrukcje: Tworzenie podstawowych ToolStrip z elementami standardowymi przy użyciu narzędzia Projektant](./controls/create-a-basic-wf-toolstrip-with-standard-items-using-the-designer.md)|
|Tworzenia grafiki przy użyciu <xref:System.Drawing>|[Wprowadzenie do programowania grafiki](./advanced/getting-started-with-graphics-programming.md)|
|Tworzenie niestandardowych formantów|[Instrukcje: Dziedziczenie z klasy UserControl](./controls/how-to-inherit-from-the-usercontrol-class.md)|

### <a name="display-and-manipulate-data"></a>Wyświetlanie i manipulowanie danymi
 Wiele aplikacji, musisz wyświetlić dane z bazy danych, plik XML, usługi XML sieci Web lub innego źródła danych. Formularze Windows udostępnia elastyczną kontrolę, który nosi nazwę <xref:System.Windows.Forms.DataGridView> kontrolkę do wyświetlania takich danych tabelarycznych w tradycyjnych formacie wierszy i kolumn, tak aby każdy element danych zajmował komórki. Kiedy używasz <xref:System.Windows.Forms.DataGridView>, można dostosować wygląd pojedyncze komórki, blokuje dowolnego wierszy i kolumn w miejscu i wyświetlić złożonych kontrolek w komórkach, m.in.

 Łączenie ze źródłami danych za pośrednictwem sieci jest prostym zadaniem przy użyciu klienci inteligentni Windows Forms. <xref:System.Windows.Forms.BindingSource> Składnika reprezentuje połączenie ze źródłem danych i udostępnia metody dla powiązania danych z kontrolkami, przejdź do poprzedniego i dalej rekordów, edytowanie rekordów i zapisywanie zmian z powrotem do oryginalnego źródła. <xref:System.Windows.Forms.BindingNavigator> Kontroli udostępnia prosty interfejs, za pośrednictwem <xref:System.Windows.Forms.BindingSource> składnika umożliwiające użytkownikom przechodzenie między rekordami.

 Formanty powiązane z danymi można łatwo utworzyć, korzystając z okna źródeł danych. W oknie źródeł danych, takich jak bazy danych, usług sieci Web i obiekty są wyświetlane w projekcie. Można utworzyć formanty powiązane z danymi przez przeciąganie elementów z tego okna na formularze w projekcie. Użytkownik może również wiązania danych istniejących kontrolek z danymi przez przeciąganie obiektów z okna źródeł danych na istniejące kontrolki.

 Inny typ wiązania danych, można zarządzać w formularzach Windows Forms jest *ustawienia*. Większość inteligentnych aplikacji klienckich, należy zachować pewne informacje o ich stanie w czasie wykonywania, takie jak rozmiar Ostatnia znana formularzy i Zachowaj dane preferencji użytkownika, takie jak domyślne lokalizacje plików zapisanych. Ustawienia aplikacji funkcji rozwiązuje te wymagania, zapewniając łatwy sposób przechowywania oba rodzaje ustawień na komputerze klienckim. Po zdefiniowaniu te ustawienia przy użyciu programu Visual Studio lub Edytor kodu, ustawienia są utrwalane w formacie XML i automatycznie odczytywać powrotem do pamięci w czasie wykonywania.

#### <a name="display-and-manipulate-data"></a>Wyświetlanie i manipulowanie danymi

Aby uzyskać szczegółowe informacje o sposobie używania tych funkcji zobacz następujące tematy Pomocy.

|Opis|Temat pomocy|
|-----------------|----------------|
|Za pomocą <xref:System.Windows.Forms.BindingSource> składnika|[Instrukcje: Powiązywanie kontrolek formularzy Windows ze składnikiem BindingSource przy użyciu narzędzia Projektant](./controls/bind-wf-controls-with-the-bindingsource.md)|
|Praca ze źródłami danych ADO.NET|[Instrukcje: Sortowanie i filtrowanie danych ADO.NET za pomocą Windows składnika BindingSource formularzy](./controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|
|Korzystanie z okna źródeł danych|[Wiązanie kontrolek Windows Forms z danymi w programie Visual Studio](/visualstudio/data-tools/bind-windows-forms-controls-to-data-in-visual-studio)|
|Przy użyciu ustawień aplikacji|[Instrukcje: Tworzenie ustawień aplikacji](./advanced/how-to-create-application-settings.md)|

### <a name="deploy-apps-to-client-computers"></a>Wdrażanie aplikacji na komputerach klienckich

Po napisaniu aplikację, konieczne jest wysłanie aplikacji dla użytkowników, aby zainstalować i uruchomić ją na komputerach klienckich. Korzystając z technologii ClickOnce, można wdrażać aplikacje z poziomu programu Visual Studio za pomocą kilku kliknięć i zapewnić swoim użytkownikom adres URL wskazujący aplikację w sieci Web. ClickOnce zarządza wszystkie elementy i zależności w aplikacji i gwarantuje, że aplikacja jest poprawnie zainstalowana na komputerze klienckim.

Aplikacje ClickOnce może być skonfigurowany do uruchamiania tylko wtedy, gdy użytkownik jest połączony z siecią lub uruchomić zarówno w trybie online i offline. Po określeniu, czy aplikacja powinna obsługiwać operacji w trybie offline, ClickOnce dodaje łącze do aplikacji w użytkownika **Start** menu. Następnie użytkownik może otwierać aplikacji, bez korzystania z adresu URL.

Podczas aktualizacji aplikacji, możesz opublikować nowy manifest wdrożenia i nową kopię aplikacji na serwerze sieci Web. ClickOnce wykryje, że nie jest dostępna aktualizacja i uaktualnienia instalacji przez użytkownika; nie niestandardowych programów jest wymagany do zaktualizowania starej zestawów.

#### <a name="deploy-clickonce-apps"></a>Wdrażanie aplikacji ClickOnce

Aby uzyskać pełne wprowadzenie do technologii ClickOnce, zobacz [wdrażania i zabezpieczeń ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment). Aby uzyskać szczegółowe informacje o sposobie używania tych funkcji zobacz poniższe tematy pomocy

|Opis|Temat pomocy|
|-----------------|----------------|
|Wdrażanie aplikacji przy użyciu technologii ClickOnce|[Instrukcje: Publikowanie aplikacji ClickOnce za pomocą Kreatora publikacji](/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [Przewodnik: Ręczne wdrażanie aplikacji ClickOnce](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|
|Aktualizowanie wdrożenia ClickOnce|[Instrukcje: Zarządzanie aktualizacjami dla aplikacji ClickOnce](/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|
|Zarządzanie zabezpieczeniami za pomocą technologii ClickOnce|[Instrukcje: Włączanie ustawień zabezpieczeń technologii ClickOnce](/visualstudio/deployment/how-to-enable-clickonce-security-settings)|

### <a name="other-controls-and-features"></a>Inne formanty i funkcje

Istnieje wiele innych funkcji w formularzach Windows Forms, wchodzące Implementowanie typowych zadań, szybkie i łatwe, takie jak obsługa tworzenie okien dialogowych, drukowanie, dodając pomocy i dokumentacji i lokalizowanie aplikacji na wiele języków. Ponadto formularze Windows opiera się na niezawodne zabezpieczenia systemu .NET Framework. Z tym systemem można zwolnić bardziej bezpieczne aplikacje swoim klientom.

#### <a name="implement-other-controls-and-features"></a>Implementowanie inne formanty i funkcje

Aby uzyskać szczegółowe informacje o sposobie używania tych funkcji zobacz następujące tematy Pomocy.

|Opis|Temat pomocy|
|-----------------|----------------|
|Drukowanie zawartości formularza|[Instrukcje: Drukowanie grafiki w formularzach Windows Forms](./advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [Instrukcje: Podglądu wydruku w formularzach Windows Forms](./advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|
|Więcej informacji na temat zabezpieczeń Windows Forms|[Przegląd zabezpieczeń w formularzach Windows Forms](security-in-windows-forms-overview.md)|

## <a name="see-also"></a>Zobacz także

- [Wprowadzenie do formularzy Windows Forms](getting-started-with-windows-forms.md)
- [Tworzenie nowego formularza systemu Windows](creating-a-new-windows-form.md)
- [ToolStrip, kontrolka — omówienie](./controls/toolstrip-control-overview-windows-forms.md)
- [DataGridView, kontrolka — omówienie](./controls/datagridview-control-overview-windows-forms.md)
- [BindingSource, składnik — omówienie](./controls/bindingsource-component-overview.md)
- [Przegląd ustawień aplikacji](./advanced/application-settings-overview.md)
- [Wskazówki dotyczące wdrażania i zabezpieczeń ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment)
