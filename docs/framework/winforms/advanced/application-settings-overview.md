---
title: Przegląd ustawień aplikacji
ms.date: 03/30/2017
f1_keywords:
- ApplicationsSettingsOverview
helpviewer_keywords:
- application settings [Windows Forms], about application settings
- dynamic properties
- user preferences [Windows Forms], tracking
ms.assetid: 0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc
ms.openlocfilehash: ec73fb61f0a4b43e47936c864e73355ee777aeb7
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040426"
---
# <a name="application-settings-overview"></a>Przegląd ustawień aplikacji
W tym temacie omówiono sposób tworzenia i przechowywania danych ustawień w imieniu aplikacji i użytkowników.

 Funkcja ustawienia aplikacji programu Windows Forms ułatwia tworzenie, przechowywanie i konserwowanie niestandardowych preferencji aplikacji oraz użytkowników na komputerze klienckim. Za pomocą ustawień aplikacji Windows Forms można przechowywać nie tylko dane aplikacji, takie jak parametry połączenia bazy danych, ale również dane specyficzne dla użytkownika, takie jak preferencje aplikacji użytkownika. Za pomocą programu Visual Studio lub niestandardowego kodu zarządzanego można utworzyć nowe ustawienia, odczytać je i zapisać na dysku, powiązać je z właściwościami w formularzach i zweryfikować dane ustawień przed załadowaniem i zapisaniem.

 Ustawienia aplikacji umożliwiają deweloperom Zapisywanie stanu w aplikacji przy użyciu bardzo małego kodu niestandardowego i zastępowanie właściwości dynamicznych we wcześniejszych wersjach .NET Framework. Ustawienia aplikacji zawierają wiele ulepszeń w porównaniu z właściwościami dynamicznymi, które są tylko do odczytu, z późnym wiązaniem i wymagają większej liczby niestandardowych programów programistycznych. Klasy właściwości dynamicznych zostały zachowane w .NET Framework 2,0, ale tylko klasy powłoki, które znacznie zawijają klasy ustawień aplikacji.

## <a name="what-are-application-settings"></a>Co to są ustawienia aplikacji?
 Aplikacje Windows Forms będą często wymagały danych, które mają kluczowe znaczenie dla uruchomienia aplikacji, ale które nie mają być uwzględniane bezpośrednio w kodzie aplikacji. Jeśli aplikacja korzysta z usługi sieci Web lub serwera bazy danych, możesz zapisać te informacje w osobnym pliku, aby można było je zmienić w przyszłości bez ponownego kompilowania. Podobnie aplikacje mogą wymagać przechowywania danych specyficznych dla bieżącego użytkownika. Większość aplikacji, na przykład, ma preferencje użytkownika, które dostosowują wygląd i zachowanie aplikacji.

 Ustawienia aplikacji dotyczą obu potrzeb, zapewniając łatwy sposób przechowywania ustawień z zakresu aplikacji i zakresu użytkownika na komputerze klienckim. Za pomocą programu Visual Studio lub edytora kodu definiuje się ustawienie dla danej właściwości, określając jego nazwę, typ danych i zakres (aplikację lub użytkownika). Możesz nawet umieścić powiązane ustawienia w nazwanych grupach, aby ułatwić ich użycie i czytelność. Po zdefiniowaniu te ustawienia są utrwalane i odczytywane w pamięci automatycznie w czasie wykonywania. Architektura podłączana umożliwia zmianę mechanizmu trwałości, ale domyślnie używany jest lokalny system plików.

 Ustawienia aplikacji działają przez utrwalanie danych jako XML do różnych plików konfiguracji (. config), odpowiadających tym, czy ustawienie jest w zakresie aplikacji, czy w zakresie użytkownika. W większości przypadków ustawienia o zakresie aplikacji są tylko do odczytu. ponieważ są one informacjami o programie, zazwyczaj nie trzeba ich zastąpić. Z kolei ustawienia o zakresie użytkownika mogą być odczytywane i bezpiecznie zapisywane w czasie wykonywania, nawet jeśli aplikacja działa w ramach częściowej relacji zaufania. Aby uzyskać więcej informacji o częściowej relacji zaufania, zobacz [zabezpieczenia w Windows Forms Omówienie](../security-in-windows-forms-overview.md).

 Ustawienia są przechowywane jako fragmenty XML w plikach konfiguracyjnych. Ustawienia o zakresie aplikacji są reprezentowane przez `<application.Settings>` element i ogólnie umieszczane w pliku *App*. exe. config, gdzie *App* to nazwa głównego pliku wykonywalnego. Ustawienia o zakresie użytkownika są reprezentowane przez `<userSettings>` element i są umieszczane w pliku *User*. config, gdzie *użytkownik* jest nazwą użytkownika osoby, która aktualnie uruchamia aplikację. Należy wdrożyć plik *App*. exe. config w swojej aplikacji. Architektura ustawień spowoduje utworzenie plików *User*. config na żądanie podczas pierwszego zapisywania ustawień dla tego użytkownika. Można również zdefiniować `<userSettings>` blok w pliku *App*. exe. config, aby zapewnić wartości domyślne dla ustawień o zakresie użytkownika.

 Formanty niestandardowe mogą również zapisywać własne ustawienia, implementując <xref:System.Configuration.IPersistComponentSettings> interfejs, który <xref:System.Configuration.IPersistComponentSettings.SaveSettings%2A> uwidacznia metodę. Formant Windows Forms <xref:System.Windows.Forms.ToolStrip> implementuje ten interfejs, aby zapisać położenie pasków narzędzi i elementów paska narzędzi między sesjami aplikacji. Aby uzyskać więcej informacji na temat kontrolek niestandardowych i ustawień aplikacji, zobacz [Ustawienia aplikacji dla formantów niestandardowych](application-settings-for-custom-controls.md).

## <a name="limitations-of-application-settings"></a>Ograniczenia ustawień aplikacji
 Nie można używać ustawień aplikacji w niezarządzanej aplikacji, która hostuje .NET Framework. Ustawienia nie będą działały w takich środowiskach jako dodatki programu Visual Studio, C++ w przypadku Microsoft Office, kontrolowania hostingu w programie Internet Explorer lub dodatków i projektów programu Microsoft Outlook.

 Obecnie nie można utworzyć powiązania z niektórymi właściwościami w Windows Forms. Najważniejszym przykładem jest <xref:System.Windows.Forms.Form.ClientSize%2A> właściwość, ponieważ powiązanie z tą właściwością może spowodować nieprzewidywalne zachowanie w czasie wykonywania. Zazwyczaj można obejść te problemy, zapisując i ładując te ustawienia programowo.

 Ustawienia aplikacji nie zawierają wbudowanej funkcji automatycznego szyfrowania informacji. Nie należy przechowywać informacji związanych z zabezpieczeniami, takich jak hasła do bazy danych, w postaci zwykłego tekstu. Jeśli chcesz przechowywać takie informacje poufne, jako że deweloper aplikacji jest odpowiedzialny za zapewnienie, że jest bezpieczny. Jeśli chcesz przechowywać parametry połączenia, zalecamy użycie zintegrowanych zabezpieczeń systemu Windows, a nie do kodowania haseł. Aby uzyskać więcej informacji, zobacz [zabezpieczenia dostępu kodu i ADO.NET](../../data/adonet/code-access-security.md).

## <a name="getting-started-with-application-settings"></a>Wprowadzenie z ustawieniami aplikacji
 Jeśli używasz programu Visual Studio, możesz zdefiniować ustawienia w Projektant formularzy systemu Windows przy użyciu właściwości **(ApplicationSettings)** w oknie **Właściwości** . Podczas definiowania ustawień w ten sposób program Visual Studio automatycznie tworzy niestandardową klasę otoki zarządzanej, która kojarzy każde ustawienie z właściwością klasy. Program Visual Studio wymaga również powiązania ustawienia z właściwością w formularzu lub kontrolce, aby ustawienia kontrolki były przywracane automatycznie, gdy formularz zostanie wyświetlony i zapisany automatycznie po zamknięciu formularza.

 Jeśli potrzebujesz bardziej szczegółowej kontroli nad ustawieniami, możesz zdefiniować własne klasy otoki ustawień aplikacji niestandardowych. Jest to realizowane przez wymienienie klasy z <xref:System.Configuration.ApplicationSettingsBase>, dodanie właściwości, która odnosi się do każdego ustawienia, i zastosowanie atrybutów specjalnych do tych właściwości. Aby uzyskać szczegółowe informacje na temat tworzenia klas otoki, zobacz [Architektura ustawień aplikacji](application-settings-architecture.md).

 Można również użyć klasy, <xref:System.Windows.Forms.Binding> aby programowo powiązać ustawienia z właściwościami formularzy i kontrolek.

## <a name="see-also"></a>Zobacz także

- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.SettingsProvider>
- <xref:System.Configuration.LocalFileSettingsProvider>
- <xref:System.Configuration.IPersistComponentSettings>
- [Instrukcje: Sprawdzanie poprawności ustawień aplikacji](how-to-validate-application-settings.md)
- [Zarządzanie ustawieniami aplikacji (.NET)](/visualstudio/ide/managing-application-settings-dotnet)
- [Instrukcje: Odczytywanie ustawień w czasie wykonywania za pomocąC#](how-to-read-settings-at-run-time-with-csharp.md)
- [Używanie ustawień aplikacji i ustawień użytkownika](using-application-settings-and-user-settings.md)
- [Architektura ustawień aplikacji](application-settings-architecture.md)
- [Ustawienia aplikacji dotyczące kontrolek niestandardowych](application-settings-for-custom-controls.md)
