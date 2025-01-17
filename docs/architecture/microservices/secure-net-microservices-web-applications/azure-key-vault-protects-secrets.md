---
title: Korzystanie z usługi Azure Key Vault w celu ochrony kluczy tajnych w czasie tworzenia
description: Zabezpieczenia w mikrousługach .NET i aplikacjach sieci Web — Azure Key Vault jest doskonałym sposobem obsługi wpisów tajnych aplikacji, które są w pełni kontrolowane przez administratorów. Administratorzy mogą nawet przypisywać i odwoływać wartości deweloperskie bez deweloperów, którzy muszą je obsłużyć.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 63bf357c95b82a820b6dfb6a2d24a5d89f66de72
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296479"
---
# <a name="use-azure-key-vault-to-protect-secrets-at-production-time"></a>Użyj Azure Key Vault, aby chronić wpisy tajne w czasie produkcji

Wpisy tajne przechowywane jako zmienne środowiskowe lub przechowywane przez narzędzie tajnego Menedżera są nadal przechowywane lokalnie i niezaszyfrowane na komputerze. Bezpieczniejszym rozwiązaniem do przechowywania wpisów tajnych jest [Azure Key Vault](https://azure.microsoft.com/services/key-vault/), które zapewnia bezpieczną, centralną lokalizację do przechowywania kluczy i wpisów tajnych.

Pakiet **Microsoft. Extensions. Configuration. AzureKeyVault** umożliwia aplikacji ASP.NET Core odczytywanie informacji o konfiguracji z Azure Key Vault. Aby rozpocząć korzystanie z wpisów tajnych z Azure Key Vault, wykonaj następujące kroki:

1. Zarejestruj swoją aplikację jako aplikację usługi Azure AD. (Dostęp do magazynów kluczy jest zarządzany przez usługę Azure AD). Można to zrobić za pomocą portalu zarządzania systemu Azure.

   Alternatywnie, jeśli aplikacja ma być uwierzytelniana przy użyciu certyfikatu zamiast hasła lub klucza tajnego klienta, można użyć polecenia cmdlet [New-AzADApplication](/powershell/module/az.resources/new-azadapplication) programu PowerShell. Certyfikat rejestrowany przy użyciu Azure Key Vault wymaga tylko klucza publicznego. Twoja aplikacja będzie używać klucza prywatnego.

2. Nadaj zarejestrowanej aplikacji dostęp do magazynu kluczy, tworząc nową nazwę główną usługi. Można to zrobić za pomocą następujących poleceń programu PowerShell:

   ```powershell
   $sp = New-AzADServicePrincipal -ApplicationId "<Application ID guid>"
   Set-AzKeyVaultAccessPolicy -VaultName "<VaultName>" -ServicePrincipalName $sp.ServicePrincipalNames[0] -PermissionsToSecrets all -ResourceGroupName "<KeyVault Resource Group>"
   ```

3. Dołącz Magazyn kluczy jako źródło konfiguracji w aplikacji przez wywołanie <xref:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault%2A?displayProperty=nameWithType> metody rozszerzenia podczas <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> tworzenia wystąpienia. Należy zauważyć, `AddAzureKeyVault` że wywołanie wymaga identyfikatora aplikacji, który został zarejestrowany i ma dostęp do magazynu kluczy w poprzednich krokach.

   Można również użyć przeciążenia `AddAzureKeyVault` , które ma certyfikat zamiast klucza tajnego klienta, tylko dołączając odwołanie do pakietu [Microsoft. IdentityModel. clients. ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) .

> [!IMPORTANT]
> Zalecamy zarejestrowanie Azure Key Vault jako ostatni dostawca konfiguracji, aby można było zastąpić wartości konfiguracji od poprzednich dostawców.

## <a name="additional-resources"></a>Dodatkowe zasoby

- **Ochrona wpisów tajnych aplikacji przy użyciu Azure Key Vault** \
  [https://docs.microsoft.com/azure/guidance/guidance-multitenant-identity-keyvault](/azure/guidance/guidance-multitenant-identity-keyvault)

- **Bezpieczne przechowywanie wpisów tajnych aplikacji podczas opracowywania** \
  [https://docs.microsoft.com/aspnet/core/security/app-secrets](/aspnet/core/security/app-secrets)

- **Konfigurowanie ochrony danych** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/overview](/aspnet/core/security/data-protection/configuration/overview)

- **Zarządzanie kluczami i okres istnienia ochrony danych w ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/default-settings](/aspnet/core/security/data-protection/configuration/default-settings)

- Repozytorium GitHub **Microsoft. Extensions. Configuration. KeyPerFile** . \
  <https://github.com/aspnet/Configuration/tree/master/src/Config.KeyPerFile>

>[!div class="step-by-step"]
>[Poprzedni](developer-app-secrets-storage.md)Następny
>[](../key-takeaways.md)
