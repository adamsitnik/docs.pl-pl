---
title: 'Instrukcje: tworzenie oświadczenia niestandardowego'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d619976b-eda3-475e-ac23-c7988a2dceb0
ms.openlocfilehash: 399aba1a6ad70ae37355f529a291ab2f604af03f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797091"
---
# <a name="how-to-create-a-custom-claim"></a>Instrukcje: tworzenie oświadczenia niestandardowego
Infrastruktura modelu tożsamości w programie Windows Communication Foundation (WCF) udostępnia zestaw wbudowanych typów i praw do funkcji pomocnika do tworzenia <xref:System.IdentityModel.Claims.Claim> wystąpień z tymi typami i prawami. Te wbudowane oświadczenia są przeznaczone do informacji o modelu znajdujących się w typach poświadczeń klienta obsługiwanych domyślnie przez program WCF. W wielu przypadkach wbudowane oświadczenia są wystarczające; Niektóre aplikacje mogą jednak wymagać oświadczeń niestandardowych. Każde z nich składa się z typu, zasobu, którego dotyczy to i po prawej stronie tego zasobu. W tym temacie opisano sposób tworzenia niestandardowego żądania.  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-primitive-data-type"></a>Aby utworzyć niestandardową wartość, która jest oparta na typie danych pierwotnych  
  
1. Utwórz niestandardową autoryzację, przekazując typ, wartość zasobu i prawo do <xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> konstruktora.  
  
    1. Wybierz unikatową wartość dla typu zgłoszenia.  
  
         Typ zgłoszenia jest unikatowym identyfikatorem ciągu. Jest on odpowiedzialny za niestandardowy Projektant roszczeń, aby upewnić się, że identyfikator ciągu, który jest używany dla typu, jest unikatowy. Aby uzyskać listę typów, które są zdefiniowane przez funkcję WCF, zobacz <xref:System.IdentityModel.Claims.ClaimTypes> Klasa.  
  
    2. Wybierz typ danych pierwotnych i wartość zasobu.  
  
         Zasób jest obiektem. Typ CLR zasobu może być typem pierwotnym, takim jak lub <xref:System.String> <xref:System.Int32>, lub dowolnym typem możliwym do serializacji. Typ CLR zasobu musi być możliwy do serializacji, ponieważ oświadczenia są serializowane w różnych punktach przez WCF. Typy pierwotne są możliwe do serializacji.  
  
    3. Wybierz prawo zdefiniowane przez funkcję WCF lub unikatową wartość dla prawa niestandardowego.  
  
         Prawo jest unikatowym identyfikatorem ciągu. Prawa zdefiniowane przez funkcję WCF są zdefiniowane w <xref:System.IdentityModel.Claims.Rights> klasie.  
  
         Jest to odpowiedzialność projektanta niestandardowego, aby upewnić się, że identyfikator ciągu, który jest używany przez prawo jest unikatowy.  
  
         Poniższy przykład kodu tworzy niestandardowe zgłoszenie z typem `http://example.org/claims/simplecustomclaim`zgłoszenia dla zasobu o nazwie `Driver's License`i z <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> prawej strony.  
  
     [!code-csharp[c_CustomClaim#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#4)]
     [!code-vb[c_CustomClaim#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#4)]  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-non-primitive-data-type"></a>Aby utworzyć niestandardową wartość, która jest oparta na typie danych niepierwotnym  
  
1. Utwórz niestandardową autoryzację, przekazując typ, wartość zasobu i prawo do <xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> konstruktora.  
  
    1. Wybierz unikatową wartość dla typu zgłoszenia.  
  
         Typ zgłoszenia jest unikatowym identyfikatorem ciągu. Jest on odpowiedzialny za niestandardowy Projektant roszczeń, aby upewnić się, że identyfikator ciągu, który jest używany dla typu, jest unikatowy. Aby uzyskać listę typów, które są zdefiniowane przez funkcję WCF, zobacz <xref:System.IdentityModel.Claims.ClaimTypes> Klasa.  
  
    2. Wybierz lub Zdefiniuj możliwy do serializacji typ inny niż pierwotny dla zasobu.  
  
         Zasób jest obiektem. Typ CLR zasobu musi być możliwy do serializacji, ponieważ oświadczenia są serializowane w różnych punktach przez WCF. Typy pierwotne są już serializowane.  
  
         Po zdefiniowaniu nowego typu należy zastosować <xref:System.Runtime.Serialization.DataContractAttribute> do klasy. Zastosuj <xref:System.Runtime.Serialization.DataMemberAttribute> również atrybut do wszystkich elementów członkowskich nowego typu, które muszą być serializowane w ramach tego żądania.  
  
         Poniższy przykład kodu definiuje niestandardowy typ zasobu o nazwie `MyResourceType`.  
  
         [!code-csharp[c_CustomClaim#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#2)] 
         [!code-vb[c_CustomClaim#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#2)]        
  
    3. Wybierz prawo zdefiniowane przez funkcję WCF lub unikatową wartość dla prawa niestandardowego.  
  
         Prawo jest unikatowym identyfikatorem ciągu. Prawa zdefiniowane przez funkcję WCF są zdefiniowane w <xref:System.IdentityModel.Claims.Rights> klasie.  
  
         Jest to odpowiedzialność projektanta niestandardowego, aby upewnić się, że identyfikator ciągu, który jest używany przez prawo jest unikatowy.  
  
         Poniższy przykład kodu tworzy niestandardowe zgłoszenie z typem `http://example.org/claims/complexcustomclaim`zgłoszenia, niestandardowym `MyResourceType`typem zasobu i z <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> prawej strony.  
  
         [!code-csharp[c_CustomClaim#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#5)] 
         [!code-vb[c_CustomClaim#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#5)]     
  
## <a name="example"></a>Przykład  
 Poniższy przykład kodu demonstruje sposób tworzenia niestandardowego zgłoszenia z typem zasobu pierwotnego i niestandardowym niepierwotnym typem zasobu.  
  
 [!code-csharp[c_CustomClaim#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#0)]
 [!code-vb[c_CustomClaim#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#0)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.Rights>
- <xref:System.IdentityModel.Claims.ClaimTypes>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [Zarządzanie oświadczeniami i autoryzacją za pomocą modelu tożsamości](../feature-details/managing-claims-and-authorization-with-the-identity-model.md)
