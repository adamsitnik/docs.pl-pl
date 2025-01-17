---
title: porównanie plików Project.JSON i csproj
description: Zobacz Mapowanie między formatami project.json i csproj elementów.
author: natemcmaster
ms.date: 03/13/2017
ms.custom: seodec18
ms.openlocfilehash: 6ac63f18bd42193e964aaeae3c54c887c9c63163
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61647362"
---
# <a name="a-mapping-between-projectjson-and-csproj-properties"></a>Mapowanie między formatami project.json i csproj właściwości

Przez [Nate McMaster](https://github.com/natemcmaster)

Podczas opracowywania narzędzi .NET Core, projekt ważne zmiany nie obsługuje już *project.json* pliki i zamiast tego Przenieś projektów .NET Core do formatu MSBuild/csproj.

W tym artykule przedstawiono sposób ustawienia w *project.json* są reprezentowane w formacie programu MSBuild/csproj, dzięki czemu możesz dowiedzieć się, jak używać nowego formatu i zapoznać się ze zmianami, wykonywane za pomocą narzędzi migracji, gdy aktualizujesz projekt, aby Najnowsza wersja narzędzi.

## <a name="the-csproj-format"></a>Formatu csproj

Nowy format \*.csproj, to format opartych na języku XML. W poniższym przykładzie pokazano węzeł główny projekt .NET Core za pomocą `Microsoft.NET.Sdk`. Dla projektów sieci web jest używany zestaw SDK `Microsoft.NET.Sdk.Web`.

```xml
<Project Sdk="Microsoft.NET.Sdk">
...
</Project>
```

## <a name="common-top-level-properties"></a>Wspólne właściwości najwyższego poziomu

### <a name="name"></a>nazwa

```json
{
  "name": "MyProjectName"
}
```

Nie jest już obsługiwana. W pliku csproj to jest określana przez nazwę pliku projektu, który zazwyczaj jest zgodna z nazwą katalogu. Na przykład `MyProjectName.csproj`.

Domyślnie, nazwa_pliku projektu określa również wartość `<AssemblyName>` i `<PackageId>` właściwości.

```xml
<PropertyGroup>
  <AssemblyName>MyProjectName</AssemblyName>
  <PackageId>MyProjectName</PackageId>
</PropertyGroup>
```

`<AssemblyName>` Będzie miał inną wartość niż `<PackageId>` Jeśli `buildOptions\outputName` właściwość została zdefiniowana w pliku project.json.
Aby uzyskać więcej informacji, zobacz [inne typowe opcje kompilacji](#other-common-build-options).

### <a name="version"></a>version

```json
{
  "version": "1.0.0-alpha-*"
}
```

Użyj `VersionPrefix` i `VersionSuffix` właściwości:

```xml
<PropertyGroup>
  <VersionPrefix>1.0.0</VersionPrefix>
  <VersionSuffix>alpha</VersionSuffix>
</PropertyGroup>
```

Można również użyć `Version` właściwości, ale mogą zastąpić ustawienia wersji podczas tworzenia pakietów:

```xml
<PropertyGroup>
  <Version>1.0.0-alpha</Version>
</PropertyGroup>
```

### <a name="other-common-root-level-options"></a>Inne typowe opcje poziomu głównego

```json
{
  "authors": [ "Anne", "Bob" ],
  "company": "Contoso",
  "language": "en-US",
  "title": "My library",
  "description": "This is my library.\r\nAnd it's really great!",
  "copyright": "Nugetizer 3000",
  "userSecretsId": "xyz123"
}
```

```xml
<PropertyGroup>
  <Authors>Anne;Bob</Authors>
  <Company>Contoso</Company>
  <NeutralLanguage>en-US</NeutralLanguage>
  <AssemblyTitle>My library</AssemblyTitle>
  <Description>This is my library.
And it's really great!</Description>
  <Copyright>Nugetizer 3000</Copyright>
  <UserSecretsId>xyz123</UserSecretsId>
</PropertyGroup>
```

## <a name="frameworks"></a>Struktury

### <a name="one-target-framework"></a>Jeden element docelowy framework

```json
{
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp1.0</TargetFramework>
</PropertyGroup>
```

### <a name="multiple-target-frameworks"></a>Wiele platform docelowych

```json
{
  "frameworks": {
    "netcoreapp1.0": {},
    "net451": {}
  }
}
```

Użyj `TargetFrameworks` właściwości, aby zdefiniować listę platform docelowych. Użyj średnika do rozdzielania wielu wartości framework.

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp1.0;net451</TargetFrameworks>
</PropertyGroup>
```

## <a name="dependencies"></a>zależności

> [!IMPORTANT]
> Jeśli zależność jest **projektu** , a nie pakiet, format jest inny.
> Aby uzyskać więcej informacji, zobacz [typ zależności](#dependency-type) sekcji.

### <a name="netstandardlibrary-metapackage"></a>NETStandard.Library meta Microsoft.aspnetcore.all

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  }
}
```

```xml
<PropertyGroup>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

### <a name="microsoftnetcoreapp-metapackage"></a>Pakietów Microsoft.NETCore.App meta Microsoft.aspnetcore.all

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.0"
  }
}
```

```xml
<PropertyGroup>
  <RuntimeFrameworkVersion>1.0.3</RuntimeFrameworkVersion>
</PropertyGroup>
```

Należy pamiętać, że `<RuntimeFrameworkVersion>` wartość migrowanych projektu jest określana przez wersję zainstalowanego zestawu SDK.

### <a name="top-level-dependencies"></a>Zależności najwyższego poziomu

```json
{
  "dependencies": {
    "Microsoft.AspNetCore": "1.1.0"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore" Version="1.1.0" />
</ItemGroup>
```

### <a name="per-framework-dependencies"></a>Zależności na struktury

```json
{
  "framework": {
    "net451": {
      "dependencies": {
        "System.Collections.Immutable": "1.3.1"
      }
    },
    "netstandard1.5": {
      "dependencies": {
        "Newtonsoft.Json": "9.0.1"
      }
    }
  }
}
```

```xml
<ItemGroup Condition="'$(TargetFramework)'=='net451'">
  <PackageReference Include="System.Collections.Immutable" Version="1.3.1" />
</ItemGroup>

<ItemGroup Condition="'$(TargetFramework)'=='netstandard1.5'">
  <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
</ItemGroup>
```

### <a name="imports"></a>importy

```json
{
  "dependencies": {
    "YamlDotNet": "4.0.1-pre309"
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dnxcore50",
        "dotnet"
      ]
    }
  }
}
```

```xml
<PropertyGroup>
  <PackageTargetFallback>dnxcore50;dotnet</PackageTargetFallback>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="YamlDotNet" Version="4.0.1-pre309" />
</ItemGroup>
```

### <a name="dependency-type"></a>Typ zależności

#### <a name="type-project"></a>Typ: Projekt

```json
{
  "dependencies": {
    "MyOtherProject": "1.0.0-*",
    "AnotherProject": {
      "type": "project"
    }
  }
}
```

```xml
<ItemGroup>
  <ProjectReference Include="..\MyOtherProject\MyOtherProject.csproj" />
  <ProjectReference Include="..\AnotherProject\AnotherProject.csproj" />
</ItemGroup>
```

> [!NOTE]
> Spowoduje to podzielenie jej, `dotnet pack --version-suffix $suffix` Określa wersję zależności odwołania projektu.

#### <a name="type-build"></a>Typ: kompilacji

```json
{
  "dependencies": {
    "Microsoft.EntityFrameworkCore.Design": {
      "version": "1.1.0",
      "type": "build"
    }
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="1.1.0" PrivateAssets="All" />
</ItemGroup>
```

#### <a name="type-platform"></a>Typ: platforma

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": {
      "version": "1.1.0",
      "type": "platform"
    }
  }
}
```

Nie ma odpowiednika w pliku csproj.

## <a name="runtimes"></a>środowiska uruchomieniowe

```json
{
  "runtimes": {
    "win7-x64": {},
    "osx.10.11-x64": {},
    "ubuntu.16.04-x64": {}
  }
}
```

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win7-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="standalone-apps-self-contained-deployment"></a>Aplikacje autonomiczne (niezależna wdrożenia)

W pliku project.json definiując `runtimes` oznacza, że sekcja aplikacji została autonomiczny podczas tworzenia i publikowania.
W programie MSBuild, wszystkie projekty są *przenośne* podczas kompilacji, ale mogą być publikowane jako autonomiczny.

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

Aby uzyskać więcej informacji, zobacz [niezależna wdrożeń (— SCD)](../deploying/index.md#self-contained-deployments-scd).

## <a name="tools"></a>narzędzia

```json
{
  "tools": {
    "Microsoft.EntityFrameworkCore.Tools.DotNet": "1.0.0-*"
  }
}
```

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="1.0.0" />
</ItemGroup>
```

> [!NOTE]
> `imports` narzędzia nie są obsługiwane w pliku csproj. Narzędzia, które muszą importów nie będzie działać z nowym `Microsoft.NET.Sdk`.

## <a name="buildoptions"></a>buildOptions

Zobacz też [pliki](#files).

### <a name="emitentrypoint"></a>emitEntryPoint

```json
{
  "buildOptions": {
    "emitEntryPoint": true
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Jeśli `emitEntryPoint` został `false`, wartość `OutputType` jest konwertowana na `Library`, czyli wartość domyślna:

```json
{
  "buildOptions": {
    "emitEntryPoint": false
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Library</OutputType>
  <!-- or, omit altogether. It defaults to 'Library' -->
</PropertyGroup>
```

### <a name="keyfile"></a>keyFile

```json
{
  "buildOptions": {
    "keyFile": "MyKey.snk"
  }
}
```

`keyFile` Element rozwija się do trzech właściwości w programie MSBuild:

```xml
<PropertyGroup>
  <AssemblyOriginatorKeyFile>MyKey.snk</AssemblyOriginatorKeyFile>
  <SignAssembly>true</SignAssembly>
  <PublicSign Condition="'$(OS)' != 'Windows_NT'">true</PublicSign>
</PropertyGroup>
```

### <a name="other-common-build-options"></a>Inne typowe opcje kompilacji

```json
{
  "buildOptions": {
    "warningsAsErrors": true,
    "nowarn": ["CS0168", "CS0219"],
    "xmlDoc": true,
    "preserveCompilationContext": true,
    "outputName": "Different.AssemblyName",
    "debugType": "portable",
    "allowUnsafe": true,
    "define": ["TEST", "OTHERCONDITION"]
  }
}
```

```xml
<PropertyGroup>
  <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
  <NoWarn>$(NoWarn);CS0168;CS0219</NoWarn>
  <GenerateDocumentationFile>true</GenerateDocumentationFile>
  <PreserveCompilationContext>true</PreserveCompilationContext>
  <AssemblyName>Different.AssemblyName</AssemblyName>
  <DebugType>portable</DebugType>
  <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  <DefineConstants>$(DefineConstants);TEST;OTHERCONDITION</DefineConstants>
</PropertyGroup>
```

## <a name="packoptions"></a>packOptions

Zobacz też [pliki](#files).

### <a name="common-pack-options"></a>Typowe opcje pakietu

```json
{
  "packOptions": {
    "summary": "numl is a machine learning library intended to ease the use of using standard modeling techniques for both prediction and clustering.",
    "tags": ["machine learning", "framework"],
    "releaseNotes": "Version 0.9.12-beta",
    "iconUrl": "http://numl.net/images/ico.png",
    "projectUrl": "http://numl.net",
    "licenseUrl": "https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md",
    "requireLicenseAcceptance": false,
    "repository": {
      "type": "git",
      "url": "https://raw.githubusercontent.com/sethjuarez/numl"
    },
    "owners": ["Seth Juarez"]
  }
}
```

```xml
<PropertyGroup>
  <!-- summary is not migrated from project.json, but you can use the <Description> property for that if needed. -->
  <PackageTags>machine learning;framework</PackageTags>
  <PackageReleaseNotes>Version 0.9.12-beta</PackageReleaseNotes>
  <PackageIconUrl>http://numl.net/images/ico.png</PackageIconUrl>
  <PackageProjectUrl>http://numl.net</PackageProjectUrl>
  <PackageLicenseUrl>https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md</PackageLicenseUrl>
  <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
  <RepositoryType>git</RepositoryType>
  <RepositoryUrl>https://raw.githubusercontent.com/sethjuarez/numl</RepositoryUrl>
  <!-- owners is not supported in MSBuild -->
</PropertyGroup>
```

Nie ma odpowiednika dla `owners` elementu w programie MSBuild.
Dla `summary`, można użyć programu MSBuild `<Description>` właściwości, mimo że wartość `summary` jest migracji automatycznie do tej właściwości, ponieważ ta właściwość jest mapowany na [ `description` ](#other-common-root-level-options) elementu.

## <a name="scripts"></a>skrypty

```json
{
  "scripts": {
    "precompile": "generateCode.cmd",
    "postpublish": [ "obfuscate.cmd", "removeTempFiles.cmd" ]
  }
}
```

Czy ich ekwiwalentów w MSBuild [cele](/visualstudio/msbuild/msbuild-targets):

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="generateCode.cmd" />
</Target>

<Target Name="MyPostCompileTarget" AfterTargets="Publish">
  <Exec Command="obfuscate.cmd" />
  <Exec Command="removeTempFiles.cmd" />
</Target>
```

## <a name="runtimeoptions"></a>runtimeOptions

```json
{
  "runtimeOptions": {
    "configProperties": {
      "System.GC.Server": true,
      "System.GC.Concurrent": true,
      "System.GC.RetainVM": true,
      "System.Threading.ThreadPool.MinThreads": 4,
      "System.Threading.ThreadPool.MaxThreads": 25
    }
  }
}
```

Wszystkie ustawienia w tej grupie, z wyjątkiem właściwości "System.GC.Server", są umieszczane w pliku o nazwie *runtimeconfig.template.json* w folderze projektu z opcjami podniesiony do głównego obiektu podczas procesu migracji:

```json
{
  "configProperties": {
    "System.GC.Concurrent": true,
    "System.GC.RetainVM": true,
    "System.Threading.ThreadPool.MinThreads": 4,
    "System.Threading.ThreadPool.MaxThreads": 25
  }
}
```

Właściwość "System.GC.Server" jest migrowana do pliku csproj:

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

Jednak te wartości można ustawić w pliku csproj, jak również właściwości programu MSBuild:

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
  <ConcurrentGarbageCollection>true</ConcurrentGarbageCollection>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
  <ThreadPoolMaxThreads>25</ThreadPoolMaxThreads>
</PropertyGroup>
```

## <a name="shared"></a>udostępnione

```json
{
  "shared": "shared/**/*.cs"
}
```

Nie są obsługiwane w pliku csproj. Zamiast tego należy utworzyć dołączać pliki zawartości w Twojej *.nuspec* pliku.
Aby uzyskać więcej informacji, zobacz [pliki zawartości w tym](/nuget/schema/nuspec#including-content-files).

## <a name="files"></a>— pliki

W *project.json*, kompilacji i dodatkiem Service pack może zostać rozszerzony do kompilowania i osadzania z różnymi folderami.
W programie MSBuild odbywa się przy użyciu [elementów](/visualstudio/msbuild/common-msbuild-project-items). Poniższy przykład przedstawia typowe konwersji:

```json
{
  "buildOptions": {
    "compile": {
      "copyToOutput": "notes.txt",
      "include": "../Shared/*.cs",
      "exclude": "../Shared/Not/*.cs"
    },
    "embed": {
      "include": "../Shared/*.resx"
    }
  },
  "packOptions": {
    "include": "Views/",
    "mappings": {
      "some/path/in/project.txt": "in/package.txt"
    }
  },
  "publishOptions": {
    "include": [
      "files/",
      "publishnotes.txt"
    ]
  }
}
```

```xml
<ItemGroup>
  <Compile Include="..\Shared\*.cs" Exclude="..\Shared\Not\*.cs" />
  <EmbeddedResource Include="..\Shared\*.resx" />
  <Content Include="Views\**\*" PackagePath="%(Identity)" />
  <None Include="some/path/in/project.txt" Pack="true" PackagePath="in/package.txt" />
  
  <None Include="notes.txt" CopyToOutputDirectory="Always" />
  <!-- CopyToOutputDirectory = { Always, PreserveNewest, Never } -->

  <Content Include="files\**\*" CopyToPublishDirectory="PreserveNewest" />
  <None Include="publishnotes.txt" CopyToPublishDirectory="Always" />
  <!-- CopyToPublishDirectory = { Always, PreserveNewest, Never } -->
</ItemGroup>
```

> [!NOTE]
> Wiele domyślnych [wzorców obsługi symboli wieloznacznych](https://en.wikipedia.org/wiki/Glob_(programming)) są dodawane automatycznie przez program .NET Core SDK.
> Aby uzyskać więcej informacji, zobacz [domyślne wartości elementów skompilować](https://aka.ms/sdkimplicititems).

Wszystkie MSBuild `ItemGroup` obsługuje elementy `Include`, `Exclude`, i `Remove`.

Układ pakietu wewnątrz .nupkg mogą być modyfikowane przy użyciu `PackagePath="path"`.

Z wyjątkiem `Content`, większość grup elementów wymagają jawne dodanie `Pack="true"` mają zostać uwzględnione w pakiecie. `Content` zostaną przełączeni w *zawartości* folder w pakiecie, ponieważ MSBuild `<IncludeContentInPack>` właściwość jest ustawiona na `true` domyślnie.
Aby uzyskać więcej informacji, zobacz [w tym zawartości w pakiecie](/nuget/schema/msbuild-targets#including-content-in-a-package).

`PackagePath="%(Identity)"` to krótkie sposób ustawienia ścieżki pakietu do ścieżki względnej projektu pliku.

## <a name="testrunner"></a>testRunner

### <a name="xunit"></a>xUnit

```json
{
  "testRunner": "xunit",
  "dependencies": {
    "dotnet-test-xunit": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="xunit" Version="2.2.0-*" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0-*" />
</ItemGroup>
```

### <a name="mstest"></a>MSTest

```json
{
  "testRunner": "mstest",
  "dependencies": {
    "dotnet-test-mstest": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.12-*" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.11-*" />
</ItemGroup>
```

## <a name="see-also"></a>Zobacz także

- [Ogólne omówienie zmian w interfejsie wiersza polecenia](../tools/cli-msbuild-architecture.md)
