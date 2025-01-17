---
title: 'Instrukcje: Tworzenie usługi przepływu pracy przy użyciu działań dotyczących komunikatów'
ms.date: 03/30/2017
ms.assetid: 53d094e2-6901-4aa1-88b8-024b27ccf78b
ms.openlocfilehash: f5bb8df5936be1890bf744300daa7ccb68e341e3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787847"
---
# <a name="how-to-create-a-workflow-service-with-messaging-activities"></a>Instrukcje: Tworzenie usługi przepływu pracy przy użyciu działań dotyczących komunikatów
W tym temacie opisano sposób tworzenia prostego przepływu pracy usługi przy użyciu działań dotyczących komunikatów. Ten temat koncentruje się na mechanika Tworzenie usługi przepływu pracy, gdy usługa składa się wyłącznie z działań dotyczących komunikatów. W usłudze rzeczywistych przepływ pracy zawiera wiele innych działań. Usługa implementuje jedną operację o nazwie Echo, która przyjmuje ciąg i zwraca ciąg do obiektu wywołującego. W tym temacie jest pierwszy w serii dwa tematy. Następny temat [How to: Dostęp do usługi z przepływu pracy aplikacji](../../../../docs/framework/wcf/feature-details/how-to-access-a-service-from-a-workflow-application.md) w tym artykule omówiono sposób tworzenia aplikacji przepływu pracy, który można wywołać usługi utworzonej w tym temacie.  
  
### <a name="to-create-a-workflow-service-project"></a>Aby utworzyć projekt usługi przepływu pracy  
  
1. Start Visual Studio 2012.  
  
2. Kliknij przycisk **pliku** menu, wybierz opcję **New**, a następnie **projektu** do wyświetlenia **okna dialogowego Nowy projekt**. Wybierz **przepływu pracy** na liście zainstalowanych szablonów i **aplikacja usługi przepływu pracy WCF** z listy typów projektów. Nadaj projektowi nazwę `MyWFService` i użyj domyślnej lokalizacji, jak pokazano na poniższej ilustracji.  
  
     Kliknij przycisk **OK** przycisk, aby odrzucić **okna dialogowego Nowy projekt**.  
  
3. Podczas tworzenia projektu plik Service1.xamlx jest otwarty w projektancie, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu przedstawia Otwórz plik Service1.xamlx w projektancie.](./media/how-to-create-a-workflow-service-with-messaging-activities/default-workflow-service.jpg)  
  
     Kliknij prawym przyciskiem myszy działanie etykietą **usługa Sekwencyjna** i wybierz **Usuń**.  
  
### <a name="to-implement-the-workflow-service"></a>Aby zaimplementować usługi przepływu pracy  
  
1. Wybierz **przybornika** karty po lewej stronie ekranu, aby wyświetlić Przybornika, a następnie kliknij przycisk pinezki, aby nie zamykaj okna. Rozwiń **komunikatów** sekcji przybornika, aby wyświetlić działań dotyczących komunikatów i komunikatów Szablony działań, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący przybornika z sekcją komunikatów rozwinięte.](./media/how-to-create-a-workflow-service-with-messaging-activities/toolbox-messaging-section.jpg)  
  
2. Przeciąganie i upuszczanie **ReceiveAndSendReply** szablon do projektanta przepływów pracy. Spowoduje to utworzenie <xref:System.Activities.Statements.Sequence> działanie przy użyciu **Receive** następuje działanie <xref:System.ServiceModel.Activities.SendReply> działania, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący szablonu ReceiveAndSendReply.](./media/how-to-create-a-workflow-service-with-messaging-activities/receiveandsendreply-template.jpg)  
  
     Należy zauważyć, że <xref:System.ServiceModel.Activities.SendReply> działania <xref:System.ServiceModel.Activities.SendReply.Request%2A> właściwość jest ustawiona na `Receive`, nazwa <xref:System.ServiceModel.Activities.Receive> działań, do którego <xref:System.ServiceModel.Activities.SendReply> działania się odwołują.  
  
3. W <xref:System.ServiceModel.Activities.Receive> typ działania `Echo` w polu tekstowym etykietą **OperationName**. Definiuje nazwy operacji usługi implementuje.  
  
     ![Zrzut ekranu pokazujący, gdzie można określić nazwy operacji.](./media/how-to-create-a-workflow-service-with-messaging-activities/define-operation-name.jpg)  
  
4. Za pomocą <xref:System.ServiceModel.Activities.Receive> działania zaznaczone, Otwórz okno właściwości w przeciwnym razie już otworzyć, klikając przycisk **widoku** menu i wybierając polecenie **okno właściwości**. W **okno właściwości** przewiń w dół, aż zobaczysz **CanCreateInstance** i zaznacz pole wyboru, jak pokazano na poniższej ilustracji. To ustawienie włącza hosta usługi przepływu pracy utworzyć nowe wystąpienie usługi (jeśli jest to konieczne), gdy wiadomość zostaje odebrana.  
  
     ![Zrzut ekranu pokazujący właściwość CanCreateInstance.](./media/how-to-create-a-workflow-service-with-messaging-activities/cancreateinstance-property.jpg)  
  
5. Wybierz <xref:System.Activities.Statements.Sequence> działania i kliknij przycisk **zmienne** przycisku w lewym dolnym rogu projektanta. Spowoduje to wyświetlenie edytora zmiennych. Kliknij przycisk **utworzyć zmienną** łącze, aby dodać zmienną do przechowywania ciągu wysyłany do operacji. Nazwa zmiennej `msg` i ustaw jego **zmiennej** typu ciąg, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący sposób dodawania zmiennej.](./media/how-to-create-a-workflow-service-with-messaging-activities/add-variable-msg-string.jpg)  
  
     Kliknij przycisk **zmienne** przycisk ponownie, aby zamknąć Edytor zmiennych.  
  
6. Kliknij przycisk **zdefiniować...** łącze w **zawartości** polu tekstowym <xref:System.ServiceModel.Activities.Receive> działanie, aby wyświetlić **definicji zawartości** okna dialogowego. Wybierz **parametry** przycisk radiowy, kliknij przycisk **dodano nowy parametr** napisz `inMsg` w **nazwa** pola tekstowego, wybierz opcję **ciągu**w **typu** listę rozwijaną pola listy, a typ `msg` w **przypisać do** pola tekstowego, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący, dodając parametry zawartości.](./media/how-to-create-a-workflow-service-with-messaging-activities/adding-parameters-content.jpg)  
  
     Określa, że działania odbierania odbiera parametr ciągu i powiązania danych z `msg` zmiennej. Kliknij przycisk **OK** zamknąć **definicji zawartości** okna dialogowego.  
  
7. Kliknij przycisk **zdefiniować...**  łącze w **zawartości** pole w <xref:System.ServiceModel.Activities.SendReply> działanie, aby wyświetlić **definicji zawartości** okna dialogowego. Wybierz **parametry** przycisk radiowy, kliknij przycisk **dodano nowy parametr** napisz `outMsg` w **nazwa** pola tekstowego, wybierz opcję **ciągu**w **typu** lista rozwijana i `msg` w **wartość** pola tekstowego, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący sposób dodać parametr outMsg.](./media/how-to-create-a-workflow-service-with-messaging-activities/outmsg-parameters-content.jpg)  
  
     Określa, że <xref:System.ServiceModel.Activities.SendReply> działanie wysyła wiadomości lub typ kontraktu komunikatu, a tych danych jest powiązany z `msg` zmiennej. Ponieważ jest to <xref:System.ServiceModel.Activities.SendReply> działania, to oznacza, że dane w `msg` używany do wypełnienia wiadomości działania wysyła z powrotem do klienta. Kliknij przycisk **OK** zamknąć **definicji zawartości** okna dialogowego.  
  
8. Zapisz i Kompiluj rozwiązanie, klikając **kompilacji** menu i wybierając polecenie **Kompiluj rozwiązanie**.  
  
## <a name="configure-the-workflow-service-project"></a>Konfigurowanie projektu usługi przepływu pracy  
 Usługa przepływu pracy zostało ukończone. W tej sekcji opisano sposób konfigurowania rozwiązania usługi przepływu pracy, aby ułatwić hostować i uruchamiać. To rozwiązanie używa ASP.NET Development Server do hostowania usługi.  
  
#### <a name="to-set-project-start-up-options"></a>Aby ustawić opcje uruchamiania projektu  
  
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **MyWFService** i wybierz **właściwości** do wyświetlenia **właściwości projektu** okna dialogowego.  
  
2. Wybierz **Web** kartę, a następnie wybierz pozycję **konkretnej strony** w obszarze **Akcja uruchamiania** i typ `Service1.xamlx` w polu tekstowym, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący okno dialogowe właściwości projektu.](./media/how-to-create-a-workflow-service-with-messaging-activities/project-properties-dialog.jpg)  
  
     Ta usługa hostuje usługi zdefiniowane w Service1.xamlx w ASP.NET Development Server.  
  
3. Naciśnij klawisze Ctrl + F5, aby uruchomić usługę. Ikona ASP.NET Development Server jest wyświetlana w prawym dolnym pulpitu, jak pokazano na poniższej ilustracji.  
  
     ![Zrzut ekranu pokazujący ikona Server dla deweloperów platformy ASP.NET.](./media/how-to-create-a-workflow-service-with-messaging-activities/asp-net-dev-server-icon.jpg)  
  
     Ponadto program Internet Explorer wyświetla stronę pomocy usługi WCF dla usługi.  
  
     ![Zrzut ekranu przedstawiający stronę pomocy usługi WCF.](./media/how-to-create-a-workflow-service-with-messaging-activities/wcf-service-help-page.jpg)  
  
4. Przejdź do [jak: Dostęp do usługi z przepływu pracy aplikacji](../../../../docs/framework/wcf/feature-details/how-to-access-a-service-from-a-workflow-application.md) temacie, aby utworzyć klienta przepływu pracy, który wywołuje tę usługę.  
  
## <a name="see-also"></a>Zobacz także

- [Usługi przepływu pracy](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [Przegląd hostowania usług przepływu pracy](../../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md)
- [Działania dotyczące komunikatów](../../../../docs/framework/wcf/feature-details/messaging-activities.md)
