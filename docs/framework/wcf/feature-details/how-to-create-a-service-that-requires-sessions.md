---
title: 'Instrukcje: tworzenie usługi, która wymaga użycia sesji'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8a7613ef-0df9-47c3-b8dc-47f42cb1fd8b
ms.openlocfilehash: 246ff5dbb9bf76ad6a93c78815f2b3e39c4380aa
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64635613"
---
# <a name="how-to-create-a-service-that-requires-sessions"></a>Instrukcje: tworzenie usługi, która wymaga użycia sesji
Sesje, Tworzenie udostępnionego stanu między co najmniej dwa punkty końcowe, które umożliwia przydatnych funkcji, takich jak wywołania zwrotne z wieloma przeskokami zabezpieczeń i skojarzenia między klientami a wystąpieniami usługi. Aby uzyskać więcej informacji o sesji w aplikacji Windows Communication Foundation (WCF), zobacz [przy użyciu sesji](../../../../docs/framework/wcf/using-sessions.md).  
  
### <a name="to-specify-that-a-contract-require-its-binding-to-support-sessions"></a>Aby określić, że kontrakt wymaga jej powiązania do obsługi sesji  
  
1. Tworzenie kontraktu usługi za pomocą co najmniej jednej operacji. Na przykład sposobu tworzenia kontraktu usługi zobacz [jak: Definiowanie kontraktu usługi](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md).  
  
2. Modyfikowanie <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType> określa kontrakt, ustawiając <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> właściwości albo:  
  
    - <xref:System.ServiceModel.SessionMode.Required?displayProperty=nameWithType> Jeśli ten kontrakt musi być uruchamiane w ramach sesji.  
  
    - <xref:System.ServiceModel.SessionMode.Allowed?displayProperty=nameWithType> Jeśli ten kontrakt mogą być uruchamiane w ramach sesji.  
  
    - <xref:System.ServiceModel.SessionMode.NotAllowed?displayProperty=nameWithType> Jeśli nie wolno uruchamiać tej Umowy w ramach sesji.  
  
3. Konfigurowanie punktu końcowego usługi do użycia powiązanie, które obsługuje sesji. W poniższym przykładzie konfiguracji prezentuje sposób użycia <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType>, które obsługuje WS`-`ReliableMessaging sesji.  
  
     [!code-xml[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]   
  
## <a name="example"></a>Przykład  
 Poniższy przykład kodu pokazuje, jak określić wymaganie sesji poziomie umowy i przy użyciu pliku konfiguracji w celu spełnienia tego wymagania, za pomocą <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType> powiązania.  
  
 [!code-csharp[SCA.Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/services.cs#1)] 
 [!code-vb[SCA.Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/services.vb#1)]      
 [!code-xml[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]     
  
## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType>
