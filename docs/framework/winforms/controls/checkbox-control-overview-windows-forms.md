---
title: CheckBox — Informacje o formancie [Formularze systemu Windows]
ms.date: 03/30/2017
f1_keywords:
- CheckBox
helpviewer_keywords:
- CheckBox control [Windows Forms], about CheckBox control
- data binding [Windows Forms], checkbox controls
- check boxes [Windows Forms], about check boxes
ms.assetid: 085a4e0b-9046-473f-b141-d0edddfb2ebb
ms.openlocfilehash: 2a18327d9836d1dbbcd5d5d6e73f217637736d20
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938973"
---
# <a name="checkbox-control-overview-windows-forms"></a>CheckBox — Informacje o formancie [Formularze systemu Windows]
Formularze Windows <xref:System.Windows.Forms.CheckBox> formant wskazuje, czy określony warunek jest włączone czy wyłączone. Często są one wykorzystywane do przedstawienia tak/nie lub zaznaczenie PRAWDA/FAŁSZ dla użytkownika. Formanty pól wyboru w grupach umożliwia wyświetlanie wielu opcji, z których użytkownik może wybrać co najmniej jeden.  
  
 Kontrolka pola wyboru jest podobny do kontrolki przycisku radiowego, w tym, że każdy obiekt jest używany do wskazania wybranej przez użytkownika. Różnią się one w tym można wybrać przycisk radiowy tylko jednej grupy naraz. Za pomocą kontrolki pola wyboru jednak dowolną liczbę pól wyboru można wybrać.  
  
 Pole wyboru mogą być połączone z elementami w bazie danych za pomocą proste powiązanie danych. Wiele pól wyboru może być zgrupowane za pomocą <xref:System.Windows.Forms.GroupBox> kontroli. Jest to przydatne dla wygląd, a także projektu interfejsu użytkownika, ponieważ kontrolki zgrupowane mogą być przenoszone między ze sobą w Projektancie formularza. Aby uzyskać więcej informacji, zobacz [powiązanie danych formularzy Windows](../windows-forms-data-binding.md) i [GroupBox, kontrolka](groupbox-control-windows-forms.md).  
  
 <xref:System.Windows.Forms.CheckBox> Kontroli ma dwie właściwości ważne <xref:System.Windows.Forms.CheckBox.Checked%2A> i <xref:System.Windows.Forms.CheckBox.CheckState%2A>. <xref:System.Windows.Forms.CheckBox.Checked%2A> Właściwość zwraca albo `true` lub `false`. <xref:System.Windows.Forms.CheckBox.CheckState%2A> Właściwość zwraca albo <xref:System.Windows.Forms.CheckState.Checked> lub <xref:System.Windows.Forms.CheckState.Unchecked>; lub, jeśli <xref:System.Windows.Forms.CheckBox.ThreeState%2A> właściwość jest ustawiona na `true`, <xref:System.Windows.Forms.CheckBox.CheckState%2A> może również zwracać <xref:System.Windows.Forms.CheckState.Indeterminate>. Stan nieokreślony pojawia się okno dialogowe z wygaszone wygląd, aby wskazać, że ta opcja jest niedostępna.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.CheckBox>
- [Instrukcje: Ustawianie opcji za pomocą formantów CheckBox formularzy Windows](how-to-set-options-with-windows-forms-checkbox-controls.md)
- [Instrukcje: Odpowiadanie do formularzy Windows Forms kliknięcia kontrolki CheckBox](how-to-respond-to-windows-forms-checkbox-clicks.md)
- [CheckBox, kontrolka](checkbox-control-windows-forms.md)
