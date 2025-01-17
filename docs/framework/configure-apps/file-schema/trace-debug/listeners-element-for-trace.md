---
title: <listeners>, element dla <trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners
helpviewer_keywords:
- <listeners> element
- listeners element
ms.assetid: 1394c2c3-6304-46db-87c1-8e8b16f5ad5b
ms.openlocfilehash: 84b67532825372e7f69d86e1ef6060f4263587eb
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699355"
---
# <a name="listeners-element-for-trace"></a>\<listeners > elementu \<trace >
Określa odbiornik, który zbiera, przechowuje i kieruje komunikaty. Odbiorniki kierują dane wyjściowe śledzenia do odpowiedniego obiektu docelowego.  
  
[ **@no__t — 2configuration >** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<system. Diagnostics >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3[ **\<trace >** ](trace-element.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5 **\<listeners >**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<listeners>   
  <add>...</add>  
  <clear/>  
  <remove ... />  
</listeners>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
 Brak.  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[@no__t — 1add >](add-element-for-listeners-for-trace.md)|Dodaje odbiornik do kolekcji `Listeners`.|  
|[@no__t — 1clear >](clear-element-for-listeners-for-trace.md)|Czyści kolekcję `Listeners` na potrzeby śledzenia.|  
|[@no__t — 1remove >](remove-element-for-listeners-for-trace.md)|Usuwa odbiornik z kolekcji `Listeners`.|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`system.diagnostics`|Określa element główny dla sekcji konfiguracji ASP.NET.|  
|`trace`|Zawiera detektory, które zbierają, przechowują i rozsyłają komunikaty śledzenia.|  
  
## <a name="remarks"></a>Uwagi  
 Klasy <xref:System.Diagnostics.Debug> i <xref:System.Diagnostics.Trace> współdzielą tę samą kolekcję **detektorów** . Jeśli dodasz obiekt odbiornika do kolekcji w jednej z tych klas, inna Klasa używa tego samego odbiornika. Klasy odbiornika dostarczane z .NET Framework pochodzą z klasy <xref:System.Diagnostics.TraceListener>.  
  
## <a name="configuration-file"></a>Plik konfiguracji  
 Ten element może być używany w pliku konfiguracji komputera (Machine. config) i w pliku konfiguracji aplikacji.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje, jak użyć elementu **\<listeners >** , aby dodać odbiorniki `MyListener` i `MyEventListener` do kolekcji **detektorów** . `MyListener` tworzy plik o nazwie `MyListener.log` i zapisuje dane wyjściowe do pliku. `MyEventListener` tworzy wpis w dzienniku zdarzeń.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="true" indentsize="0">  
      <listeners>  
        <add name="myListener"   
          type="System.Diagnostics.TextWriterTraceListener,   
            system, version=1.0.3300.0, Culture=neutral,   
            PublicKeyToken=b77a5c561934e089"   
          initializeData="c:\myListener.log" />  
        <add name="MyEventListener"  
          type="System.Diagnostics.EventLogTraceListener,   
            system, version=1.0.3300.0, Culture=neutral,   
            PublicKeyToken=b77a5c561934e089"  
          initializeData="MyConfigEventLog"/>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Diagnostics.TraceListener>
- [Schemat ustawień śledzenia i debugowania](index.md)
