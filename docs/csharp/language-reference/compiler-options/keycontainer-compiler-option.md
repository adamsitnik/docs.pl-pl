---
title: -containerer (C# opcje kompilatora)
ms.date: 05/16/2018
f1_keywords:
- /keycontainer
helpviewer_keywords:
- /keycontainer compiler option [C#]
- keycontainer compiler option [C#]
- -keycontainer compiler option [C#]
ms.assetid: b3982b6d-2382-4f7e-bebd-ce98eaa30763
ms.openlocfilehash: fead2d4296cfa6fb0195cb4b43f6448c0fc7e6a9
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970147"
---
# <a name="-keycontainer-c-compiler-options"></a>-containerer (C# opcje kompilatora)
Określa nazwę kontenera klucza kryptograficznego.  
  
## <a name="syntax"></a>Składnia  
  
```console  
-keycontainer:string  
```  
  
## <a name="arguments"></a>Argumenty  
 `string`  
 Nazwa kontenera klucza o silnej nazwie.  
  
## <a name="remarks"></a>Uwagi  
 Gdy jest używana opcja **-containerer** , kompilator tworzy składnik udostępniony. Kompilator wstawia klucz publiczny z określonego kontenera do manifestu zestawu i podpisuje końcowy zestaw z kluczem prywatnym. Aby wygenerować plik klucza, wpisz `sn -k file` w wierszu polecenia. `sn -i`instaluje parę kluczy w kontenerze. Ta opcja nie jest obsługiwana, gdy kompilator działa w CoreCLR. Aby podpisać zestaw podczas kompilowania na CoreCLR, użyj opcji [-KeyFile](keyfile-compiler-option.md) .
  
 W przypadku kompilowania z [modułem-target:](./target-module-compiler-option.md)nazwa pliku klucza jest przechowywana w module i wbudowana w zestaw podczas kompilowania tego modułu do zestawu za pomocą [-addmodule](./addmodule-compiler-option.md).  
  
 Można również określić tę opcję jako atrybut niestandardowy (<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=nameWithType>) w kodzie źródłowym dla dowolnego modułu języka pośredniego (MSIL) firmy Microsoft.  
  
 Możesz również przekazać informacje o szyfrowaniu do kompilatora za pomocą [-KeyFile](./keyfile-compiler-option.md). Użyj [-delaysign](./delaysign-compiler-option.md) , jeśli chcesz, aby klucz publiczny został dodany do manifestu zestawu, ale chcesz opóźnić podpisywanie zestawu do momentu przetestowania.  
  
 Aby uzyskać więcej informacji, zobacz [Tworzenie i używanie zestawów o silnych nazwach](../../../standard/assembly/create-use-strong-named.md) oraz [opóźnienie podpisywania zestawu](../../../standard/assembly/delay-sign.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Aby ustawić tę opcję kompilatora w środowisku programowania Visual Studio  
  
1. Ta opcja kompilatora nie jest dostępna w środowisku deweloperskim programu Visual Studio.  
  
 Można programowo uzyskać dostęp do tej opcji kompilatora <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A>przy użyciu.  
  
## <a name="see-also"></a>Zobacz także

- [C#Kompilator — opcja keyfile](keyfile-compiler-option.md)
- [Opcje kompilatora C#](index.md)
- [Zarządzanie właściwościami projektu i rozwiązania](/visualstudio/ide/managing-project-and-solution-properties)
