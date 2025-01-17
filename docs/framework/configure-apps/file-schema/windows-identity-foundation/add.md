---
title: <add>
ms.date: 03/30/2017
ms.assetid: 4712a888-f154-4395-8887-ef14a88a6497
author: BrucePerlerMS
ms.openlocfilehash: 932e8452542ace66824fba1262694c220ce88676
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252185"
---
# <a name="add"></a>\<add>
Dodaje określony program obsługi tokenów zabezpieczających do kolekcji obsługi tokenów.  
  
[ **\<> konfiguracji**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. identityModel**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> obiektów securityTokenHandler**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Dodaj >**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type=xs:string>  
        <optionalConfigurationElement>  
        </optionalConfigurationElement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|— typ|Nazwa typu CLR programu obsługi tokenów, który ma zostać dodany. Aby uzyskać więcej informacji na temat sposobu określania `type` atrybutu, zobacz [odwołania do typów niestandardowych](https://docs.microsoft.com/previous-versions/windows-identity-foundation/gg638728(v=msdn.10)#custom-type-references).|  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<samlSecurityTokenRequirement>](samlsecuritytokenrequirement.md)|Zapewnia konfigurację <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> klasy <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> , klasy lub klasy pochodnej jednej z tych klas.|  
|[\<sessionTokenRequirement >](sessiontokenrequirement.md)|Zapewnia konfigurację <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> klasy lub klas pochodnych.|  
|[\<userNameSecurityTokenHandlerRequirement>](usernamesecuritytokenhandlerrequirement.md)|Zapewnia konfigurację <xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler> klasy lub klas pochodnych.|  
|[\<x509SecurityTokenHandlerRequirement>](x509securitytokenhandlerrequirement.md)|Zapewnia opcjonalną konfigurację <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler> klasy lub klas pochodnych.|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<securityTokenHandlers>](securitytokenhandlers.md)|Określa kolekcję programów obsługi tokenów zabezpieczających, które są zarejestrowane w punkcie końcowym.|  
  
## <a name="remarks"></a>Uwagi  
 `<add>` Element może przyjmować jeden element podrzędny, który określa konfigurację programu obsługi tokenów. Jest to zależne od tego, czy Klasa obsługi, `type` do której odwołuje się atrybut `<add>` elementu, zapewnia obsługę tej funkcji. Klasy obsługi tokenów, które udostępniają tę funkcję, muszą uwidaczniać <xref:System.Xml.XmlElement> Konstruktor, który pobiera obiekt.  
  
```  
public class CustomTokenHandler : Microsoft.IdentityModel.Tokens.SecurityTokenHandler  
{  
    public CustomTokenHandler( XmlElement customConfig )  
    {  
    }  
}  
```  
  
 Niektóre wbudowane klasy procedury obsługi tokenów zabezpieczających zapewniają tę funkcję. Te klasy to <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> ,<xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>,, i<xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>. <xref:System.IdentityModel.Services.Tokens.MembershipUserNameSecurityTokenHandler>  
  
> [!IMPORTANT]
> Kolekcja obsługi tokenów może zawierać tylko jedną procedurę obsługi dla danego typu. Oznacza to, na przykład, że jeśli chcesz dodać program obsługi, który pochodzi od <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> klasy do kolekcji, musisz najpierw <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>usunąć element, który jest domyślnie obecny, z kolekcji. Można użyć elementu [ \<Remove >](remove.md) , aby usunąć pojedynczą procedurę obsługi z kolekcji lub użyć elementu [ \<Clear >](clear.md) , aby usunąć wszystkie programy obsługi z kolekcji.  
  
 Ustawienia określone w ustawieniach przesłonięcia programu obsługi określone w kolekcji obsługi tokenów w [ \<elemencie securityTokenHandlerConfiguration >](securitytokenhandlerconfiguration.md) i określonych na poziomie usługi w ramach [ \< identityConfiguration >](identityconfiguration.md) elementu.  
  
## <a name="example"></a>Przykład  
 Poniższy kod XML pokazuje użycie `<add>` elementów i `<remove>` , aby zastąpić domyślną procedurę obsługi tokena sesji za pomocą procedury obsługi niestandardowego tokenu sesji. Kod XML jest pobierany z `ClaimsAwareWebFarm` przykładu.  
  
```xml  
<securityTokenHandlers>  
  <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
  <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
</securityTokenHandlers>  
```
