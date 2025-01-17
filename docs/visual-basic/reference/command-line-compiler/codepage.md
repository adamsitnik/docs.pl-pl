---
title: -CodePage (Visual Basic)
ms.date: 03/09/2018
helpviewer_keywords:
- -codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
ms.openlocfilehash: e4cdc27ab021fe055f157b78946538f2b76870e1
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002358"
---
# <a name="-codepage-visual-basic"></a>-CodePage (Visual Basic)
Określa stronę kodową, która ma być używana dla wszystkich plików kodu źródłowego w kompilacji.  
  
## <a name="syntax"></a>Składnia  
  
```console  
-codepage:id  
```  
  
## <a name="arguments"></a>Argumenty  
  
|Termin|Definicja|  
|---|---|  
|`id`|Wymagany. Kompilator używa strony kodowej określonej przez `id`, aby interpretować Kodowanie plików źródłowych.|  
  
## <a name="remarks"></a>Uwagi  
 Aby skompilować kod źródłowy zapisany z określonym kodowaniem, można użyć `-codepage`, aby określić, która strona kodowa powinna być używana. Opcja `-codepage` dotyczy wszystkich plików kodu źródłowego w kompilacji. Aby uzyskać więcej informacji, zobacz [kodowanie znaków w .NET Framework](../../../standard/base-types/character-encoding.md).  
  
 Opcja `-codepage` nie jest wymagana, jeśli pliki kodu źródłowego zostały zapisane przy użyciu bieżącej strony kodowej ANSI, Unicode lub UTF-8 z podpisem. Program Visual Studio zapisuje wszystkie pliki kodu źródłowego z bieżącą stroną kodową ANSI domyślnie, chyba że użytkownik określi inne kodowanie w oknie dialogowym **kodowanie** . Program Visual Studio używa okna dialogowego **kodowanie** do otwierania plików kodu źródłowego zapisanych z inną stroną kodową.  
  
> [!NOTE]
> Opcja `-codepage` nie jest dostępna w środowisku deweloperskim programu Visual Studio. jest on dostępny tylko w przypadku kompilowania z wiersza polecenia.  
  
## <a name="see-also"></a>Zobacz także

- [Kompilator wiersza polecenia Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
