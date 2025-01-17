---
title: Migracja i współdziałanie
ms.date: 03/30/2017
f1_keywords:
- AutoGeneratedOrientationPage
helpviewer_keywords:
- Windows Presentation Foundation [WPF], interoperability
- WPF [WPF], migration
- Windows Forms controls [WPF interoperability]
- controls [WPF interoperability]
- Windows Presentation Foundation [WPF], migration
- interoperability [WPF]
- WPF [WPF], interoperability
- migration [WPF]
ms.assetid: d655de05-bf63-4814-bc64-6b3be01c70a2
ms.openlocfilehash: fcb7ece1081ae0858148cef883429b205478689b
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040889"
---
# <a name="migration-and-interoperability"></a>Migracja i współdziałanie
Ta strona zawiera linki do dokumentów, w których omówiono sposób implementacji współdziałania między aplikacjami [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] i innymi typami aplikacji systemu Microsoft Windows.  
  
## <a name="in-this-section"></a>W tej sekcji  
 [Współdziałanie WPF i Windows Forms](wpf-and-windows-forms-interoperation.md)  
 [WPF i Win32 — współdziałanie](wpf-and-win32-interoperation.md)  
 [WPF i Direct3D9 — współdziałanie](wpf-and-direct3d9-interoperation.md)  
  
## <a name="reference"></a>Tematy pomocy  
  
|Termin|Definicja|  
|----------|----------------|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|Element, którego można użyć do hostowania formantu [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] jako elementu strony [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]owej.|  
|<xref:System.Windows.Forms.Integration.ElementHost>|Kontrolka [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], której można użyć do hostowania [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] kontroli.|  
|<xref:System.Windows.Interop.HwndSource>|Hostuje region [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] w aplikacji [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].|  
|<xref:System.Windows.Interop.HwndHost>|Klasa bazowa dla <xref:System.Windows.Forms.Integration.WindowsFormsHost>definiuje niektóre podstawowe funkcje, które są używane przez wszystkie technologie oparte na HWND, gdy są hostowane przez aplikację [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Podklasa ta umożliwia hostowanie okna [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] w aplikacji [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|  
|<xref:System.Windows.Interop.BrowserInteropHelper>|Klasa pomocnika służąca do raportowania warunków środowiska przeglądarki dla [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacji hostowanej w przeglądarce.|  
  
## <a name="related-sections"></a>Sekcje pokrewne
