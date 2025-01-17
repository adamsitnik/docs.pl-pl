---
title: <assert> Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/assert
- http://schemas.microsoft.com/.NetConfiguration/v2.0#assert
helpviewer_keywords:
- <assert> element
- assert element
ms.assetid: ef4c3229-b151-4d85-8091-e6456af9b935
ms.openlocfilehash: 30ec24aefcf8c4d1e110238a2c60a958eded5545
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699383"
---
# <a name="assert-element"></a>\<assert > elementu
Określa, czy podczas wywoływania metody <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> ma być wyświetlane okno komunikatu. określa również nazwę pliku, do którego mają być zapisane wiadomości.  
  
[ **@no__t — 2configuration >** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<system. Diagnostics >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 **\<assert >**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<assert assertuienabled="true|false" logfilename="file name"/>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`assertuienabled`|Atrybut opcjonalny.<br /><br /> Określa, czy ma być wyświetlane okno komunikatu, gdy metoda **Debug. Assert** zwraca **wartość false**.|  
|`logfilename`|Atrybut opcjonalny.<br /><br /> Określa nazwę pliku, do którego ma zostać zapisany komunikat, jeśli **Debug. Assert** zwraca **wartość false**.|  
  
## <a name="assertuienabled-attribute"></a>AssertUiEnabled — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|`true`|Wyświetla okno komunikatu. Domyślnie włączone.|  
|`false`|Nie wyświetla okna komunikatu.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|`configuration`|Element główny w każdym pliku konfiguracji używanym przez środowisko uruchomieniowe języka wspólnego i aplikacje programu .NET Framework.|  
|`system.diagnostics`|Określa detektory śledzenia, które zbierają, przechowują i rozsyłają komunikaty oraz poziom, w którym ustawiono przełącznik śledzenia.|  
  
## <a name="remarks"></a>Uwagi  
 Oba atrybuty elementu **\<assert >** są opcjonalne. Można wyłączyć okna komunikatów bez określania pliku, w którym mają zostać zapisane komunikaty, lub można określić plik, do którego mają być zapisane komunikaty, pozostawiając pola komunikatów włączone.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład pokazuje, jak wyłączyć wyświetlanie okien komunikatów podczas wywoływania **debugowania. Assert** i Zapisz komunikaty w `c:\log.txt`.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <assert assertuienabled="false" logfilename="c:\log.txt"/>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Diagnostics.Debug>
- [Schemat ustawień śledzenia i debugowania](index.md)
