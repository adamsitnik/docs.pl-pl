---
title: Program WIF i farmy serwerów internetowych
ms.date: 03/30/2017
ms.assetid: fc3cd7fa-2b45-4614-a44f-8fa9b9d15284
author: BrucePerlerMS
ms.openlocfilehash: 32d2875ebe0a46b9f9b1856ed70a30114793e492
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045255"
---
# <a name="wif-and-web-farms"></a>Program WIF i farmy serwerów internetowych
W przypadku korzystania z programu Windows Identity Foundation (WIF) w celu zabezpieczenia zasobów jednostki uzależnionej (RP) wdrożonej w kolektywie serwerów sieci Web należy wykonać określone kroki, aby upewnić się, że WIF może przetwarzać tokeny z wystąpień aplikacji RP uruchomionej w różnych Komputery w farmie. Przetwarzanie obejmuje sprawdzanie poprawności sygnatur tokenów sesji, szyfrowanie i odszyfrowywanie tokenów sesji, buforowanie tokenów sesji oraz Wykrywanie powtarzających się tokenów zabezpieczających.  
  
 W typowym przypadku, gdy WIF jest używany do zabezpieczania zasobów aplikacji RP — czy jednostka UZALEŻNIONa jest uruchomiona na pojedynczym komputerze lub w kolektywie serwerów sieci Web — sesja jest ustanawiana z klientem na podstawie tokenu zabezpieczającego uzyskanego z usługi tokenu zabezpieczającego (STS). Ma to na celu uniknięcie wymuszenia uwierzytelniania klienta w usłudze STS dla każdego zasobu aplikacji, który jest zabezpieczony za pomocą WIF. Aby uzyskać więcej informacji o tym, jak WIF obsługuje sesje, zobacz [Zarządzanie sesją WIF](wif-session-management.md).  
  
 Gdy są używane ustawienia domyślne, WIF wykonuje następujące czynności:  
  
- Używa wystąpienia <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> klasy do odczytu i zapisu tokenu sesji (wystąpienie <xref:System.IdentityModel.Tokens.SessionSecurityToken> klasy), które przenosi oświadczenia i inne informacje o tokenie zabezpieczającym, który został użyty do uwierzytelniania, a także informacje o sesji sam. Token sesji jest spakowany i przechowywany w pliku cookie sesji. Domyślnie program <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> <xref:System.IdentityModel.ProtectedDataCookieTransform> używa klasy, która używa interfejsu API ochrony danych (DPAPI) do ochrony tokenu sesji. DPAPI zapewnia ochronę przy użyciu poświadczeń użytkownika lub komputera i przechowuje dane klucza w profilu użytkownika.  
  
- Używa domyślnej implementacji <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> klasy w pamięci do przechowywania i przetwarzania tokenu sesji.  
  
 Te ustawienia domyślne działają w scenariuszach, w których aplikacja RP jest wdrażana na pojedynczym komputerze; Jednak po wdrożeniu w kolektywie serwerów sieci Web każde żądanie HTTP może zostać wysłane do i przetworzone przez inne wystąpienie aplikacji RP uruchomionej na innym komputerze. W tym scenariuszu domyślne ustawienia WIF opisane powyżej nie będą działały, ponieważ zarówno ochrona tokenów, jak i buforowanie tokenów są zależne od określonego komputera.  
  
 Aby wdrożyć aplikację RP w kolektywie serwerów sieci Web, należy się upewnić, że przetwarzanie tokenów sesji (jak również w przypadku ponownie uruchomionych tokenów) nie jest zależne od aplikacji uruchomionej na określonym komputerze. Jednym ze sposobów wykonania tej czynności jest zaimplementowanie aplikacji RP w taki sposób, aby korzystała z funkcji `<machineKey>` udostępnianych przez element konfiguracji ASP.NET i udostępnia rozproszone buforowanie na potrzeby przetwarzania tokenów sesji i ponownie odtwarzanych tokenów. `<machineKey>` Element pozwala określić klucze potrzebne do walidacji, szyfrowania i odszyfrowywania tokenów w pliku konfiguracji, co umożliwia określenie tych samych kluczy na różnych komputerach w kolektywie serwerów sieci Web. WIF udostępnia wyspecjalizowaną procedurę obsługi tokenów sesji <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>, która chroni tokeny przy użyciu kluczy określonych `<machineKey>` w elemencie. Aby zaimplementować tę strategię, można przestrzegać następujących wytycznych:  
  
- Użyj elementu ASP.NET `<machineKey>` w konfiguracji, aby jawnie określić klucze podpisywania i szyfrowania, które mogą być używane na różnych komputerach w farmie. Poniższy kod XML przedstawia specyfikację `<machineKey>` elementu `<system.web>` w elemencie w pliku konfiguracji.  
  
    ```xml  
    <machineKey compatibilityMode="Framework45" decryptionKey="CC510D … 8925E6" validationKey="BEAC8 … 6A4B1DE" />  
    ```  
  
- Skonfiguruj aplikację do użycia <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> przez dodanie jej do kolekcji obsługi tokenów. Należy najpierw usunąć <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> (lub wszelkie procedury obsługi pochodzące <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> z klasy) z kolekcji programu obsługi tokenów, jeśli taka procedura obsługi jest obecna. Używa klasy, która chroni dane plików cookie sesji za pomocą materiału `<machineKey>` kryptograficznego określonego w elemencie. <xref:System.IdentityModel.Services.MachineKeyTransform> <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> Poniższy kod XML przedstawia sposób dodawania <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> do kolekcji programu obsługi tokenów.  
  
    ```xml  
    <securityTokenHandlers>  
      <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
      <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    </securityTokenHandlers>  
    ```  
  
- Pochodzą z <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> i Implementuj rozproszone buforowanie, czyli pamięć podręczną, która jest dostępna ze wszystkich komputerów w farmie, w której może zostać uruchomiony system RP. Skonfiguruj składnik RP, aby używał rozproszonej pamięci podręcznej przez określenie [ \<elementu sessionSecurityTokenCache >](../configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) w pliku konfiguracji. Można zastąpić <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A?displayProperty=nameWithType> metodę w klasie pochodnej, aby zaimplementować elementy podrzędne elementu, `<sessionSecurityTokenCache>` jeśli są wymagane.  
  
    ```xml  
    <caches>  
      <sessionSecurityTokenCache type="MyCacheLibrary.MySharedSessionSecurityTokenCache, MyCacheLibrary">  
        <!--optional child configuration elements, if implemented by the derived class -->  
      </sessionSecurityTokenCache>  
    </caches>  
    ```  
  
     Jednym ze sposobów implementacji rozproszonej pamięci podręcznej jest zapewnienie frontonu programu WCF dla niestandardową pamięć podręczną. Aby uzyskać więcej informacji na temat implementowania usługi buforowania WCF, zobacz [Usługa buforowania WCF](#BKMK_TheWCFCachingService). Aby uzyskać więcej informacji na temat implementowania klienta WCF, który może być używany przez aplikację RP do wywoływania usługi buforowania, zobacz [klienta buforowania WCF](#BKMK_TheWCFClient).  
  
- Jeśli aplikacja wykryje ponownie uruchomione tokeny, należy przestrzegać podobnej strategii rozproszonej pamięci podręcznej dla buforu powtarzania tokenów, pobierając z <xref:System.IdentityModel.Tokens.TokenReplayCache> i wskazując usługę buforowania powtarzania tokenów [ \<w tokenReplayCache >](../configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md) element konfiguracji.  
  
> [!IMPORTANT]
> Wszystkie przykładowe XML i kod w tym temacie są pobierane z przykładu [ClaimsAwareWebFarm](https://go.microsoft.com/fwlink/?LinkID=248408) .  
  
> [!IMPORTANT]
> Przykłady w tym temacie są podane jako-is i nie są przeznaczone do użycia w kodzie produkcyjnym bez modyfikacji.  
  
<a name="BKMK_TheWCFCachingService"></a>   
## <a name="the-wcf-caching-service"></a>Usługa buforowania WCF  
 Poniższy interfejs definiuje umowę między usługą buforowania WCF i klientem WCF używanym przez aplikację jednostki uzależnionej do komunikowania się z nią. Zasadniczo uwidacznia metody <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> klasy jako operacje usługi.  
  
```csharp
[ServiceContract()]  
public interface ISessionSecurityTokenCacheService  
{  
    [OperationContract]  
    void AddOrUpdate(string endpointId, string contextId, string keyGeneration, SessionSecurityToken value, DateTime expiryTime);  
  
    [OperationContract]  
    IEnumerable<SessionSecurityToken> GetAll(string endpointId, string contextId);  
  
    [OperationContract]  
    SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration);  
  
    [OperationContract(Name = "RemoveAll")]  
    void RemoveAll(string endpointId, string contextId);  
  
    [OperationContract(Name = "RemoveAllByEndpointId")]  
    void RemoveAll(string endpointId);  
  
    [OperationContract]  
    void Remove(string endpointId, string contextId, string keyGeneration);  
}  
```  
  
 Poniższy kod przedstawia implementację usługi buforowania WCF. W tym przykładzie użyto domyślnej pamięci podręcznej tokenu sesji w pamięci wdrożonej przez WIF. Alternatywnie, można zaimplementować trwałą pamięć podręczną w bazie danych. `ISessionSecurityTokenCacheService`definiuje opisany powyżej interfejs. W tym przykładzie nie wszystkie metody wymagane do zaimplementowania interfejsu są wyświetlane dla zwięzłości.  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace WcfSessionSecurityTokenCacheService  
{  
    [ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
    public class SessionSecurityTokenCacheService : ISessionSecurityTokenCacheService  
    {  
        SessionSecurityTokenCache internalCache;  
  
        // sets the internal cache used by the service to the default WIF in-memory cache.  
        public SessionSecurityTokenCacheService()  
        {  
            internalCache = new IdentityModelCaches().SessionSecurityTokenCache;  
        }  
  
        ...  
  
        public SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration)  
        {  
            // Delegates to the default, in-memory MruSessionSecurityTokenCache used by WIF  
            SessionSecurityToken token = internalCache.Get(new SessionSecurityTokenCacheKey(endpointId, GetContextId(contextId), GetKeyGeneration(keyGeneration)));  
            return token;  
        }  
  
        ...  
  
        private static UniqueId GetContextId(string contextIdString)  
        {  
            return contextIdString == null ? null : new UniqueId(contextIdString);  
        }  
  
        private static UniqueId GetKeyGeneration(string keyGenerationString)  
        {  
            return keyGenerationString == null ? null : new UniqueId(keyGenerationString);  
        }  
    }  
}  
```  
  
<a name="BKMK_TheWCFClient"></a>   
## <a name="the-wcf-caching-client"></a>Klient buforowania WCF  
 W tej sekcji przedstawiono implementację klasy, która pochodzi od <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> i która deleguje wywołania do usługi buforowania. Aplikację RP można skonfigurować tak, aby używała tej klasy za pomocą [ \<elementu sessionSecurityTokenCache >](../configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) , jak w poniższym kodzie XML  
  
```xml  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
 Klasa przesłania <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A> metodę, aby uzyskać punkt końcowy usługi z niestandardowego `<cacheServiceAddress>` elementu `<sessionSecurityTokenCache>` podrzędnego elementu. Używa tego punktu końcowego do zainicjowania `ISessionSecurityTokenCacheService` kanału, w którym może komunikować się z usługą.  W tym przykładzie nie wszystkie metody wymagane do zaimplementowania <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> klasy są wyświetlane dla zwięzłości.  
  
```csharp
using System;  
using System.Configuration;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace CacheLibrary  
{  
    /// <summary>  
    /// This class acts as a proxy to the WcfSessionSecurityTokenCacheService.  
    /// </summary>  
    public class SharedSessionSecurityTokenCache : SessionSecurityTokenCache, ICustomIdentityConfiguration  
    {  
        private ISessionSecurityTokenCacheService WcfSessionSecurityTokenCacheServiceClient;  
  
        internal SharedSessionSecurityTokenCache()  
        {  
        }  
  
        /// <summary>  
        /// Creates a client channel to call the service host.  
        /// </summary>  
        protected void Initialize(string cacheServiceAddress)  
        {  
            if (this.WcfSessionSecurityTokenCacheServiceClient != null)  
            {  
                return;  
            }  
  
            ChannelFactory<ISessionSecurityTokenCacheService> cf = new ChannelFactory<ISessionSecurityTokenCacheService>(  
                new WS2007HttpBinding(SecurityMode.None),  
                new EndpointAddress(cacheServiceAddress));  
            this.WcfSessionSecurityTokenCacheServiceClient = cf.CreateChannel();  
        }  
  
        #region SessionSecurityTokenCache Members  
        // Delegates the following operations to the centralized session security token cache service in the web farm.  
  
        ...  
  
        public override SessionSecurityToken Get(SessionSecurityTokenCacheKey key)  
        {  
            return this.WcfSessionSecurityTokenCacheServiceClient.Get(key.EndpointId, GetContextIdString(key), GetKeyGenerationString(key));  
        }  
  
        ...  
  
        #endregion  
  
        #region ICustomIdentityConfiguration Members  
        // Called from configuration infrastructure to load custom elements  
        public void LoadCustomConfiguration(XmlNodeList nodeList)  
        {  
            // Retrieve the endpoint address of the centralized session security token cache service running in the web farm  
            if (nodeList.Count == 0)  
            {  
                throw new ConfigurationException("No child config element found under <sessionSecurityTokenCache>.");  
            }  
  
            XmlElement cacheServiceAddressElement = nodeList.Item(0) as XmlElement;  
            if (cacheServiceAddressElement.LocalName != "cacheServiceAddress")  
            {  
                throw new ConfigurationException("First child config element under <sessionSecurityTokenCache> is expected to be <cacheServiceAddress>.");  
            }  
  
            string cacheServiceAddress = null;  
            if (cacheServiceAddressElement.Attributes["url"] != null)  
            {  
                cacheServiceAddress = cacheServiceAddressElement.Attributes["url"].Value;  
            }  
            else  
            {  
                throw new ConfigurationException("<cacheServiceAddress> is expected to contain a 'url' attribute.");  
            }  
  
            // Initialize the proxy to the WebFarmSessionSecurityTokenCacheService  
            this.Initialize(cacheServiceAddress);  
        }  
        #endregion  
  
        private static string GetKeyGenerationString(SessionSecurityTokenCacheKey key)  
        {  
            return key.KeyGeneration == null ? null : key.KeyGeneration.ToString();  
        }  
  
        private static string GetContextIdString(SessionSecurityTokenCacheKey key)  
        {  
            return GetContextIdString(key.ContextId);  
        }  
  
        private static string GetContextIdString(UniqueId contextId)  
        {  
            return contextId == null ? null : contextId.ToString();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>
- <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>
- <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>
- [Zarządzanie sesjami programu WIF](wif-session-management.md)
