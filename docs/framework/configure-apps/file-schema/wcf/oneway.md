---
title: <oneWay>
ms.date: 03/30/2017
ms.assetid: 00e67e0e-77c0-4695-9138-c0997b0e5f3c
ms.openlocfilehash: a5c773ea91de882920775ac8dc0ecc1da68a6c9f
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738791"
---
# <a name="oneway"></a>\<oneWay >
Umożliwia routing pakietów i stosowanie jednokierunkowych metod dla niestandardowego powiązania.  
  
[ **\<configuration >** ](../configuration-element.md) \
&nbsp; &nbsp;[ **\<system. serviceModel >** ](system-servicemodel.md) \
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<powiązań**](bindings.md) >\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\<[**CustomBinding**](custombinding.md) >\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<powiązania >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<oneWay >**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<oneWay packetRoutable="Boolean">
  <channelPoolSettings idleTimeout="TimeSpan"
                       leaseTimeout="TimeSpan"
                       maxOutboundConnectionsPerEndpoint="Integer" />
</oneWay>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`packetRoutable`|Wartość logiczna określająca, czy jest włączona funkcja routingu pakietów. Wartość domyślna to `false`.|  
|`MaxAcceptedChannels`|Liczba całkowita określająca maksymalną liczbę kanałów, które mogą być akceptowane.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<channelPoolSettings >](channelpoolsettings.md)|Obiekt <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement>, który zawiera właściwości puli kanałów dla bieżącego kanału.|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[> powiązań \<](bindings.md)|Definiuje wszystkie możliwości powiązań niestandardowego powiązania.|  
  
## <a name="remarks"></a>Uwagi  
 Aby włączyć routing pakietów, wymagana jest jednokierunkowa warstwa konwersji, która zawiera ten element. Użytkownik może utworzyć niestandardowe powiązanie, które tworzy warstwy tego powiązania przez transport obsługujący sesję lub żądanie-odpowiedź, aby umożliwić jej Routing. Ten element jest również przydatny, gdy chcesz uwidocznić jednokierunkowe metody w bardziej natywny sposób. Więcej przekształceń można zastosować do tej warstwy, na przykład złożonego dupleksu i niezawodnej obsługi komunikatów.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.Channels.OneWayBindingElement>
- <xref:System.ServiceModel.Configuration.OneWayElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Powiązania](../../../wcf/bindings.md)
- [Rozszerzanie powiązań](../../../wcf/extending/extending-bindings.md)
- [Powiązania niestandardowe](../../../wcf/extending/custom-bindings.md)
- [\<niestandardowebinding >](custombinding.md)
