---
title: Konwersja typów w programie .NET Framework
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- widening conversions
- explicit conversions
- narrowing conversions
- type conversion, about type conversion
- type conversion
- converting types
- narrowing coercion
- Explicit operator
- IConvertible interface
- base types, converting
- op_Implicit method
- widening coercion
- op_Explicit method
- Convert class
- implicit conversions
- Implicit operator
- data types [.NET Framework], converting
ms.assetid: ba36154f-064c-47d3-9f05-72f93a7ca96d
ms.openlocfilehash: b125b3c6527da405deb600ba7334ef18220f1601
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73132878"
---
# <a name="type-conversion-in-the-net-framework"></a>Konwersja typów w programie .NET Framework
<a name="top"></a>Każda wartość ma skojarzony typ, który definiuje atrybuty, takie jak ilość miejsca przydzieloną do wartości, zakres możliwych wartości, które może mieć, oraz członków, które udostępnia. Wiele wartości można wyrazić za pomocą co najmniej dwóch typów. Na przykład wartość 4 może być wyrażona jako liczba całkowita lub wartość zmiennoprzecinkowa. Konwersja typu tworzy wartość nowego typu, która jest równoważna wartości starego typu, ale nie zawsze powoduje zachowanie tożsamości (dokładnej wartości) oryginalnego obiektu.  
  
 .NET Framework automatycznie obsługuje następujące konwersje:  
  
- Konwersja z klasy pochodnej na klasę bazową. Oznacza to, na przykład, że wystąpienie dowolnej klasy lub struktury można przekonwertować na wystąpienie <xref:System.Object>.  Ta konwersja nie wymaga operatora rzutowania ani konwersji.  
  
- Konwersja z klasy bazowej z powrotem do oryginalnej klasy pochodnej. W C#programie ta konwersja wymaga operatora rzutowania. W Visual Basic wymaga operatora `CType`, jeśli `Option Strict` jest włączona.  
  
- Konwersja z typu, który implementuje interfejs do obiektu interfejsu, który reprezentuje ten interfejs. Ta konwersja nie wymaga operatora rzutowania ani konwersji.  
  
- Konwersja z obiektu interfejsu z powrotem do oryginalnego typu, który implementuje ten interfejs.  W C#programie ta konwersja wymaga operatora rzutowania. W Visual Basic wymaga operatora `CType`, jeśli `Option Strict` jest włączona.  
  
 Oprócz tych automatycznych konwersji .NET Framework udostępnia kilka funkcji, które obsługują konwersję typów niestandardowych. Należą do nich między innymi:  
  
- Operator `Implicit`, który definiuje dostępne rozszerzenia konwersji między typami. Aby uzyskać więcej informacji, zobacz sekcję [niejawna konwersja z niejawnym operatorem](#implicit_conversion_with_the_implicit_operator) .  
  
- Operator `Explicit`, który definiuje dostępne konwersje wąskie między typami. Aby uzyskać więcej informacji, zobacz [jawna konwersja za pomocą jawnego operatora](#explicit_conversion_with_the_explicit_operator) .  
  
- Interfejs <xref:System.IConvertible>, który definiuje konwersje do poszczególnych typów danych .NET Framework podstawowych. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [interfejsu obiektem IConvertible](#the_iconvertible_interface) .  
  
- Klasa <xref:System.Convert>, która dostarcza zestaw metod implementujących metody w interfejsie <xref:System.IConvertible>. Aby uzyskać więcej informacji, zobacz sekcję [konwertowanie klasy](#Convert) .  
  
- Klasa <xref:System.ComponentModel.TypeConverter>, która jest klasą bazową, która może zostać rozszerzona w celu obsługi konwersji określonego typu do dowolnego innego typu. Aby uzyskać więcej informacji, zobacz sekcję [Klasa TypeConverter](#the_typeconverter_class) .  
  
<a name="implicit_conversion_with_the_implicit_operator"></a>   
## <a name="implicit-conversion-with-the-implicit-operator"></a>Niejawna konwersja za pomocą operatora Implicit  
 Konwersje rozszerzające obejmują utworzenie nowej wartości z wartości istniejącego typu, która ma bardziej ograniczony zakres lub bardziej ograniczoną listę elementów członkowskich niż typ docelowy. Konwersje rozszerzające nie mogą powodować utraty danych (chociaż mogą powodować utratę dokładności). Dane nie mogą być tracone, więc kompilatory mogą obsługiwać konwersję niejawnie (niewidocznie), dzięki czemu użytkownik nie musi używać jawnej metody konwersji ani operatora rzutowania.  
  
> [!NOTE]
> Mimo że kod wywołujący niejawną konwersję może wywołać metodę konwersji lub użyć operatora rzutowania, ich użycie nie jest wymagane przez kompilatory obsługujące konwersje niejawne.  
  
 Na przykład typ <xref:System.Decimal> obsługuje konwersje niejawne z <xref:System.Byte>, <xref:System.Char>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.UInt16>, <xref:System.UInt32>i <xref:System.UInt64> wartości. Poniższy przykład ilustruje niektóre z tych niejawnych konwersji podczas przypisywania wartości do zmiennej <xref:System.Decimal>.  
  
 [!code-csharp[Conceptual.Conversion#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#1)]
 [!code-vb[Conceptual.Conversion#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#1)]  
  
 Jeśli kompilator określonego języka obsługuje operatory niestandardowe, niejawne konwersje można także definiować we własnych typach niestandardowych. Poniższy przykład zawiera częściową implementację typu danych bajtu ze znakiem o nazwie `ByteWithSign`, która używa reprezentacji i wielkości liter. Obsługuje ona niejawną konwersję wartości <xref:System.Byte> i <xref:System.SByte> na wartości `ByteWithSign`.  
  
 [!code-csharp[Conceptual.Conversion#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#2)]
 [!code-vb[Conceptual.Conversion#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#2)]  
  
 Kod klienta może następnie zadeklarować zmienną `ByteWithSign` i przypisać ją <xref:System.Byte> i <xref:System.SByte> wartości bez wykonywania jakichkolwiek jawnych konwersji lub użycia operatorów rzutowania, jak pokazano w poniższym przykładzie.  
  
 [!code-csharp[Conceptual.Conversion#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#3)]
 [!code-vb[Conceptual.Conversion#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#3)]  
  
 [Powrót do początku](#top)  
  
<a name="explicit_conversion_with_the_explicit_operator"></a>   
## <a name="explicit-conversion-with-the-explicit-operator"></a>Jawna konwersja za pomocą operatora Explicit  
 Konwersje zawężające obejmują utworzenie nowej wartości z wartości istniejącego typu, która ma większy zakres lub większą listę elementów członkowskich niż typ docelowy. Konwersja zawężająca może spowodować utratę danych, więc kompilatory często wymagają, aby taka konwersja została wykonana jawnie za pomocą wywołania metody konwersji lub operatora rzutowania. Oznacza to, że konwersja musi być jawnie obsługiwana w kodzie dewelopera.  
  
> [!NOTE]
> Najważniejszym celem wymaganie metody konwersji lub operatora rzutowania dla konwersji zawężania jest umożliwienie deweloperowi świadomości utraty danych lub <xref:System.OverflowException>, tak aby można było obsługiwać je w kodzie. Jednak niektóre kompilatory umożliwiają nieprzestrzeganie tego wymagania. Na przykład w Visual Basic, jeśli `Option Strict` jest wyłączone (ustawienie domyślne), kompilator Visual Basic próbuje wykonać konwersje zawęża niejawnie.  
  
 Na przykład typy danych <xref:System.UInt32>, <xref:System.Int64>i <xref:System.UInt64> mają zakresy, które przekraczają typ danych <xref:System.Int32>, jak pokazano w poniższej tabeli.  
  
|Typ|Porównanie z zakresem typu Int32|  
|----------|------------------------------------|  
|<xref:System.Int64>|<xref:System.Int64.MaxValue?displayProperty=nameWithType> jest większa niż <xref:System.Int32.MaxValue?displayProperty=nameWithType>, a <xref:System.Int64.MinValue?displayProperty=nameWithType> jest mniejsza niż (ma większy zakres ujemny niż) <xref:System.Int32.MinValue?displayProperty=nameWithType>.|  
|<xref:System.UInt32>|<xref:System.UInt32.MaxValue?displayProperty=nameWithType> jest większa niż <xref:System.Int32.MaxValue?displayProperty=nameWithType>.|  
|<xref:System.UInt64>|<xref:System.UInt64.MaxValue?displayProperty=nameWithType> jest większa niż <xref:System.Int32.MaxValue?displayProperty=nameWithType>.|  
  
 Aby obsłużyć takie Konwersje, .NET Framework zezwala na typy do definiowania operatora `Explicit`. Kompilatory poszczególnych języków mogą następnie zaimplementować tego operatora przy użyciu własnej składni lub można wywołać element członkowski klasy <xref:System.Convert>, aby wykonać konwersję. (Aby uzyskać więcej informacji na temat klasy <xref:System.Convert>, zapoznaj [się z klasą Convert](#Convert) w dalszej części tego tematu.) Poniższy przykład ilustruje użycie funkcji języka do obsługi jawnej konwersji tych wartości całkowitych, które potencjalnie poza zakresem, do wartości <xref:System.Int32>.  
  
 [!code-csharp[Conceptual.Conversion#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#4)]
 [!code-vb[Conceptual.Conversion#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#4)]  
  
 Konwersje jawne mogą generować różne wyniki w różnych językach, a wyniki te mogą się różnić od wartości zwracanej przez odpowiadającą metodę <xref:System.Convert>. Na przykład jeśli <xref:System.Double> wartość 12,63251 jest konwertowana na <xref:System.Int32>, metoda Visual Basic `CInt` i .NET Framework <xref:System.Convert.ToInt32%28System.Double%29?displayProperty=nameWithType> Metoda zaokrągla <xref:System.Double>, aby zwracała wartość 13, ale operator C# `(int)` obcina <xref:System.Double> do Zwróć wartość 12. Podobnie operator C# `(int)` nie obsługuje konwersji typu Boolean na liczbę całkowitą, ale metoda Visual Basic `CInt` konwertuje wartość `true` na-1. Z drugiej strony Metoda <xref:System.Convert.ToInt32%28System.Boolean%29?displayProperty=nameWithType> konwertuje wartość `true` na 1.  
  
 Większość kompilatorów zezwala na wykonywanie jawnych konwersji w sposób kontrolowany i niekontrolowany. Gdy sprawdzona konwersja jest wykonywana, zostanie wygenerowane <xref:System.OverflowException>, gdy wartość typu do przekonwertowania jest spoza zakresu typu docelowego. Gdy w tych samych warunkach jest wykonywania konwersja niekontrolowana, konwersja może nie zgłosić wyjątku, ale dokładne zachowanie jest niezdefiniowane i może powstać niepoprawna wartość.  
  
> [!NOTE]
> W C#programie sprawdzone konwersje można wykonać za pomocą słowa kluczowego `checked` razem z operatorem rzutowania lub określając opcję kompilatora `/checked+`. Z drugiej strony konwersje niesprawdzone można wykonać za pomocą słowa kluczowego `unchecked` razem z operatorem rzutowania lub określając opcję kompilatora `/checked-`. Domyślnie konwersje jawne są niekontrolowane. W Visual Basic sprawdzone konwersje można wykonać, czyszcząc pole wyboru **Usuń sprawdzanie przepełnienia liczby całkowitej** w oknie dialogowym **Zaawansowane ustawienia kompilatora** projektu lub określając opcję kompilatora `/removeintchecks-`. Z drugiej strony konwersje niesprawdzone można wykonać, zaznaczając pole wyboru **Usuń sprawdzanie przepełnienia liczby całkowitej** w oknie dialogowym **Zaawansowane ustawienia kompilatora** projektu lub określając opcję kompilatora `/removeintchecks+`. Domyślnie konwersje jawne są kontrolowane.  
  
 W poniższym C# przykładzie za pomocą słów kluczowych `checked` i `unchecked` są zilustrowane różnice w zachowaniu, gdy wartość spoza zakresu <xref:System.Byte> jest konwertowana na <xref:System.Byte>. Sprawdzona konwersja zgłasza wyjątek, ale niesprawdzona konwersja przypisuje <xref:System.Byte.MaxValue?displayProperty=nameWithType> do zmiennej <xref:System.Byte>.  
  
 [!code-csharp[Conceptual.Conversion#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#12)]  
  
 Jeśli kompilator danego języka obsługuje niestandardowe operatory przeciążone, konwersje jawne można także definiować we własnych typach niestandardowych. Poniższy przykład zawiera częściową implementację typu danych bajtu ze znakiem o nazwie `ByteWithSign`, która używa reprezentacji i wielkości liter. Obsługuje ona jawną konwersję wartości <xref:System.Int32> i <xref:System.UInt32> na wartości `ByteWithSign`.  
  
 [!code-csharp[Conceptual.Conversion#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#5)]
 [!code-vb[Conceptual.Conversion#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#5)]  
  
 Kod klienta może następnie zadeklarować zmienną `ByteWithSign` i przypisać ją <xref:System.Int32> i <xref:System.UInt32> wartości, jeśli przypisania zawierają operator rzutowania lub metodę konwersji, jak pokazano w poniższym przykładzie.  
  
 [!code-csharp[Conceptual.Conversion#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#6)]
 [!code-vb[Conceptual.Conversion#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#6)]  
  
 [Powrót do początku](#top)  
  
<a name="the_iconvertible_interface"></a>   
## <a name="the-iconvertible-interface"></a>Interfejs IConvertible  
 Aby zapewnić obsługę konwersji dowolnego typu na typ podstawowy środowiska uruchomieniowego języka wspólnego, .NET Framework zapewnia interfejs <xref:System.IConvertible>. Typ implementujący musi dostarczyć następujące elementy:  
  
- Metoda zwracająca <xref:System.TypeCode> typu implementującego.  
  
- Metody konwersji typu implementującego na każdy typ podstawowy środowiska uruchomieniowego języka wspólnego (<xref:System.Boolean>, <xref:System.Byte>, <xref:System.DateTime>, <xref:System.Decimal>, <xref:System.Double>itd.).  
  
- Uogólnioną metodę konwersji służącą do konwertowania wystąpienia typu implementującego na inny określony typ. Konwersje, które nie są obsługiwane, powinny zgłosić <xref:System.InvalidCastException>.  
  
 Każdy typ podstawowy środowiska uruchomieniowego języka wspólnego (czyli <xref:System.Boolean>, <xref:System.Byte>, <xref:System.Char>, <xref:System.DateTime>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single><xref:System.String>, <xref:System.UInt16>, <xref:System.UInt32>i <xref:System.UInt64>), a także typy <xref:System.DBNull> i <xref:System.Enum>, implementują interfejs <xref:System.IConvertible>. Są to jednak jawne implementacje interfejsu; metodę konwersji można wywołać tylko za pomocą zmiennej interfejsu <xref:System.IConvertible>, jak pokazano w poniższym przykładzie. Ten przykład konwertuje wartość <xref:System.Int32> na odpowiadającą jej wartość <xref:System.Char>.  
  
 [!code-csharp[Conceptual.Conversion#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible1.cs#7)]
 [!code-vb[Conceptual.Conversion#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible1.vb#7)]  
  
 Wymaganie, aby metoda konwersji była wywoływana w jej interfejsie, a nie w typie implementującym, powoduje, że jawne implementacje interfejsu są relatywnie kosztowne. Zamiast tego zalecamy, aby wywoływać odpowiedni element członkowski klasy <xref:System.Convert> do konwersji między typami podstawowymi środowiska uruchomieniowego języka wspólnego. Aby uzyskać więcej informacji, zobacz następną sekcję [klasy Convert](#Convert).  
  
> [!NOTE]
> Oprócz interfejsu <xref:System.IConvertible> i klasy <xref:System.Convert> dostarczonej przez .NET Framework poszczególne języki mogą również zapewniać sposoby wykonywania konwersji. Na przykład C# używa operatorów rzutowania; Visual Basic używa funkcji konwersji implementowanych przez kompilator, takich jak `CType`, `CInt`i `DirectCast`.  
  
 W większości przypadków interfejs <xref:System.IConvertible> jest przeznaczony do obsługi konwersji między typami podstawowymi w .NET Framework. Jednak ten interfejs może też być implementowany przez typ niestandardowy w celu obsługi konwersji tego typu na inny typ niestandardowy. Aby uzyskać więcej informacji, zobacz sekcję [konwersje niestandardowe przy użyciu metody ChangeType](#ChangeType) w dalszej części tego tematu.  
  
 [Powrót do początku](#top)  
  
<a name="Convert"></a>   
## <a name="the-convert-class"></a>Klasa Convert  
 Chociaż implementacja interfejsu <xref:System.IConvertible> poszczególnych typów podstawowych może być wywoływana w celu wykonania konwersji typu, wywoływanie metod klasy <xref:System.Convert?displayProperty=nameWithType> jest zalecanym sposobem konwersji z jednego typu podstawowego na inny. Ponadto Metoda <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=nameWithType> może służyć do konwersji z określonego typu niestandardowego na inny typ.  
  
### <a name="conversions-between-base-types"></a>Konwersje między typami podstawowymi  
 Klasa <xref:System.Convert> zapewnia neutralną językowo sposób wykonywania konwersji między typami podstawowymi i jest dostępna dla wszystkich języków przeznaczonych dla środowiska uruchomieniowego języka wspólnego. Zawiera kompletny zestaw metod zarówno do rozszerzania, jak i zawężania konwersji, i zgłasza <xref:System.InvalidCastException> dla konwersji, które nie są obsługiwane (na przykład konwersja wartości <xref:System.DateTime> do wartości całkowitej). Konwersje wąskie są wykonywane w sprawdzonym kontekście, a w przypadku niepowodzenia konwersji zostanie wygenerowany <xref:System.OverflowException>.  
  
> [!IMPORTANT]
> Ponieważ Klasa <xref:System.Convert> obejmuje metody konwersji do i z każdego typu podstawowego, eliminuje konieczność wywołania <xref:System.IConvertible> jawnej implementacji interfejsu każdego typu podstawowego.  
  
 Poniższy przykład ilustruje użycie klasy <xref:System.Convert?displayProperty=nameWithType> w celu wykonania kilku konwersji rozszerzających i zawężających między .NET Framework typów podstawowych.  
  
 [!code-csharp[Conceptual.Conversion#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/convert1.cs#8)]
 [!code-vb[Conceptual.Conversion#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/convert1.vb#8)]  
  
 W niektórych przypadkach, zwłaszcza w przypadku konwersji do i z wartości zmiennoprzecinkowych, konwersja może pociągnąć za niego utratę precyzji, nawet jeśli nie generuje <xref:System.OverflowException>. W poniższym przykładzie pokazano taką utratę dokładności. W pierwszym przypadku wartość <xref:System.Decimal> ma mniejszą precyzję (mniejszą liczbę cyfr), gdy jest konwertowana na <xref:System.Double>. W drugim przypadku <xref:System.Double> wartość jest zaokrąglana z 42,72 do 43, aby zakończyć konwersję.  
  
 [!code-csharp[Conceptual.Conversion#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/convert1.cs#9)]
 [!code-vb[Conceptual.Conversion#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/convert1.vb#9)]  
  
 Dla tabeli zawierającej konwersje rozszerzające i zawężające obsługiwane przez klasę <xref:System.Convert>, zobacz [tabele konwersji typów](../../../docs/standard/base-types/conversion-tables.md).  
  
<a name="ChangeType"></a>   
### <a name="custom-conversions-with-the-changetype-method"></a>Konwersje niestandardowe z użyciem metody ChangeType  
 Oprócz obsługi konwersji do poszczególnych typów podstawowych, Klasa <xref:System.Convert> może służyć do konwersji typu niestandardowego na jeden lub więcej wstępnie zdefiniowanych typów. Ta konwersja jest wykonywana przez metodę <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=nameWithType>, która z kolei zawija wywołanie metody <xref:System.IConvertible.ToType%2A?displayProperty=nameWithType> parametru `value`. Oznacza to, że obiekt reprezentowany przez parametr `value` musi zapewniać implementację interfejsu <xref:System.IConvertible>.  
  
> [!NOTE]
> Ponieważ <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%29?displayProperty=nameWithType> i <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=nameWithType> metody używają obiektu <xref:System.Type> do określenia typu docelowego, do którego `value` jest konwertowana, mogą służyć do przeprowadzenia dynamicznej konwersji do obiektu, którego typ nie jest znany w czasie kompilacji. Należy jednak pamiętać, że implementacja <xref:System.IConvertible> `value` musi nadal obsługiwać tę konwersję.  
  
 Poniższy przykład ilustruje możliwe implementację interfejsu <xref:System.IConvertible>, który umożliwia konwertowanie obiektu `TemperatureCelsius` na obiekt `TemperatureFahrenheit` i na odwrót. W przykładzie zdefiniowano klasę bazową `Temperature`, która implementuje interfejs <xref:System.IConvertible> i zastępuje metodę <xref:System.Object.ToString%2A?displayProperty=nameWithType>. Klasy pochodne `TemperatureCelsius` i `TemperatureFahrenheit` każdy przesłania `ToType` i metody `ToString` klasy bazowej.  
  
 [!code-csharp[Conceptual.Conversion#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible2.cs#10)]
 [!code-vb[Conceptual.Conversion#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible2.vb#10)]  
  
 Poniższy przykład ilustruje kilka wywołań tych <xref:System.IConvertible> implementacji, aby skonwertować obiekty `TemperatureCelsius` do `TemperatureFahrenheit` obiektów i na odwrót.  
  
 [!code-csharp[Conceptual.Conversion#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible2.cs#11)]
 [!code-vb[Conceptual.Conversion#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible2.vb#11)]  
  
 [Powrót do początku](#top)  
  
<a name="the_typeconverter_class"></a>   
## <a name="the-typeconverter-class"></a>Klasa TypeConverter  
 .NET Framework umożliwia również zdefiniowanie konwertera typów dla typu niestandardowego przez rozszerzenie klasy <xref:System.ComponentModel.TypeConverter?displayProperty=nameWithType> i skojarzenie konwertera typów z typem za pomocą atrybutu <xref:System.ComponentModel.TypeConverterAttribute?displayProperty=nameWithType>. W poniższej tabeli przedstawiono różnice między tym podejściem a implementacją interfejsu <xref:System.IConvertible> dla typu niestandardowego.  
  
> [!NOTE]
> Obsługa typu niestandardowego w czasie projektowania jest możliwa tylko wtedy, gdy zdefiniowano dla niego konwerter typów.  
  
|Konwersja z użyciem klasy TypeConverter|Konwersja z użyciem interfejsu IConvertible|  
|------------------------------------|-----------------------------------|  
|Jest zaimplementowany dla niestandardowego typu przez wyznaczanie oddzielnej klasy z <xref:System.ComponentModel.TypeConverter>. Ta klasa pochodna jest skojarzona z typem niestandardowym przez zastosowanie atrybutu <xref:System.ComponentModel.TypeConverterAttribute>.|Jest implementowana przez typ niestandardowy w celu wykonania konwersji. Użytkownik typu wywołuje metodę konwersji <xref:System.IConvertible> typu.|  
|Może być używana w czasie projektowania i w czasie wykonywania.|Może być używana tylko w czasie wykonywania.|  
|Używa odbicia; w związku z tym jest wolniejsza niż konwersja włączona przez <xref:System.IConvertible>.|Nie używa odbicia.|  
|Umożliwia dwukierunkowe konwersje typów z typu niestandardowego na inne typy danych i z innych typów danych na typ niestandardowy. Na przykład <xref:System.ComponentModel.TypeConverter> zdefiniowane dla `MyType` umożliwia konwersje z `MyType` na <xref:System.String>oraz od <xref:System.String> `MyType`.|Umożliwia konwersję z typu niestandardowego na inne typy danych, ale nie z innych typów danych na typ niestandardowy.|  
  
 Aby uzyskać więcej informacji o używaniu konwerterów typów do wykonywania konwersji, zobacz <xref:System.ComponentModel.TypeConverter?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Convert?displayProperty=nameWithType>
- <xref:System.IConvertible>
- [Tabele konwersji typów](../../../docs/standard/base-types/conversion-tables.md)
