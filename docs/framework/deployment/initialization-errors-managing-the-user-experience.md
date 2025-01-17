---
title: 'Błędy inicjowania .NET Framework: Zarządzanie czynnościami użytkownika'
ms.date: 03/30/2017
helpviewer_keywords:
- no framework found experience
- initialization errors [.NET Framework]
- .NET Framework, initialization errors
ms.assetid: 680a7382-957f-4f6e-b178-4e866004a07e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ce022e92e8b6770c42800a04a349eff751bdb708
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052063"
---
# <a name="net-framework-initialization-errors-managing-the-user-experience"></a>Błędy inicjowania .NET Framework: Zarządzanie czynnościami użytkownika

System aktywacji środowiska uruchomieniowego języka wspólnego (CLR) określa wersję środowiska CLR, która będzie używana do uruchamiania kodu aplikacji zarządzanej. W niektórych przypadkach system aktywacji może nie być w stanie znaleźć wersji środowiska CLR do załadowania. Ta sytuacja zwykle występuje, gdy aplikacja wymaga wersji środowiska CLR, która jest nieprawidłowa lub nie jest zainstalowana na danym komputerze. Jeśli żądana wersja nie zostanie znaleziona, system aktywacji środowiska CLR zwróci kod błędu HRESULT z funkcji lub interfejsu, który został wywołany, i może wyświetlić komunikat o błędzie dla użytkownika, który uruchomił aplikację. W tym artykule przedstawiono listę kodów HRESULT i wyjaśniono, jak można zapobiec wyświetlaniu komunikatu o błędzie.

Środowisko CLR udostępnia infrastrukturę rejestrowania ułatwiającą Debugowanie problemów z aktywacją środowiska CLR, zgodnie [z opisem w temacie How to: Debuguj problemy](how-to-debug-clr-activation-issues.md)z aktywacją środowiska CLR. Tej infrastruktury nie należy mylić z [dziennikami powiązań zestawów](../tools/fuslogvw-exe-assembly-binding-log-viewer.md), które są całkowicie inne.

## <a name="clr-activation-hresult-codes"></a>Kody HRESULT aktywacji środowiska CLR

Interfejsy API aktywacji środowiska CLR zwracają kody HRESULT, aby zgłosić wynik operacji aktywacji do hosta. Hosty CLR powinny zawsze sprawdzać te wartości zwracane przed kontynuowaniem dodatkowych operacji.

- CLR_E_SHIM_RUNTIMELOAD

- CLR_E_SHIM_RUNTIMEEXPORT

- CLR_E_SHIM_INSTALLROOT

- CLR_E_SHIM_INSTALLCOMP

- CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND

- CLR_E_SHIM_SHUTDOWNINPROGRESS

## <a name="ui-for-initialization-errors"></a>Interfejs użytkownika dla błędów inicjowania

Jeśli system aktywacji środowiska CLR nie może załadować prawidłowej wersji środowiska uruchomieniowego wymaganego przez aplikację, program wyświetli komunikat o błędzie informujący o tym, że ich komputer nie jest prawidłowo skonfigurowany do uruchamiania aplikacji i udostępnia je możliwość naprawienia sytuacji. Następujący komunikat o błędzie jest zazwyczaj prezentowany w takiej sytuacji. Użytkownik może wybrać opcję **tak** , aby przejść do witryny internetowej firmy Microsoft, w której można pobrać poprawną wersję .NET Framework aplikacji.

![Błąd inicjowania .NET Framework] — okno dialogowe (./media/initialization-errors-managing-the-user-experience/initialization-error-dialog.png "Typowy komunikat o błędzie dotyczący błędów inicjowania")

## <a name="resolving-the-initialization-error"></a>Rozwiązywanie błędu inicjowania

Deweloperem jest wiele opcji kontrolowania komunikatu o błędzie inicjalizacji .NET Framework. Można na przykład użyć flagi interfejsu API, aby zapobiec wyświetlaniu komunikatu, zgodnie z opisem w następnej sekcji. Jednak nadal trzeba rozwiązać problem uniemożliwiający aplikacji załadowanie żądanego środowiska uruchomieniowego. W przeciwnym razie aplikacja może nie działać wcale lub niektóre funkcje mogą być niedostępne.

Aby rozwiązać podstawowe problemy i zapewnić najlepsze środowisko użytkownika (mniej komunikatów o błędach), zalecamy wykonanie następujących czynności:

- W przypadku aplikacji .NET Framework 3,5 (i starszych): Skonfiguruj aplikację do obsługi .NET Framework 4 lub nowszej wersji (zobacz [instrukcje](../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)).

- Dla aplikacji .NET Framework 4: Zainstaluj pakiet redystrybucyjny .NET Framework 4 w ramach konfiguracji aplikacji. Zobacz [Przewodnik wdrażania dla deweloperów](deployment-guide-for-developers.md).

## <a name="controlling-the-error-message"></a>Kontrolowanie komunikatu o błędzie

Wyświetlenie komunikatu o błędzie w celu komunikowania się, że żądana wersja .NET Framework nie została znaleziona, może być wyświetlana jako przydatna usługa lub niewielki Annoyance dla użytkowników. W obu przypadkach można kontrolować ten interfejs użytkownika przez przekazanie flag do interfejsów API aktywacji.

Metoda [ICLRMetaHostPolicy:: GetRequestedRuntime —](../unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) akceptuje element członkowski wyliczenia [METAHOST_POLICY_FLAGS](../unmanaged-api/hosting/metahost-policy-flags-enumeration.md) jako dane wejściowe. Możesz dołączyć flagę METAHOST_POLICY_SHOW_ERROR_DIALOG, aby zażądać komunikatu o błędzie, jeśli nie znaleziono wymaganej wersji środowiska CLR. Domyślnie komunikat o błędzie nie jest wyświetlany. (Metoda [ICLRMetaHost:: GetRuntime](../unmanaged-api/hosting/iclrmetahost-getruntime-method.md) nie akceptuje tej flagi i nie zapewnia żadnych innych metod wyświetlania komunikatu o błędzie).

System Windows udostępnia funkcję [SetErrorMode](https://go.microsoft.com/fwlink/p/?LinkID=255242) , której można użyć do zadeklarowania, czy komunikaty o błędach mają być wyświetlane jako wynik kodu, który jest uruchamiany w ramach procesu. Możesz określić flagę SEM_FAILCRITICALERRORS, aby zapobiec wyświetlaniu komunikatu o błędzie.

Jednak w niektórych scenariuszach ważne jest zastąpienie ustawień SEM_FAILCRITICALERRORS ustawionych przez proces aplikacji. Na przykład jeśli masz natywny składnik COM obsługujący środowisko CLR i który jest hostowany w procesie, w którym ustawiono SEM_FAILCRITICALERRORS, możesz chcieć zastąpić flagę w zależności od wpływu wyświetlania komunikatów o błędach w ramach tego procesu aplikacji. W takim przypadku można użyć jednej z następujących flag, aby przesłonić SEM_FAILCRITICALERRORS:

- Użyj METAHOST_POLICY_IGNORE_ERROR_MODE z metodą [ICLRMetaHostPolicy:: GetRequestedRuntime —](../unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) .

- Użyj RUNTIME_INFO_IGNORE_ERROR_MODE z funkcją [GetRequestedRuntimeInfo —](../unmanaged-api/hosting/getrequestedruntimeinfo-function.md) .

## <a name="ui-policy-for-clr-provided-hosts"></a>Zasady interfejsu użytkownika dla hostów udostępnianych przez środowisko CLR

Środowisko CLR zawiera zestaw hostów dla różnych scenariuszy, a wszystkie te hosty wyświetlają komunikat o błędzie, gdy wystąpią problemy z załadowaniem wymaganej wersji środowiska uruchomieniowego. Poniższa tabela zawiera listę hostów i ich zasad dotyczących komunikatów o błędach.

|Host CLR|Opis|Zasady dotyczące komunikatów o błędach|Czy komunikat o błędzie może być wyłączony?|
|--------------|-----------------|--------------------------|------------------------------------|
|Zarządzany Host EXE|Uruchamia zarządzaną exe.|Jest wyświetlany w przypadku brakującej wersji .NET Framework|Nie|
|Zarządzany Host COM|Ładuje zarządzane składniki COM do procesu.|Jest wyświetlany w przypadku brakującej wersji .NET Framework|Tak, ustawiając flagę SEM_FAILCRITICALERRORS|
|Host ClickOnce|Uruchamia aplikacje ClickOnce.|Jest wyświetlany w przypadku braku .NET Framework wersji, począwszy od .NET Framework 4,5|Nie|
|Host XBAP|Uruchamia aplikacje aplikacji XBAP platformy WPF.|Jest wyświetlany w przypadku braku .NET Framework wersji, począwszy od .NET Framework 4,5|Nie|

## <a name="windows-8-behavior-and-ui"></a>Zachowanie i interfejs użytkownika systemu Windows 8

System aktywacji środowiska CLR zapewnia takie samo zachowanie i interfejs użytkownika [!INCLUDE[win8](../../../includes/win8-md.md)] , jak w przypadku innych wersji systemu operacyjnego Windows, z wyjątkiem sytuacji, gdy występują problemy z ładowaniem środowiska CLR 2,0. [!INCLUDE[win8](../../../includes/win8-md.md)]zawiera .NET Framework 4,5, który używa CLR 4,5. [!INCLUDE[win8](../../../includes/win8-md.md)] Jednakże nie obejmuje .NET Framework 2,0, 3,0 lub 3,5, które są używane przez środowisko CLR 2,0. W związku z tym aplikacje, które są zależne od CLR 2,0, [!INCLUDE[win8](../../../includes/win8-md.md)] nie są domyślnie uruchamiane. Zamiast tego wyświetlają następujące okno dialogowe umożliwiające użytkownikom instalowanie .NET Framework 3,5. Użytkownicy mogą również włączyć .NET Framework 3,5 w panelu sterowania. Obie opcje zostały omówione w artykule [instalowanie .NET Framework 3,5 w systemie Windows 10, Windows 8.1 i Windows 8](../install/dotnet-35-windows-10.md).

Okno ![dialogowe instalacji 3,5 w systemie Windows 8](./media/initialization-errors-managing-the-user-experience/install-framework-on-demand-dialog.png "Monituj o zainstalowanie .NET Framework 3,5 na żądanie")

> [!NOTE]
> .NET Framework 4,5 zastępuje .NET Framework 4 (CLR 4) na komputerze użytkownika. W [!INCLUDE[win8](../../../includes/win8-md.md)]związku z tym .NET Framework 4 aplikacje działają bezproblemowo, bez wyświetlania tego okna dialogowego.

Po zainstalowaniu .NET Framework 3,5 Użytkownicy mogą uruchamiać aplikacje, które są zależne od .NET Framework 2,0, 3,0 lub 3,5 na swoich [!INCLUDE[win8](../../../includes/win8-md.md)] komputerach. Mogą również uruchamiać aplikacje .NET Framework 1,0 i 1,1, pod warunkiem, że te aplikacje nie są jawnie skonfigurowane do uruchamiania wyłącznie na .NET Framework 1,0 lub 1,1. Zobacz [Migrowanie z .NET Framework 1,1](../migration-guide/migrating-from-the-net-framework-1-1.md).

Począwszy od .NET Framework 4,5, Ulepszono rejestrowanie aktywacji środowiska CLR w celu uwzględnienia wpisów dziennika, które są rejestrowane, kiedy i dlaczego zostanie wyświetlony komunikat o błędzie inicjalizacji. Aby uzyskać więcej informacji, zobacz [jak: Debuguj problemy](how-to-debug-clr-activation-issues.md)z aktywacją środowiska CLR.

## <a name="see-also"></a>Zobacz także

- [Przewodnik wdrażania dla deweloperów](deployment-guide-for-developers.md)
- [Instrukcje: Skonfiguruj aplikację do obsługi .NET Framework 4 lub nowszej wersji](../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
- [Instrukcje: Debugowanie problemów dotyczących aktywacji środowiska CLR](how-to-debug-clr-activation-issues.md)
- [Instalowanie programu .NET Framework 3.5 w systemie Windows 10, Windows 8.1 lub Windows 8](../install/dotnet-35-windows-10.md)
