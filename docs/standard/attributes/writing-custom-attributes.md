---
title: Wpisywanie atrybutów niestandardowych
ms.date: 07/17/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- multiple attribute instances
- AttributeTargets enumeration
- attributes [.NET Framework], custom
- AllowMultiple property
- custom attributes
- AttributeUsageAttribute class, custom attributes
- Inherited property
- attribute classes, declaring
ms.assetid: 97216f69-bde8-49fd-ac40-f18c500ef5dc
ms.openlocfilehash: 6570c6994c0f2e6571361c3eadc73b02a55f1584
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140584"
---
# <a name="writing-custom-attributes"></a>Wpisywanie atrybutów niestandardowych
Do zaprojektowania własnych atrybutów niestandardowych nie ma potrzeby tworzenia wzorców wielu nowych koncepcji. Jeśli znasz programowanie zorientowane obiektowo i wiesz, jak projektować klasy, masz już większość koniecznych informacji. Atrybuty niestandardowe są zasadniczo tradycyjnymi klasami, które są wyprowadzane bezpośrednio lub pośrednio z <xref:System.Attribute?displayProperty=nameWithType>. Podobnie jak tradycyjne klasy, atrybuty niestandardowe zawierają metody, które przechowują i pobierają dane.  
  
 Podstawowe kroki w celu prawidłowego projektowania klas atrybutów niestandardowych są następujące:  
  
- [Stosowanie AttributeUsageAttribute](#applying-the-attributeusageattribute)  
  
- [Deklarowanie klasy atrybutów](#declaring-the-attribute-class)  
  
- [Deklarowanie konstruktorów](#declaring-constructors)  
  
- [Deklarowanie właściwości](#declaring-properties)  
  
 W tej sekcji opisano wszystkie te kroki i zakończymy z [przykładem atrybutu niestandardowego](#custom-attribute-example).  
  
## <a name="applying-the-attributeusageattribute"></a>Stosowanie AttributeUsageAttribute  
 Deklaracja atrybutu niestandardowego rozpoczyna się od <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>, który definiuje niektóre kluczowe cechy klasy atrybutów. Na przykład można określić, czy atrybut może być dziedziczony przez inne klasy, czy też określić, do których elementów można zastosować atrybut. Poniższy fragment kodu ilustruje sposób używania <xref:System.AttributeUsageAttribute>.  
  
 [!code-cpp[Conceptual.Attributes.Usage#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#5)]
 [!code-csharp[Conceptual.Attributes.Usage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#5)]
 [!code-vb[Conceptual.Attributes.Usage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#5)]  
  
 <xref:System.AttributeUsageAttribute> ma trzy składowe, które są ważne dla tworzenia atrybutów niestandardowych: [AttributeTargets](#attributetargets-member), [Odziedziczone](#inherited-property)i [AllowMultiple](#allowmultiple-property).  
  
### <a name="attributetargets-member"></a>AttributeTargets element członkowski  
 W poprzednim przykładzie określono <xref:System.AttributeTargets.All?displayProperty=nameWithType>, wskazujący, że ten atrybut może być stosowany do wszystkich elementów programu. Alternatywnie można określić <xref:System.AttributeTargets.Class?displayProperty=nameWithType>, wskazując, że atrybut może być stosowany tylko do klasy lub <xref:System.AttributeTargets.Method?displayProperty=nameWithType>, co oznacza, że atrybut może być stosowany tylko do metody. Wszystkie elementy programu mogą być oznaczone do opisu przez atrybut niestandardowy w ten sposób.  
  
 Można również przekazać wiele wartości <xref:System.AttributeTargets>. Poniższy fragment kodu określa, że atrybut niestandardowy można zastosować do dowolnej klasy lub metody.  
  
 [!code-cpp[Conceptual.Attributes.Usage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#6)]
 [!code-csharp[Conceptual.Attributes.Usage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#6)]
 [!code-vb[Conceptual.Attributes.Usage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#6)]  
  
### <a name="inherited-property"></a>Właściwość dziedziczona  
 Właściwość <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> wskazuje, czy atrybut może być dziedziczony przez klasy, które pochodzą od klas, do których zastosowano atrybut. Ta właściwość przyjmuje `true` (wartość domyślna) lub `false`. W poniższym przykładzie `MyAttribute` ma domyślną wartość <xref:System.AttributeUsageAttribute.Inherited%2A> `true`, podczas gdy `YourAttribute` ma <xref:System.AttributeUsageAttribute.Inherited%2A> wartość `false`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Attributes.Usage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#7)]
 [!code-vb[Conceptual.Attributes.Usage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#7)]  
  
 Te dwa atrybuty są następnie stosowane do metody w klasie bazowej `MyClass`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#9)]
 [!code-csharp[Conceptual.Attributes.Usage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#9)]
 [!code-vb[Conceptual.Attributes.Usage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#9)]  
  
 Na koniec Klasa `YourClass` jest dziedziczona z klasy bazowej `MyClass`. Metoda `MyMethod` zawiera `MyAttribute`, ale nie `YourAttribute`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#10)]
 [!code-csharp[Conceptual.Attributes.Usage#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#10)]
 [!code-vb[Conceptual.Attributes.Usage#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#10)]  
  
### <a name="allowmultiple-property"></a>Właściwość AllowMultiple  
 Właściwość <xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=nameWithType> wskazuje, czy w elemencie może istnieć wiele wystąpień atrybutu. Jeśli ustawiono `true`, dozwolone są wiele wystąpień; Jeśli jest ustawiona na `false` (wartość domyślna), dozwolone jest tylko jedno wystąpienie.  
  
 W poniższym przykładzie `MyAttribute` ma domyślną wartość <xref:System.AttributeUsageAttribute.AllowMultiple%2A> `false`, podczas gdy `YourAttribute` ma wartość `true`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#11)]
 [!code-csharp[Conceptual.Attributes.Usage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#11)]
 [!code-vb[Conceptual.Attributes.Usage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#11)]  
  
 Jeśli zastosowano wiele wystąpień tych atrybutów, `MyAttribute` generuje błąd kompilatora. Poniższy przykład kodu pokazuje prawidłowe użycie `YourAttribute` i nieprawidłowe użycie `MyAttribute`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#13)]
 [!code-csharp[Conceptual.Attributes.Usage#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#13)]
 [!code-vb[Conceptual.Attributes.Usage#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#13)]  
  
 Jeśli właściwość <xref:System.AttributeUsageAttribute.AllowMultiple%2A> i Właściwość <xref:System.AttributeUsageAttribute.Inherited%2A> są ustawione na `true`, Klasa dziedziczona z innej klasy może dziedziczyć atrybut i mieć inne wystąpienie tego samego atrybutu stosowane w tej samej klasie podrzędnej. Jeśli <xref:System.AttributeUsageAttribute.AllowMultiple%2A> jest ustawiona na `false`, wartości wszelkich atrybutów w klasie nadrzędnej zostaną zastąpione przez nowe wystąpienia tego samego atrybutu w klasie podrzędnej.  
  
## <a name="declaring-the-attribute-class"></a>Deklarowanie klasy atrybutów  
 Po zastosowaniu <xref:System.AttributeUsageAttribute>można rozpocząć Definiowanie określonych atrybutów. Deklaracja klasy atrybutu wygląda podobnie do deklaracji tradycyjnej klasy, jak pokazano w poniższym kodzie.  
  
 [!code-cpp[Conceptual.Attributes.Usage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#14)]
 [!code-csharp[Conceptual.Attributes.Usage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#14)]
 [!code-vb[Conceptual.Attributes.Usage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#14)]  
  
 Ta definicja atrybutu ilustruje następujące kwestie:  
  
- Klasy atrybutów muszą być zadeklarowane jako klasy publiczne.  
  
- Zgodnie z Konwencją nazwa klasy ma kończyć się **atrybutem**programu Word. Chociaż nie jest to wymagane, ta konwencja jest zalecana dla czytelności. Gdy atrybut jest stosowany, włączenie atrybutu słowa jest opcjonalne.  
  
- Wszystkie klasy atrybutów muszą dziedziczyć bezpośrednio lub pośrednio z <xref:System.Attribute?displayProperty=nameWithType>.  
  
- W programie Microsoft Visual Basic wszystkie klasy atrybutów niestandardowych muszą mieć atrybut <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>.  
  
## <a name="declaring-constructors"></a>Deklarowanie konstruktorów  
 Atrybuty są inicjowane za pomocą konstruktorów w taki sam sposób jak w przypadku tradycyjnych klas. Poniższy fragment kodu ilustruje typowy Konstruktor atrybutu. Ten konstruktor publiczny przyjmuje parametr i ustawia zmienną członkowską równą jej wartości.  
  
 [!code-cpp[Conceptual.Attributes.Usage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#15)]
 [!code-csharp[Conceptual.Attributes.Usage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#15)]
 [!code-vb[Conceptual.Attributes.Usage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#15)]  
  
 Można przeciążyć konstruktora, aby pomieścić różne kombinacje wartości. Jeśli zdefiniowano również [Właściwość](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)) klasy atrybutów niestandardowych, podczas inicjowania atrybutu można użyć kombinacji nazwanych i pozycyjnych parametrów. Zwykle wszystkie wymagane parametry są definiowane jako położenie i wszystkie parametry opcjonalne jako nazwane. W tym przypadku nie można zainicjować atrybutu bez wymaganego parametru. Wszystkie inne parametry są opcjonalne. Należy zauważyć, że w Visual Basic konstruktory dla klasy atrybutów nie powinny używać argumentu ParamArray.  
  
 Poniższy przykład kodu pokazuje, jak atrybut, który używa poprzedniego konstruktora można zastosować przy użyciu opcjonalnych i wymaganych parametrów. Przyjęto założenie, że atrybut ma jedną wymaganą wartość logiczną i jedną opcjonalną Właściwość ciągu.  
  
 [!code-cpp[Conceptual.Attributes.Usage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#17)]
 [!code-csharp[Conceptual.Attributes.Usage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#17)]
 [!code-vb[Conceptual.Attributes.Usage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#17)]  
  
## <a name="declaring-properties"></a>Deklarowanie właściwości  
 Jeśli chcesz zdefiniować nazwany parametr lub podać łatwy sposób zwracania wartości przechowywanych przez atrybut, zadeklaruj [Właściwość](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)). Właściwości atrybutu należy zadeklarować jako jednostki publiczne z opisem typu danych, które zostaną zwrócone. Zdefiniuj zmienną, która będzie przechowywać wartość właściwości i skojarz ją z metodami **Get** i **Set** . Poniższy przykład kodu demonstruje sposób implementacji prostej właściwości w atrybucie.  
  
 [!code-cpp[Conceptual.Attributes.Usage#16](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#16)]
 [!code-csharp[Conceptual.Attributes.Usage#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#16)]
 [!code-vb[Conceptual.Attributes.Usage#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#16)]  
  
## <a name="custom-attribute-example"></a>Przykład atrybutu niestandardowego  
 Ta sekcja obejmuje poprzednie informacje i pokazuje sposób projektowania prostego atrybutu, który dokumentuje informacje o autorze sekcji kodu. Atrybut w tym przykładzie przechowuje nazwę i poziom programisty oraz czy kod został sprawdzony. Używa trzech prywatnych zmiennych do przechowywania rzeczywistych wartości do zapisania. Każda zmienna jest reprezentowana przez publiczną właściwość, która pobiera i ustawia wartości. Na koniec Konstruktor jest zdefiniowany przy użyciu dwóch wymaganych parametrów.  
  
 [!code-cpp[Conceptual.Attributes.Usage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#4)]
 [!code-csharp[Conceptual.Attributes.Usage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#4)]
 [!code-vb[Conceptual.Attributes.Usage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#4)]  
  
 Można zastosować ten atrybut przy użyciu pełnej nazwy, `DeveloperAttribute`lub przy użyciu skróconej nazwy, `Developer`, w jeden z następujących sposobów.  
  
 [!code-cpp[Conceptual.Attributes.Usage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#12)]
 [!code-csharp[Conceptual.Attributes.Usage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#12)]
 [!code-vb[Conceptual.Attributes.Usage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#12)]  
  
 Pierwszy przykład pokazuje atrybut zastosowany z tylko wymaganymi nazwanymi parametrami, podczas gdy drugi przykład pokazuje atrybut zastosowany do parametrów wymaganych i opcjonalnych.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>
- [Atrybuty](../../../docs/standard/attributes/index.md)
