---
title: 'Instrukcje: pobieranie odcisku palca certyfikatu'
ms.date: 03/30/2017
helpviewer_keywords:
- certificates [WCF], retrieving thumbprint
ms.assetid: da3101aa-78cd-4c34-9652-d1f24777eeab
ms.openlocfilehash: 51debbbcfec2fd5b82460e1dd1d6ece8e77bfc13
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62000782"
---
# <a name="how-to-retrieve-the-thumbprint-of-a-certificate"></a>Instrukcje: pobieranie odcisku palca certyfikatu
Podczas pisania aplikacji Windows Communication Foundation (WCF), który używa certyfikatu X.509 do uwierzytelniania, często jest niezbędne do określenia oświadczenia znalezione w certyfikacie. Na przykład, należy podać oświadczenia odcisk palca, korzystając z <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> wyliczenia w <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> metody. Znajdowanie wartość oświadczenia wymaga wykonania dwóch kroków. Najpierw otwórz przystawkę Microsoft Management Console (MMC) dla certyfikatów. (Zobacz [jak: Wyświetlanie certyfikatów za pomocą przystawki programu MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).) Po drugie zgodnie z opisem w tym miejscu, Znajdź odpowiedni certyfikat i skopiować jego odcisk palca (lub inne wartości oświadczenia).  
  
 Jeśli używasz certyfikatu do uwierzytelniania usługi, ważne jest, aby Zanotuj wartość ustawienia **wystawiony dla** kolumny (pierwsza kolumna w konsoli). Gdy przy użyciu protokołu Secure Sockets Layer (SSL), jak zabezpieczenia transportu, jeden z pierwszym kontrole wykonywane jest porównanie z base adresów identyfikator (URI) usługi, aby **wystawiony dla** wartość. Wartości muszą być zgodne, lub zostało zatrzymane z procesem uwierzytelniania.  
  
 Polecenia cmdlet programu Powershell, New-SelfSignedCertificate umożliwia również tworzenie certyfikatów tymczasowych do użytku tylko podczas programowania. Domyślnie jednak takiego certyfikatu nie jest wystawiony przez urząd certyfikacji i nie nadaje się do celów produkcyjnych. Aby uzyskać więcej informacji, zobacz [jak: Tworzenie certyfikatów tymczasowych do użycia podczas tworzenia](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md).  
  
### <a name="to-retrieve-a-certificates-thumbprint"></a>Aby pobrać odcisk palca certyfikatu  
  
1. Otwórz przystawkę Microsoft Management Console (MMC) dla certyfikatów. (Zobacz [jak: Wyświetlanie certyfikatów za pomocą przystawki programu MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).)  
  
2. W **katalog główny konsoli** okna lewą okienku kliknij **certyfikaty (komputer lokalny)**.  
  
3. Kliknij przycisk **osobistych** folder, aby ją rozwinąć.  
  
4. Kliknij przycisk **certyfikaty** folder, aby ją rozwinąć.  
  
5. Na liście certyfikatów, należy pamiętać, **przeznaczone do celów** nagłówka. Znajdź certyfikat, który zawiera listę **uwierzytelnianie klienta** jako zamierzony cel.  
  
6. Kliknij dwukrotnie certyfikat.  
  
7. W **certyfikatu** okno dialogowe, kliknij przycisk **szczegóły** kartę.  
  
8. Przewiń listę pól, a następnie kliknij przycisk **odcisk palca**.  
  
9. Kopiowanie znaków szesnastkowych z pola pytania. Jeśli to odcisk palca jest używany w kodzie `X509FindType`, usuwaj odstępy między liczb szesnastkowych. Na przykład odciskiem palca "a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a 7b" powinien być określony jako "a909502dd82ae41433e6f83886b00d4277a32a7b" w kodzie.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>
- [Instrukcje: Konfigurowanie portu z certyfikatem SSL](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)
- [Instrukcje: Wyświetlanie certyfikatów za pomocą przystawki programu MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)
- [Instrukcje: Tworzenie certyfikatów tymczasowych do użytku w trakcie opracowywania](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)
