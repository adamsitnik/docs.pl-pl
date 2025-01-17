---
ms.openlocfilehash: 3d0a90a57c2b1c2759b8420e74c284668d54e9cb
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72526765"
---
### <a name="duplicated-apis-removed-from-windows-forms"></a>Zduplikowane interfejsy API zostały usunięte z Windows Forms

Niektóre interfejsy API przypadkowo zduplikowane w przestrzeni nazw <xref:System.Windows.Forms?displayProperty=fullName>, zaczynające się na platformie .NET Core 3,0 Preview 4, zostały usunięte w programie .NET Core 3,0 RC1.

#### <a name="change-description"></a>Zmień opis

Program .NET Core 3,0 w wersji zapoznawczej 4 przypadkowo duplikuje kilka typów w przestrzeni nazw <xref:System.Windows.Forms?displayProperty=fullName>, które już istniały w przestrzeni nazw <xref:System.ComponentModel.Design?displayProperty=fullName>. Począwszy od platformy .NET Core 3,0 RC1, te zduplikowane typy nie są już dostępne. Poniższa tabela zawiera listę typów pierwotnych i duplikatów typów:

|Typ oryginalny|Zduplikowany typ|
|---|---|
|<xref:System.ComponentModel.Design.DesignerActionListsChangedEventArgs?displayProperty=fullName>|`System.Windows.Forms.DesignerActionListsChangedEventArgs`|
|<xref:System.ComponentModel.Design.DesignerActionListsChangedEventHandler?displayProperty=fullName>|`System.Windows.Forms.DesignerActionListsChangedEventHandler`|
|<xref:System.ComponentModel.Design.DesignerActionListsChangedType?displayProperty=fullName>|`System.Windows.Forms.DesignerActionListsChangedType`|
|<xref:System.ComponentModel.Design.DesignerActionUIService?displayProperty=fullName>|`System.Windows.Forms.DesignerActionUIService`|
|<xref:System.ComponentModel.Design.DesignerCommandSet?displayProperty=fullName>|`System.Windows.Forms.DesignerCommandSet`|

#### <a name="version-introduced"></a>Wprowadzona wersja

3,0 RC1

#### <a name="recommended-action"></a>Zalecana akcja

Zaktualizuj kod, aby odwołać się do oryginalnego typu, jak pokazano w kolumnie **pierwotnego typu** tabeli.

#### <a name="category"></a>Kategoria

Windows Forms

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- Nie wykrywalne za pośrednictwem analizy interfejsu API.

<!--

### Affected APIs

- Not detectable via API analysis.

-->
