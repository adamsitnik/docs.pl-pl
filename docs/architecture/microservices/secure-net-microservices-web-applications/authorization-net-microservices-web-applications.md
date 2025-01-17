---
title: Informacje o autoryzacji w mikrousługach .NET i aplikacjach internetowych
description: Zabezpieczenia w mikrousługach .NET i aplikacjach sieci Web — zapoznaj się z głównymi opcjami autoryzacji w ASP.NET Core aplikacje — oparta na rolach i oparta na zasadach.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 36cd8eaf7ffe78a29762398044dc1803adc1b200
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296469"
---
# <a name="about-authorization-in-net-microservices-and-web-applications"></a>Informacje o autoryzacji w mikrousługach .NET i aplikacjach internetowych

Po uwierzytelnieniu ASP.NET Core internetowe interfejsy API muszą autoryzować dostęp. Ten proces umożliwia usłudze udostępnianie interfejsów API niektórym uwierzytelnionym użytkownikom, ale nie wszystkim. [Autoryzację](/aspnet/core/security/authorization/introduction) można wykonać w oparciu o role użytkowników lub na podstawie zasad niestandardowych, które mogą obejmować sprawdzanie oświadczeń lub innych algorytmów heurystycznych.

Ograniczanie dostępu do trasy ASP.NET Core MVC jest tak proste jak stosowanie atrybutu Autoryzuj do metody akcji (lub do klasy kontrolera, jeśli wszystkie akcje kontrolera wymagają autoryzacji), jak pokazano w poniższym przykładzie:

```csharp
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    [Authorize]
    public ActionResult Logout()
    {
    }
}
```

Domyślnie dodanie atrybutu Autoryzuj bez parametrów spowoduje ograniczenie dostępu do uwierzytelnionych użytkowników dla tego kontrolera lub akcji. Aby dodatkowo ograniczyć interfejs API do dostępności tylko dla określonych użytkowników, atrybut można rozszerzyć, aby określić wymagane role lub zasady, które użytkownicy muszą spełnić.

## <a name="implement-role-based-authorization"></a>Implementowanie autoryzacji opartej na rolach

Tożsamość ASP.NET Core ma wbudowaną koncepcję ról. Oprócz użytkowników, ASP.NET Core tożsamość przechowuje informacje o różnych rolach używanych przez aplikację i śledzi użytkowników, którym przypisano role. Te przypisania można programowo zmienić za pomocą `RoleManager` typu, który aktualizuje role w magazynie trwałym, `UserManager` oraz typ, który może udzielić lub odwołać role użytkowników.

W przypadku uwierzytelniania za pomocą tokenów okaziciela JWT, oprogramowanie pośredniczące uwierzytelniania okaziciela JWT ASP.NET Core wypełniać role użytkownika na podstawie oświadczeń ról znalezionych w tokenie. Aby ograniczyć dostęp do akcji lub kontrolera MVC do użytkowników w określonych rolach, można dołączyć parametr Role w adnotacji Autoryzuj (Attribute), jak pokazano w poniższym fragmencie kodu:

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

W tym przykładzie tylko użytkownicy z rolą Administrator lub PowerUser mogą uzyskać dostęp do interfejsów API w kontrolerze ControlPanel (na przykład wykonując akcję SetTime). Interfejs API zamykania jest dodatkowo ograniczony, aby zezwalać na dostęp tylko użytkownikom w roli administratora.

Aby wymagać, aby użytkownik znajdował się w wielu rolach, należy użyć wielu atrybutów autoryzacji, jak pokazano w następującym przykładzie:

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
[Authorize(Roles = "RemoteEmployee ")]
[Authorize(Policy = "CustomPolicy")]
public ActionResult API1 ()
{
}
```

W tym przykładzie do wywołania API1 użytkownik musi:

- Należy do roli administrator *lub* PowerUser, *a* także

- Należy do roli RemoteEmployee *i*

- Zaspokoj niestandardową procedurę obsługi autoryzacji CustomPolicy.

## <a name="implement-policy-based-authorization"></a>Implementowanie autoryzacji opartej na zasadach

Niestandardowe reguły autoryzacji można także napisać przy użyciu [zasad autoryzacji](https://docs.asp.net/en/latest/security/authorization/policies.html). Ta sekcja zawiera omówienie. Aby uzyskać więcej informacji, zobacz [warsztat ASP.NET Authorization](https://github.com/blowdart/AspNetAuthorizationWorkshop).

Niestandardowe zasady autoryzacji są rejestrowane w metodzie Startup. ConfigureServices przy użyciu usługi. Metoda addauthorization. Ta metoda pobiera delegata, który konfiguruje argument AuthorizationOptions.

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("AdministratorsOnly", policy =>
        policy.RequireRole("Administrator"));
    options.AddPolicy("EmployeesOnly", policy =>
        policy.RequireClaim("EmployeeNumber"));
    options.AddPolicy("Over21", policy =>
        policy.Requirements.Add(new MinimumAgeRequirement(21)));
});
```

Jak pokazano w przykładzie, zasady można kojarzyć z różnymi typami wymagań. Po zarejestrowaniu zasad można je stosować do akcji lub kontrolera przez przekazanie nazwy zasad jako argumentu zasad atrybutu Autoryzuj (na przykład `[Authorize(Policy="EmployeesOnly")]`) zasady mogą mieć wiele wymagań, a nie tylko jeden (jak pokazano w tych Przykłady).

W poprzednim przykładzie pierwsze wywołanie addpolicy jest tylko alternatywnym sposobem autoryzacji przez rolę. Jeśli `[Authorize(Policy="AdministratorsOnly")]` zostanie on zastosowany do interfejsu API, tylko użytkownicy z rolą Administrator będą mogli uzyskać do niego dostęp.

Drugie <xref:Microsoft.AspNetCore.Authorization.AuthorizationOptions.AddPolicy%2A> wywołanie pokazuje łatwy sposób, aby wymagać, aby określone żądanie było obecne dla użytkownika. <xref:Microsoft.AspNetCore.Authorization.AuthorizationPolicyBuilder.RequireClaim%2A> Metoda również opcjonalnie pobiera oczekiwane wartości dla żądania. Jeśli wartości są określone, wymaganie jest spełnione tylko wtedy, gdy użytkownik ma zarówno żądanie poprawnego typu, jak i jedną z określonych wartości. Jeśli używasz oprogramowania pośredniczącego uwierzytelniania okaziciela JWT, wszystkie właściwości JWT będą dostępne jako oświadczenia użytkownika.

Najbardziej interesujące zasady pokazane w tym miejscu znajdują `AddPolicy` się w trzeciej metodzie, ponieważ używa ona niestandardowego wymagania autoryzacji. Za pomocą niestandardowych wymagań dotyczących autoryzacji możesz mieć doskonałą kontrolę nad sposobem autoryzacji. Aby to działało, należy zaimplementować następujące typy:

- Typ wymagania, który pochodzi od <xref:Microsoft.AspNetCore.Authorization.IAuthorizationRequirement> i który zawiera pola określające szczegóły wymagania. W tym przykładzie jest to pole wiek dla typu przykładowego `MinimumAgeRequirement` .

- Program obsługi, który <xref:Microsoft.AspNetCore.Authorization.AuthorizationHandler%601>implementuje, gdzie T jest <xref:Microsoft.AspNetCore.Authorization.IAuthorizationRequirement> typem, który może spełniać program obsługi. Procedura obsługi musi implementować <xref:Microsoft.AspNetCore.Authorization.AuthorizationHandler%601.HandleRequirementAsync%2A> metodę, która sprawdza, czy określony kontekst zawierający informacje o użytkowniku spełnia wymagania.

Jeśli użytkownik spełnia wymagania, wywołanie `context.Succeed` będzie wskazywać, że użytkownik jest autoryzowany. Jeśli istnieje wiele sposobów, że użytkownik może spełnić wymagania dotyczące autoryzacji, można utworzyć wiele programów obsługi.

Oprócz rejestrowania niestandardowych wymagań dotyczących zasad z `AddPolicy` wywołaniami należy również zarejestrować niestandardowe programy obsługi wymagań za pomocą iniekcji zależności (`services.AddTransient<IAuthorizationHandler, MinimumAgeHandler>()`).

Przykładem niestandardowego wymagania dotyczącego autoryzacji i obsługi sprawdzania wieku użytkownika (na podstawie `DateOfBirth` roszczeń) jest dostępny w dokumentacji dotyczącej [autoryzacji](https://docs.asp.net/en/latest/security/authorization/policies.html)ASP.NET Core.

## <a name="additional-resources"></a>Dodatkowe zasoby

- **Uwierzytelnianie ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/security/authentication/identity](/aspnet/core/security/authentication/identity)

- **Autoryzacja ASP.NET Core** \
  [https://docs.microsoft.com/aspnet/core/security/authorization/introduction](/aspnet/core/security/authorization/introduction)

- **Autoryzacja oparta na rolach** \
  [https://docs.microsoft.com/aspnet/core/security/authorization/roles](/aspnet/core/security/authorization/roles)

- **Niestandardowa Autoryzacja oparta na zasadach** \
  [https://docs.microsoft.com/aspnet/core/security/authorization/policies](/aspnet/core/security/authorization/policies)

>[!div class="step-by-step"]
>[Poprzedni](index.md)Następny
>[](developer-app-secrets-storage.md)
