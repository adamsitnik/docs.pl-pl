---
title: 'Łagodzenie: niestandardowe implementacje IMessageFilter. PreFilterMessage'
ms.date: 03/30/2017
ms.assetid: 9cf47c5b-0bb2-45df-9437-61cd7e7c2f4d
ms.openlocfilehash: 7757e8d1fd0258ab2d972b7321082e4afa37f710
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73457943"
---
# <a name="mitigation-custom-imessagefilterprefiltermessage-implementations"></a>Łagodzenie: niestandardowe implementacje IMessageFilter. PreFilterMessage

W Windows Forms aplikacje, które są przeznaczone dla wersji .NET Framework zaczynających się od .NET Framework 4.6.1, niestandardowa implementacja <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> może bezpiecznie filtrować komunikaty, gdy metoda <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> jest wywoływana, jeśli <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> implementacja:

- Wykonuje jedną lub obie następujące czynności:

  - Dodaje filtr komunikatów przez wywołanie metody <xref:System.Windows.Forms.Application.AddMessageFilter%2A>.

  - Usuwa filtr komunikatów przez wywołanie metody <xref:System.Windows.Forms.Application.RemoveMessageFilter%2A>. Method.

- **I** pompy komunikatów przez wywołanie metody <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=nameWithType>.

## <a name="impact"></a>Wpływ

Ta zmiana ma wpływ tylko na Windows Forms aplikacje, które są przeznaczone dla wersji .NET Framework, począwszy od .NET Framework 4.6.1.

W przypadku aplikacji Windows Forms przeznaczonych dla poprzednich wersji .NET Framework takie implementacje w niektórych przypadkach zgłaszają wyjątek <xref:System.IndexOutOfRangeException>, gdy wywoływana jest metoda <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType>

## <a name="mitigation"></a>Ograniczenie

Jeśli ta zmiana jest niepożądana, aplikacje przeznaczone dla .NET Framework 4.6.1 lub nowszej wersji mogą zrezygnować z niego, dodając następujące ustawienia konfiguracji\<do sekcji [> środowiska uruchomieniowego](../configure-apps/file-schema/runtime/runtime-element.md) w pliku konfiguracyjnym aplikacji:

```xml
<runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Forms.DontSupportReentrantFilterMessage=true" />
</runtime>
```

Ponadto aplikacje, które są przeznaczone dla poprzednich wersji .NET Framework ale działają w .NET Framework 4.6.1 lub nowszej wersji, mogą zrezygnować z tego zachowania, dodając następujące ustawienia konfiguracji do sekcji [> runtime\<](../configure-apps/file-schema/runtime/runtime-element.md) plik konfiguracji aplikacji:

```xml
<runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Forms.DontSupportReentrantFilterMessage=false" />
</runtime>
```

## <a name="see-also"></a>Zobacz także

- [Zgodność aplikacji](application-compatibility.md)
