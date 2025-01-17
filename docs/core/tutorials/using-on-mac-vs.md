---
title: Rozpoczynanie pracy z platformą .NET Core w systemie macOS przy użyciu programu Visual Studio dla komputerów Mac
description: W tym temacie omówiono tworzenie prostej aplikacji konsolowej przy użyciu Visual Studio dla komputerów Mac i .NET Core.
author: mairaw
ms.date: 07/11/2019
ms.custom: seodec18
ms.openlocfilehash: 77e676c327b62369e7ddb9444bf8f246d3c5c2e8
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182502"
---
# <a name="get-started-with-net-core-on-macos-using-visual-studio-for-mac"></a>Rozpoczynanie pracy z platformą .NET Core w systemie macOS przy użyciu programu Visual Studio dla komputerów Mac

Visual Studio dla komputerów Mac udostępnia w pełni funkcjonalne zintegrowane środowisko programistyczne (IDE) do tworzenia aplikacji platformy .NET Core. W tym temacie omówiono tworzenie prostej aplikacji konsolowej przy użyciu Visual Studio dla komputerów Mac i .NET Core.

> [!NOTE]
> Opinie są wysoce wyceniane. Istnieją dwa sposoby przekazywania opinii zespołowi programistycznemu na Visual Studio dla komputerów Mac:
>
> * W Visual Studio dla komputerów Mac wybierz pozycję **Pomoc** > **Zgłoś problem** z menu lub **Zgłoś problem** na ekranie powitalnym, co spowoduje otwarcie okna do zgłoszenia usterki. Swoje opinie możesz śledzić w portalu [Społeczność deweloperów](https://developercommunity.visualstudio.com/spaces/8/index.html).
> * Aby skorzystać z sugestii, wybierz pozycję **Pomoc** > **Podaj sugestię** z menu lub **Podaj sugestię** na ekranie powitalnym, co spowoduje przejście do [strony internetowej społeczność deweloperów Visual Studio dla komputerów Mac](https://developercommunity.visualstudio.com/content/idea/post.html?space=41).

## <a name="prerequisites"></a>Wymagania wstępne

Zapoznaj się z tematem [wymagania wstępne dotyczące programu .NET Core w systemie Mac](../macos-prerequisites.md) .

Zapoznaj się z artykułem [obsługi .NET Core](/visualstudio/mac/net-core-support) , aby upewnić się, że używasz obsługiwanej wersji programu .NET Core.

## <a name="get-started"></a>Wprowadzenie

Jeśli zainstalowano już wymagania wstępne i Visual Studio dla komputerów Mac, Pomiń tę sekcję i Kontynuuj, aby [utworzyć projekt](#creating-a-project). Wykonaj następujące kroki, aby zainstalować wymagania wstępne i Visual Studio dla komputerów Mac:

Pobierz [instalatora Visual Studio dla komputerów Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link). Uruchom Instalatora. Przeczytaj i zaakceptuj umowę licencyjną. Podczas instalacji wybierz opcję zainstalowania platformy .NET Core. Masz możliwość zainstalowania platformy Xamarin, wieloplatformowej technologii tworzenia aplikacji mobilnych. Instalowanie programu Xamarin i powiązanych z nim składników jest opcjonalne w przypadku programowania w środowisku .NET Core. Aby zapoznać się z procesem instalacji Visual Studio dla komputerów Mac, zobacz [dokumentację usługi Visual Studio dla komputerów Mac](/visualstudio/mac/). Po zakończeniu instalacji uruchom Visual Studio dla komputerów Mac IDE.

## <a name="creating-a-project"></a>Tworzenie projektu

1. W oknie uruchamiania wybierz pozycję **Nowy** .

   ![Przycisk Nowy na ekranie startowym Visual Studio dla komputerów Mac](./media/using-on-mac-vs/visual-studio-mac-new-project.png)

1. W oknie dialogowym **Nowy projekt** wybierz pozycję **aplikacja** w węźle **.NET Core** . Wybierz szablon **aplikacji konsolowej** , a następnie przycisk **dalej**.

   ![Lista nowych szablonów projektu](./media/using-on-mac-vs/visual-studio-mac-new-dialog.png)

1. Jeśli masz zainstalowaną więcej niż jedną wersję programu .NET Core, Wybierz platformę docelową dla projektu.

1. Wpisz "HelloWorld" dla **nazwy projektu**. Wybierz pozycję **Utwórz**.

   ![Okno dialogowe Konfigurowanie nowej aplikacji konsolowej](./media/using-on-mac-vs/visual-studio-mac-new-options.png)

1. Zaczekaj na przywrócenie zależności projektu. Projekt ma C# jeden plik, *program.cs* `Program` , zawierający klasę z `Main` metodą. `Console.WriteLine` Instrukcja zwróci wartość "Hello World!" do konsoli programu, gdy aplikacja jest uruchomiona.

   ![Okno główne z otwartym plikiem Program.cs](./media/using-on-mac-vs/visual-studio-mac-editor.png)

## <a name="run-the-application"></a>Uruchamianie aplikacji

Uruchom aplikację w trybie debugowania za pomocą polecenia ⌘ ↵ (Command + Enter) lub w trybie wydania przy użyciu ⌥ ⌘ ↵ (Option + Command + Enter).

![W okienku danych wyjściowych aplikacji zostanie wyświetlona Hello world!](./media/using-on-mac-vs/visual-studio-mac-output.png)

## <a name="next-step"></a>Następny krok

[Tworzenie kompletnego rozwiązania .NET Core w systemie macOS za pomocą Visual Studio dla komputerów Mac](using-on-mac-vs-full-solution.md) tematu pokazuje, jak utworzyć kompletne rozwiązanie .NET Core, które obejmuje bibliotekę wielokrotnego użytku i testy jednostkowe.
