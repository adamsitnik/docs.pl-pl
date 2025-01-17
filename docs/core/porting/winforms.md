---
title: Port aplikacji Windows Forms do programu .NET Core 3,0
description: Naucz się, w jaki sposób portować .NET Framework aplikację Windows Forms do programu .NET Core 3,0 dla systemu Windows.
author: Thraka
ms.author: adegeo
ms.date: 03/01/2019
ms.custom: ''
ms.openlocfilehash: 7480c86af1acd482adff5e3e24dc229f24af0e5b
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216321"
---
# <a name="how-to-port-a-windows-forms-desktop-app-to-net-core"></a>Instrukcje: Port aplikacji klasycznej Windows Forms do programu .NET Core

W tym artykule opisano sposób przenoszenia aplikacji klasycznej opartej na Windows Forms z .NET Framework do programu .NET Core 3,0. Zestaw .NET Core 3,0 SDK obejmuje obsługę aplikacji Windows Forms. Windows Forms nadal jest strukturą tylko dla systemu Windows i działa tylko w systemie Windows. W tym przykładzie jest używany interfejs wiersza polecenia zestaw .NET Core SDK do tworzenia projektu i zarządzania nim.

W tym artykule różne nazwy są używane do identyfikowania typów plików używanych do migracji. Podczas migrowania projektu pliki będą wyglądać inaczej, dlatego można je dopasować do nich w sposób psychiczny do wymienionych poniżej:

| Plik | Opis |
| ---- | ----------- |
| **MyApps.sln** | Nazwa pliku rozwiązania. |
| **MyForms.csproj** | Nazwa .NET Framework Windows Forms projektu do portów. |
| **MyFormsCore.csproj** | Nazwa nowego projektu .NET Core, który tworzysz. |
| **MyAppCore.exe** | Plik wykonywalny aplikacji .NET Core Windows Forms. |

## <a name="prerequisites"></a>Wymagania wstępne

- [Program Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) dla wszystkich zadań, które chcesz wykonać.

  Zainstaluj następujące obciążenia programu Visual Studio:
  - Programowanie aplikacji klasycznych dla platformy .NET
  - Programowanie dla wielu platform w środowisku .NET

- Projekt działającego Windows Forms w rozwiązaniu, które kompiluje i uruchamia bez problemu.
- Projekt musi być zakodowany w C#. 
- Zainstaluj najnowszą wersję zapoznawczą [programu .NET Core 3,0](https://aka.ms/netcore3download) .

>[!NOTE]
>**Program Visual Studio 2017** nie obsługuje projektów programu .net Core 3,0. **Program Visual Studio 2019** obsługuje projekty platformy .net Core 3,0, ale nie obsługuje jeszcze projektanta wizualizacji dla projektów .net core 3,0 Windows Forms. Aby użyć projektanta wizualnego, musisz mieć projekt .NET Windows Forms w rozwiązaniu, które współużytkuje pliki formularzy z projektem platformy .NET Core.

### <a name="consider"></a>Pod

Podczas przenoszenia aplikacji Windows Forms .NET Framework należy wziąć pod uwagę kilka rzeczy.

01. Sprawdź, czy aplikacja jest dobrym kandydatem do migracji.

    Użyj [analizatora przenośności platformy .NET](../../standard/analyzers/portability-analyzer.md) , aby określić, czy projekt zostanie zmigrowany do programu .net Core 3,0. Jeśli projekt zawiera problemy z platformą .NET Core 3,0, Analizator pomaga zidentyfikować te problemy.

01. Używasz innej wersji Windows Forms.

    Po wydaniu programu .NET Core 3,0 w wersji zapoznawczej 1 Windows Forms mógł zostać otwartym źródłem w serwisie GitHub. Kod dla Windows Forms .NET Core jest rozwidleniem bazy kodu .NET Framework Windows Forms. Istnieją pewne różnice, które nie są dostępne dla aplikacji.

01. [Pakiet zgodności systemu Windows][compat-pack] może pomóc w migracji.

    Niektóre interfejsy API, które są dostępne w .NET Framework nie są dostępne w programie .NET Core 3,0. [Pakiet zgodności systemu Windows][compat-pack] dodaje wiele z tych interfejsów API i może pomóc aplikacji Windows Forms być zgodny z platformą .NET Core.

01. Zaktualizuj pakiety NuGet używane przez Twój projekt.

    Zawsze dobrym sposobem jest użycie najnowszych wersji pakietów NuGet przed migracją. Jeśli aplikacja odwołuje się do wszystkich pakietów NuGet, zaktualizuj je do najnowszej wersji. Upewnij się, że aplikacja została pomyślnie skompilowana. Po uaktualnieniu, jeśli występują jakiekolwiek błędy pakietów, można obniżyć pakiet do najnowszej wersji, która nie powoduje przerwania kodu.

01. Program Visual Studio 2019 jeszcze nie obsługuje projektanta formularzy dla programu .NET Core 3,0

    Obecnie należy zachować istniejące .NET Framework Windows Forms pliku projektu, jeśli chcesz użyć projektanta formularzy z programu Visual Studio.

## <a name="create-a-new-sdk-project"></a>Utwórz nowy projekt zestawu SDK

Nowy projekt platformy .NET Core 3,0, który tworzysz, musi znajdować się w innym katalogu niż projekt .NET Framework. Jeśli oba te elementy znajdują się w tym samym katalogu, może wystąpić konflikt z plikami, które są generowane w katalogu **obj** . W tym przykładzie utworzymy katalog o nazwie **MyFormsAppCore** w katalogu **SolutionFolder** :

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
└───MyFormsAppCore      <--- New folder for core project
```

Następnie należy utworzyć projekt **MyFormsCore. csproj** w katalogu **MyFormsAppCore** . Ten plik można utworzyć ręcznie przy użyciu edytora tekstu. Wklej następujący kod XML:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>
  </PropertyGroup>

</Project>
```

Jeśli nie chcesz tworzyć pliku projektu ręcznie, możesz użyć programu Visual Studio lub zestaw .NET Core SDK do wygenerowania projektu. Należy jednak usunąć wszystkie inne pliki wygenerowane przez szablon projektu, z wyjątkiem pliku projektu. Aby użyć zestawu SDK, uruchom następujące polecenie w katalogu **SolutionFolder** :

```dotnetcli
dotnet new winforms -o MyFormsAppCore -n MyFormsCore
```

Po utworzeniu **MyFormsCore. csproj**struktura katalogów powinna wyglądać następująco:

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
└───MyFormsAppCore
    └───MyFormsCore.csproj
```

Należy dodać projekt **MyFormsCore. csproj** do elementu **webapps. sln** z programem Visual Studio lub interfejs wiersza polecenia platformy .NET Core z katalogu **SolutionFolder** :

```dotnetcli
dotnet sln add .\MyFormsAppCore\MyFormsCore.csproj
```

## <a name="fix-assembly-info-generation"></a>Napraw generowanie informacji o zestawie

Windows Forms projekty, które zostały utworzone za pomocą .NET Framework `AssemblyInfo.cs` obejmują plik, który zawiera atrybuty zestawu, takie jak wersja zestawu do wygenerowania. Projekty w stylu zestawu SDK automatycznie generują te informacje na podstawie pliku projektu zestawu SDK. W przypadku obu typów "informacje o zestawie" powstaje konflikt. Rozwiąż ten problem, wyłączając automatyczne generowanie, co wymusza, aby projekt korzystał `AssemblyInfo.cs` z istniejącego pliku.

Istnieją trzy ustawienia do dodania do węzła głównego `<PropertyGroup>` . 

- **GenerateAssemblyInfo**\
Ustawienie tej właściwości na `false`, nie spowoduje wygenerowanie atrybutów zestawu. Pozwala to uniknąć konfliktu z istniejącym `AssemblyInfo.cs` plikiem z projektu .NET Framework.

- **AssemblyName**\
Wartością tej właściwości jest wyjściowy plik binarny tworzony podczas kompilowania. Nazwa nie wymaga dodanego rozszerzenia. Na przykład przy użyciu `MyCoreApp` polecenia `MyCoreApp.exe`Generuj.

- **RootNamespace**\
Domyślna przestrzeń nazw używana przez projekt. Powinna być zgodna z domyślną przestrzenią nazw projektu .NET Framework.

Dodaj te trzy elementy do `<PropertyGroup>` węzła `MyFormsCore.csproj` w pliku:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>

    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    <AssemblyName>MyCoreApp</AssemblyName>
    <RootNamespace>WindowsFormsApp1</RootNamespace>
  </PropertyGroup>

</Project>
```

## <a name="add-source-code"></a>Dodaj kod źródłowy

Teraz projekt **MyFormsCore. csproj** nie kompiluje żadnego kodu. Domyślnie projekty platformy .NET Core automatycznie uwzględniają cały kod źródłowy w bieżącym katalogu i wszystkich katalogach podrzędnych. Należy skonfigurować projekt do dołączania kodu z projektu .NET Framework przy użyciu ścieżki względnej. Jeśli projekt .NET Framework używał plików **resx** dla ikon i zasobów formularzy, należy uwzględnić te pliki. 

Dodaj następujący `<ItemGroup>` węzeł do projektu. Każda instrukcja zawiera wzorzec globalizowania pliku, który zawiera katalogi podrzędne.

```xml
  <ItemGroup>
    <Compile Include="..\MyFormsApp\**\*.cs" />
    <EmbeddedResource Include="..\MyFormsApp\**\*.resx" />
  </ItemGroup>
```

Alternatywnie można utworzyć `<Compile>` wpis lub `<EmbeddedResource>` dla każdego pliku w projekcie .NET Framework.

## <a name="add-nuget-packages"></a>Dodaj pakiety NuGet

Dodaj każdy pakiet NuGet, do którego odwołuje się projekt .NET Framework, do projektu .NET Core. 

Prawdopodobnie aplikacja Windows Forms .NET Framework ma plik **Packages. config** zawierający listę wszystkich pakietów NuGet, do których odwołuje się projekt. Możesz zapoznać się z tą listą, aby określić, które pakiety NuGet dodać do projektu .NET Core. Na przykład jeśli projekt .NET Framework, do `MetroFramework`którego odwołuje się pakiety `MetroFramework.Fonts` , `MetroFramework.Design`i NuGet, należy dodać każdy do projektu z Visual Studio lub interfejs wiersza polecenia platformy .NET Core z katalogu **SolutionFolder** :

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework.Design
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework.Fonts
```

Poprzednie polecenia spowodują dodanie następujących odwołań NuGet do projektu **MyFormsCore. csproj** :

```xml
  <ItemGroup>
    <PackageReference Include="MetroFramework" Version="1.2.0.3" />
    <PackageReference Include="MetroFramework.Design" Version="1.2.0.3" />
    <PackageReference Include="MetroFramework.Fonts" Version="1.2.0.3" />
  </ItemGroup>
```

## <a name="port-control-libraries"></a>Biblioteki kontrolek portu

Jeśli masz projekt biblioteki formantów Windows Forms do portu, kierunki są takie same jak w przypadku portów .NET Framework projektu aplikacji Windows Forms, z wyjątkiem kilku ustawień. I zamiast kompilowania do pliku wykonywalnego, należy skompilować do biblioteki. Różnica między projektem wykonywalnym i projektem biblioteki, oprócz ścieżki dla pliku elementy globalne, który zawiera kod źródłowy, jest minimalna.

Korzystając z przykładu poprzedniego kroku, program umożliwia rozwinięcie projektów i plików, z którymi pracujemy.

| Plik | Opis |
| ---- | ----------- |
| **MyApps.sln** | Nazwa pliku rozwiązania. |
| **MyControls.csproj** | Nazwa .NET Framework Windows Forms kontroluje projekt do portu. |
| **MyControlsCore.csproj** | Nazwa nowego projektu biblioteki .NET Core, który tworzysz. |
| **MyCoreControls.dll** | Biblioteka formantów Windows Forms .NET Core. |

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
├───MyFormsAppCore
│   └───MyFormsCore.csproj
│
├───MyFormsControls
│   └───MyControls.csproj
└───MyFormsControlsCore
    └───MyControlsCore.csproj   <--- New project for core controls
```

Uwzględnij różnice między `MyControlsCore.csproj` projektem i wcześniej utworzonym `MyFormsCore.csproj` projektem.

```diff
 <Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

   <PropertyGroup>
-    <OutputType>WinExe</OutputType>
     <TargetFramework>netcoreapp3.0</TargetFramework>
     <UseWindowsForms>true</UseWindowsForms>

     <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
-    <AssemblyName>MyCoreApp</AssemblyName>
-    <RootNamespace>WindowsFormsApp1</RootNamespace>
+    <AssemblyName>MyControlsCore</AssemblyName>
+    <RootNamespace>WindowsFormsControlLibrary1</RootNamespace>
   </PropertyGroup>

   <ItemGroup>
-    <Compile Include="..\MyFormsApp\**\*.cs" />
-    <EmbeddedResource Include="..\MyFormsApp\**\*.resx" />
+    <Compile Include="..\MyFormsControls\**\*.cs" />
+    <EmbeddedResource Include="..\MyFormsControls\**\*.resx" />
   </ItemGroup>

 </Project>
```

Poniżej znajduje się przykład pliku projektu biblioteki formantów Windows Forms .NET Core:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>

    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    <AssemblyName>MyCoreControls</AssemblyName>
    <RootNamespace>WindowsFormsControlLibrary1</RootNamespace>
  </PropertyGroup>
  
  <ItemGroup>
    <Compile Include="..\MyFormsControls\**\*.cs" />
    <EmbeddedResource Include="..\MyFormsControls\**\*.resx" />
  </ItemGroup>
  
</Project>
```

Jak widać, `<OutputType>` węzeł został usunięty, który domyślnie kompilator tworzy bibliotekę zamiast pliku wykonywalnego. `<AssemblyName>` I`<RootNamespace>` zostały zmienione. W `<RootNamespace>` odróżnieniu od przestrzeni nazw biblioteki formantów Windows Forms, która jest przeprojektowana. A wreszcie węzły `<Compile>` i `<EmbeddedResource>` zostały dostosowane tak, aby wskazywały folder bibliotek formantów Windows Forms, które są przełączone.

Następnie w głównym projekcie programu .NET Core **MyFormsCore. csproj** Dodaj odwołanie do nowej biblioteki formantów Windows Forms .NET Core. Dodaj odwołanie z programu Visual Studio lub interfejs wiersza polecenia platformy .NET Core z katalogu **SolutionFolder** :

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj reference .\MyFormsControlsCore\MyControlsCore.csproj
```

Poprzednie polecenie dodaje następujący do projektu **MyFormsCore. csproj** :

```xml
  <ItemGroup>
    <ProjectReference Include="..\MyFormsControlsCore\MyControlsCore.csproj" />
  </ItemGroup>
```

## <a name="problems-compiling"></a>Problemy skompilowane

Jeśli masz problemy z kompilowaniem projektów, możesz używać niektórych interfejsów API tylko dla systemu Windows, które są dostępne w .NET Framework ale nie są dostępne w środowisku .NET Core. Możesz spróbować dodać pakiet NuGet pakietu [zgodności systemu Windows][compat-pack] do projektu. Ten pakiet działa tylko w systemie Windows i dodaje około 20 000 interfejsów API systemu Windows do projektów .NET Core i .NET Standard.

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package Microsoft.Windows.Compatibility
```

Poprzednie polecenie dodaje następujący do projektu **MyFormsCore. csproj** :

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.Windows.Compatibility" Version="2.0.1" />
  </ItemGroup>
```

## <a name="windows-forms-designer"></a>Projektant Windows Forms

Zgodnie z opisem w tym artykule program Visual Studio 2019 obsługuje tylko projektanta formularzy w projektach .NET Framework. Tworząc równoległy projekt platformy .NET Core, można testować projekt przy użyciu platformy .NET Core podczas projektowania formularzy przy użyciu projektu .NET Framework. Plik rozwiązania zawiera zarówno projekty .NET Framework, jak i .NET Core. Dodawanie i projektowanie formularzy i kontrolek w projekcie .NET Framework i opartych na wzorcach globalizowania plików dodanych do projektów .NET Core, wszystkie nowe lub zmienione pliki zostaną automatycznie uwzględnione w projektach .NET Core.

Gdy program Visual Studio 2019 obsługuje Projektant formularzy systemu Windows, można skopiować/wkleić zawartość pliku projektu .NET Core do pliku projektu .NET Framework. Następnie usuń pliki wzorców globalizowania dodane z `<Source>` elementami i. `<EmbeddedResource>` Popraw ścieżki do dowolnych odwołań do projektu używanych przez aplikację. Efektywnie uaktualnia projekt .NET Framework do projektu .NET Core.
 
## <a name="next-steps"></a>Następne kroki

- Przeczytaj więcej na temat [pakietu zgodności systemu Windows][compat-pack].
- Obejrzyj [film wideo podczas przenoszenia](https://www.youtube.com/watch?v=upVQEUc_KwU) projektu Windows Forms .NET Framework do programu .NET Core.

[compat-pack]: windows-compat-pack.md
