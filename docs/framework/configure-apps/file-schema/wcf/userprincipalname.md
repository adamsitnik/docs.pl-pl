---
title: <userPrincipalName>
ms.date: 03/30/2017
ms.assetid: 68032f69-149e-4613-bae4-18314d4fd294
ms.openlocfilehash: 299af8c4a013d17d7c5b7285f6fb89892c4164a8
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854819"
---
# <a name="userprincipalname"></a>\<userPrincipalName>
Określa główną nazwę użytkownika (UPN) usługi do uwierzytelnienia przez klienta.  
  
Aby uzyskać więcej informacji na temat ustawiania nazwy UPN, zobacz [tożsamość usługi i uwierzytelnianie](../../../wcf/feature-details/service-identity-and-authentication.md).  
  
[ **\<> konfiguracji**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. serviceModel**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> klienta**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> punktu końcowego**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> tożsamości**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> userPrincipalName**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<userPrincipalName value="String" />
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|value|Nazwa konta użytkownika (czasem określana jako nazwa logowania użytkownika) i nazwa domeny identyfikującej domenę, w której znajduje się konto użytkownika. Jest to standardowe użycie logowania do domeny systemu Windows. Format to: someone@example.com (jak w przypadku adresu e-mail).|  
  
### <a name="child-elements"></a>Elementy podrzędne  
 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<> tożsamości](identity.md)|Określa tożsamość usługi do uwierzytelnienia przez klienta.|  
  
## <a name="remarks"></a>Uwagi  
 Bezpieczny Windows Communication Foundation (WCF), który nawiązuje połączenie z punktem końcowym z tą tożsamością używa nazwy UPN podczas uwierzytelniania SSPI przy użyciu punktu końcowego.  
  
## <a name="example"></a>Przykład  
 Poniższy kod konfiguracji określa nazwę UPN usługi do uwierzytelnienia przez klienta.  
  
```xml  
<identity>
  <userPrincipalName value="someone@cohowinery.com" />
</identity>
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- <xref:System.ServiceModel.UpnEndpointIdentity>
- [Uwierzytelnianie i tożsamość usług](../../../wcf/feature-details/service-identity-and-authentication.md)
- [\<> tożsamości](identity.md)
