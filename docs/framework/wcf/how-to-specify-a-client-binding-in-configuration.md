---
title: 'Instrukcje: Określanie wiązań klienta w konfiguracji'
ms.date: 03/30/2017
ms.assetid: 4a7c79aa-50ee-4991-891e-adc0599323a7
ms.openlocfilehash: b16f4b062f7f97a5855b06bdcf348911ee0497d2
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/15/2019
ms.locfileid: "72320862"
---
# <a name="how-to-specify-a-client-binding-in-configuration"></a>Instrukcje: Określanie wiązań klienta w konfiguracji
W tym przykładzie aplikacja konsoli klienta zostanie utworzona w celu korzystania z usługi kalkulatora, a powiązanie dla tego klienta jest określone w konfiguracji w sposób deklaratywny. Klient uzyskuje dostęp do `CalculatorService`, który implementuje interfejs `ICalculator`, a zarówno usługa, jak i klient używają klasy <xref:System.ServiceModel.BasicHttpBinding>.  
  
 W opisanej procedurze przyjęto założenie, że usługa kalkulatora jest uruchomiona. Aby uzyskać informacje na temat sposobu tworzenia usługi, zobacz [How to: Określanie powiązania usługi w konfiguracji](how-to-specify-a-service-binding-in-configuration.md). Używa także narzędzia do [przesyłania metadanych modelu ServiceModel (Svcutil. exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) , które zapewnia Windows Communication Foundation (WCF), aby automatycznie generować składniki klienta. Narzędzie generuje kod klienta i konfigurację w celu uzyskania dostępu do usługi.  
  
 Klient jest skompilowany w dwóch częściach. Svcutil. exe generuje `ClientCalculator` implementujący interfejs `ICalculator`. Ta aplikacja kliencka jest następnie tworzona przez konstruowanie wystąpienia `ClientCalculator`.  
  
 Zazwyczaj najlepszym rozwiązaniem jest określenie informacji o powiązaniach i adresie w konfiguracji, a nie w sposób konieczny w kodzie. Definiowanie punktów końcowych w kodzie zazwyczaj nie jest praktyczne, ponieważ powiązania i adresy dla wdrożonej usługi są zwykle inne niż te używane podczas tworzenia usługi. Ogólnie rzecz biorąc, przechowywanie informacji o powiązaniach i adresach poza kodem pozwala na ich zmianę bez konieczności ponownego kompilowania lub wdrażania aplikacji.  
  
 Wszystkie poniższe kroki konfiguracji można wykonać za pomocą [Narzędzia Edytora konfiguracji (SvcConfigEditor. exe)](configuration-editor-tool-svcconfigeditor-exe.md).  
  
 Aby uzyskać kopię źródła tego przykładu, zobacz przykład [podstawowabinding](./samples/basicbinding.md) .  
  
### <a name="specifying-a-client-binding-in-configuration"></a>Określanie powiązania klienta w konfiguracji  
  
1. Użyj Svcutil. exe z wiersza polecenia w celu wygenerowania kodu z metadanych usługi.  
  
    ```console  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2. Wygenerowany klient zawiera interfejs `ICalculator`, który definiuje kontrakt usługi, który musi spełniać implementacja klienta.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#1)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#1)]  
  
3. Wygenerowany klient również zawiera implementację `ClientCalculator`.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#2)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#2)]  
  
4. Svcutil. exe generuje również konfigurację dla klienta, który używa klasy <xref:System.ServiceModel.BasicHttpBinding>. W przypadku korzystania z programu Visual Studio Nazwij ten plik App. config. Należy zauważyć, że informacje o adresie i powiązaniu nie są określone w dowolnym miejscu w ramach implementacji usługi. Ponadto kod nie musi być zapisany, aby można było pobrać te informacje z pliku konfiguracyjnego.  
  
     [!code-xml[C_HowTo_ConfigureClientBinding#100](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/common/client.exe.config#100)]   
            
5. Utwórz wystąpienie `ClientCalculator` w aplikacji, a następnie Wywołaj operacje usługi.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/client.cs#3)]  
  
6. Kompiluj i uruchom klienta.  
  
## <a name="see-also"></a>Zobacz także

- [Konfigurowanie usług i klientów za pomocą powiązań](using-bindings-to-configure-services-and-clients.md)
