---
ms.openlocfilehash: 297af393e86c65e84ea7271d98eab36dbc6dbb0e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "62091709"
---
### <a name="some-workflow-drag-and-drop-apis-are-obsolete"></a>Niektóre interfejsy API przeciągnij i upuść przepływu pracy są nieaktualne

|   |   |
|---|---|
|Szczegóły|Ten interfejs API przeciągnij i upuść przepływu pracy jest przestarzały i spowoduje ostrzeżenia kompilatora, jeśli aplikacja zostanie ponownie skompilowany przed 4.5.|
|Sugestia|Nowe <xref:System.Activities.Presentation.DragDropHelper?displayProperty=name> interfejsów API, które obsługują operacje z wieloma obiektami, które powinny być używane zamiast tego. Alternatywnie można pominąć ostrzeżenia kompilacji lub można uniknąć za pomocą starszego kompilatora. Interfejsy API są nadal obsługiwane.|
|Zakres|Mały|
|Wersja|4.5|
|Typ|Przekierowanie|
|Dotyczy interfejsów API|<ul><li><xref:System.Activities.Presentation.DragDropHelper.DoDragMove(System.Activities.Presentation.WorkflowViewElement,System.Windows.Point)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetCompositeView(System.Windows.DragEventArgs)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetDraggedModelItem(System.Windows.DragEventArgs)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetDroppedObject(System.Windows.DependencyObject,System.Windows.DragEventArgs,System.Activities.Presentation.EditingContext)?displayProperty=nameWithType></li></ul>|
