---
title: Ograniczenia właściwości Interval składnika Timer formularzy systemu Windows
ms.date: 03/30/2017
helpviewer_keywords:
- timers [Windows Forms], event intervals
- Interval property [Windows Forms], limitations
- timers [Windows Forms], Windows-based
- Timer component [Windows Forms], limitations of Interval property
ms.assetid: 7e5fb513-77e7-4046-a8e8-aab94e61ca0f
ms.openlocfilehash: a9c4fda179e45ad2cf2ee2183e5881e97b763cdc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2019
ms.locfileid: "64644932"
---
# <a name="limitations-of-the-windows-forms-timer-components-interval-property"></a>Ograniczenia właściwości Interval składnika Timer formularzy systemu Windows
Formularze Windows <xref:System.Windows.Forms.Timer> składnik ma <xref:System.Windows.Forms.Timer.Interval%2A> właściwość, która określa liczbę milisekund, które przechodzą między zdarzenie czasomierza jeden, a następnie. Jeśli składnik jest wyłączony, czasomierz w dalszym ciągu otrzymywać <xref:System.Windows.Forms.Timer.Tick> zdarzeń w przybliżeniu jednakowej odstępach czasu.  
  
 Ten składnik jest przeznaczony dla środowiska Windows Forms. Jeśli potrzebujesz czasomierza, która jest odpowiednia w środowisku serwera, zobacz [wprowadzenie do serwerowych czasomierzy](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90)).  
  
## <a name="the-interval-property"></a>Właściwości interwału  
 <xref:System.Windows.Forms.Timer.Interval%2A> Właściwość ma pewne ograniczenia, które należy wziąć pod uwagę podczas programowania <xref:System.Windows.Forms.Timer> składników:  
  
- Jeśli aplikacja lub innej aplikacji wysokimi wymaganiami w systemie — takiej jak długo pętli, intensywnie korzystających z obliczeń, dysków, sieci lub dostępu do portu — aplikacja nie może pobrać zdarzenia czasomierza, tak często, jak <xref:System.Windows.Forms.Timer.Interval%2A> określa właściwości.  
  
- Interwał nie musi upłynąć dokładnie na czas. W celu zapewnienia dokładności, czasomierz powinien sprawdzanie zegara systemowego zgodnie z potrzebami, a nie spróbuj śledzić czas skumulowana wewnętrznie.  
  
- Dokładność <xref:System.Windows.Forms.Timer.Interval%2A> właściwość jest podana w milisekundach. Niektóre komputery udostępniają licznika o wysokiej rozdzielczości o rozdzielczości wyższej niż milisekund. Dostępność tych liczników jest zależna od sprzętu procesora komputera.
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Forms.Timer>
- [Timer, składnik](timer-component-windows-forms.md)
- [Timer, składnik — omówienie](timer-component-overview-windows-forms.md)
