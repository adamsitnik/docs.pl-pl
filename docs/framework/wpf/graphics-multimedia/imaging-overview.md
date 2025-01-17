---
title: Przegląd Obrazowanie
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- metadata [WPF], images
- displaying images [WPF]
- Imaging API [WPF]
- image metadata [WPF]
- converting images [WPF]
- encoding image formats [WPF]
- format decoding for images [WPF]
- painting with images [WPF]
- stretching images [WPF]
- images [WPF], about imaging
- format encoding for images [WPF]
- cropping images [WPF]
- decoding image formats [WPF]
- rotating images [WPF]
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
ms.openlocfilehash: b60f2871062a12d3bee91a9c6d9883222b3034f4
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73733567"
---
# <a name="imaging-overview"></a>Przegląd Obrazowanie
Ten temat zawiera wprowadzenie do składnika Microsoft Windows Presentation Foundation Imaging. Program WPF Imaging umożliwia deweloperom wyświetlanie, przekształcanie i formatowanie obrazów.  

## <a name="wpf-imaging-component"></a>Składnik programu WPF Imaging  
 Program WPF Imaging oferuje znaczące ulepszenia w zakresie możliwości tworzenia obrazów w systemie Microsoft Windows. Funkcje tworzenia obrazu, takie jak wyświetlanie mapy bitowej lub użycie obrazu w przypadku wspólnej kontrolki, były wcześniej oparte na bibliotekach Microsoft Windows GDI (GDI) lub Windows Microsoft GDI+. Ten interfejs API zapewnia podstawowe funkcje tworzenia obrazu, ale nie ma żadnych funkcji, takich jak obsługa rozszerzalności koderów-dekoder i obsługa obrazów o wysokiej wierności. Program WPF Imaging został zaprojektowany w celu pokonania wad GDI i GDI+ oraz udostępnienie nowego zestawu interfejsów API do wyświetlania i używania obrazów w aplikacjach.  
  
 Istnieją dwa sposoby dostępu do interfejsu API przetwarzania obrazów WPF, składnika zarządzanego i składnika niezarządzanego. Składnik niezarządzany udostępnia następujące funkcje.  
  
- Model rozszerzalności dla nowych lub własnościowych formatów obrazu.  
  
- Ulepszona wydajność i zabezpieczenia formatów obrazów natywnych, w tym mapy bitowej (BMP), Wspólna Grupa ekspertów fotograficznych (JPEG), Portable Network Graphics (PNG), Tagged Image File Format (TIFF), Photo Microsoft Windows Media, Graphics Interchange Format (GIF), i ikona (. ico).  
  
- Zachowywanie dużej ilości danych obrazu z dużymi bitami do 8 bitów na kanał (32 bitów na piksel).  
  
- Niebezpieczne skalowanie obrazów, kadrowanie i obracanie.  
  
- Uproszczone zarządzanie kolorami.  
  
- Obsługa metadanych w pliku, które są zastrzeżone.  
  
- Zarządzany składnik wykorzystuje niezarządzaną infrastrukturę, aby zapewnić bezproblemową integrację obrazów z innymi funkcjami [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], takimi jak [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], animacje i grafiki. Składnik zarządzany również korzysta z modelu rozszerzalności kodera-dekodeka programu Windows Presentation Foundation (WPF), który umożliwia automatyczne rozpoznawanie nowych formatów obrazów w aplikacjach [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 Większość zarządzanych interfejsów API programu WPF Imaging znajduje się w przestrzeni nazw <xref:System.Windows.Media.Imaging?displayProperty=nameWithType>, chociaż kilka ważnych typów, takich jak <xref:System.Windows.Media.ImageBrush> i <xref:System.Windows.Media.ImageDrawing> znajdują się w przestrzeni nazw <xref:System.Windows.Media?displayProperty=nameWithType> i <xref:System.Windows.Controls.Image> znajdują się w przestrzeni nazw <xref:System.Windows.Controls?displayProperty=nameWithType>.  
  
 Ten temat zawiera dodatkowe informacje o zarządzanym składniku programu. Aby uzyskać więcej informacji na temat niezarządzanego interfejsu API, zobacz dokumentację [składnika niezarządzanego programu WPF Imaging](/windows/desktop/wic/-wic-lh) .  
  
<a name="_imageformats"></a>   
## <a name="wpf-image-formats"></a>Formaty obrazów WPF  

 Koder-dekoder służy do dekodowania lub kodowania określonego formatu multimediów. Program WPF Imaging zawiera koder-dekoder dla formatów obrazów BMP, JPEG, PNG, TIFF, zdjęć, GIF i ikon. Każdy z tych kodeków pozwala aplikacjom dekodować i, z wyjątkiem ikony, zakodować odpowiednie formaty obrazu.  
  
 <xref:System.Windows.Media.Imaging.BitmapSource> jest ważną klasą używaną podczas dekodowania i kodowania obrazów. Jest to podstawowy blok konstrukcyjny potoku tworzenia obrazów WPF i reprezentuje pojedynczy, stały zestaw pikseli o określonym rozmiarze i rozdzielczości. <xref:System.Windows.Media.Imaging.BitmapSource> może być pojedynczą ramką obrazu z wieloma ramkami lub może być wynikiem transformacji wykonanej na <xref:System.Windows.Media.Imaging.BitmapSource>. Jest elementem nadrzędnym wielu klas podstawowych używanych w programie [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] Imaging, takich jak <xref:System.Windows.Media.Imaging.BitmapFrame>.  
  
 <xref:System.Windows.Media.Imaging.BitmapFrame> jest używany do przechowywania rzeczywistych danych mapy bitowej w formacie obrazu. Wiele formatów obrazów obsługuje tylko pojedyncze <xref:System.Windows.Media.Imaging.BitmapFrame>, ale formaty takie jak GIF i TIFF obsługują wiele ramek na obraz. Ramki są używane przez dekodery jako dane wejściowe i są przesyłane do koderów w celu utworzenia plików obrazów.  
  
 W poniższym przykładzie pokazano, jak <xref:System.Windows.Media.Imaging.BitmapFrame> jest tworzony na podstawie <xref:System.Windows.Media.Imaging.BitmapSource>, a następnie dodawany do obrazu TIFF.  
  
 [!code-csharp[BitmapFrameExample#10](~/samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### <a name="image-format-decoding"></a>Dekodowanie formatu obrazu  
 Dekodowanie obrazu jest tłumaczeniem formatu obrazu na dane obrazu, które mogą być używane przez system. Dane obrazu mogą być następnie używane do wyświetlania, przetwarzania lub kodowania w innym formacie. Wybór dekodera jest oparty na formacie obrazu. Wybór kodera-dekoder jest automatyczny, chyba że określono określony dekoder. Przykłady w sekcji [Wyświetlanie obrazów w WPF](#_displayingimages) przedstawiają automatyczne dekodowanie. Dekodery formatu niestandardowego opracowane przy użyciu niezarządzanych interfejsów programu WPF Imaging i zarejestrowane w systemie automatycznie biorą udział w wyborze dekodera. Umożliwia to automatyczne wyświetlanie formatów niestandardowych w aplikacjach [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 Poniższy przykład ilustruje użycie dekodera mapy bitowej do zdekodowania obrazu formatu BMP.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### <a name="image-format-encoding"></a>Kodowanie formatu obrazu  
 Kodowanie obrazu to tłumaczenie danych obrazu do określonego formatu obrazu. Zakodowane dane obrazu mogą być następnie używane do tworzenia nowych plików obrazu. Program WPF Imaging udostępnia kodery dla każdego z opisanych powyżej formatów obrazu.  
  
 Poniższy przykład ilustruje użycie kodera do zapisania nowo utworzonego obrazu mapy bitowej.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## <a name="displaying-images-in-wpf"></a>Wyświetlanie obrazów w WPF  
 Istnieje kilka sposobów wyświetlania obrazu w aplikacji Windows Presentation Foundation (WPF). Obrazy można wyświetlać przy użyciu kontrolki <xref:System.Windows.Controls.Image>, rysowanej na wizualizacji przy użyciu <xref:System.Windows.Media.ImageBrush>lub rysowanej przy użyciu <xref:System.Windows.Media.ImageDrawing>.  
  
### <a name="using-the-image-control"></a>Korzystanie z kontrolki obrazu  
 <xref:System.Windows.Controls.Image> jest elementem struktury i głównym sposobem wyświetlania obrazów w aplikacjach. W [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]<xref:System.Windows.Controls.Image> można używać na dwa sposoby: Składnia atrybutu lub Składnia właściwości. Poniższy przykład pokazuje, jak renderować obraz 200 pikseli szerokości przy użyciu składni atrybutów i składni tagów właściwości. Aby uzyskać więcej informacji na temat składni atrybutów i składni właściwości, zobacz [Omówienie właściwości zależności](../advanced/dependency-properties-overview.md).  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 Wiele przykładów używa obiektu <xref:System.Windows.Media.Imaging.BitmapImage> do odwoływania się do pliku obrazu. <xref:System.Windows.Media.Imaging.BitmapImage> to wyspecjalizowany <xref:System.Windows.Media.Imaging.BitmapSource> zoptymalizowany pod kątem [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ładowania i jest łatwym sposobem wyświetlania obrazów jako <xref:System.Windows.Controls.Image.Source%2A> kontrolki <xref:System.Windows.Controls.Image>.  
  
 Poniższy przykład pokazuje, jak renderować obraz 200 pikseli szerokości przy użyciu kodu.  
  
> [!NOTE]
> <xref:System.Windows.Media.Imaging.BitmapImage> implementuje interfejs <xref:System.ComponentModel.ISupportInitialize> w celu optymalizacji inicjalizacji dla wielu właściwości. Zmiany właściwości mogą wystąpić tylko podczas inicjowania obiektu. Wywołaj <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A>, aby sygnalizować, że inicjalizacja została rozpoczęta, i <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A>, aby sygnalizować zakończenie inicjalizacji. Po zainicjowaniu zmiany właściwości zostaną zignorowane.  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### <a name="rotating-converting-and-cropping-images"></a>Obracanie, konwertowanie i przycinanie obrazów  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] umożliwia użytkownikom przekształcanie obrazów za pomocą właściwości <xref:System.Windows.Media.Imaging.BitmapImage> lub przy użyciu dodatkowych obiektów <xref:System.Windows.Media.Imaging.BitmapSource>, takich jak <xref:System.Windows.Media.Imaging.CroppedBitmap> lub <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>. Te przekształcenia obrazu umożliwiają skalowanie lub obracanie obrazu, Zmienianie formatu pikseli obrazu lub Kadrowanie obrazu.  
  
 Obracanie obrazów odbywa się przy użyciu właściwości <xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A> <xref:System.Windows.Media.Imaging.BitmapImage>. Obrót można wykonać tylko w przyrostach o 90 stopni. W poniższym przykładzie obraz jest obrócony o 90 stopni.  
  
 [!code-xaml[ImageElementExample#TransformedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 Konwersja obrazu do innego formatu pikseli, takiego jak skala szarości, odbywa się przy użyciu <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>. W poniższych przykładach obraz jest konwertowany na <xref:System.Windows.Media.PixelFormats.Gray4%2A>.  
  
 [!code-xaml[ImageElementExample_snip#ConvertedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 Aby przyciąć obraz, można użyć właściwości <xref:System.Windows.UIElement.Clip%2A> <xref:System.Windows.Controls.Image> lub <xref:System.Windows.Media.Imaging.CroppedBitmap>. Zwykle, jeśli chcesz wyświetlić część obrazu, należy użyć <xref:System.Windows.UIElement.Clip%2A>. Jeśli zachodzi potrzeba zakodowania i zapisania obrazu przyciętego, należy użyć <xref:System.Windows.Media.Imaging.CroppedBitmap>. W poniższym przykładzie obraz jest przycięty przy użyciu właściwości Clip przy użyciu <xref:System.Windows.Media.EllipseGeometry>.  
  
 [!code-xaml[ImageElementExample_snip#CroppedXAMLUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### <a name="stretching-images"></a>Rozciąganie obrazów  
 Właściwość <xref:System.Windows.Controls.Image.Stretch%2A> kontroluje, w jaki sposób obraz jest rozciągany w celu wypełnienia jego kontenera. Właściwość <xref:System.Windows.Controls.Image.Stretch%2A> akceptuje następujące wartości zdefiniowane przez Wyliczenie <xref:System.Windows.Media.Stretch>:  
  
- <xref:System.Windows.Media.Stretch.None>: obraz nie jest rozciągany w celu wypełnienia obszaru wyjściowego. Jeśli obraz jest większy niż obszar wyjściowy, obraz jest rysowany w obszarze danych wyjściowych, co nie pasuje.  
  
- <xref:System.Windows.Media.Stretch.Fill>: obraz jest skalowany w celu dopasowania do obszaru wyjściowego. Ze względu na to, że wysokość i Szerokość obrazu są skalowane niezależnie, oryginalny współczynnik proporcji obrazu może nie zostać zachowany. Oznacza to, że obraz może być zniekształcany w celu całkowitego wypełnienia kontenera danych wyjściowych.  
  
- <xref:System.Windows.Media.Stretch.Uniform>: obraz jest skalowany tak, aby mieścił się w całości w obszarze danych wyjściowych. Współczynnik proporcji obrazu jest zachowywany.  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>: obraz jest skalowany tak, aby całkowicie wypełniał obszar wyjściowy podczas zachowywania oryginalnego współczynnika proporcji obrazu.  
  
 Poniższy przykład stosuje do <xref:System.Windows.Controls.Image>wszystkie dostępne wyliczenia <xref:System.Windows.Media.Stretch>.  
  
 Na poniższej ilustracji przedstawiono dane wyjściowe z przykładu i przedstawiono wpływ różnych ustawień <xref:System.Windows.Controls.Image.Stretch%2A>, które mają zastosowanie do obrazu.  
  
 ![Różne ustawienia rozciągania TileBrush](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
Różne ustawienia rozciągania  
  
 [!code-xaml[ImageElementExample_snip#ImageStretchExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### <a name="painting-with-images"></a>Malowanie przy użyciu obrazów  
 Obrazy mogą być również wyświetlane w aplikacji przez malowanie przy użyciu <xref:System.Windows.Media.Brush>. Pędzle umożliwiają malowanie [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] obiektów ze wszystkimi elementami od prostych, pełnych kolorów do złożonych zestawów wzorców i obrazów. Aby malować przy użyciu obrazów, użyj <xref:System.Windows.Media.ImageBrush>. <xref:System.Windows.Media.ImageBrush> jest typem <xref:System.Windows.Media.TileBrush>, który definiuje jego zawartość jako obraz mapy bitowej. <xref:System.Windows.Media.ImageBrush> wyświetla pojedynczy obraz, który jest określony przez jego właściwość <xref:System.Windows.Media.ImageBrush.ImageSource%2A>. Można kontrolować sposób rozciągania i wyrównania obrazu, co pozwala uniknąć zniekształceń i generować wzorce oraz inne efekty. Na poniższej ilustracji przedstawiono niektóre efekty, które można osiągnąć przy użyciu <xref:System.Windows.Media.ImageBrush>.  
  
 ![Przykłady danych wyjściowych ImageBrush](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
Pędzle obrazu mogą wypełniać kształty, kontrolki, tekst i nie tylko  
  
 Poniższy przykład ilustruje sposób rysowania tła przycisku z obrazem przy użyciu <xref:System.Windows.Media.ImageBrush>.  
  
 [!code-xaml[UsingImageBrush#4](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 Aby uzyskać dodatkowe informacje na temat <xref:System.Windows.Media.ImageBrush> i malowania obrazów [, zobacz malowanie przy użyciu obrazów, rysunków i wizualizacji](painting-with-images-drawings-and-visuals.md).  
  
<a name="_metadata"></a>   
## <a name="image-metadata"></a>Metadane obrazu  
 Niektóre pliki obrazów zawierają metadane opisujące zawartość lub charakterystykę pliku. Na przykład większość kamer cyfrowych tworzy obrazy zawierające metadane dotyczące marki i modelu aparatu używane do przechwytywania obrazu. Każdy format obrazu obsługuje metadane inaczej, ale program WPF Imaging zapewnia jednolity sposób przechowywania i pobierania metadanych dla każdego obsługiwanego formatu obrazu.  
  
 Dostęp do metadanych jest dostarczany za pomocą właściwości <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> obiektu <xref:System.Windows.Media.Imaging.BitmapSource>. <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> zwraca obiekt <xref:System.Windows.Media.Imaging.BitmapMetadata>, który zawiera wszystkie metadane zawarte w obrazie. Te dane mogą znajdować się w jednym schemacie metadanych lub w połączeniu z różnymi schematami. Program WPF Imaging obsługuje następujące schematy metadanych obrazów: plik z programem Exchange (EXIF), tekst (dane tekstowe PNG), katalog plików obrazów (IFD), międzynarodowa prasa telekomunikacyjna (IPTC) i rozszerzalna platforma metadanych (XMP).  
  
 Aby uprościć proces odczytywania metadanych, <xref:System.Windows.Media.Imaging.BitmapMetadata> udostępnia kilka nazwanych właściwości, które można łatwo uzyskać do nich dostęp, takich jak <xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A>, <xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A>i <xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>. Wiele z tych nazwanych właściwości może również służyć do pisania metadanych. Dodatkowa obsługa odczytywania metadanych jest dostarczana przez czytelnika zapytania metadanych. Metoda <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> służy do pobierania czytnika zapytań metadanych przez podanie ciągu zapytania, takiego jak *"/APP1/EXIF/"* . W poniższym przykładzie <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> jest używany do uzyskania tekstu przechowywanego w lokalizacji *"/text/Description"* .  
  
 [!code-cpp[BitmapMetadata#GetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 Do zapisywania metadanych jest używany moduł zapisujący zapytania metadanych. <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> uzyskuje składnik zapisywania zapytań i ustawia żądaną wartość. W poniższym przykładzie <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> jest używany do zapisania tekstu przechowywanego w lokalizacji *"/text/Description"* .  
  
 [!code-cpp[BitmapMetadata#SetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## <a name="codec-extensibility"></a>Rozszerzalność kodeka  
 Podstawowa funkcja programu WPF Imaging jest modelem rozszerzalności dla nowych koderów-dekoder obrazu. Te niezarządzane interfejsy umożliwiają deweloperom koderów-dekoderów z [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], tak aby nowe formaty obrazów mogły być automatycznie używane przez aplikacje [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 Przykład interfejsu API rozszerzalności można znaleźć w [przykładowym kodeku Win32](https://go.microsoft.com/fwlink/?LinkID=160052). Ten przykład pokazuje, jak utworzyć dekoder i koder dla niestandardowego formatu obrazu.  
  
> [!NOTE]
> Koder-dekoder musi być cyfrowo podpisany, aby system mógł go rozpoznać.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Media.Imaging.BitmapSource>
- <xref:System.Windows.Media.Imaging.BitmapImage>
- <xref:System.Windows.Controls.Image>
- <xref:System.Windows.Media.Imaging.BitmapMetadata>
- [Grafika 2D i obrazowanie](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Przykładowy koder-dekoder Win32](https://go.microsoft.com/fwlink/?LinkID=160052)
