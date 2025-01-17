---
title: Omówienie programu Windows Workflow
ms.date: 03/30/2017
ms.assetid: fc44adbe-1412-49ae-81af-0298be44aae6
ms.openlocfilehash: 285ab75f7f67bbb9ffa18367eff126c04227f193
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2019
ms.locfileid: "65876139"
---
# <a name="windows-workflow-overview"></a>Omówienie programu Windows Workflow
Przepływ pracy jest zbiorem elemental jednostek nazywanych *działania* , są przechowywane jako obiekty modelu, który zawiera opis procesu rzeczywistych. Przepływy pracy, zapewniają sposób opisania kolejności wykonania i zależności między elementami krótkotrwałej pracy krótkim lub długim. Ta Praca przechodzi przez model od początku do końca, a działania może być wykonywane przez osoby lub funkcji systemu.  
  
## <a name="workflow-run-time-engine"></a>Aparat środowiska wykonawczego przepływów pracy  
 Każdego uruchomionego wystąpienia przepływu pracy jest tworzony i utrzymywane przez aparat środowiska wykonawczego w procesie, że proces hosta wchodzi w interakcję z za pomocą jednego z następujących czynności:  
  
- Element <xref:System.Activities.WorkflowInvoker>, który wywołuje przepływu pracy, takich jak metody.  
  
- Element <xref:System.Activities.WorkflowApplication> dla jawną kontrolę nad wykonywaniem wystąpienia jeden przepływ pracy.  
  
- A <xref:System.ServiceModel.WorkflowServiceHost> oparta na komunikatach interakcji w scenariuszach obejmujące wiele wystąpień.  
  
 Każda z tych klas opakowuje podstawowe środowisko wykonawcze działania, reprezentowane jako <xref:System.Activities.ActivityInstance> odpowiedzialny za wykonywanie działania. Może istnieć kilka <xref:System.Activities.ActivityInstance> obiektów w domenie aplikacji uruchomionych jednocześnie.  
  
 Każdy z poprzednich obiektów interakcji trzy hosta jest tworzony z drzewa działań określone jako program przepływu pracy. Za pomocą tych typów lub niestandardowego hosta, który otacza <xref:System.Activities.ActivityInstance>, przepływy pracy mogą być wykonywane w żaden proces Windows, łącznie z aplikacji konsoli, aplikacje oparte na formularzach, usług Windows, witryn sieci Web platformy ASP.NET i Windows Communication Foundation (WCF) usługi.  
  
 ![Składniki przepływu pracy w procesie hosta](./media/44c79d1d-178b-4487-87ed-3e33015a3842.gif "44c79d1d-178b-4487-87ed-3e33015a3842")  
Składniki przepływu pracy w procesie hosta  
  
## <a name="interaction-between-workflow-components"></a>Interakcje między składnikami przepływu pracy  
 Poniższy diagram przedstawia, jak składniki przepływu pracy współdziałają ze sobą.  
  
 ![Diagram przedstawiający sposób interakcji części przepływu pracy.](./media/overview/workflow-component-interatction.gif)  
  
 Na powyższym diagramie <xref:System.Activities.WorkflowInvoker.Invoke%2A> metody <xref:System.Activities.WorkflowInvoker> klasa jest używana do wywołania kilka wystąpień przepływu pracy. <xref:System.Activities.WorkflowInvoker> Służy do uproszczonego przepływów pracy, które nie ma potrzeby zarządzania z hosta przepływy pracy, wymagających zarządzania z hosta (takie jak <xref:System.Activities.Bookmark> wznowienie) musi zostać wykonana przy użyciu <xref:System.Activities.WorkflowApplication.Run%2A> zamiast tego. Nie jest wymagane oczekiwania dla jednego wystąpienia przepływu pracy do wykonania przed wywołaniem Aparat środowiska wykonawczego obsługuje jednoczesne uruchamianie wielu wystąpień przepływu pracy.  Przepływy pracy wywoływane są następujące:  
  
- A <xref:System.Activities.Statements.Sequence> działania, który zawiera <xref:System.Activities.Statements.WriteLine> działania podrzędnego. A <xref:System.Activities.Variable> elementu nadrzędnego działania jest powiązany z <xref:System.Activities.InArgument> działania podrzędnego. Aby uzyskać więcej informacji na temat zmiennych, argumentów i powiązania zobacz [zmienne i argumenty](variables-and-arguments.md).  
  
- Niestandardowe działanie o nazwie `ReadLine`. <xref:System.Activities.OutArgument> z `ReadLine` działania są zwracane do wywołania <xref:System.Activities.WorkflowInvoker.Invoke%2A> metody.  
  
- Niestandardowe działanie, która pochodzi od klasy <xref:System.Activities.CodeActivity> klasy abstrakcyjnej. <xref:System.Activities.CodeActivity> Mogą uzyskiwać dostęp do funkcji wykonawczej (takich jak śledzenie i właściwości) przy użyciu <xref:System.Activities.CodeActivityContext> który jest dostępny jako parametr <xref:System.Activities.CodeActivity.Execute%2A> metody. Aby uzyskać więcej informacji o tych funkcjach czasu wykonywania, zobacz [przepływu pracy i śledzenie](workflow-tracking-and-tracing.md) i [właściwości wykonania przepływu pracy](workflow-execution-properties.md).  
  
## <a name="see-also"></a>Zobacz także

- [BizTalk Server 2006 lub WF? Wybór narzędzia prawo przepływu pracy dla projektu](https://go.microsoft.com/fwlink/?LinkId=154901)
