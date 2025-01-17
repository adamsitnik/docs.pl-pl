---
title: -filealign (C# opcje kompilatora)
ms.date: 07/20/2015
f1_keywords:
- /filealign
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
ms.openlocfilehash: aed8b412ea1580f7dfa4f87333598d76a85b5e64
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69603009"
---
# <a name="-filealign-c-compiler-options"></a>-filealign (C# opcje kompilatora)
Opcja **-filealign** umożliwia określenie rozmiaru sekcji w pliku wyjściowym.  
  
## <a name="syntax"></a>Składnia  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a>Argumenty  
 `number`  
 Wartość określająca rozmiar sekcji w pliku wyjściowym. Prawidłowe wartości to 512, 1024, 2048, 4096 i 8192. Te wartości są w bajtach.  
  
## <a name="remarks"></a>Uwagi  
 Każda sekcja zostanie wyrównana na granicy, która jest wielokrotnością wartości **filealign** . Nie ma żadnych stałych ustawień domyślnych. Jeśli nie określono parametru **-filealign** , środowisko uruchomieniowe języka wspólnego wybiera wartość domyślną w czasie kompilacji.  
  
 Określenie rozmiaru sekcji wpływa na rozmiar pliku wyjściowego. Modyfikowanie rozmiaru sekcji może być przydatne w przypadku programów, które będą uruchamiane na mniejszych urządzeniach.  
  
 Użyj [polecenia DUMPBIN](/cpp/build/reference/dumpbin-options) , aby wyświetlić informacje o sekcjach w pliku wyjściowym.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Aby ustawić tę opcję kompilatora w środowisku programowania Visual Studio  
  
1. Otwórz stronę **Właściwości** projektu.  
  
2. Kliknij stronę właściwości **kompilacja** .  
  
3. Kliknij przycisk **Zaawansowane** .  
  
4. Zmodyfikuj właściwość **wyrównania pliku** .  
  
 Aby uzyskać informacje na temat sposobu, w jaki można programowo ustawić <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>tę opcję kompilatora, zobacz.  
  
## <a name="see-also"></a>Zobacz także

- [Opcje kompilatora C#](./index.md)
- [Zarządzanie właściwościami projektu i rozwiązania](/visualstudio/ide/managing-project-and-solution-properties)
