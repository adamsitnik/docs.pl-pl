---
ms.openlocfilehash: a4e20e0468d861138ad801c9dbfa15340b3f388c
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394282"
---
### <a name="authentication-oauthhandler-exchangecodeasync-signature-changed"></a>Uwierzytelnianie: OAuthHandler ExchangeCodeAsync zmieniono sygnaturę

W ASP.NET Core 3,0 sygnatura `OAuthHandler.ExchangeCodeAsync` została zmieniona z:

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(string code, string redirectUri) { throw null; }
```

Do:

```csharp
protected virtual System.Threading.Tasks.Task<Microsoft.AspNetCore.Authentication.OAuth.OAuthTokenResponse> ExchangeCodeAsync(Microsoft.AspNetCore.Authentication.OAuth.OAuthCodeExchangeContext context) { throw null; }
```

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="old-behavior"></a>Stare zachowanie

Ciągi `code` i `redirectUri` zostały przekazane jako oddzielne argumenty.

#### <a name="new-behavior"></a>Nowe zachowanie

`Code` i `RedirectUri` są właściwościami `OAuthCodeExchangeContext`, które można ustawić za pośrednictwem konstruktora `OAuthCodeExchangeContext`. Nowy typ `OAuthCodeExchangeContext` jest jedynym argumentem przekazaną do `OAuthHandler.ExchangeCodeAsync`.

#### <a name="reason-for-change"></a>Przyczyna zmiany

Ta zmiana pozwala na dostarczenie dodatkowych parametrów w sposób rozdzielny. Nie ma potrzeby tworzenia nowych przeciążeń `ExchangeCodeAsync`.

#### <a name="recommended-action"></a>Zalecana akcja

Utwórz `OAuthCodeExchangeContext` z odpowiednimi wartościami `code` i `redirectUri`. Należy podać wystąpienie <xref:Microsoft.AspNetCore.Authentication.AuthenticationProperties>. To pojedyncze wystąpienie `OAuthCodeExchangeContext` może być przekazane do `OAuthHandler.ExchangeCodeAsync` zamiast wielu argumentów.

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

<xref:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler%601.ExchangeCodeAsync(System.String,System.String)?displayProperty=nameWithType>

<!--

#### Affected APIs

`M:Microsoft.AspNetCore.Authentication.OAuth.OAuthHandler`1.ExchangeCodeAsync(System.String,System.String)`

-->
