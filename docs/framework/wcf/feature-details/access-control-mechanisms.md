---
title: Mechanizmy kontroli dostępu
ms.date: 03/30/2017
helpviewer_keywords:
- WCF security
- access control [WCF]
ms.assetid: 9d576122-3f55-4425-9acf-b23d0781e966
ms.openlocfilehash: 14f348300d8ab9276a86b4cf8d91823d39b9aba3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964986"
---
# <a name="access-control-mechanisms"></a>Mechanizmy kontroli dostępu
Dostęp można kontrolować w kilka sposobów przy użyciu Windows Communication Foundation (WCF). W tym temacie krótko omówiono różne mechanizmy i przedstawiono sugestie dotyczące sytuacji, w których należy ich używać. ma ona na celu ułatwienie wyboru właściwego mechanizmu do użycia. Technologie dostępu są wymienione w kolejności złożoności. Najprostszą jest to <xref:System.Security.Permissions.PrincipalPermissionAttribute>, że najbardziej złożona jest model tożsamości.  
  
 Oprócz tych mechanizmów personifikacja i delegowanie z użyciem WCF jest wyjaśniona w [delegacji i personifikacji](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
## <a name="principalpermissionattribute"></a>PrincipalPermissionAttribute  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute> Służy do ograniczania dostępu do metody usługi. Gdy atrybut zostanie zastosowany do metody, można go użyć do żądania tożsamości określonego obiektu wywołującego lub członkostwa w grupie systemu Windows lub roli ASP.NET. Jeśli klient jest uwierzytelniany przy użyciu certyfikatu X. 509, otrzymuje podstawową tożsamość, która składa się z nazwy podmiotu i odcisku palca certyfikatu.  
  
 Za pomocą <xref:System.Security.Permissions.PrincipalPermissionAttribute> programu można kontrolować dostęp do zasobów na komputerze, na którym uruchomiona jest usługa, a użytkownicy usługi zawsze będą częścią tej samej domeny systemu Windows, w której uruchomiona jest usługa. Można łatwo utworzyć grupy systemu Windows, które mają określone poziomy dostępu (np. Brak, tylko do odczytu lub odczyt i zapis).  
  
 Aby uzyskać więcej informacji o korzystaniu z atrybutu [, zobacz How to: Ogranicz dostęp za pomocą klasy](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)PrincipalPermissionAttribute. Aby uzyskać więcej informacji na temat tożsamości, zobacz [tożsamość usługi i uwierzytelnianie](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
## <a name="aspnet-membership-provider"></a>Dostawca członkostwa ASP.NET  
 Funkcją ASP.NET jest dostawca członkostwa. Mimo że dostawca członkostwa nie jest technicznie mechanizm kontroli dostępu, umożliwia kontrolowanie dostępu do usługi poprzez ograniczenie zestawu możliwych tożsamości, które mogą uzyskać dostęp do punktu końcowego usługi. Funkcja członkostwa obejmuje bazę danych, która może zostać wypełniona przy użyciu kombinacji nazwy użytkownika i hasła, które umożliwiają użytkownikom witryny sieci Web ustanawianie kont z tą lokacją. Aby uzyskać dostęp do usługi korzystającej z dostawcy członkostwa, użytkownik musi zalogować się przy użyciu nazwy użytkownika i hasła.  
  
> [!NOTE]
> Przed użyciem usługi WCF do celów autoryzacji należy najpierw wypełnić bazę danych przy użyciu funkcji ASP.NET.  
  
 Możesz również użyć funkcji członkostwa, jeśli masz już bazę danych członkowską z istniejącej witryny sieci Web ASP.NET i chcesz umożliwić tym samym użytkownikom korzystanie z usługi, autoryzowane przy użyciu tych samych nazw użytkowników i haseł.  
  
 Aby uzyskać więcej informacji o korzystaniu z funkcji członkostwa w usłudze WCF, [zobacz How to: Użyj dostawcy](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)członkostwa ASP.NET.  
  
## <a name="aspnet-role-provider"></a>Dostawca roli ASP.NET  
 Kolejną funkcją ASP.NET jest możliwość zarządzania autoryzacją przy użyciu ról. Dostawca roli ASP.NET umożliwia deweloperom tworzenie ról dla użytkowników i przypisywanie poszczególnych użytkowników do ról lub ról. Podobnie jak w przypadku dostawcy członkostwa, role i przypisania są przechowywane w bazie danych i mogą być wypełniane przy użyciu narzędzi dostarczonych przez określoną implementację dostawcy roli ASP.NET. Podobnie jak w przypadku funkcji członkostwa deweloperzy programu WCF mogą korzystać z informacji znajdujących się w bazie danych w celu autoryzowania użytkowników usługi przez role. Mogą na przykład używać dostawcy ról w połączeniu z `PrincipalPermissionAttribute` mechanizm kontroli dostępu opisany powyżej.  
  
 Możesz również użyć dostawcy roli ASP.NET, jeśli masz istniejącą bazę danych dostawcy ról ASP.NET i chcesz użyć tego samego zestawu reguł i przypisań użytkowników w usłudze WCF.  
  
 Aby uzyskać więcej informacji o korzystaniu z funkcji dostawcy roli [, zobacz How to: Używanie dostawcy roli ASP.NET z usługą](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md).  
  
## <a name="authorization-manager"></a>Menedżer autoryzacji  
 Inna funkcja łączy Menedżera autoryzacji (AzMan) z dostawcą roli ASP.NET w celu autoryzowania klientów. Gdy usługa ASP.NET hostuje usługę sieci Web, AzMan można zintegrować z aplikacją, aby autoryzacja w usłudze była przeprowadzana przez AzMan. ASP.NET role Manager udostępnia interfejs API, który umożliwia zarządzanie rolami aplikacji, Dodawanie i usuwanie użytkowników z ról oraz sprawdzanie przynależności do roli, ale nie pozwala na wykonywanie zapytań o to, czy użytkownik jest uprawniony do wykonywania nazwanego zadania lub operacji. AzMan pozwala definiować poszczególne operacje i łączyć je z zadaniami. Za pomocą AZMan, oprócz sprawdzania roli, można również sprawdzić, czy użytkownik może wykonać zadanie. Przypisanie roli i autoryzacja zadań można skonfigurować poza aplikacją lub wykonywać programowo w aplikacji. Przystawka Administracja AzMana programu Microsoft Management Console (MMC) umożliwia administratorom zmianę zadań wykonywanych przez rolę w czasie wykonywania oraz zarządzanie członkostwem poszczególnych użytkowników.  
  
 Możesz również użyć AzMan i dostawcy ról ASP.NET, jeśli masz już dostęp do istniejącej instalacji AzMan i chcesz autoryzować użytkowników usługi przy użyciu funkcji kombinacji AzMan/dostawcy ról.  
  
 Aby uzyskać więcej informacji na temat AzMan i dostawcy ról ASP.NET, [zobacz How to: Użyj Menedżera autoryzacji (AzMan) z ASP.NET 2,0](https://go.microsoft.com/fwlink/?LinkId=88951). Aby uzyskać więcej informacji o korzystaniu z AzMan i dostawcy roli dla usług WCF [, zobacz How to: Używanie dostawcy roli Menedżera autoryzacji ASP.NET z usługą](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md).  
  
## <a name="identity-model"></a>Model tożsamości  
 Model tożsamości to zestaw interfejsów API, które umożliwiają zarządzanie oświadczeniami i zasadami w celu autoryzowania klientów. Korzystając z modelu tożsamości, można przeanalizować każde oświadczenie zawarte w poświadczeniach, których obiekt wywołujący użył do samodzielnego uwierzytelnienia w usłudze, porównać oświadczenia z zestawem zasad usługi i przyznać lub odmówić dostępu na podstawie porównania.  
  
 Użyj modelu tożsamości, jeśli potrzebujesz precyzyjnej kontroli i możliwość ustawiania określonych kryteriów przed udzieleniem dostępu. Na przykład podczas korzystania z <xref:System.Security.Permissions.PrincipalPermissionAttribute>, kryterium jest po prostu, że tożsamość użytkownika jest uwierzytelniana i należy do określonej roli. Natomiast przy użyciu modelu tożsamości można utworzyć zasady, które określają, że użytkownik musi mieć ponad 18 lat i dysponować ważną licencją sterownika przed zezwoleniem na wyświetlanie dokumentu.  
  
 Przykładem możliwości skorzystania z kontroli dostępu opartej na żądaniach modelu tożsamości jest użycie poświadczeń Federacji w scenariuszu wystawionego tokenu. Aby uzyskać więcej informacji na temat Federacji i wystawionych tokenów, zobacz [federacyjnego i](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)wystawione tokeny.  
  
 Aby uzyskać więcej informacji na temat modelu tożsamości, zobacz [Zarządzanie oświadczeniami i autoryzacją za pomocą modelu tożsamości](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Security.Permissions.PrincipalPermissionAttribute>
- [Instrukcje: Ograniczanie dostępu przy użyciu klasy PrincipalPermissionAttribute](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)
- [Instrukcje: Używanie dostawcy roli ASP.NET z usługą](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
- [Instrukcje: Używanie dostawcy roli Menedżera autoryzacji ASP.NET z usługą](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)
- [Zarządzanie oświadczeniami i autoryzacją za pomocą modelu tożsamości](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
- [Delegowanie i personifikacja](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
