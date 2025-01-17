---
title: <dns>
ms.date: 03/30/2017
ms.assetid: 81819dae-4825-43b7-bccd-f16d2d3d2f06
ms.openlocfilehash: c68cabd03eca71b41a0d0acce26897fa2653f4d3
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855377"
---
# <a name="dns"></a>\<dns>
Określa oczekiwaną tożsamość serwera. Ta tożsamość jest prawidłowa dla trybu uwierzytelniania certyfikatu x509, jeśli certyfikat serwera zawiera system DNS o tej samej wartości. Obowiązuje również w przypadku trybu uwierzytelniania systemu Windows, jeśli nazwa SPN ma taką samą wartość.  
  
Aby uzyskać więcej informacji na temat ustawiania wartości elementu, zobacz [tożsamość usługi i uwierzytelnianie](../../../wcf/feature-details/service-identity-and-authentication.md).  
  
[ **\<> konfiguracji**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. serviceModel**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> klienta**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> punktu końcowego**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> tożsamości**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> DNS**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<dns value = "String" />
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|value|Serwer DNS certyfikatu. DNS to standardowy branżowy protokół używany do lokalizowania komputerów w sieci opartej na protokole IP. Użytkownicy mogą pamiętać nazwy wyświetlane, takie jak <https://go.microsoft.com/fwlink/?prd=10929> lub [https://go.microsoft.com/fwlink/?LinkID=96165](https://go.microsoft.com/fwlink/?LinkID=96165), łatwiejsze niż adresy oparte na liczbie, takie jak 207.46.131.137.|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<> tożsamości](identity.md)|Określa tożsamość usługi do uwierzytelnienia przez klienta.|  
  
## <a name="example"></a>Przykład  
 Poniższy kod konfiguracji określa DNS certyfikatu X. 509, który jest używany do uwierzytelniania serwera.  
  
```xml  
<identity>
  <dns value = "www.cohowinery.com" />
</identity>
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- <xref:System.ServiceModel.DnsEndpointIdentity>
- [Uwierzytelnianie i tożsamość usług](../../../wcf/feature-details/service-identity-and-authentication.md)
- [\<> tożsamości](identity.md)
