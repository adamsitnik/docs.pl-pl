---
title: Wprowadzenie do platformy .NET Core
description: Znajdź zasoby, aby dowiedzieć się, jak tworzyć aplikacje .NET Core w systemach Windows, Linux i macOS.
author: thraka
ms.author: adegeo
ms.date: 09/19/2019
ms.openlocfilehash: 9dbc3ebc8d43fe2570a90f4e10fd155a5b114351
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72521628"
---
# <a name="get-started-with-net-core"></a>Wprowadzenie do platformy .NET Core

Ten artykuł zawiera informacje na temat rozpoczynania pracy z platformą .NET Core. Program .NET Core można zainstalować w systemach Windows, Linux i macOS. Możesz zakodować w ulubionym edytorze tekstów i tworzyć Międzyplatformowe biblioteki i aplikacje. 

Jeśli nie masz pewności, co to jest platforma .NET Core, lub jak odnosi się do innych technologii .NET, Zacznij od omówienia [programu .NET](https://dotnet.microsoft.com/learn/dotnet/what-is-dotnet) . Po prostu, .NET Core to wieloplatformowa implementacja platformy .NET.

## <a name="create-an-application"></a>Tworzenie aplikacji

Najpierw pobierz i zainstaluj [zestaw .NET Core SDK](https://dotnet.microsoft.com/download) na komputerze.

Następnie otwórz Terminal, taki jak **PowerShell**, **wiersza polecenia**lub **bash**. Wpisz następujące polecenia `dotnet`, aby utworzyć i uruchomić C# aplikację:

```dotnetcli
dotnet new console --output sample1
dotnet run --project sample1
```

Powinny zostać wyświetlone następujące dane wyjściowe:

```console
Hello World!
```

Nabycia! Utworzono prostą aplikację platformy .NET Core. Można również użyć [Visual Studio Code](tutorials/with-visual-studio-code.md), [Visual Studio](tutorials/with-visual-studio.md) (tylko Windows) lub [Visual Studio dla komputerów Mac](tutorials/using-on-mac-vs.md) (tylko macOS), aby utworzyć aplikację platformy .NET Core.

## <a name="tutorials"></a>Samouczki

Możesz rozpocząć tworzenie aplikacji platformy .NET Core, wykonując te Samouczki krok po kroku.

<!-- markdownlint-disable MD025 -->

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

- [Kompiluj aplikację C# "Hello World" przy użyciu platformy .NET Core w programie Visual Studio 2017.](./tutorials/with-visual-studio.md)
- [Kompiluj bibliotekę C# klas z platformą .NET Core w programie Visual Studio 2017.](./tutorials/library-with-visual-studio.md)
- [Kompiluj Visual Basic "Hello world" z platformą .NET Core w programie Visual Studio 2017.](./tutorials/vb-with-visual-studio.md)
- [Kompiluj bibliotekę klas z Visual Basic i .NET Core w programie Visual Studio 2017.](./tutorials/vb-library-with-visual-studio.md)  
- Obejrzyj film wideo na [temat sposobu instalowania i używania Visual Studio Code i platformy .NET Core](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core/).
- Obejrzyj film wideo na [temat sposobu instalowania i używania programów Visual Studio 2017 i .NET Core](https://channel9.msdn.com/Blogs/dotnet/Get-Started-NET-Core-Visual-Studio-2017/).
- [Wprowadzenie do programu .NET Core przy użyciu wiersza polecenia.](tutorials/using-with-xplat-cli.md)

Listę obsługiwanych wersji systemu Windows można znaleźć w artykule [dotyczącym wymagań wstępnych dotyczących programowania systemu Windows](windows-prerequisites.md) .

# <a name="linuxtablinux"></a>[System](#tab/linux)

Aby rozpocząć tworzenie aplikacji platformy .NET Core, wykonaj następujące Samouczki krok po kroku:

- [Wprowadzenie do programu .NET Core przy użyciu wiersza polecenia.](tutorials/using-with-xplat-cli.md)
- Obejrzyj film wideo [z wprowadzeniem do Visual Studio Code przy C# użyciu oprogramowania i platformy .NET Core w systemie Ubuntu](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu).

Listę obsługiwanych dystrybucje i wersji systemu Linux można znaleźć w artykule dotyczącym [wymagań wstępnych dotyczących programowania w systemie Linux](linux-prerequisites.md) .

# <a name="macostabmacos"></a>[macOS](#tab/macos)

Aby rozpocząć tworzenie aplikacji platformy .NET Core, wykonaj następujące Samouczki krok po kroku:

- Obejrzyj film wideo [z wprowadzeniem do Visual Studio Code przy C# użyciu oprogramowania i platformy .NET Core w systemie macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-NET-Core-Mac).
- [Wprowadzenie do programu .NET Core w systemie macOS przy użyciu Visual Studio Code.](tutorials/using-on-macos.md)
- [Wprowadzenie do programu .NET Core przy użyciu wiersza polecenia.](tutorials/using-with-xplat-cli.md)
- [Rozpoczynanie pracy z platformą .NET Core w systemie macOS przy użyciu Visual Studio dla komputerów Mac.](tutorials/using-on-mac-vs.md)
- [Utwórz kompletne rozwiązanie platformy .NET Core w systemie macOS przy użyciu Visual Studio dla komputerów Mac.](tutorials/using-on-mac-vs-full-solution.md)

Listę obsługiwanych wersji systemu OS X/macOS można znaleźć w artykule [dotyczącym wymagań wstępnych dotyczących programowania macOS](macos-prerequisites.md) .

---
