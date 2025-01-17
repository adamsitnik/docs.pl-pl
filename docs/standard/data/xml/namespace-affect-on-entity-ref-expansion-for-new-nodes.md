---
title: Wpływ przestrzeni nazw na rozwijanie odwołań do jednostek w przypadku nowych węzłów zawierających elementy i atrybuty
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 64359aee-aab0-4042-9a32-d19789af6ca7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1a92f1b08719c926e6384c220e3695de26dbb4fd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967327"
---
# <a name="namespace-affect-on-entity-reference-expansion-for-new-nodes-containing-elements-and-attributes"></a>Wpływ przestrzeni nazw na rozwijanie odwołań do jednostek w przypadku nowych węzłów zawierających elementy i atrybuty
Ponieważ zawartość deklaracji jednostki może zawierać niemal wszystko, istnieje możliwość, że zawartość może zawierać element, taki jak `<!ENTITY aname "<elem>test</elem>">`.  
  
 Gdy plik XML jest analizowany, `&aname;` nie jest rozwinięty wraz z jego zawartością zastępczą podczas analizowania. Rozszerzanie kodu XML nie jest wykonywane, ponieważ rozpoznawanie przestrzeni nazw dla elementu nie może wystąpić, dopóki węzeł nie zostanie umieszczony w dokumencie. Do tego czasu nie ma informacji o tym, co przestrzeń nazw znajduje się w zakresie. Gdy węzeł zostanie umieszczony w dokumencie, pojawia się rozpoznawanie przestrzeni nazw, a uzyskana zawartość jednostki jest analizowana do odpowiednich węzłów.  
  
> [!NOTE]
> Gdy rozszerzenie zostanie wykonane w nowo utworzonym węźle odwołania do jednostki, nigdy nie wystąpi ponownie. W związku z tym przestrzenie nazw używane w zamiannym tekście dla elementu są powiązane w chwili, gdy węzeł nadrzędny jest ustawiony. Można jednak zmienić przestrzeń nazw dla istniejących węzłów odwołań do jednostki, gdy usuniesz i wstawię je w innym miejscu lub w węzłach odwołania do jednostki, które są sklonowane przy użyciu metody **CloneNode** .  
  
## <a name="see-also"></a>Zobacz także

- [Model DOM (XML Document Object Model)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
