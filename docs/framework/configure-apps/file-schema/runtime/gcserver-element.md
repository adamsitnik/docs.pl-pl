---
title: <gcServer> Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcServer
- http://schemas.microsoft.com/.NetConfiguration/v2.0#gcServer
helpviewer_keywords:
- gcServer element
- <gcServer> element
ms.assetid: 8d25b80e-2581-4803-bd87-a59528e3cb03
ms.openlocfilehash: 98ecc7069df20a92492e9a6276a0d88331ccc0bb
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73116666"
---
# <a name="gcserver-element"></a>\<element > gcServer
Określa, czy środowisko uruchomieniowe języka wspólnego uruchamia odzyskiwanie pamięci serwera.  
  
[ **\<configuration >** ](../configuration-element.md) \
&nbsp;&nbsp;[ **\<środowiska uruchomieniowego >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<gcServer >**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<gcServer    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`enabled`|Atrybut wymagany.<br /><br /> Określa, czy środowisko uruchomieniowe uruchamia odzyskiwanie pamięci serwera.|  
  
## <a name="enabled-attribute"></a>Atrybut włączony  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`false`|Nie uruchamia odzyskiwania pamięci serwera. Domyślnie włączone.|  
|`true`|Uruchamia odzyskiwanie pamięci serwera.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`runtime`|Zawiera informacje dotyczące powiązania zestawu oraz wyrzucania elementów bezużytecznych.|  
  
## <a name="remarks"></a>Uwagi  
 Środowisko uruchomieniowe języka wspólnego (CLR) obsługuje dwa typy wyrzucania elementów bezużytecznych: odzyskiwanie pamięci stacji roboczej, które jest dostępne we wszystkich systemach i wyrzucanie elementów bezużytecznych serwera, które jest dostępne w systemach wieloprocesorowych. Za pomocą elementu `<gcServer>` można kontrolować typ wyrzucania elementów bezużytecznych wykonywanych przez środowisko CLR. Użyj właściwości <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=nameWithType>, aby określić, czy jest włączone odzyskiwanie pamięci serwera.  
  
 W przypadku komputerów z jednym procesorem domyślna opcja wyrzucania elementów bezużytecznych stacji roboczej powinna być najszybszą opcją. Stacja robocza lub serwer może być używana w przypadku komputerów dwuprocesorowych. Wyrzucanie elementów bezużytecznych serwera powinno być najszybszą opcją dla więcej niż dwóch procesorów.  
  
 Tego elementu można używać tylko w pliku konfiguracji aplikacji; jest on ignorowany, jeśli znajduje się w pliku konfiguracji komputera.  
  
> [!NOTE]
> W .NET Framework 4 i starszych wersjach współbieżne wyrzucanie elementów bezużytecznych nie jest dostępne po włączeniu odzyskiwania pamięci serwera. Począwszy od .NET Framework 4,5, wyrzucanie elementów bezużytecznych serwera jest współbieżne. Aby użyć niewspółbieżnego wyrzucania elementów bezużytecznych serwera, ustaw `<gcServer>` element `true` i [\<> elementu](gcconcurrent-element.md) `false`.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład umożliwia wyrzucanie elementów bezużytecznych na serwerze.  
  
```xml  
<configuration>  
   <runtime>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=nameWithType>
- [Schemat ustawień środowiska uruchomieniowego](index.md)
- [Schemat pliku konfiguracji](../index.md)
- [Aby wyłączyć współbieżne wyrzucanie elementów bezużytecznych](gcconcurrent-element.md#to-disable-background-garbage-collection)
