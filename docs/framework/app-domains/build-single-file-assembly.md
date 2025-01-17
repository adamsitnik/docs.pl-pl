---
title: 'Instrukcje: kompilowanie zestawu .NET Framework jednego pliku'
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest, single-file assemblies
- library assemblies
- command-line compilers
- assemblies [.NET Framework], single-file
- output file name for assemblies
- code modules
- single-file assemblies
dev_langs:
- csharp
- vb
ms.assetid: a6063221-43a5-4d3e-814c-288a4ec69aec
ms.openlocfilehash: af1bfb89b01a316a858cbb45bf19a26a16d90016
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73119948"
---
# <a name="how-to-build-a-net-framework-single-file-assembly"></a>Instrukcje: kompilowanie zestawu .NET Framework jednego pliku

Zestaw jednoplikowy, który jest najprostszym typem zestawu, zawiera informacje o typie i implementację, a także [manifest zestawu](../../standard/assembly/manifest.md). Można użyć kompilatorów wiersza polecenia lub programu Visual Studio, aby utworzyć zestaw jednoplikowy, który jest przeznaczony dla .NET Framework. Domyślnie kompilator tworzy plik zestawu z rozszerzeniem *. exe* .

> [!NOTE]
> Programu Visual Studio C# for i Visual Basic można używać tylko do tworzenia zestawów jednoplikowych. Jeśli chcesz utworzyć zestawy wieloplikowe, musisz użyć kompilatorów wiersza polecenia lub wizualizacji C++.

W poniższych procedurach pokazano, jak utworzyć zestawy Jednoplikowe za pomocą kompilatorów wiersza polecenia.

## <a name="create-an-assembly-with-an-exe-extension"></a>Utwórz zestaw z rozszerzeniem. exe

W wierszu polecenia wpisz następujące polecenie:

\<*polecenie kompilatora*> \<*Nazwa modułu*>

W tym poleceniu *kompilator* jest poleceniem kompilatora dla języka używanego w module kodu, a *Nazwa modułu* to nazwa modułu kodu do skompilowania do zestawu.

Poniższy przykład tworzy zestaw o nazwie mój *Code. exe* z modułu kodu o nazwie `myCode`.

```csharp
csc myCode.cs
```

```vb
vbc myCode.vb
```

## <a name="create-an-assembly-with-an-exe-extension-and-specify-the-output-file-name"></a>Tworzenie zestawu z rozszerzeniem. exe i Określanie nazwy pliku wyjściowego

W wierszu polecenia wpisz następujące polecenie:

\<*polecenie kompilatora*>  **/out:** \<*nazwy pliku*> \<*Nazwa modułu*>

W tym poleceniu *kompilator* jest poleceniem kompilatora dla języka używanego w module kodu, *Nazwa pliku* jest nazwą pliku wyjściowego, a *Nazwa modułu* to nazwa modułu kodu do skompilowania do zestawu.

Poniższy przykład tworzy zestaw o nazwie mój *Assembly. exe* z modułu kodu o nazwie `myCode`.

```csharp
csc -out:myAssembly.exe myCode.cs
```

```vb
vbc -out:myAssembly.exe myCode.vb
```

## <a name="create-library-assemblies"></a>Utwórz zestawy bibliotek
 Zestaw biblioteki jest podobny do biblioteki klas. Zawiera typy, do których odwołują się inne zestawy, ale nie ma punktu wejścia, aby rozpocząć wykonywanie.

Aby utworzyć zestaw biblioteki, w wierszu polecenia wpisz następujące polecenie:

\<*polecenie kompilatora*>  **-t:Library** \<*Nazwa modułu*>

W tym poleceniu *kompilator* jest poleceniem kompilatora dla języka używanego w module kodu, a *Nazwa modułu* to nazwa modułu kodu do skompilowania do zestawu. Można również użyć innych opcji kompilatora, takich jak opcja **-out:** .

Poniższy przykład tworzy zestaw biblioteki o nazwie *myCodeAssembly. dll* z modułu kodu o nazwie `myCode`.

```csharp
csc -out:myCodeLibrary.dll -t:library myCode.cs
```

```vb
vbc -out:myCodeLibrary.dll -t:library myCode.vb
```

## <a name="see-also"></a>Zobacz także

- [Tworzenie zestawów](../../standard/assembly/create.md)
- [Zestawy wieloplikowe](multifile-assemblies.md)
- [Instrukcje: kompilowanie zestawu wieloplikowego](build-multifile-assembly.md)
- [Program z zestawami](../../standard/assembly/program.md)
