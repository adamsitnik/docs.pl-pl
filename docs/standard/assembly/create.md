---
title: Tworzenie zestawów
ms.date: 08/19/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- single-file assemblies
- assemblies [.NET Framework], creating
- multifile assemblies
ms.assetid: 54832ee9-dca8-4c8b-913c-c0b9d265e9a4
ms.openlocfilehash: 81fffb2b2e1d56d6068bf6f663a13fad6968a383
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73740510"
---
# <a name="create-assemblies"></a>Tworzenie zestawów

Można tworzyć zestawy Jednoplikowe lub wieloplikowe za pomocą IDE, takie jak Visual Studio, lub kompilatory i narzędzia dostarczone przez Windows SDK. Najprostszym zestawem jest pojedynczy plik, który ma prostą nazwę i jest ładowany do pojedynczej domeny aplikacji. Ten zestaw nie może odwoływać się do innych zestawów poza katalogiem aplikacji i nie jest sprawdzany Sprawdzanie wersji. Aby odinstalować aplikację utworzoną z zestawu, wystarczy usunąć znajdujący się w niej katalog. W przypadku wielu deweloperów zestaw z tymi funkcjami jest wymagany do wdrożenia aplikacji.

Zestaw wieloplikowy można utworzyć z kilku modułów kodu i plików zasobów. Możesz również utworzyć zestaw, który może być współużytkowany przez wiele aplikacji. Zestaw współużytkowany musi mieć silną nazwę i można go wdrożyć w globalnej pamięci podręcznej zestawów.

Istnieje kilka opcji grupowania modułów kodu i zasobów w zestawy, w zależności od następujących czynników:

- Przechowywanie wersji

     Grupuj moduły, które powinny mieć te same informacje o wersji.

- wdrażania

     Grupuj moduły kodu i zasoby, które obsługują model wdrażania.

- Było

     Grupuj moduły, jeśli mogą być logicznie używane razem do pewnego celu. Na przykład zestaw składający się z typów i klas używanych rzadko do konserwacji programu można umieścić w tym samym zestawie. Ponadto typy, które mają być współużytkowane z wieloma aplikacjami, powinny być pogrupowane w zestaw, a zestaw powinien być podpisany za pomocą silnej nazwy.

- Zabezpieczenia

     Moduły grupy zawierające typy, które wymagają tych samych uprawnień zabezpieczeń.

- Zakresów

     Moduły grupy zawierające typy, których widoczność powinna być ograniczona do tego samego zestawu.

Istnieją specjalne zagadnienia dotyczące tworzenia zestawów środowiska uruchomieniowego języka wspólnego dla niezarządzanych aplikacji COM. Aby uzyskać więcej informacji na temat pracy z kodem niezarządzanym, zobacz [udostępnianie .NET Framework składników do modelu COM](../../framework/interop/exposing-dotnet-components-to-com.md).

## <a name="see-also"></a>Zobacz także

- [Przechowywanie wersji zestawu](versioning.md)
- [Instrukcje: kompilowanie zestawu jednoplikowego](../../framework/app-domains/build-single-file-assembly.md)
- [Instrukcje: kompilowanie zestawu wieloplikowego](../../framework/app-domains/build-multifile-assembly.md)
- [Jak środowisko uruchomieniowe lokalizuje zestawy](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [Zestawy wieloplikowe](../../framework/app-domains/multifile-assemblies.md)
