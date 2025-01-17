---
title: Zarządzanie wstrzymanymi wystąpieniami
ms.date: 03/30/2017
ms.assetid: f5ca3faa-ba1f-4857-b92c-d927e4b29598
ms.openlocfilehash: 7a2f36ac2c127376eea56601f54aa5e571d66a55
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037891"
---
# <a name="suspended-instance-management"></a>Zarządzanie wstrzymanymi wystąpieniami
Ten przykład pokazuje, jak zarządzać wystąpieniami przepływów pracy, które zostały zawieszone.  Domyślna akcja dla elementu <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> is `AbandonAndSuspend`. Oznacza to, że domyślnie Nieobsłużone wyjątki zgłaszane z wystąpienia przepływu pracy hostowanego w programie <xref:System.ServiceModel.WorkflowServiceHost> spowodują, że wystąpienie zostanie usunięte z pamięci (porzucone) i trwałe/utrwalone wersje wystąpienia zostanie oznaczone jako wstrzymane. Nie będzie można uruchomić wstrzymanego wystąpienia przepływu pracy, dopóki nie zostanie ono zawieszone.

 Przykład pokazuje, jak można zaimplementować narzędzie wiersza polecenia, aby wykonać zapytanie o wstrzymane wystąpienia oraz jak dać użytkownikowi możliwość wznowienia lub zakończenia wystąpienia. W tym przykładzie usługa przepływu pracy celowo zgłasza wyjątek, powodując jego zawieszenie. Narzędzia wiersza polecenia można następnie użyć, aby wykonać zapytanie dotyczące wystąpienia, a następnie wznowić lub przerwać wystąpienie.

## <a name="demonstrates"></a>Demonstracje
 <xref:System.ServiceModel.WorkflowServiceHost>z <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> i<xref:System.ServiceModel.Activities.WorkflowControlEndpoint> w Windows Workflow Foundation (WF).

## <a name="discussion"></a>Dyskusji
 Narzędzie wiersza polecenia zaimplementowane w tym przykładzie jest specyficzne dla implementacji magazynu wystąpień SQL, która jest dostarczana [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]przez program. Jeśli masz niestandardową implementację magazynu wystąpień, możesz dostosować to narzędzie, zastępując `WorkflowInstanceCommand` implementacje w przykładzie z implementacjami specyficznymi dla Twojego magazynu wystąpień.

 Podana implementacja uruchamia polecenia SQL względem magazynu wystąpień SQL bezpośrednio w celu wyświetlenia listy wstrzymanych wystąpień i opiera się na dodaniu <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> <xref:System.ServiceModel.WorkflowServiceHost> do elementu w celu wznowienia lub zakończenia wystąpień.

#### <a name="to-set-up-build-and-run-the-sample"></a>Aby skonfigurować, skompilować i uruchomić przykład

1. Ten przykład wymaga włączenia następujących składników systemu Windows:

    1. Serwer usługi kolejkowania komunikatów (MSMQ) firmy Microsoft

    2. SQL Server Express

2. Skonfiguruj bazę danych SQL Server.

    1. W wierszu polecenia programu Visual Studio 2010 Uruchom polecenie "Setup. cmd" z przykładowego katalogu SuspendedInstanceManagement, który wykonuje następujące czynności:

        1. Tworzy bazę danych trwałości przy użyciu SQL Server Express. Jeśli baza danych trwałości już istnieje, zostanie usunięta i ponownie utworzona

        2. Konfiguruje bazę danych do trwałości.

        3. Dodaje usługi IIS APPPOOL\DefaultAppPool i NT AUTHORITY\Network do roli InstanceStoreUsers, która została zdefiniowana podczas konfigurowania bazy danych do trwałości.

3. Skonfiguruj kolejkę usługi.

    1. W programie Visual Studio 2010 kliknij prawym przyciskiem myszy projekt **SampleWorkflowApp** , a następnie kliknij pozycję **Ustaw jako projekt startowy**.

    2. Kompiluj i uruchamiaj SampleWorkflowApp, naciskając klawisz **F5**. Spowoduje to utworzenie wymaganej kolejki.

    3. Naciśnij klawisz **Enter** , aby zatrzymać SampleWorkflowApp.

    4. Otwórz konsolę zarządzania komputerem, uruchamiając polecenie compmgmt. msc z poziomu wiersza polecenia.

    5. Rozwiń węzeł **usługi i aplikacje**, kolejkowanie **komunikatów**, **kolejki prywatne**.

    6. Kliknij prawym przyciskiem myszy kolejkę **ReceiveTx** i wybierz pozycję **Właściwości**.

    7. Wybierz kartę **zabezpieczenia** i zezwól **wszystkim** na posiadanie uprawnień do **odbierania wiadomości**, **wglądu wiadomości**i **wysyłania wiadomości**.

4. Teraz uruchom przykład.

    1. W programie Visual Studio 2010 ponownie uruchom projekt SampleWorkflowApp bez debugowania przez naciśnięcie **klawiszy CTRL + F5**. Dwa adresy punktów końcowych będą drukowane w oknie konsoli: jeden dla punktu końcowego aplikacji, a następnie inny z <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>. Tworzone jest wystąpienie przepływu pracy, a śledzenie rekordów dla tego wystąpienia pojawi się w oknie konsoli. Wystąpienie przepływu pracy spowoduje zgłoszenie wyjątku powodującego zawieszenie i przerwanie wystąpienia.

    2. Narzędzia wiersza polecenia można następnie użyć do wykonania dalszych czynności na każdym z tych wystąpień. Składnia argumentów wiersza polecenia jest następująca::

         `SuspendedInstanceManagement -Command:[CommandName] -Server:[ServerName] -Database:[DatabaseName] -InstanceId:[InstanceId]`

         Obsługiwane są następujące polecenia: `Query`, `Resume`, i `Terminate`.  Przełącznik InstanceId jest wymagany tylko dla `Resume` operacji i. `Terminate`

#### <a name="to-cleanup-optional"></a>Aby oczyścić (opcjonalnie)

1. Otwórz konsolę zarządzania komputerem, uruchamiając `vs2010` polecenie compmgmt. msc z poziomu wiersza polecenia.

2. Rozwiń węzeł **usługi i aplikacje**, kolejkowanie **komunikatów**, **kolejki prywatne**.

3. Usuń kolejkę **ReceiveTx** .

4. Aby usunąć bazę danych trwałości, uruchom polecenie Oczyść. cmd.

> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\SuspendedInstanceManagement`
