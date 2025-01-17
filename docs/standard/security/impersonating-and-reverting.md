---
title: Personifikacja i przywracanie
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WindowsIdentity objects, impersonating
- security [.NET Framework], impersonating Windows accounts
- impersonating Windows accounts
ms.assetid: b93d402c-6c28-4f50-b2bc-d9607dc3e470
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 97b15ea2202ca410dd517db63a7145d27f62bb48
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018596"
---
# <a name="impersonating-and-reverting"></a>Personifikacja i przywracanie
Czasami może być konieczne do uzyskania tokenu konta Windows dokonać personifikacji konta Windows. Na przykład aplikacji opartych na programie ASP.NET może być konieczne działanie w imieniu kilku użytkowników w różnym czasie. Aplikację może akceptuje token, który reprezentuje administrator z Internet Information Services (IIS), personifikacji tego użytkownika, w trakcie operacji i powrócić do poprzedniej tożsamości. Następnie go może zaakceptować token za pomocą programu IIS, który reprezentuje użytkownika z prawami mniej, wykonać kilka operacji i przywrócić ponownie.  
  
 W sytuacjach, w której aplikacja musi dokonać personifikacji konta Windows, który nie został dołączony do bieżącego wątku przez usługi IIS należy pobrać tokenu dla konta i użyć go do aktywowania konta. Można to zrobić, wykonując następujące czynności:  
  
1. Pobieranie tokenu konta dla danego użytkownika przez wywołania do niezarządzanej **funkcji LogonUser** metody. Ta metoda nie znajduje się w bibliotece klasy bazowej .NET Framework, ale znajduje się w niezarządzanej **advapi32.dll**. Uzyskiwanie dostępu do metody w kodzie niezarządzanym jest zaawansowanym działaniem i wykracza poza zakres tej dyskusji. Aby uzyskać więcej informacji, zobacz [współdziałanie z kodem niezarządzanym](../../../docs/framework/interop/index.md). Aby uzyskać więcej informacji na temat **funkcji LogonUser** metody i **advapi32.dll**, znajdują się w dokumentacji zestawu SDK platformy.  
  
2. Utwórz nowe wystąpienie klasy **WindowsIdentity** klasy, przekazując tokenu. Poniższy kod przedstawia to wywołanie, gdy `hToken` reprezentuje Windows token.  
  
    ```csharp  
    WindowsIdentity impersonatedIdentity = new WindowsIdentity(hToken);  
    ```  
  
    ```vb  
    Dim impersonatedIdentity As New WindowsIdentity(hToken)  
    ```  
  
3. Rozpocznij personifikacji, tworząc nowe wystąpienie klasy <xref:System.Security.Principal.WindowsImpersonationContext> klasy i inicjując go przy użyciu <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A?displayProperty=nameWithType> metody klasy zainicjowane, jak pokazano w poniższym kodzie.  
  
    ```csharp  
    WindowsImpersonationContext myImpersonation = impersonatedIdentity.Impersonate();  
    ```  
  
    ```vb  
    WindowsImpersonationContext myImpersonation = impersonatedIdentity.Impersonate()  
    ```  
  
4. Jeśli nie potrzebujesz już być Personifikowane przez aplikację, należy wywołać <xref:System.Security.Principal.WindowsImpersonationContext.Undo%2A?displayProperty=nameWithType> metodę, aby przywrócić personifikacji, jak pokazano w poniższym kodzie.  
  
    ```csharp  
    myImpersonation.Undo();  
    ```  
  
    ```vb  
    myImpersonation.Undo()  
    ```  
  
 Jeśli zaufanego kodu jest już dołączony <xref:System.Security.Principal.WindowsPrincipal> obiekt wątku, można wywołać metodę wystąpienia **Personifikuj**, nie przyjmuje tokenu konta. Należy pamiętać, że ta opcja jest przydatna podczas **WindowsPrincipal** obiektu w wątku reprezentuje użytkownik inny niż ten, w którym proces jest w trakcie wykonywania. Na przykład można napotkać tę sytuację, za pomocą programu ASP.NET z uwierzytelnianiem Windows, włączone i wyłączone personifikacji. W tym przypadku proces działa przy użyciu konta skonfigurowane w Internet Information Services (IIS), gdy bieżący podmiot zabezpieczeń reprezentuje użytkownika Windows, który uzyskuje dostęp do strony.  
  
 Należy pamiętać, że żadna z nich nie **Personifikuj** ani **Cofnij** zmiany **jednostki** obiektu (<xref:System.Security.Principal.IPrincipal>) skojarzony z bieżącym kontekstem wywołania. Zamiast personifikacji i cofanie zmian tokenu skojarzone z bieżącym procesem systemu operacyjnego...  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Security.Principal.WindowsIdentity>
- <xref:System.Security.Principal.WindowsImpersonationContext>
- [Obiekty główne i obiekty tożsamości](../../../docs/standard/security/principal-and-identity-objects.md)
- [Współdziałanie z kodem niezarządzanym](../../../docs/framework/interop/index.md)
