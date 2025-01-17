---
title: Poziomy zmiany grafiki
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], performance
- rendering graphics [WPF]
- rendering tiers [WPF]
- graphics rendering tiers [WPF]
- graphics [WPF], rendering tiers
ms.assetid: 08dd1606-02a2-4122-9351-c0afd2ec3a70
ms.openlocfilehash: 9da519f8d258673498f45a425c13863437cac597
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69937518"
---
# <a name="graphics-rendering-tiers"></a>Poziomy zmiany grafiki
Warstwa renderowania definiuje poziom graficznej możliwości sprzętowej i wydajności dla urządzenia, na którym działa [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacja.  

<a name="graphics_hardware"></a>   
## <a name="graphics-hardware"></a>Sprzęt graficzny  
 Funkcje sprzętu grafiki, które mają największy wpływ na poziomy warstwy renderowania są następujące:  
  
- **Pamięć RAM wideo** Ilość pamięci wideo na sprzęcie graficznym określa rozmiar i liczbę buforów, które mogą być używane do składania grafiki.  
  
- Program do **cieniowania pikseli** Program do cieniowania pikseli jest funkcją przetwarzania grafiki, która oblicza wpływ na piksele. W zależności od rozdzielczości wyświetlanej grafiki może istnieć kilka milionów pikseli, które muszą zostać przetworzone dla każdej ramki wyświetlanej.  
  
- Program do cieniowania wierzchołków Program do cieniowania wierzchołków jest funkcją przetwarzania grafiki, która wykonuje operacje matematyczne na danych wierzchołka obiektu.  
  
- **Obsługa** wieloteksturowa Obsługa wieloteksturowego odnosi się do możliwości zastosowania dwóch lub większej liczby odrębnych tekstur podczas operacji mieszania na obiekcie graficznym 3W. Stopień wsparcia wieloteksturowego zależy od liczby jednostek wieloteksturowych na sprzęcie graficznym.  
  
<a name="rendering_tier_definitions"></a>   
## <a name="rendering-tier-definitions"></a>Definicje warstwy renderowania  
 Funkcje sprzętu graficznego określają możliwości [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] renderowania aplikacji. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] System definiuje trzy warstwy renderowania:  
  
- **Warstwa renderowania 0** Brak przyspieszania sprzętowego. Wszystkie funkcje grafiki wykorzystują przyspieszenie oprogramowania. Poziom wersji programu DirectX jest mniejszy niż wersja 9,0.  
  
- **Warstwa renderowania 1** Niektóre funkcje grafiki wykorzystują przyspieszenie sprzętowe grafiki. Poziom wersji programu DirectX jest większy lub równy wersji 9,0.  
  
- **Renderowanie warstwy 2** Większość funkcji graficznych wykorzystuje przyspieszenie sprzętowe grafiki. Poziom wersji programu DirectX jest większy lub równy wersji 9,0.  
  
 <xref:System.Windows.Media.RenderCapability.Tier%2A?displayProperty=nameWithType> Właściwość pozwala na pobranie warstwy renderowania w czasie wykonywania aplikacji. Warstwa renderowania służy do określenia, czy urządzenie obsługuje pewne funkcje grafiki, które przyspieszają sprzętowo. Aplikacja może następnie zastosować różne ścieżki kodu w czasie wykonywania w zależności od warstwy renderowania obsługiwanej przez urządzenie.  
  
### <a name="rendering-tier-0"></a>Warstwa renderowania 0  
 Wartość warstwy renderowania równa 0 oznacza, że dla aplikacji na urządzeniu nie ma dostępnego przyspieszania sprzętowego. Na tym poziomie warstwy należy założyć, że wszystkie grafiki będą renderowane przez oprogramowanie bez przyspieszania sprzętowego. Funkcja tej warstwy odpowiada wersji programu DirectX, która jest mniejsza niż 9,0.  
  
### <a name="rendering-tier-1-and-rendering-tier-2"></a>Renderowanie warstwy 1 i warstwy renderowania 2  
  
> [!NOTE]
> Począwszy od .NET Framework 4, warstwa renderowania 1 została ponownie zdefiniowana w taki sposób, aby obejmowała tylko sprzęt graficzny obsługujący program DirectX 9,0 lub nowszy. Sprzęt graficzny obsługujący program DirectX 7 lub 8 jest teraz zdefiniowany jako warstwa renderowania 0.  
  
 Wartość warstwy renderowania 1 lub 2 oznacza, że większość funkcji graficznych programu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] będzie używać przyspieszania sprzętowego, jeśli wymagane zasoby systemowe są dostępne i nie zostały wyczerpane. Odnosi się to do wersji DirectX, która jest większa lub równa 9,0.  
  
 W poniższej tabeli przedstawiono różnice w wymaganiach sprzętowych dotyczących renderowania warstwy 1 i warstwy renderowania 2:  
  
|Funkcja|Warstwa 1|Warstwa 2|  
|-------------|------------|------------|  
|Wersja programu DirectX|Musi być większe lub równe 9,0.|Musi być większe lub równe 9,0.|  
|Pamięć RAM wideo|Musi być większa lub równa 60MB.|Musi być większa lub równa 120MB.|  
|Program do cieniowania pikseli|Poziom wersji musi być większy lub równy 2,0.|Poziom wersji musi być większy lub równy 2,0.|  
|Program do cieniowania wierzchołków|Brak wymagań.|Poziom wersji musi być większy lub równy 2,0.|  
|Jednostki wieloteksturowe|Brak wymagań.|Liczba jednostek musi być większa lub równa 4.|  
  
 Następujące funkcje i możliwości są przyspieszane sprzętowo w celu renderowania warstwy 1 i warstwy renderowania 2:  
  
|Funkcja|Uwagi|  
|-------------|-----------|  
|Renderowanie 2D|Większość renderowania 2D jest obsługiwana.|  
|Rasteryzacja 3W|Większość rasteryzacji 3W jest obsługiwana.|  
|Filtrowanie anizotropowego 3W|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]próbuje użyć filtrowania anizotropowego podczas renderowania zawartości 3W. Filtrowanie anizotropowego odnosi się do zwiększenia jakości obrazu tekstury na powierzchniach, które są daleko i intensywnie pochylone w odniesieniu do aparatu.|  
|mapowanie MCI 3W|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]próbuje użyć mapowania MIP podczas renderowania zawartości 3W. Mapowanie MIP podnosi jakość renderowania tekstury, gdy tekstura zajmuje mniejsze pole widzenia w <xref:System.Windows.Controls.Viewport3D>.|  
|Gradienty promieniowe|Chociaż są obsługiwane, Unikaj stosowania <xref:System.Windows.Media.RadialGradientBrush> w dużych obiektach.|  
|obliczenia oświetlenia 3W|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]wykonuje oświetlenie według wierzchołków, co oznacza, że w każdym wierzchołku dla każdego materiału zastosowanego do siatki należy obliczyć intensywność światła.|  
|Renderowanie tekstu|Renderowanie czcionki podrzędnej pikseli używa dostępnych programów do cieniowania pikseli na sprzęcie graficznym.|  
  
 Następujące funkcje i możliwości są przyspieszane sprzętowo tylko dla warstwy renderowania 2:  
  
|Funkcja|Uwagi|  
|-------------|-----------|  
|Antyaliasowanie 3W|Antyaliasowanie 3W jest obsługiwane tylko w systemach operacyjnych, które obsługują model wyświetlania sterowników systemu Windows (WDDM), takie [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] jak [!INCLUDE[win7](../../../../includes/win7-md.md)]i.|  
  
 Następujące funkcje i możliwości **nie** są przyspieszane sprzętowo:  
  
|Funkcja|Uwagi|  
|-------------|-----------|  
|Wydrukowana zawartość|Cała wydrukowana zawartość jest renderowana [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] przy użyciu potoku oprogramowania.|  
|Zrasteryzowany zawartość, która używa<xref:System.Windows.Media.Imaging.RenderTargetBitmap>|Każda zawartość renderowana przy użyciu <xref:System.Windows.Media.Imaging.RenderTargetBitmap.Render%2A> <xref:System.Windows.Media.Imaging.RenderTargetBitmap>metody.|  
|Rozmieszczanie zawartości z użyciem<xref:System.Windows.Media.TileBrush>|Dowolna zawartość z <xref:System.Windows.Media.TileBrush.TileMode%2A> <xref:System.Windows.Media.TileBrush> rozdziałami, w której właściwość jest <xref:System.Windows.Media.TileMode.Tile>ustawiona na.|  
|Powierzchnie, które przekraczają maksymalny rozmiar tekstury sprzętu graficznego|W przypadku większości sprzętu graficznego duże powierzchnie są 2048x2048 lub 4096x4096 pikseli.|  
|Każda operacja, której wymagania dotyczące pamięci RAM wideo przekracza pamięć sprzętową urządzenia graficznego|Można monitorować użycie pamięci RAM wideo aplikacji przy użyciu narzędzia perforacja, które jest zawarte w [pakiecie wydajności WPF](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa969767(v=vs.100)) w Windows SDK.|  
|Okna z warstwami|Warstwowe okna umożliwiają [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacjom renderowanie zawartości na ekranie w nieprostokątnym oknie. W systemach operacyjnych obsługujących system Windows Display Driver Model (WDDM), takich [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] jak [!INCLUDE[win7](../../../../includes/win7-md.md)]i, okna z warstwami są przyspieszane sprzętowo. W innych systemach, takich jak [!INCLUDE[winxp](../../../../includes/winxp-md.md)], okna z warstwami są renderowane przez oprogramowanie bez przyspieszania sprzętowego.<br /><br /> Okna z warstwami można włączyć w [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] programie, ustawiając następujące <xref:System.Windows.Window> właściwości:<br /><br /> -   <xref:System.Windows.Window.WindowStyle%2A> = <xref:System.Windows.WindowStyle.None><br />-   <xref:System.Windows.Window.AllowsTransparency%2A> = `true`<br />-   <xref:System.Windows.Controls.Control.Background%2A> = <xref:System.Windows.Media.Brushes.Transparent%2A>|  
  
<a name="other_resources"></a>   
## <a name="other-resources"></a>Inne zasoby  
 Poniższe zasoby mogą pomóc w analizie charakterystyki [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] wydajności aplikacji.  
  
### <a name="graphics-rendering-registry-settings"></a>Ustawienie rejestru renderowania grafiki  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]udostępnia cztery ustawienia rejestru do kontrolowania [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] renderowania:  
  
|Ustawienie|Opis|  
|-------------|-----------------|  
|**Wyłącz opcję przyspieszania sprzętowego**|Określa, czy przyspieszenie sprzętowe powinno być włączone.|  
|**Maksymalna wartość wielopróbkowa**|Określa stopień próbkowania wielostronicowego do wygładzania zawartości 3-D.|  
|**Wymagane ustawienie daty sterownika wideo**|Określa, czy system wyłącza przyspieszenie sprzętowe dla sterowników wydanych przed listopad 2004.|  
|**Użyj opcji rasteryzatora odwołań**|Określa, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] czy powinien być używany Rasteryzacja odwołania.|  
  
 Dostęp do tych ustawień można uzyskać za pomocą dowolnego narzędzia konfiguracji zewnętrznej, które wie, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] jak odwoływać się do ustawień rejestru. Te ustawienia można również utworzyć lub zmodyfikować, uzyskując dostęp do wartości bezpośrednio przy użyciu Edytora rejestru systemu Windows. Aby uzyskać więcej informacji, zobacz [Ustawienia rejestru renderowania grafiki](../graphics-multimedia/graphics-rendering-registry-settings.md).  
  
### <a name="wpf-performance-profiling-tools"></a>narzędzia profilowania wydajności WPF  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]udostępnia pakiet narzędzi profilowania wydajności, które umożliwiają analizowanie zachowania aplikacji w czasie wykonywania i Określanie typów optymalizacji wydajności, które można zastosować. W poniższej tabeli wymieniono narzędzia profilowania wydajności, które znajdują się w narzędziu Windows SDK, zestaw wydajności WPF:  
  
|Narzędzie|Opis|  
|----------|-----------------|  
|Perforator|Służy do analizowania zachowania renderowania.|  
|Visual Profiler|Służy do profilowania korzystania z [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usług, takich jak układ i obsługa zdarzeń, według elementów w drzewie wizualnym.|  
  
 Zestaw wydajności WPF oferuje bogaty i graficzny widok danych wydajności. Aby uzyskać więcej informacji na temat narzędzi wydajności WPF, zobacz [WPF Performance Suite](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa969767(v=vs.100)).  
  
### <a name="directx-diagnostic-tool"></a>Narzędzie diagnostyczne DirectX  
 Narzędzie diagnostyczne DirectX, dxdiag. exe, zostało zaprojektowane w celu ułatwienia rozwiązywania problemów związanych z programem DirectX. Domyślny folder instalacji dla narzędzia diagnostycznego DirectX to:  
  
 `~\Windows\System32`  
  
 Po uruchomieniu narzędzia diagnostycznego DirectX okno główne zawiera zestaw kart, które umożliwiają wyświetlanie i diagnozowanie informacji związanych z technologią DirectX. Na przykład karta **system** zawiera informacje o systemie komputera i określa wersję programu DirectX, która jest zainstalowana na komputerze.  
  
 ![Screenhot: Narzędzie]diagnostyczne DirectX(./media/directxdiagnostictool-01.png "DirectXDiagnosticTool_01")  
Okno główne narzędzia diagnostycznego DirectX  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Media.RenderCapability>
- <xref:System.Windows.Media.RenderOptions>
- [Optymalizacja wydajności aplikacji WPF](optimizing-wpf-application-performance.md)
- [Pakiet wydajności WPF](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa969767(v=vs.100))
- [Ustawienia rejestru renderowania grafiki](../graphics-multimedia/graphics-rendering-registry-settings.md)
- [Animacja — porady i wskazówki](../graphics-multimedia/animation-tips-and-tricks.md)
