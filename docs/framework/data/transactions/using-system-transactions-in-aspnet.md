---
title: Używanie elementu System.Transactions w programie ASP.NET
ms.date: 03/30/2017
ms.assetid: 1982c300-7ea6-4242-95ed-dc28ccfacac9
ms.openlocfilehash: 2bddebc13897408839e18f42b17a9fbaefdc5b87
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040407"
---
# <a name="using-systemtransactions-in-aspnet"></a>Używanie elementu System.Transactions w programie ASP.NET
W tym temacie opisano, jak można pomyślnie użyć <xref:System.Transactions> wewnątrz aplikacji ASP.NET.

## <a name="enable-distributedtransactionpermission-in-aspnet"></a>Włącz DistributedTransactionPermission w programie ASP.NET
 <xref:System.Transactions>obsługuje częściowo zaufanych wywołań i jest oznaczona za pomocą `AllowPartiallyTrustedCallers` atrybutu (APTCA). Poziomy zaufania dla <xref:System.Transactions> są zdefiniowane w oparciu o typy zasobów (na przykład pamięć systemowa, udostępnione zasoby dla całego procesu, zasoby systemowe i inne zasoby), które <xref:System.Transactions> uwidaczniane i poziom zaufania, który powinien być wymagany do uzyskiwania dostępu do tych produkcyjnych. W środowisku częściowej relacji zaufania, zestaw nie będący pełnym zaufaniem może używać tylko transakcji w domenie aplikacji (w tym przypadku jedynym chronionym zasobem jest pamięć systemowa), chyba że zostanie udzielony <xref:System.Transactions.DistributedTransactionPermission>.

 <xref:System.Transactions.DistributedTransactionPermission>jest wymagany przy każdym eskalacji transakcji zarządzania można zarządzać przez transakcję Koordynator MSDTC (Microsoft Distributed). Tego rodzaju scenariusza wykorzystuje zasoby całego procesu i szczególnie globalne zasób, który jest zarezerwowane miejsce w dzienniku MSDTC. Przykładem tego użycia jest fronton sieci Web do bazy danych lub aplikacji, która korzysta z bazy danych w ramach usług, które zapewnia.

 ASP.NET ma własny zestaw poziomów zaufania i kojarzy określony zestaw uprawnień z tymi poziomami zaufania za pomocą plików zasad. Aby uzyskać więcej informacji, zobacz [ASP.NET poziomów zaufania i plików zasad](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100)). Podczas pierwszej instalacji Windows SDK żadne z domyślnych plików zasad ASP.NET nie są skojarzone z <xref:System.Transactions.DistributedTransactionPermission>. W związku z tym, gdy transakcja w aplikacji ASP.NET jest przekazaniem do zarządzania przez MSDTC, eskalacja kończy się niepowodzeniem z <xref:System.Security.SecurityException> na <xref:System.Transactions.DistributedTransactionPermission>. Aby włączyć eskalację transakcji w środowisku ASP.NET częściowego zaufania, należy przyznać <xref:System.Transactions.DistributedTransactionPermission> na tych samych domyślnych poziomach zaufania co w przypadku <xref:System.Data.SqlClient.SqlClientPermission>. Możesz skonfigurować własny niestandardowy poziom zaufania i plik zasad, aby go obsługiwać, lub zmodyfikować domyślne pliki zasad, które są **Web_hightrust. config** i **web_mediumtrust. config**.

 Aby zmodyfikować pliki zasad, Dodaj element `SecurityClass` dla `DistributedTransactionPermission` do elementu `SecurityClasses` w obszarze `PolicyLevel` i Dodaj odpowiedni element `IPermission` w obszarze ASP.NET `NamedPermissionSet` dla elementu System. Transactions. Następujący PLik konfiguracji pokazuje to.

```xml
<SecurityClasses>
   <SecurityClass Name="DistributedTransactionPermission" Description="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
...
</SecurityClasses>

<PermissionSet
  class="NamedPermissionSet"
  version="1"
  Name="ASP.Net">
     <IPermission
        class="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
        version="1"
        Unrestricted="true"
     />
...
</PermissionSet>
```

 Aby uzyskać więcej informacji na temat zasad zabezpieczeń ASP.NET, zobacz [SecurityPolicy elementu (ASP.NET Settings Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100)).

## <a name="dynamic-compilation"></a>Dynamicznej kompilacji
 Jeśli chcesz zaimportować i używać <xref:System.Transactions> w aplikacji ASP.NET, która jest dynamicznie kompilowana w programie Access, należy umieścić odwołanie do zestawu <xref:System.Transactions> w pliku konfiguracji. W konkretnym przypadku należy dodać odwołanie do sekcji `compilation/assemblies` domyślnego głównego pliku konfiguracyjnego **Web. config** lub pliku konfiguracji konkretnej aplikacji sieci Web. Poniższy przykład ilustruje to.

```xml
<configuration>
   <system.web>
      <compilation>
         <assemblies>
      <add assembly="System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
         </assemblies>
      </compilation>
   </system.web>
</configuration>
```

 Aby uzyskać więcej informacji, zobacz [Dodawanie elementu do zestawów dla kompilacji (Schemat ustawień ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/37e2zyhb(v=vs.100)).

## <a name="see-also"></a>Zobacz także

- [ASP.NET poziomów zaufania i plików zasad](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))
- [securityPolicy, element (Schemat ustawień ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))
- [Eskalacja zarządzania transakcjami](transaction-management-escalation.md)
