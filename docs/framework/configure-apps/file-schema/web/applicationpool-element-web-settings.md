---
title: <applicationPool>, element (ustawienia internetowe)
ms.date: 03/30/2017
helpviewer_keywords:
- applicationPool element
- <applicationPool> element
ms.assetid: 46d1baaa-e343-4639-b70d-2a43a9f62b2a
ms.openlocfilehash: c88f4e5407e550047eaf0f5c8d0d2924da611e93
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699220"
---
# <a name="applicationpool-element-web-settings"></a>\<applicationPool >, element (Ustawienia sieci Web)
Określa ustawienia konfiguracji, które są używane przez ASP.NET do zarządzania zachowaniem całego procesu, gdy aplikacja ASP.NET działa w trybie zintegrowanym w usługach IIS 7,0 lub nowszym.  
  
> [!IMPORTANT]
> Ten element i funkcja, które obsługuje, działają tylko wtedy, gdy aplikacja ASP.NET jest hostowana w usługach IIS 7,0 lub nowszych.  
  
[ **@no__t — 2configuration >** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4system. Web >** ](system-web-element-web-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 **\<applicationPool >**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<applicationPool   
    maxConcurrentRequestsPerCPU="5000"   
    maxConcurrentThreadsPerCPU="0"   
    requestQueueLimit="5000" />  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`maxConcurrentRequestsPerCPU`|Określa liczbę równoczesnych żądań ASP.NET na procesor CPU.|  
|`maxConcurrentThreadsPerCPU`|Określa, ile równoczesnych wątków może być uruchomionych dla puli aplikacji dla każdego procesora CPU. Zapewnia to alternatywny sposób kontrolowania współbieżności ASP.NET, ponieważ można ograniczyć liczbę zarządzanych wątków, które mogą być używane na potrzeby procesora, aby obsłużyć żądania. Domyślnie to ustawienie ma wartość 0, co oznacza, że ASP.NET nie ogranicza liczby wątków, które mogą być tworzone na procesor, chociaż Pula wątków CLR ogranicza liczbę wątków, które można utworzyć.|  
|`requestQueueLimit`|Określa maksymalną liczbę żądań, które mogą być umieszczone w kolejce dla ASP.NET w pojedynczym procesie. Gdy co najmniej dwie aplikacje ASP.NET są uruchamiane w jednej puli aplikacji, zestaw zbiorczy żądań wysyłanych do dowolnej aplikacji w puli aplikacji podlega temu ustawieniu.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[@no__t -1System. Web >](system-web-element-web-settings.md)|Zawiera informacje o tym, jak ASP.NET współdziała z aplikacją hosta.|  
  
## <a name="remarks"></a>Uwagi  

Po uruchomieniu usług IIS 7,0 lub nowszej wersji w trybie zintegrowanym Ta kombinacja elementów umożliwia skonfigurowanie sposobu, w jaki ASP.NET zarządza wątkami i kolejkami żądań, gdy aplikacja jest hostowana w puli aplikacji IIS. W przypadku uruchomienia usług IIS 6 lub uruchamiania usług IIS 7,0 w trybie klasycznym lub w trybie ISAPI te ustawienia są ignorowane.  
  
Ustawienia `applicationPool` mają zastosowanie do wszystkich pul aplikacji, które są uruchamiane w określonej wersji .NET Framework. Ustawienia są zawarte w pliku aspnet. config. Istnieje wersja tego pliku dla wersji 2,0 i 4,0 .NET Framework. (Wersje 3,0 i 3,5 .NET Framework współużytkują plik ASPNET. config z wersją 2,0).  
  
> [!IMPORTANT]
> W przypadku uruchamiania usług IIS 7,0 na [!INCLUDE[win7](../../../../../includes/win7-md.md)] można skonfigurować oddzielny plik ASPNET. config dla każdej puli aplikacji. Pozwala to na dostosowanie wydajności wątków dla każdej puli aplikacji.  
  
W przypadku ustawienia `maxConcurrentRequestsPerCPU` domyślne ustawienie "5000" w .NET Framework 4 skutecznie wyłącza ograniczanie żądań, które jest kontrolowane przez ASP.NET, chyba że rzeczywiście masz 5000 lub więcej żądań na procesor. Ustawienie domyślne jest zależne od tego, czy w puli wątków CLR w celu automatycznego zarządzania współbieżnością na procesor CPU. Aplikacje, które znacznie wykorzystują asynchroniczne przetwarzanie żądań lub mają wiele długotrwałych żądań zablokowanych we/wy sieci, będą korzystać z zwiększonego limitu domyślnego w .NET Framework 4. Ustawienie wartości `maxConcurrentRequestsPerCPU` spowoduje wyłączenie używania zarządzanych wątków do przetwarzania żądań ASP.NET. Gdy aplikacja jest uruchamiana w puli aplikacji IIS, żądania pozostają w wątku we/wy usług IIS i w związku z tym współbieżność jest ograniczana przez ustawienia wątku IIS.  
  
Ustawienie `requestQueueLimit` działa tak samo jak atrybut `requestQueueLimit` elementu [processModel](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7w2sway1(v=vs.100)) , który jest ustawiany w plikach Web. config dla aplikacji ASP.NET. Jednak ustawienie `requestQueueLimit` w pliku aspnet. config zastępuje ustawienie `requestQueueLimit` w pliku Web. config. Innymi słowy, jeśli oba atrybuty są ustawione (domyślnie jest to prawdziwe), ustawienie `requestQueueLimit` w pliku aspnet. config ma pierwszeństwo.  
  
## <a name="example"></a>Przykład  

Poniższy przykład pokazuje, jak skonfigurować zachowanie ASP.NET całego procesu w pliku aspnet. config w następujących okolicznościach:  
  
- Aplikacja jest hostowana w puli aplikacji usług IIS 7,0.  
  
- Usługi IIS 7,0 są uruchomione w trybie zintegrowanym.  
  
- Aplikacja korzysta z .NET Framework 3,5 z dodatkiem SP1 lub nowszej wersji.  
  
Wartości w przykładzie są wartościami domyślnymi.  
  
```xml  
<configuration>  
  <system.web>  
    <applicationPool   
        maxConcurrentRequestsPerCPU="5000"  
        maxConcurrentThreadsPerCPU="0"   
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## <a name="element-information"></a>Informacje o elementach  
  
|||  
|-|-|  
|Przestrzeń nazw||  
|Nazwa schematu||  
|Plik walidacji||  
|Może być puste||  
  
## <a name="see-also"></a>Zobacz także

- [@no__t -1System. Web > element (Ustawienia sieci Web)](system-web-element-web-settings.md)
