---
title: Typy ogólne w .NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generic methods, type inference
- generics [.NET Framework], collections
- generic interfaces [.NET Framework]
- constructed generic types
- nested generic types
- generic type definitions
- generic classes [.NET Framework]
- generics [.NET Framework], interfaces
- generics [.NET Framework], about
- generics [.NET Framework]
- generic collections [.NET Framework]
- generic delegates [.NET Framework]
- generic type arguments
- generics [.NET Framework], delegates
- generics [.NET Framework], features
- constraints [.NET Framework]
- generic types
- generic type parameters
ms.assetid: 2994d786-c5c7-4666-ab23-4c83129fe39c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5c9f15a7ff30d5647338bf1954aca441b47281b5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69948738"
---
# <a name="generics-in-net"></a>Typy ogólne w .NET

<a name="top"></a>Typy ogólne umożliwiają dostosowanie metody, klasy, struktury lub interfejsu do precyzyjnego typu danych, na którym działa. Na przykład zamiast używać <xref:System.Collections.Hashtable> klasy, która umożliwia określenie kluczy i wartości dowolnego typu, można <xref:System.Collections.Generic.Dictionary%602> użyć klasy generycznej i określić typ dozwolony dla klucza i typ dozwolony dla tej wartości. Korzyści płynące z typów ogólnych to zwiększone wykorzystanie kodu i bezpieczeństwo typów.  
  
 Ten temat zawiera omówienie typów ogólnych w programie .NET oraz podsumowania rodzajów lub metod ogólnych. Ten temat zawiera następujące sekcje:  
  
- [Definiowanie i używanie typów ogólnych](#defining_and_using_generics)  
  
- [Terminologia ogólna](#generics_terminology)  
  
- [Obsługa biblioteki klas i języka](#class_library_and_language_support)  
  
- [Typy zagnieżdżone i generyczne](#nested_types_and_generics)  
  
- [Tematy pokrewne](#related_topics)  
  
- [Dokumentacja](#reference)  
  
<a name="defining_and_using_generics"></a>   
## <a name="defining-and-using-generics"></a>Definiowanie i używanie typów ogólnych  
 Typy ogólne to klasy, struktury, interfejsy i metody, które mają symbole zastępcze (parametry typu) dla jednego lub kilku typów, które są przez nie przechowywane lub używane. Klasa kolekcji generycznej może używać parametru typu jako symbolu zastępczego dla typu obiektów, które przechowuje; parametry typu są wyświetlane jako typy pól i typy parametrów jego metod. Metoda generyczna może używać swojego parametru typu jako typu wartości zwracanej lub jako typ jednego z jego parametrów formalnych. Poniższy kod ilustruje prostą definicję klasy ogólnej.  
  
 [!code-cpp[Conceptual.Generics.Overview#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#2)]
 [!code-csharp[Conceptual.Generics.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#2)]
 [!code-vb[Conceptual.Generics.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#2)]  
  
 Podczas tworzenia wystąpienia klasy generycznej należy określić rzeczywiste typy, które mają zostać zastąpione dla parametrów typu. Powoduje to ustanowienie nowej klasy generycznej, nazywanej klasą ogólną, z wybranymi typami, które zastępują wszędzie, że wyświetlane są parametry typu. Wynik jest bezpieczną klasą, która jest dostosowywana do wybranego typu, jak ilustruje poniższy kod.  
  
 [!code-cpp[Conceptual.Generics.Overview#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#3)]
 [!code-csharp[Conceptual.Generics.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#3)]
 [!code-vb[Conceptual.Generics.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#3)]  
  
<a name="generics_terminology"></a>   
### <a name="generics-terminology"></a>Terminologia ogólna  
 Poniższe terminy są używane do omówienia typów ogólnych w programie .NET:  
  
- *Definicja typu ogólnego* jest deklaracją klasy, struktury lub interfejsu, która działa jako szablon, z symbolami zastępczymi dla typów, które mogą zawierać lub używać. Na przykład <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> Klasa może zawierać dwa typy: klucze i wartości. Ponieważ definicja typu ogólnego jest tylko szablonem, nie można tworzyć wystąpień klasy, struktury lub interfejsu, który jest definicją typu ogólnego.  
  
- *Parametry typu ogólnego*lub *parametry typu*są symbolami zastępczymi w definicji typu ogólnego lub metody. Typ ogólny ma dwa parametry typu `TValue`, `TKey` który reprezentuje typy jego kluczy i wartości. <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>  
  
- *Skonstruowany typ ogólny*lub *skonstruowany*jest wynikiem określenia typów dla parametrów typu ogólnego definicji typu ogólnego.  
  
- *Argument typu ogólnego* jest dowolnego typu, który jest zastępowany dla parametru typu ogólnego.  
  
- Ogólny *Typ* ogólnego terminu obejmuje zarówno typy skonstruowane, jak i definicje typów ogólnych.  
  
- *Kowariancja* i *kontrawariancja* parametrów typu ogólnego umożliwiają używanie skonstruowanych typów ogólnych, których argumenty typu są bardziej pochodne (Kowariancja) lub mniej pochodne (kontrawariancja) niż docelowy typ skonstruowany. Kowariancja i kontrawariancja są określane zbiorczo jako *WARIANCJA*. Aby uzyskać więcej informacji, zobacz [Kowariancja i kontrawariancja](../../../docs/standard/generics/covariance-and-contravariance.md).  
  
- *Ograniczenia* są ograniczone do parametrów typu ogólnego. Można na przykład ograniczyć parametr typu do typów <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> implementujących interfejs ogólny, aby mieć pewność, że wystąpienia typu mogą być uporządkowane. Można również ograniczyć parametry typu do typów, które mają konkretną klasę bazową, które mają konstruktora bez parametrów lub które są typami referencyjnymi lub typami wartości. Użytkownicy typu ogólnego nie mogą wystawiać argumentów typu, które nie spełniają ograniczeń.  
  
- *Ogólna definicja metody* jest metodą z dwoma listami parametrów: listą parametrów typu ogólnego i listą parametrów formalnych. Parametry typu mogą występować jako zwracany typ lub jako typy parametrów formalnych, jak pokazano w poniższym kodzie.  
  
 [!code-cpp[Conceptual.Generics.Overview#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#4)]
 [!code-csharp[Conceptual.Generics.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#4)]
 [!code-vb[Conceptual.Generics.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#4)]  
  
 Metody generyczne mogą występować w typach generycznych lub nierodzajowych. Należy pamiętać, że metoda nie jest rodzajowa, tylko ponieważ należy do typu ogólnego, lub nawet ponieważ ma formalne parametry, których typy są parametrami ogólnymi typu otaczającego. Metoda jest generyczna tylko wtedy, gdy ma własną listę parametrów typu. W poniższym kodzie tylko Metoda `G` jest ogólna.  
  
 [!code-cpp[Conceptual.Generics.Overview#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#5)]
 [!code-csharp[Conceptual.Generics.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#5)]
 [!code-vb[Conceptual.Generics.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#5)]  
  
 [Powrót do początku](#top)  
  
<a name="advantages_limitations"></a>   
## <a name="advantages-and-disadvantages-of-generics"></a>Zalety i wady typów ogólnych  
 Istnieje wiele zalet używania ogólnych kolekcji i delegatów:  
  
- Bezpieczeństwo typu. Typy ogólne przesuwają obciążenie typu bezpieczeństwo od użytkownika do kompilatora. Nie ma potrzeby pisania kodu do przetestowania pod kątem poprawnego typu danych, ponieważ jest wymuszany w czasie kompilacji. Konieczne jest zmniejszenie liczby operacji rzutowania typów i możliwości błędów czasu wykonywania.  
  
- Mniej kod i kod są łatwiej ponownie używane. Nie ma potrzeby dziedziczenia z typu podstawowego i przesłonięcia elementów członkowskich. Na przykład, <xref:System.Collections.Generic.LinkedList%601> jest gotowy do natychmiastowego użycia. Na przykład można utworzyć połączoną listę ciągów z następującą deklaracją zmiennej:  
  
     [!code-cpp[HowToGeneric#24](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/source2.cpp#24)]
     [!code-csharp[HowToGeneric#24](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/source2.cs#24)]
     [!code-vb[HowToGeneric#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/source2.vb#24)]  
  
- Lepsza wydajność. Ogólne typy kolekcji są zwykle wykonywane lepiej w przypadku przechowywania i manipulowania typami wartości, ponieważ nie ma potrzeby umieszczania typów wartości.  
  
- Delegaty ogólne włączają bezpieczne dla typów wywołania zwrotne bez konieczności tworzenia wielu klas delegatów. Na <xref:System.Predicate%601> przykład Delegat ogólny umożliwia utworzenie metody implementującej własne kryteria wyszukiwania dla określonego typu i użycie metody z <xref:System.Array> metodami typu, takimi jak <xref:System.Array.Find%2A>, <xref:System.Array.FindLast%2A>, i <xref:System.Array.FindAll%2A> .  
  
- Typy ogólne upraszczają dynamicznie generowany kod. W przypadku używania typów ogólnych z dynamicznie generowanym kodem nie trzeba generować tego typu. Zwiększa to liczbę scenariuszy, w których można użyć uproszczonych metod dynamicznych zamiast generowania całych zestawów. Aby uzyskać więcej informacji, zobacz [jak: Definiowanie i wykonywanie metod](../../../docs/framework/reflection-and-codedom/how-to-define-and-execute-dynamic-methods.md) dynamicznych i. <xref:System.Reflection.Emit.DynamicMethod>  
  
 Poniżej przedstawiono niektóre ograniczenia dotyczące typów ogólnych:  
  
- Typy ogólne mogą pochodzić z większości klas bazowych, takich jak <xref:System.MarshalByRefObject> (i ograniczenia mogą służyć do wymagania, aby parametry typu ogólnego pochodzą z klas podstawowych, <xref:System.MarshalByRefObject>takich jak). Jednak .NET Framework nie obsługuje typów ogólnych powiązanych z kontekstem. Typ ogólny może pochodzić od <xref:System.ContextBoundObject>, ale próba utworzenia wystąpienia tego typu <xref:System.TypeLoadException>powoduje wystąpienie.  
  
- Wyliczenia nie mogą mieć parametrów typu ogólnego. Wyliczenie może być ogólne tylko zdarzenia (na przykład ponieważ jest zagnieżdżone w typie ogólnym, który jest definiowany przy użyciu Visual Basic, C#lub C++). Aby uzyskać więcej informacji, zobacz "wyliczenia" w [systemie Common Type System](../../../docs/standard/base-types/common-type-system.md).  
  
- Lekkie metody dynamiczne nie mogą być ogólne.  
  
- W Visual Basic, C#i C++, nie można utworzyć wystąpienia typu zagnieżdżonego, który jest ujęty w typ ogólny, chyba że typy zostały przypisane do parametrów typu wszystkich typów otaczających. Innym sposobem wymawiania tego jest to, że w odbiciu zagnieżdżony typ, który jest zdefiniowany przy użyciu tych języków, zawiera parametry typu dla wszystkich typów otaczających. Pozwala to na używanie parametrów typu otaczających typów, które mają być używane w definicjach elementów członkowskich typu zagnieżdżonego. Aby uzyskać więcej informacji, zobacz "typy zagnieżdżone" <xref:System.Type.MakeGenericType%2A>w temacie.  
  
    > [!NOTE]
    > Zagnieżdżony typ, który jest definiowany przez emitowanie kodu w zestawie dynamicznym lub przy użyciu [Ilasm. exe (ASEMBLER Il)](../../../docs/framework/tools/ilasm-exe-il-assembler.md) , nie jest wymagany do uwzględnienia parametrów typu otaczających je typów; Jednakże, jeśli nie zawiera ich, parametry typu nie znajdują się w zakresie klasy zagnieżdżonej.  
  
     Aby uzyskać więcej informacji, zobacz "typy zagnieżdżone" <xref:System.Type.MakeGenericType%2A>w temacie.  
  
 [Powrót do początku](#top)  
  
<a name="class_library_and_language_support"></a>   
## <a name="class-library-and-language-support"></a>Obsługa biblioteki klas i języka  
 Platforma .NET udostępnia szereg klas ogólnych kolekcji w następujących obszarach nazw:  
  
- Przestrzeń nazw zawiera większość ogólnych typów kolekcji dostarczonych przez platformę .NET, takich <xref:System.Collections.Generic.List%601> jak i <xref:System.Collections.Generic.Dictionary%602> klasy ogólne. <xref:System.Collections.Generic>  
  
- Przestrzeń nazw zawiera dodatkowe typy kolekcji ogólnych, takie <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> jak Klasa generyczna, które są przydatne do udostępniania modeli obiektów użytkownikom klas. <xref:System.Collections.ObjectModel>  
  
 Interfejsy ogólne do implementowania porównywania sortowania i równości są dostępne <xref:System> w przestrzeni nazw oraz z ogólnymi typami delegatów dla programów obsługi zdarzeń, konwersji i predykatów wyszukiwania.  
  
 Obsługa typów ogólnych została dodana do <xref:System.Reflection> przestrzeni nazw służących do badania typu ogólnego i metod ogólnych w celu <xref:System.Reflection.Emit> emitowania zestawów dynamicznych zawierających typy ogólne i metody oraz do <xref:System.CodeDom> generowania wykresów źródłowych obejmują one typy ogólne.  
  
 Środowisko uruchomieniowe języka wspólnego udostępnia nowe opcode i prefiksy do obsługi typów ogólnych w języku pośrednim firmy Microsoft (MSIL <xref:System.Reflection.Emit.OpCodes.Stelem>) <xref:System.Reflection.Emit.OpCodes.Ldelem>, <xref:System.Reflection.Emit.OpCodes.Unbox_Any>w <xref:System.Reflection.Emit.OpCodes.Constrained>tym, <xref:System.Reflection.Emit.OpCodes.Readonly>,,, i.  
  
 C++Wizualizacja C#, i Visual Basic wszystkie zapewniają pełną obsługę definiowania i używania typów ogólnych. Aby uzyskać więcej informacji na temat obsługi języków, zobacz [typy ogólne w Visual Basic](../../visual-basic/programming-guide/language-features/data-types/generic-types.md), [wprowadzenie do rodzajów ogólnych](../../csharp/programming-guide/generics/index.md)i [Omówienie typów ogólnych w C++wizualizacji ](/cpp/windows/overview-of-generics-in-visual-cpp).  
  
 [Powrót do początku](#top)  
  
<a name="nested_types_and_generics"></a>   
## <a name="nested-types-and-generics"></a>Typy zagnieżdżone i generyczne  
 Typ, który jest zagnieżdżony w typie ogólnym, może zależeć od parametrów typu otaczającego typu ogólnego. Środowisko uruchomieniowe języka wspólnego traktuje zagnieżdżone typy jako ogólne, nawet jeśli nie mają własnych parametrów typu ogólnego. Podczas tworzenia wystąpienia typu zagnieżdżonego należy określić argumenty typu dla wszystkich typów ogólnych.  
  
 [Powrót do początku](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Tematy pokrewne  
  
|Tytuł|Opis|  
|-----------|-----------------|  
|[Kolekcje ogólne w .NET](../../../docs/standard/generics/collections.md)|Opisuje ogólne klasy kolekcji i inne typy ogólne w programie .NET.|  
|[Delegaci ogólni do manipulowania tablicami i listami](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)|Zawiera opis ogólnych delegatów dla konwersji, predykatów wyszukiwania i akcji, które mają być podejmowane w elementach tablicy lub kolekcji.|  
|[Interfejsy ogólne](../../../docs/standard/generics/interfaces.md)|Opisuje ogólne interfejsy, które udostępniają typowe funkcje w różnych rodzinach typów ogólnych.|  
|[Kowariancja i kontrawariancja](../../../docs/standard/generics/covariance-and-contravariance.md)|Opisuje kowariancję i kontrawariancja w parametrach typu ogólnego.|  
|[Często używane typy kolekcji](../../../docs/standard/collections/commonly-used-collection-types.md)|Zawiera podsumowanie informacji o charakterystyce i scenariuszach użycia typów kolekcji w programie .NET, w tym typów ogólnych.|  
|[Kiedy należy używać kolekcji ogólnych](../../../docs/standard/collections/when-to-use-generic-collections.md)|Opisuje ogólne reguły określania, kiedy należy używać typów kolekcji generycznej.|  
|[Instrukcje: Definiowanie typu ogólnego przy użyciu emisji odbicia](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)|Wyjaśnia, jak generować dynamiczne zestawy, które zawierają typy ogólne i metody.|  
|[Typy ogólne w Visual Basic](../../visual-basic/programming-guide/language-features/data-types/generic-types.md)|Opisuje funkcję generyczną dla Visual Basic użytkowników, w tym Tematy porad dotyczących używania i definiowania typów ogólnych.|  
|[Wprowadzenie do typów ogólnych](../../csharp/programming-guide/generics/index.md)|Zawiera omówienie definiowania typów ogólnych dla C# użytkowników i korzystania z nich.|  
|[Przegląd typów ogólnych w Visual C++](/cpp/windows/overview-of-generics-in-visual-cpp)|Zawiera opis funkcji ogólnych dla C++ użytkowników, w tym różnice między rodzajami i szablonami.|  
  
<a name="reference"></a>   
## <a name="reference"></a>Tematy pomocy  
 <xref:System.Collections.Generic>  
  
 <xref:System.Collections.ObjectModel>  
  
 <xref:System.Reflection.Emit.OpCodes?displayProperty=nameWithType>  
  
 [Powrót do początku](#top)
