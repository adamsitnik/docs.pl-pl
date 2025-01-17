---
title: <relativeBindForResources> Element
ms.date: 03/30/2017
helpviewer_keywords:
- RelativeBindForResources element
- <relativeBindForResources> element
ms.assetid: 846ffa47-7257-4ce3-8cac-7ff627e0e34f
ms.openlocfilehash: 6a418fc546313b74bb965a0b223eca9c2e5acc08
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73115799"
---
# <a name="relativebindforresources-element"></a>\<element > relativeBindForResources
Optymalizuje sondę dla zestawów satelickich.  
  
[ **\<configuration >** ](../configuration-element.md) \
&nbsp;&nbsp;[ **\<środowiska uruchomieniowego >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<relativeBindForResources >**  
  
## <a name="syntax"></a>Składnia  
  
```xml
<relativeBindForResources    
   enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`enabled`|Atrybut wymagany.<br /><br /> Określa, czy środowisko uruchomieniowe języka wspólnego optymalizuje sondę dla zestawów satelickich.|  
  
## <a name="enabled-attribute"></a>Atrybut włączony  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`false`|Środowisko uruchomieniowe nie optymalizuje sondy dla zestawów satelickich. Jest to wartość domyślna.|  
|`true`|Środowisko uruchomieniowe optymalizuje sondę dla zestawów satelickich.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`runtime`|Zawiera informacje dotyczące opcji inicjowania środowiska uruchomieniowego.|  
  
## <a name="remarks"></a>Uwagi  
 Ogólnie rzecz biorąc, Menedżer zasobów sondy dla zasobów, zgodnie z opisem w temacie [pakowanie i wdrażanie zasobów](../../../resources/packaging-and-deploying-resources-in-desktop-apps.md) . Oznacza to, że podczas Menedżer zasobów sond dla konkretnej zlokalizowanej wersji zasobu może on wyglądać w globalnej pamięci podręcznej zestawów, wyszukać w folderze specyficznym dla kultury w bazie kodu aplikacji, Instalator Windows zapytań dla zestawów satelickich i podnieść zdarzenie <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>. Element `<relativeBindForResources>` optymalizuje sposób, w jaki Menedżer zasobów sondy dla zestawów satelickich. Może zwiększyć wydajność podczas sondowania zasobów w następujących warunkach:  
  
- Gdy zestaw satelicki zostanie wdrożony w tej samej lokalizacji co zestaw kodu. Innymi słowy, jeśli zestaw kodu jest zainstalowany w globalnej pamięci podręcznej zestawów, należy również zainstalować w tym miejscu zestawy satelickie. Jeśli zestaw kodu jest zainstalowany w bazie kodu aplikacji, zestawy satelickie muszą być również zainstalowane w folderze specyficznym dla kultury w bazie kodu.  
  
- Gdy Instalator Windows nie jest używany lub jest używany rzadko w przypadku instalacji zestawów satelitarnych na żądanie.  
  
- Gdy kod aplikacji nie obsługuje zdarzenia <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>.  
  
 Ustawienie atrybutu `enabled` elementu `<relativeBindForResources>`, aby `true` zoptymalizować sondę Menedżer zasobów dla zestawów satelitarnych w następujący sposób:  
  
- Używa lokalizacji zestawu kodu nadrzędnego do sondowania dla zestawu satelickiego.  
  
- Nie bada Instalator Windows dla zestawów satelickich.  
  
- Nie zgłasza zdarzenia <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Zobacz także

- [Opakowanie i wdrażanie zasobów](../../../resources/packaging-and-deploying-resources-in-desktop-apps.md)
- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
