---
title: Kompilator XSLT (xsltc.exe)
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 672a5ac8-8305-4d28-ba10-11089c2c0924
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 729e6caa36ed8c2f6e77153f8d8ae356513b0603
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956993"
---
# <a name="xslt-compiler-xsltcexe"></a>Kompilator XSLT (xsltc.exe)
Kompilator XSLT (xsltc. exe) kompiluje arkusze stylów XSLT i generuje zestaw. Skompilowany arkusz stylów można następnie przesłać bezpośrednio do metody <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=nameWithType>. Nie można generować podpisanych zestawów za pomocą xsltc. exe.  
  
 Narzędzie xsltc. exe jest dołączone do programu Visual Studio. Aby uzyskać więcej informacji, zobacz [Visual Studio — pliki do pobrania](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).  
  
## <a name="syntax"></a>Składnia  
  
```console  
xsltc [options] [/class:<name>] <sourceFile> [[/class:<name>] <sourceFile>...]  
```  
  
## <a name="argument"></a>Argument  
  
|Argument|Opis|  
|--------------|-----------------|  
|`sourceFile`|Określa nazwę arkusza stylów. Arkusz stylów musi być plikiem lokalnym lub znajdować się w intranecie.|  
  
## <a name="options"></a>Opcje  
  
|Opcja|Opis|  
|------------|-----------------|  
|`/c[lass]:``name`|Określa nazwę klasy dla poniższego arkusza stylów. Nazwa klasy może być w pełni kwalifikowana.<br /><br /> Nazwa klasy jest domyślnie nazwą arkusza stylów. Na przykład jeśli arkusz stylów są kompilowane. xsl, domyślna nazwa klasy to Customers.|  
|`/debug[` +&#124;-`]`|Określa, czy informacje o debugowaniu mają być generowane.<br /><br /> Określenie `+` lub `/debug` powoduje, że kompilator generuje informacje o debugowaniu i umieszcza je w pliku bazy danych programu (PDB). Nazwa wygenerowanego pliku PDB jest @no__t -0. pdb.<br /><br /> Określenie `-`, która obowiązuje, jeśli nie określono `/debug`, nie powoduje utworzenia informacji o debugowaniu. Zestaw detaliczny jest generowany. **Uwaga:**  Kompilowanie w trybie debugowania może znacząco wpłynąć na wydajność XSLT.|  
|`/help`|Wyświetla składnię polecenia i opcje narzędzia.|  
|`/nologo`|Pomija wyświetlanie komunikatu o prawach autorskich kompilatora.|  
|`/platform:``string`|Określa platformy, na których można uruchomić zestaw. Poniżej opisano prawidłowe wartości platformy:<br /><br /> `x86` kompiluje zestaw do uruchomienia przez 32-bitowe, zgodne ze standardem x86 środowisko uruchomieniowe języka wspólnego<br /><br /> `x64` kompiluje zestaw do uruchomienia przez 64-bitowe środowisko uruchomieniowe języka wspólnego na komputerze, który obsługuje zestaw instrukcji AMD64 lub EM64T.<br /><br /> Procesor Itanium kompiluje zestaw do uruchomienia przez 64-bitowe środowisko uruchomieniowe języka wspólnego na komputerze z procesorem Itanium.<br /><br /> `anycpu` kompiluje zestaw do uruchamiania na dowolnej platformie. Domyślnie włączone.|  
|`/out:``assemblyName`|Określa nazwę zestawu, który jest wynikiem. Nazwa zestawu jest domyślnie ustawiana na nazwę głównego arkusza stylów lub pierwszego arkusza stylów, jeśli istnieje wiele arkuszy stylów.<br /><br /> Jeśli arkusz stylów zawiera skrypty, skrypty są zapisywane w osobnym zestawie. Nazwy zestawów skryptów są generowane na podstawie głównej nazwy zestawu. Na przykład jeśli dla nazwy zestawu określono CustOrders. dll, pierwszy zestaw skryptu ma nazwę CustOrders_Script1. dll.|  
|`/settings:``document+-, script+-, DTD+-,`|Określa, czy zezwalać na używanie funkcji `document()`, skryptu XSLT czy definicji typu dokumentu (DTD) w arkuszu stylów.<br /><br /> Zachowanie domyślne powoduje wyłączenie obsługi dla DTD, funkcji `document()` i skryptów.|  
|`@``file`|Pozwala określić plik, który zawiera opcje kompilatora.|  
|`?`|Wyświetla składnię polecenia i opcje narzędzia.|  
  
## <a name="remarks"></a>Uwagi  
 Rozwiązania XSLT mogą składać się z wielu modułów arkusza stylów. Narzędzie xsltc. exe generuje zestawy z arkuszy stylów. Zestawy można następnie przesłać do metody <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=nameWithType>. Może to pomóc w zmniejszeniu kosztów wydajności w niektórych scenariuszach wdrażania XSLT.  
  
> [!NOTE]
> Należy również uwzględnić skompilowany zestaw jako odwołanie w aplikacji.  
  
 Narzędzie xsltc. exe nie sprawdza poprawności nazw klas (@no__t *-0)* ani zestawów (`/out:`*AssemblyName*). Błędy są zgłaszane przez środowisko uruchomieniowe języka wspólnego, jeśli nazwy są nieprawidłowe.  
  
## <a name="examples"></a>Przykłady  
 Poniższe polecenie kompiluje arkusz stylów i tworzy zestaw o nazwie booksort. dll.  
  
```console  
xsltc booksort.xsl  
```  
  
 Poniższe polecenie kompiluje arkusz stylów i tworzy plik Assembly i PDB o nazwie booksort. dll i booksort. pdb odpowiednio.  
  
```console  
xsltc booksort.xsl /debug  
```  
  
 Poniższe polecenie kompiluje arkusz stylów zawierający element msxsl: Script i tworzy dwa zestawy o nazwie Calc. dll i calc_Script1. dll.  
  
```console  
xsltc /settings:script+ calc.xsl  
```  
  
 Następujące polecenie umożliwia przetwarzanie DTD i obsługę skryptów oraz tworzy dwa zestawy o nazwie myTest_Script1. dll i. dll.  
  
```console  
xsltc /settings:DTD+,script+ /out:myTest calc.xsl  
```  
  
 Poniższe polecenie kompiluje dwa moduły arkusza stylów i tworzy pojedynczy zestaw o nazwie booksort. dll.  
  
```console  
xsltc booksort.xsl output.xsl  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.Xsl.XslCompiledTransform>
- [Instrukcje: Wykonywanie przekształcenia XSLT przy użyciu zestawu](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md)
- [Przekształcenia XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)
