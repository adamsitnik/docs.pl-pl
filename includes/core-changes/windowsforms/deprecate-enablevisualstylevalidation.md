---
ms.openlocfilehash: 84b6bfc32f5a73597b227098e5aee1e3450cf85b
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73198520"
---
### <a name="switchsystemwindowsformsenablevisualstylevalidation-compatibility-switch-not-supported"></a>Przełącznik. System. Windows. Forms. EnableVisualStyleValidation nie jest obsługiwany.

Przełącznik zgodności `Switch.System.Windows.Forms.EnableVisualStyleValidation` nie jest obsługiwany w Windows Forms na platformie .NET Core 3,0.

#### <a name="change-description"></a>Zmień opis

W .NET Framework przełącznik zgodności `Switch.System.Windows.Forms.EnableVisualStyleValidation` zezwolił aplikacji na rezygnację z walidacji stylów wizualnych dostarczonych w postaci liczbowej.

W programie .NET Core przełącznik `Switch.System.Windows.Forms.EnableVisualStyleValidation` nie jest obsługiwany.

#### <a name="version-introduced"></a>Wprowadzona wersja

3,0 wersja zapoznawcza 9

#### <a name="recommended-action"></a>Zalecana akcja

Usuń przełącznik. Przełącznik nie jest obsługiwany i żadna alternatywna funkcja nie jest dostępna.

#### <a name="category"></a>Kategoria

Windows Forms

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- Brak

<!-- 

### Affected APIs

- Not detectable via API analysis

-->
