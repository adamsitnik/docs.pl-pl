---
title: Zręczność kryptograficzna w zabezpieczeniach WCF
ms.date: 03/30/2017
ms.assetid: c2c549e5-ac19-40c5-b686-8f67f52b6dbf
ms.openlocfilehash: b8e3b6dc62baf31901520d7f5edac0529e937016
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490939"
---
# <a name="cryptographic-agility-in-wcf-security"></a>Zręczność kryptograficzna w zabezpieczeniach WCF

Ten przykład pokazuje, jak określić w algorytmie standard/niestandardowa w celu zapewnienia implementację kryptografii agile klienta usługi Windows Communication Foundation (WCF) i usługi. Przykład składa się z następujących projektów:

**Usługa**

Jest to obsługiwanej samodzielnie usługi WCF, która implementuje `ICalculator` interfejs i zabezpiecza punktu końcowego za pomocą <xref:System.ServiceModel.WSHttpBinding> przy użyciu bezpiecznej sesji i niezawodnej sesji wyłączone. Usługa definiuje niestandardową `SecurityAlgorithmSuite` klasy, aby określić algorytmy kryptograficzne, które ma być używany do zabezpieczenia komunikatów.

**Klient**

Jest to klienta WCF, która uzyskuje dostęp do usługi po pomyślnym uwierzytelnieniu. Wywołuje operacje udostępniane przez `ICalculator` interfejs i implementowany przez usługę. Klient definiuje również niestandardowe tego samego `SecurityAlgorithmSuite` klasy, aby określić algorytmy kryptograficzne, które ma być używany do zabezpieczenia komunikatów.

## <a name="to-use-this-sample"></a>Aby użyć tego przykładu

1. Otwórz rozwiązanie CryptoAgility.sln w programie Visual Studio 2012.

2. Naciśnij klawisze CTRL + SHIFT + B, aby skompilować rozwiązanie.

3. Otwórz Eksplorator plików i przejdź do katalogu \WCF\Basic\Security\CryptoAgility\Service\bin i uruchom plik service.exe z uprawnieniami administratora, kliknij prawym przyciskiem myszy service.exe i wybierając **Uruchom jako administrator**.

4. Przejdź do katalogu \WCF\Basic\Security\CryptoAgility\Client\bin, a następnie uruchom plik client.exe normalnie.

> [!IMPORTANT]
> Przykłady może już być zainstalowany na tym komputerze. Przed kontynuowaniem sprawdź, czy są dostępne dla następującego katalogu (ustawienie domyślne).
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Jeśli ten katalog nie istnieje, przejdź do strony [Windows Communication Foundation (WCF) i przykłady Windows Workflow Foundation (WF) dla platformy .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) do pobierania wszystkich Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykładów. W tym przykładzie znajduje się w następującym katalogu.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Security\CryptoAgility`

## <a name="see-also"></a>Zobacz także

- [Windows Communication Foundation zabezpieczeń](../feature-details/security.md)
