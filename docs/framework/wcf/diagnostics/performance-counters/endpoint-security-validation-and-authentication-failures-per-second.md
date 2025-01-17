---
title: 'Punkt końcowy: Niepowodzenia uwierzytelniania i weryfikacji zabezpieczeń na sekundę'
ms.date: 03/30/2017
ms.assetid: 89a70b90-d7e4-4b03-9b84-4dc88ce3d605
ms.openlocfilehash: a6d76a0d11c52d20aebd44a85862c802cc0a68f7
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/29/2019
ms.locfileid: "64912479"
---
# <a name="endpoint-security-validation-and-authentication-failures-per-second"></a>Punkt końcowy: Niepowodzenia uwierzytelniania i weryfikacji zabezpieczeń na sekundę
Nazwa komputera: Niepowodzenia uwierzytelniania i weryfikacji zabezpieczeń na sekundę  
  
## <a name="description"></a>Opis  
 Ten licznik jest zwiększany, gdy komunikat zostanie odrzucony, ze względu na problem z zabezpieczeniami nie pasuje do żadnego licznika "Zabezpieczenia połączeń nie masz praw". Takie problemy obejmują:  
  
- Nie można odczytać tokenu klienta z komunikatu.  
  
- Token klienta nie powiodło się uwierzytelnianie (na przykład nieprawidłowe hasło).  
  
- Weryfikacja podpisu nie powiodła się (na przykład wiadomości zostały zmodyfikowane).  
  
- Komunikat jest duplikatem z poprzedniej wersji, która może się zdarzyć podczas ataku powtarzania.  
  
- Wystąpił błąd odszyfrowywania.  
  
- Niektóre wymagane elementy (na przykład brak sygnatur czasowych lub zaszyfrowanych danych, blokowanie) brakuje wiadomości.  
  
- Wystąpił błąd podczas uzgadniania TLSNEGO/SPNEGO.  
  
 Ten licznik jest typ licznika wydajności [PERF_COUNTER_COUNTER](https://go.microsoft.com/fwlink/?LinkID=94649), którego wartość jest obliczana przy użyciu następującej formuły:  
  
 (N1-N0)/((D1-D0)/F)
