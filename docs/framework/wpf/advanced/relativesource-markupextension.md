---
title: RelativeSource MarkupExtension
ms.date: 03/30/2017
f1_keywords:
- RelativeSource
helpviewer_keywords:
- RelativeSource markup extensions [WPF]
- XAML [WPF], RelativeSource markup extension
ms.assetid: 26be4721-49b5-4717-a92e-7d54ad0d3a81
ms.openlocfilehash: 28f3aa500014b768bd07723511613a42df8689aa
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458772"
---
# <a name="relativesource-markupextension"></a>RelativeSource MarkupExtension

Określa właściwości źródła powiązań <xref:System.Windows.Data.RelativeSource>, które ma być używane w ramach [rozszerzenia znacznika powiązania](binding-markup-extension.md)lub podczas ustawiania właściwości <xref:System.Windows.Data.Binding.RelativeSource%2A> elementu <xref:System.Windows.Data.Binding> ustalonego w języku XAML.

## <a name="xaml-attribute-usage"></a>Użycie atrybutu języka XAML

```xml
<Binding RelativeSource="{RelativeSource modeEnumValue}" .../>
```

## <a name="xaml-attribute-usage-nested-within-binding-extension"></a>Użycie atrybutu języka XAML (zagnieżdżonego w rozszerzeniu Binding)

```xml
<object property="{Binding RelativeSource={RelativeSource modeEnumValue} ...}" .../>
```

## <a name="xaml-object-element-usage"></a>Użycie elementu obiektu języka XAML

```xml
<Binding>
  <Binding.RelativeSource>
    <RelativeSource Mode="modeEnumValue"/>
  </Binding.RelativeSource>
</Binding>
```

—lub—

```xml
<Binding>
  <Binding.RelativeSource>
    <RelativeSource
      Mode="FindAncestor"
      AncestorType="{x:Type typeName}"
      AncestorLevel="intLevel"
    />
  </Binding.RelativeSource>
</Binding>
```

## <a name="xaml-values"></a>Wartości XAML

|||
|-|-|
|`modeEnumValue`|Jeden z poniższych:<br /><br /> -Token ciągu `Self`; odnosi się do <xref:System.Windows.Data.RelativeSource>, jak zostało utworzone z właściwością <xref:System.Windows.Data.RelativeSource.Mode%2A> ustawioną na <xref:System.Windows.Data.RelativeSourceMode.Self>.<br />-Token ciągu `TemplatedParent`; odnosi się do <xref:System.Windows.Data.RelativeSource>, jak zostało utworzone z właściwością <xref:System.Windows.Data.RelativeSource.Mode%2A> ustawioną na <xref:System.Windows.Data.RelativeSourceMode.TemplatedParent>.<br />-Token ciągu `PreviousData`; odnosi się do <xref:System.Windows.Data.RelativeSource>, jak zostało utworzone z właściwością <xref:System.Windows.Data.RelativeSource.Mode%2A> ustawioną na <xref:System.Windows.Data.RelativeSourceMode.PreviousData>.<br />-Zobacz poniżej, aby uzyskać informacje o trybie `FindAncestor`.|
|`FindAncestor`|Token ciągu `FindAncestor`. Użycie tego tokenu spowoduje przejście do trybu, w którym `RelativeSource` określa typ elementu nadrzędnego i opcjonalnie poziom nadrzędny. Odnosi się to do <xref:System.Windows.Data.RelativeSource>, jak zostało utworzone z właściwością <xref:System.Windows.Data.RelativeSource.Mode%2A> ustawioną na <xref:System.Windows.Data.RelativeSourceMode.FindAncestor>.|
|`typeName`|Wymagany w trybie `FindAncestor`. Nazwa typu, który wypełnia Właściwość <xref:System.Windows.Data.RelativeSource.AncestorType%2A>.|
|`intLevel`|Opcjonalne dla trybu `FindAncestor`. Poziom elementu nadrzędnego (patrząc w kierunku nadrzędności w drzewie logicznym).|

## <a name="remarks"></a>Uwagi

Użycie powiązań `{RelativeSource TemplatedParent}` jest kluczową techniką, która odnosi się do większej koncepcji separacji interfejsu użytkownika kontrolki i logiki kontrolki. Umożliwia tworzenie powiązań z wewnątrz definicji szablonu do elementu nadrzędnego używającego szablonu (tzn. do wystąpienia obiektu, do którego w czasie wykonywania szablon jest stosowany). W takim przypadku rozszerzenie " [TemplateBinding Markup](templatebinding-markup-extension.md) " jest w istocie skrót dla następującego wyrażenia powiązania: `{Binding RelativeSource={RelativeSource TemplatedParent}}`. `TemplateBinding` lub `{RelativeSource TemplatedParent}` użycia są odpowiednie tylko w kodzie XAML, który definiuje szablon. Aby uzyskać więcej informacji, zobacz [TemplateBinding Markup Extension](templatebinding-markup-extension.md).

`{RelativeSource FindAncestor}` jest używany głównie w szablonach kontroli lub przewidywalnym samoobsługowym kompozycjom interfejsu użytkownika, w przypadkach, gdy kontrolka zawsze powinna znajdować się w drzewie wizualnym określonego typu nadrzędnego. Na przykład elementy formantu Items mogą używać `FindAncestor` użycia, aby powiązać z właściwościami ich elementów w nadrzędnym elemencie nadrzędnym. Lub elementy, które są częścią kompozycji formantu w szablonie, mogą używać powiązań `FindAncestor` do elementów nadrzędnych w tej samej strukturze kompozycji.

W składni elementu obiektu dla `FindAncestor` trybu pokazanego w sekcjach składni języka XAML druga składnia elementu obiektu jest używana w trybie `FindAncestor`. Tryb `FindAncestor` wymaga wartości <xref:System.Windows.Data.RelativeSource.AncestorType%2A>. Należy ustawić <xref:System.Windows.Data.RelativeSource.AncestorType%2A> jako atrybut przy użyciu odwołania do [rozszerzenia znacznika x:Type —](../../xaml-services/x-type-markup-extension.md) do typu elementu nadrzędnego, który ma zostać wyszukany. Wartość <xref:System.Windows.Data.RelativeSource.AncestorType%2A> jest używana, gdy żądanie powiązania jest przetwarzane w czasie wykonywania.

W trybie `FindAncestor` Właściwość opcjonalna <xref:System.Windows.Data.RelativeSource.AncestorLevel%2A> może pomóc w odróżnieniu wyszukiwania nadrzędnego w przypadkach, gdy istnieje więcej niż jeden element nadrzędny tego typu istniejący w drzewie elementów.

Aby uzyskać więcej informacji na temat używania trybu `FindAncestor`, zobacz <xref:System.Windows.Data.RelativeSource>.

`{RelativeSource Self}` jest przydatne w scenariuszach, w których jedna Właściwość wystąpienia powinna zależeć od wartości innej właściwości tego samego wystąpienia, a żadna relacja głównej właściwości zależności (na przykład przekształcenie) już istnieje między tymi dwiema właściwościami. Chociaż jest to rzadki, że dwie właściwości istnieją w obiekcie, tak że wartości są identyczne (i są identyczne), można również zastosować `Converter` parametru do powiązania, które ma `{RelativeSource Self}`, i użyć konwertera do konwersji między źródłem i docelowym Typ. Inny scenariusz dla `{RelativeSource Self}` jest częścią <xref:System.Windows.MultiDataTrigger>.

Na przykład poniższy kod XAML definiuje <xref:System.Windows.Shapes.Rectangle> elementu, w taki sposób, aby niezależnie od wartości wprowadzonej dla <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.Shapes.Rectangle> jest zawsze kwadratem: `<Rectangle Width="200" Height="{Binding RelativeSource={RelativeSource Self}, Path=Width}" .../>`

`{RelativeSource PreviousData}` jest przydatne w szablonach danych lub w przypadkach, gdy powiązania używają kolekcji jako źródła danych. Możesz użyć `{RelativeSource PreviousData}`, aby wyróżnić relacje między sąsiednimi elementami danych w kolekcji. Pokrewna Technika polega na ustanowieniu <xref:System.Windows.Data.MultiBinding> między bieżącą i poprzednimi elementami w źródle danych, a następnie użyć konwertera dla tego powiązania, aby określić różnicę między dwoma elementami i ich właściwościami.

W poniższym przykładzie pierwsze <xref:System.Windows.Controls.TextBlock> w szablonie Items wyświetla bieżącą liczbę. Drugie powiązanie <xref:System.Windows.Controls.TextBlock> jest <xref:System.Windows.Data.MultiBinding>, która nominalnie ma dwa elementy <xref:System.Windows.Data.Binding>e: bieżący rekord i powiązanie, które w sposób celowy używa poprzedniego rekordu danych przy użyciu `{RelativeSource PreviousData}`. Następnie konwerter <xref:System.Windows.Data.MultiBinding> oblicza różnicę i zwraca go do powiązania.

```xml
<ListBox Name="fibolist">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
            <TextBlock Text="{Binding}"/>
            <TextBlock>, difference = </TextBlock>
                <TextBlock>
                    <TextBlock.Text>
                        <MultiBinding Converter="{StaticResource DiffConverter}">
                            <Binding/>
                            <Binding RelativeSource="{RelativeSource PreviousData}"/>
                        </MultiBinding>
                    </TextBlock.Text>
                </TextBlock>
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
```

Opisywanie powiązania danych jako koncepcji nie jest tutaj omówione, zobacz temat [powiązanie danych — omówienie](../../../desktop-wpf/data/data-binding-overview.md).

W implementacji procesora [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML obsługa tego rozszerzenia znacznika jest definiowana przez klasę <xref:System.Windows.Data.RelativeSource>.

`RelativeSource` to rozszerzenie znaczników. Rozszerzenia znaczników są zazwyczaj implementowane w sytuacji, gdy istnieje wymóg, aby wartości atrybutów były wyprowadzane w postaci innej niż wartości literałów lub nazwy programów obsługi, a wymóg ma charakter bardziej globalny niż zwykłe umieszczenie konwerterów typów w niektórych typach lub właściwościach. Wszystkie rozszerzenia znaczników w języku XAML używają znaków `{` i `}` w ich składni atrybutów, która jest konwencją, za pomocą której procesor XAML rozpoznaje, że rozszerzenie znacznika musi przetworzyć atrybut. Aby uzyskać więcej informacji, zobacz [rozszerzenia znaczników i XAML WPF](markup-extensions-and-wpf-xaml.md).

## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Data.Binding>
- [Tworzenie szablonów i stylów](../controls/styling-and-templating.md)
- [Przegląd XAML (WPF)](xaml-overview-wpf.md)
- [Rozszerzenia znaczników i WPF XAML](markup-extensions-and-wpf-xaml.md)
- [Powiązanie danych — omówienie](../../../desktop-wpf/data/data-binding-overview.md)
- [Powiązanie deklaracji — omówienie](../data/binding-declarations-overview.md)
- [x:Type, rozszerzenie znaczników](../../xaml-services/x-type-markup-extension.md)
