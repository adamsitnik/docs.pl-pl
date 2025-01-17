---
title: Migrowanie aplikacji ze Sklepu Windows do architektury .NET Native
ms.date: 03/30/2017
ms.assetid: 4153aa18-6f56-4a0a-865b-d3da743a1d05
ms.openlocfilehash: 1942574e832ca7593d91c71370cc0af0c3051617
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73455613"
---
# <a name="migrate-your-windows-store-app-to-net-native"></a>Migrowanie aplikacji ze sklepu Windows do .NET Native

.NET Native zapewnia statyczną kompilację aplikacji w Sklepie Windows lub na komputerze dewelopera. Różni się to od kompilacji dynamicznej wykonywanej dla aplikacji ze sklepu Windows przez kompilator just-in-Time (JIT) lub [natywny Generator obrazu (Ngen. exe)](../tools/ngen-exe-native-image-generator.md) na urządzeniu. Pomimo różnic, .NET Native próbuje zachować zgodność z [platformą .NET dla aplikacji ze sklepu Windows](https://docs.microsoft.com/previous-versions/windows/apps/br230302%28v=vs.140%29). W większości przypadków elementy, które działają na platformie .NET dla aplikacji ze sklepu Windows, działają również z .NET Native.  Jednak w niektórych przypadkach mogą wystąpić zmiany behawioralne. W tym dokumencie omówiono różnice między standardową platformą .NET dla aplikacji ze sklepu Windows i .NET Native w następujących obszarach:

- [Ogólne różnice w środowisku uruchomieniowym](#Runtime)

- [Różnice w programowaniu dynamicznym](#Dynamic)

- [Inne różnice dotyczące odbicia](#Reflection)

- [Nieobsługiwane scenariusze i interfejsy API](#Unsupported)

- [Różnice w programie Visual Studio](#VS)

<a name="Runtime"></a>

## <a name="general-runtime-differences"></a>Ogólne różnice w środowisku uruchomieniowym

- Wyjątki, takie jak <xref:System.TypeLoadException>, które są generowane przez kompilator JIT, gdy aplikacja jest uruchamiana w środowisku uruchomieniowym języka wspólnego (CLR) zazwyczaj powoduje błędy w czasie kompilacji w przypadku przetworzenia przez .NET Native.

- Nie wywołuj metody <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> z wątku interfejsu użytkownika aplikacji. Może to spowodować zakleszczenie .NET Native.

- Nie należy polegać na kolejności wywołania konstruktora klasy statycznej. W .NET Native kolejność wywoływania różni się od kolejności w standardowym środowisku uruchomieniowym. (Nawet w przypadku standardowego środowiska uruchomieniowego nie należy polegać na kolejności wykonywania konstruktorów klas statycznych).

- Nieskończona pętla bez wykonywania wywołania (na przykład `while(true);`) w dowolnym wątku może spowodować zatrzymanie aplikacji. Podobnie duże lub nieskończone oczekiwania mogą spowodować zatrzymanie aplikacji.

- Niektóre ogólne cykle inicjowania nie generują wyjątków w .NET Native. Na przykład poniższy kod zgłasza wyjątek <xref:System.TypeLoadException> w standardowym środowisku CLR. W .NET Native nie jest.

  [!code-csharp[ProjectN#8](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat1.cs#8)]

- W niektórych przypadkach .NET Native oferuje różne implementacje bibliotek klasy .NET Framework. Obiekt zwrócony z metody zawsze implementuje elementy członkowskie zwracanego typu. Jednak ze względu na to, że jego implementacja zapasowa jest inna, można nie być w stanie rzutować go na ten sam zestaw typów, co w przypadku innych platform .NET Framework. Na przykład w niektórych przypadkach może nie być możliwe rzutowanie obiektu interfejsu <xref:System.Collections.Generic.IEnumerable%601> zwróconego przez metody, takie jak <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=nameWithType> lub <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=nameWithType> do `T[]`.

- Pamięć podręczna usługi WinInet nie jest domyślnie włączona w programie .NET dla aplikacji ze sklepu Windows, ale jest włączona .NET Native. Poprawia to wydajność, ale ma implikacje dla zestawu roboczego. Nie jest wymagana żadna akcja dewelopera.

<a name="Dynamic"></a>

## <a name="dynamic-programming-differences"></a>Różnice w programowaniu dynamicznym

.NET Native statycznie linki w kodzie z .NET Framework, aby udostępnić kod aplikacji w celu uzyskania maksymalnej wydajności. Jednak rozmiary binarne muszą pozostać małe, więc nie można wykonać całego .NET Framework. Kompilator .NET Native rozwiązuje to ograniczenie przy użyciu funkcji zmniejszającej zależność, która usuwa odwołania do nieużywanego kodu. Jednak .NET Native mogą nie obsługiwać ani generować informacji o typie i kodzie, gdy te informacje nie mogą zostać wywnioskowane statycznie w czasie kompilacji, ale zamiast tego są pobierane dynamicznie w czasie wykonywania.

.NET Native umożliwia programowanie odbicia i dynamicznego. Jednak nie wszystkie typy mogą być oznaczone do odbicia, ponieważ spowodowałoby to, że rozmiar wygenerowanego kodu jest zbyt duży (szczególnie ze względu na to, że jest obsługiwane odbicie w publicznych interfejsach API w .NET Framework). Kompilator .NET Native umożliwia inteligentne wybór typów, które powinny obsługiwać odbicie, i utrzymuje metadane i generuje kod tylko dla tych typów.

Na przykład powiązanie danych wymaga, aby aplikacja mogła mapować nazwy właściwości do funkcji. W programie .NET dla aplikacji do sklepu Windows środowisko uruchomieniowe języka wspólnego automatycznie używa odbicia w celu zapewnienia tej możliwości dla typów zarządzanych i publicznie dostępnych typów natywnych. W .NET Native kompilator automatycznie zawiera metadane dla typów, do których są powiązane dane.

Kompilator .NET Native może również obsługiwać powszechnie używane typy ogólne, takie jak <xref:System.Collections.Generic.List%601> i <xref:System.Collections.Generic.Dictionary%602>, które działają bez konieczności stosowania jakichkolwiek wskazówek lub dyrektyw. [Dynamiczne](../../csharp/language-reference/builtin-types/reference-types.md#the-dynamic-type) słowo kluczowe jest również obsługiwane w ramach pewnych limitów.

> [!NOTE]
> Należy dokładnie przetestować wszystkie dynamiczne ścieżki kodu podczas przenoszenia aplikacji do .NET Native.

Domyślna konfiguracja .NET Native jest wystarczająca dla większości deweloperów, ale niektórzy deweloperzy mogą chcieć dostosować konfiguracje przy użyciu pliku dyrektywy środowiska uruchomieniowego (. Rd. xml). Ponadto w niektórych przypadkach kompilator .NET Native nie jest w stanie określić, które metadane muszą być dostępne do odbicia, i opierają się na wskazówkach, szczególnie w następujących przypadkach:

- Niektórych konstrukcji, takich jak <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> i <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType>, nie można określić statycznie.

- Ponieważ kompilator nie może określić wystąpień, typ ogólny, który ma być uwzględniany, musi być określony przez dyrektywy środowiska uruchomieniowego. To nie tylko dlatego, że cały kod musi być uwzględniony, ale odbicie na typach ogólnych może tworzyć nieskończony cykl (na przykład gdy metoda ogólna jest wywoływana w typie ogólnym).

> [!NOTE]
> Dyrektywy środowiska uruchomieniowego są zdefiniowane w pliku dyrektywy środowiska uruchomieniowego (. Rd. xml). Aby uzyskać ogólne informacje na temat korzystania z tego pliku, zobacz [wprowadzenie](getting-started-with-net-native.md). Aby uzyskać informacje o dyrektywach środowiska uruchomieniowego, zobacz [Dokumentacja pliku konfiguracji dyrektyw środowiska uruchomieniowego (RD. xml)](runtime-directives-rd-xml-configuration-file-reference.md).

.NET Native również zawiera narzędzia profilowania, które ułatwiają deweloperom określenie, które typy poza domyślnym zestawem powinny obsługiwać odbicie.

<a name="Reflection"></a>

## <a name="other-reflection-related-differences"></a>Inne różnice dotyczące odbicia

Istnieje wiele innych różnic dotyczących zachowań między platformą .NET dla aplikacji do sklepu Windows i .NET Native.

W .NET Native:

- Prywatne odbicie typów i elementów członkowskich w bibliotece klas .NET Framework nie jest obsługiwane. Można jednak odzwierciedlić własne typy prywatne i członków, a także typy i elementy członkowskie w bibliotekach innych firm.

- Właściwość <xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=nameWithType> prawidłowo zwraca `false` dla obiektu <xref:System.Reflection.ParameterInfo>, który reprezentuje wartość zwracaną. W programie .NET dla aplikacji ze sklepu Windows zwraca `true`. Język pośredni (IL) nie obsługuje tego bezpośrednio, a interpretacja pozostała do języka.

- Publiczne składowe w strukturach <xref:System.RuntimeFieldHandle> i <xref:System.RuntimeMethodHandle> nie są obsługiwane. Te typy są obsługiwane tylko dla LINQ, drzew wyrażeń i inicjalizacji tablicy statycznej.

- <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=nameWithType> i <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=nameWithType> obejmują ukryte składowe w klasach bazowych, więc mogą zostać zastąpione bez jawnych zastąpień. Jest to również prawdziwe w przypadku innych metod [RuntimeReflectionExtensions. GetRuntime *](xref:System.Reflection.RuntimeReflectionExtensions) .

- <xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> i <xref:System.Type.MakeByRefType%2A?displayProperty=nameWithType> nie powiodą się podczas próby utworzenia niektórych kombinacji (na przykład tablicy ByRef).

- Nie można używać odbicia do wywoływania elementów członkowskich, które mają parametry wskaźnika.

- Nie można użyć odbicia w celu pobrania lub ustawienia pola wskaźnika.

- Gdy liczba argumentów jest nieprawidłowa i typ jednego z argumentów jest niepoprawny, .NET Native generuje <xref:System.ArgumentException> zamiast <xref:System.Reflection.TargetParameterCountException>.

- Serializacja binarna wyjątków zazwyczaj nie jest obsługiwana. W związku z tym do słownika <xref:System.Exception.Data%2A?displayProperty=nameWithType> można dodać obiekty, które nie są możliwe do serializacji.

<a name="Unsupported"></a>

## <a name="unsupported-scenarios-and-apis"></a>Nieobsługiwane scenariusze i interfejsy API

W poniższych sekcjach zamieszczono listę nieobsługiwanych scenariuszy i interfejsów API na potrzeby ogólnego programowania, międzyoperacyjności i technologii, takich jak HTTPClient i Windows Communication Foundation (WCF):

- [Opracowywanie ogólne](#General)

- [HttpClient](#HttpClient)

- [Interop](#Interop)

- [Nieobsługiwane interfejsy API](#APIs)

<a name="General"></a>

### <a name="general-development-differences"></a>Ogólne różnice w programowaniu

**Typy wartości**

- W przypadku zastąpienia metod <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> i <xref:System.ValueType.GetHashCode%2A?displayProperty=nameWithType> dla typu wartości nie należy wywoływać implementacji klas podstawowych. W programie .NET dla aplikacji do sklepu Windows te metody polegają na odbiciu. W czasie kompilacji .NET Native generuje implementację, która nie polega na odbiciu w czasie wykonywania. Oznacza to, że jeśli nie zastąpisz tych dwóch metod, będą one działały zgodnie z oczekiwaniami, ponieważ .NET Native generuje implementację w czasie kompilacji. Jednak zastąpienie tych metod, ale wywołanie implementacji klasy bazowej powoduje wyjątek.

- Typy wartości większe niż jeden megabajt nie są obsługiwane.

- Typy wartości nie mogą mieć konstruktora bez parametrów w .NET Native. (C# i Visual Basic zabraniać konstruktorów bez parametrów w typach wartości. Można je jednak utworzyć w języku IL.)

**Tablice**

- Tablice z dolną granicą inną niż zero nie są obsługiwane. Zwykle te tablice są tworzone przez wywołanie przeciążenia <xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=nameWithType>.

- Dynamiczne tworzenie tablic wielowymiarowych nie jest obsługiwane. Takie tablice są zwykle tworzone przez wywołanie przeciążenia metody <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType>, która zawiera parametr `lengths` lub przez wywołanie metody <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=nameWithType>.

- Tablice wielowymiarowe, które mają co najmniej cztery wymiary, nie są obsługiwane. oznacza to, że ich <xref:System.Array.Rank%2A?displayProperty=nameWithType> wartość właściwości jest równa co najmniej cztery. Zamiast tego używaj [tablic nieregularnych](../../csharp/programming-guide/arrays/jagged-arrays.md) (tablicowych tablic). Na przykład `array[x,y,z]` jest nieprawidłowy, ale `array[x][y][z]` nie jest.

- WARIANCJA dla tablic wielowymiarowych nie jest obsługiwana i powoduje wyjątek <xref:System.InvalidCastException> w czasie wykonywania.

**Typy ogólne**

- Nieskończone rozwijanie typów ogólnych powoduje błąd kompilatora. Na przykład następujący kod nie zostanie skompilowany:

  [!code-csharp[ProjectN#9](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat2.cs#9)]

**Wskaźniki**

- Tablice wskaźników nie są obsługiwane.

- Nie można użyć odbicia w celu pobrania lub ustawienia pola wskaźnika.

**Serializacja**

Atrybut <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> nie jest obsługiwany. Zamiast tego użyj atrybutu <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29>.

**Zasoby**

Użycie zlokalizowanych zasobów z klasą <xref:System.Diagnostics.Tracing.EventSource> nie jest obsługiwane. Właściwość <xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=nameWithType> nie definiuje zlokalizowanych zasobów.

**Delegaci**

`Delegate.BeginInvoke` i `Delegate.EndInvoke` nie są obsługiwane.

**Różne interfejsy API**

- Właściwośćname [. GUID](xref:System.Type.GUID) zgłasza wyjątek <xref:System.PlatformNotSupportedException>, jeśli atrybut <xref:System.Runtime.InteropServices.GuidAttribute> nie jest stosowany do typu. Identyfikator GUID jest używany głównie do obsługi modelu COM.

- Metoda <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> prawidłowo analizuje ciągi zawierające daty krótkie w .NET Native. Jednak nie zachowuje zgodności z zmianami dotyczącymi analizy daty i godziny opisanej w artykułach bazy wiedzy Microsoft [KB2803771](https://support.microsoft.com/kb/2803771) i [KB2803755](https://support.microsoft.com/kb/2803755).

- `("E")` <xref:System.Numerics.BigInteger.ToString%2A?displayProperty=nameWithType> jest prawidłowo zaokrąglona w .NET Native. W niektórych wersjach środowiska CLR ciąg wynikowy jest obcinany zamiast zaokrąglania.

<a name="HttpClient"></a>

### <a name="httpclient-differences"></a>Różnice HttpClient

W .NET Native Klasa <xref:System.Net.Http.HttpClientHandler> wewnętrznie używa interfejsu WinINet (za pośrednictwem klasy <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter>) zamiast klas <xref:System.Net.WebRequest> i <xref:System.Net.WebResponse> używanych w standardowym środowisku .NET dla aplikacji do sklepu Windows.  Usługa WinINet nie obsługuje wszystkich opcji konfiguracji obsługiwanych przez klasę <xref:System.Net.Http.HttpClientHandler>.  W efekcie:

- Niektóre właściwości możliwości na <xref:System.Net.Http.HttpClientHandler> zwracają `false` na .NET Native, podczas gdy zwracają `true` w standardowym programie .NET dla aplikacji ze sklepu Windows.

- Niektóre właściwości konfiguracji `get` metod dostępu zawsze zwracają stałą wartość na .NET Native, która różni się od domyślnej konfigurowalnej wartości w programie .NET dla aplikacji ze sklepu Windows.

Niektóre dodatkowe różnice w zachowaniu zostały omówione w poniższych podsekcjach.

**Serwera proxy**

Klasa <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> nie obsługuje konfigurowania ani zastępowania serwera proxy dla poszczególnych żądań.  Oznacza to, że wszystkie żądania dotyczące .NET Native korzystają z serwera proxy skonfigurowany systemowo lub bez serwera proxy, w zależności od wartości właściwości <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=nameWithType>.  W programie .NET dla aplikacji do sklepu Windows serwer proxy jest zdefiniowany przez właściwość <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType>.  Na .NET Native ustawienie <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> na wartość inną niż `null` zgłasza wyjątek <xref:System.PlatformNotSupportedException>.  Właściwość <xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=nameWithType> zwraca `false` na .NET Native, podczas gdy zwraca `true` w standardowym .NET Framework dla aplikacji ze sklepu Windows.

**Automatyczne przekierowanie**

Klasa <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> nie zezwala na skonfigurowanie maksymalnej liczby przekierowań automatycznych.  Wartość właściwości <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=nameWithType> jest domyślnie 50 w standardowym środowisku .NET dla aplikacji ze sklepu Windows i można ją modyfikować. Na .NET Native wartość tej właściwości wynosi 10 i próba zmodyfikowania spowoduje zgłoszenie wyjątku <xref:System.PlatformNotSupportedException>.  Właściwość <xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=nameWithType> zwraca `false` na .NET Native, podczas gdy zwraca `true` w programie .NET dla aplikacji ze sklepu Windows.

**Automatyczna dekompresja**

Platforma .NET dla aplikacji do sklepu Windows pozwala ustawić właściwość <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=nameWithType> na <xref:System.Net.DecompressionMethods.Deflate>, <xref:System.Net.DecompressionMethods.GZip>, <xref:System.Net.DecompressionMethods.Deflate> i <xref:System.Net.DecompressionMethods.GZip>lub <xref:System.Net.DecompressionMethods.None>.  .NET Native obsługuje tylko <xref:System.Net.DecompressionMethods.Deflate> razem z <xref:System.Net.DecompressionMethods.GZip>lub <xref:System.Net.DecompressionMethods.None>.  Podjęto próbę ustawienia właściwości <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> na <xref:System.Net.DecompressionMethods.Deflate> lub <xref:System.Net.DecompressionMethods.GZip> autonomicznie ustawia ją na <xref:System.Net.DecompressionMethods.Deflate> i <xref:System.Net.DecompressionMethods.GZip>.

**Plik cookie**

Obsługa plików cookie jest wykonywana jednocześnie przez <xref:System.Net.Http.HttpClient> i WinINet.  Pliki cookie z <xref:System.Net.CookieContainer> są łączone z plikami cookie w pamięci podręcznej plików cookie WinINet.  Usunięcie pliku cookie z <xref:System.Net.CookieContainer> zapobiega wysyłaniu plików cookie przez <xref:System.Net.Http.HttpClient>, ale jeśli plik cookie był już widziany przez program WinINet, a pliki cookie nie zostały przez niego usunięte.  Nie można programowo usunąć pliku cookie z usługi WinINet przy użyciu interfejsu API <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.HttpClientHandler>lub <xref:System.Net.CookieContainer>.  Ustawienie właściwości <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=nameWithType> na `false` powoduje, że tylko <xref:System.Net.Http.HttpClient> zatrzymać wysyłanie plików cookie; Usługa WinINet może nadal zawierać swoje pliki cookie w żądaniu.

**Uwierzytelniające**

W programie .NET dla aplikacji ze sklepu Windows właściwości <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=nameWithType> i <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=nameWithType> działają niezależnie.  Ponadto Właściwość <xref:System.Net.Http.HttpClientHandler.Credentials%2A> akceptuje każdy obiekt, który implementuje interfejs <xref:System.Net.ICredentials>.  W .NET Native ustawienie właściwości <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> na `true` powoduje, że właściwość <xref:System.Net.Http.HttpClientHandler.Credentials%2A> stanie się `null`.  Ponadto Właściwość <xref:System.Net.Http.HttpClientHandler.Credentials%2A> można ustawić tylko dla `null`, <xref:System.Net.CredentialCache.DefaultCredentials%2A>lub obiektu typu <xref:System.Net.NetworkCredential>.  Przypisanie dowolnego innego obiektu <xref:System.Net.ICredentials>, najpopularniejszy <xref:System.Net.CredentialCache>, do właściwości <xref:System.Net.Http.HttpClientHandler.Credentials%2A> zgłasza <xref:System.PlatformNotSupportedException>.

**Inne nieobsługiwane lub niekonfigurowalne funkcje**

W .NET Native:

- Wartość właściwości <xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=nameWithType> jest zawsze <xref:System.Net.Http.ClientCertificateOption.Automatic>.  W programie .NET dla aplikacji do sklepu Windows wartość domyślna to <xref:System.Net.Http.ClientCertificateOption.Manual>.

- Nie można skonfigurować właściwości <xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=nameWithType>.

- Właściwość <xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=nameWithType> jest zawsze `true`.  W programie .NET dla aplikacji do sklepu Windows wartość domyślna to `false`.

- Nagłówek `SetCookie2` w odpowiedziach jest ignorowany jako przestarzały.

<a name="Interop"></a>
### <a name="interop-differences"></a>Różnice międzyoperacyjnych
 **Przestarzałe interfejsy API**

 Wiele rzadko używanych interfejsów API do współdziałania z kodem zarządzanym jest przestarzałe. W przypadku korzystania z .NET Native te interfejsy API mogą zgłosić wyjątek <xref:System.NotImplementedException> lub <xref:System.PlatformNotSupportedException> lub spowodować błąd kompilatora. W programie .NET dla aplikacji ze sklepu Windows te interfejsy API są oznaczane jako przestarzałe, chociaż wywołanie ich powoduje wygenerowanie ostrzeżenia kompilatora, a nie błędu kompilatora.

 Przestarzałe interfejsy API do organizowania `VARIANT` obejmują:

- <xref:System.Runtime.InteropServices.BStrWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VariantWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VarEnum?displayProperty=nameWithType>

 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> jest obsługiwana, ale zgłasza wyjątek w niektórych scenariuszach, na przykład gdy jest używany z wariantami [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) lub ByRef.

 Przestarzałe interfejsy API obsługi [interfejsu IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) obejmują:

- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType>

Przestarzałe interfejsy API dla klasycznych zdarzeń COM obejmują:

- <xref:System.Runtime.InteropServices.ComEventsHelper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>

Przestarzałe interfejsy API w interfejsie <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType>, które nie są obsługiwane w .NET Native, obejmują:

- <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> (wszystkie elementy członkowskie)
- <xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=nameWithType> (wszystkie elementy członkowskie)
- <xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=nameWithType> (wszystkie elementy członkowskie)
- <xref:System.Runtime.InteropServices.Marshal.GetComInterfaceForObject%28System.Object%2CSystem.Type%2CSystem.Runtime.InteropServices.CustomQueryInterfaceMode%29?displayProperty=fullName>

Inne Nieobsługiwane funkcje międzyoperacyjności obejmują:

- <xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=nameWithType> (wszystkie elementy członkowskie)
- <xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=nameWithType> (wszystkie elementy członkowskie)
- <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AnsiBStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AsAny?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.CustomMarshaler?displayProperty=fullName>

 Rzadko używane kierowanie interfejsów API:

- <xref:System.Runtime.InteropServices.Marshal.ReadByte%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt16%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt32%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt64%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadIntPtr%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteByte%28System.Object%2CSystem.Int32%2CSystem.Byte%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt16%28System.Object%2CSystem.Int32%2CSystem.Int16%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt32%28System.Object%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt64%28System.Object%2CSystem.Int32%2CSystem.Int64%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteIntPtr%28System.Object%2CSystem.Int32%2CSystem.IntPtr%29?displayProperty=fullName>

 **Wywołanie platformy i zgodność z modelem COM**

 Większość scenariuszy wywołania i międzyoperacyjności platformy COM jest nadal obsługiwana w .NET Native. W szczególności obsługiwane są wszystkie współdziałanie z interfejsami API środowisko wykonawcze systemu Windows (WinRT) i wszystkie elementy Marshaling wymagane dla środowisko wykonawcze systemu Windows. Obejmuje to kierowanie wsparcie dla:

- Tablice (w tym <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType>)

- `BStr`

- Delegaty

- Ciągi (Unicode, ANSI i HSTRING)

- Struktury (`byref` i `byval`)

- Unie

- Uchwyty Win32

- Wszystkie konstrukcje WinRT

- Częściowa obsługa organizowania typów wariantów. Obsługiwane są następujące elementy:

  - <xref:System.Boolean>

  - <xref:System.Byte>

  - <xref:System.Decimal>

  - <xref:System.Double>

  - <xref:System.Int16>

  - <xref:System.Int32>

  - <xref:System.Int64>

  - <xref:System.SByte>

  - <xref:System.Single>

  - <xref:System.UInt16>

  - <xref:System.UInt32>

  - <xref:System.UInt64>

  - `BStr`

  - [IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)

Jednak .NET Native nie obsługuje następujących funkcji:

- Używanie klasycznych zdarzeń COM

- Implementowanie interfejsu <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> w typie zarządzanym

- Implementowanie interfejsu [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) w typie zarządzanym za pomocą atrybutu <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType>. Należy jednak pamiętać, że nie można wywoływać obiektów COM za poorednictwem `IDispatch`, a obiekt zarządzany nie może zaimplementować `IDispatch`.

Używanie odbicia do wywołania metody Invoke platformy nie jest obsługiwane. To ograniczenie można obejść przez zapakowanie wywołania metody w innej metodzie i użycie odbicia w celu wywołania otoki.

<a name="APIs"></a>

### <a name="other-differences-from-net-apis-for-windows-store-apps"></a>Inne różnice dotyczące interfejsów API platformy .NET dla aplikacji ze sklepu Windows

Ta sekcja zawiera listę pozostałych interfejsów API, które nie są obsługiwane w programie .NET Native. Największym zestawem nieobsługiwanych interfejsów API są Windows Communication Foundation (WCF) interfejsy API.

**Adnotacje DataAnnotations (System. ComponentModel. DataAnnotations)**

Typy w <xref:System.ComponentModel.DataAnnotations> i <xref:System.ComponentModel.DataAnnotations.Schema> przestrzenie nazw nie są obsługiwane w .NET Native. Należą do nich następujące typy, które są obecne w programie .NET dla aplikacji ze sklepu Windows dla systemu Windows 8:

- <xref:System.ComponentModel.DataAnnotations.AssociationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ConcurrencyCheckAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.CustomValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataType?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataTypeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayColumnAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayFormatAttribute>
- <xref:System.ComponentModel.DataAnnotations.EditableAttribute>
- <xref:System.ComponentModel.DataAnnotations.EnumDataTypeAttribute>
- <xref:System.ComponentModel.DataAnnotations.FilterUIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.KeyAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RangeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RequiredAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.StringLengthAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.TimestampAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.UIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationContext?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationResult?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Validator?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedOption?displayProperty=nameWithType>

 **Visual Basic**

Visual Basic nie jest obecnie obsługiwana w .NET Native. Następujące typy w przestrzeniach nazw <xref:Microsoft.VisualBasic> i <xref:Microsoft.VisualBasic.CompilerServices> nie są dostępne w .NET Native:

- <xref:Microsoft.VisualBasic.CallType?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Constants?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.HideModuleNameAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.DesignerGeneratedAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.IncompleteInitialization?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.NewLateBinding?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl.ForLoopControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Operators?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionCompareAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionTextAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ProjectData?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StandardModuleAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StaticLocalInitFlag?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Utils?displayProperty=nameWithType>

**Kontekst odbicia (przestrzeń nazw System. odbicie. Context)**

Klasa <xref:System.Reflection.Context.CustomReflectionContext?displayProperty=nameWithType> nie jest obsługiwana w .NET Native.

**RTC (System .NET. http. RTC)**

Klasa `System.Net.Http.RtcRequestFactory` nie jest obsługiwana w .NET Native.

**Windows Communication Foundation (WCF) (System. ServiceModel.\*)**

Typy w [przestrzeniach nazw System. ServiceModel. *](xref:System.ServiceModel) nie są obsługiwane w .NET Native. Należą do nich następujące typy:

- <xref:System.ServiceModel.ActionNotSupportedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpMessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.BeginOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.ChannelBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.EndOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.InvokeAsyncCompletedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationState?displayProperty=nameWithType>
- <xref:System.ServiceModel.DataContractFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.DnsEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddress?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddressBuilder?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=nameWithType>
- <xref:System.ServiceModel.EnvelopeVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.ExceptionDetail?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultCode?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReason?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReasonText?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpBindingBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.IDefaultCommunicationTimeouts?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtension%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensionCollection%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.InvalidMessageContractException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageBodyMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeader%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeaderException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverTcp?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpMessageEncoding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContextScope?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationFormatStyle?displayProperty=nameWithType>
- <xref:System.ServiceModel.ProtocolException?displayProperty=nameWithType>
- <xref:System.ServiceModel.QuotaExceededException?displayProperty=nameWithType>
- <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServerTooBusyException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceActivationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceKnownTypeAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.SpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TransferMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.UnknownMessageReceivedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.UpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeaderCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressingVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelManagerBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelParameterCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.FaultConverter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpRequestMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpResponseMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IHttpCookieContainerManager?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageBuffer?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoder?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoderFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaderInfo?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaders?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageProperties?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageState?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.RequestContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityHeaderLayout?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportUsage?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ClientCredentials?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageBodyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDirection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.EndpointDispatcher?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientOperationSelector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.BasicSecurityProfileVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.HttpDigestClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecureConversationVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityAccessDeniedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityPolicyVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.TrustVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.WindowsClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.UserNameSecurityTokenParameters?displayProperty=nameWithType>

### <a name="differences-in-serializers"></a>Różnice w serializatorach

Poniższe różnice dotyczą serializacji i deserializacji z klasami <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>i <xref:System.Xml.Serialization.XmlSerializer>:

- W .NET Native, <xref:System.Runtime.Serialization.DataContractSerializer> i <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> nie można serializować lub deserializować klasy pochodnej, która ma składową klasy bazowej, której typ nie jest typem serializacji głównej. Na przykład w poniższym kodzie próba serializacji lub deserializacji `Y` powoduje błąd:

  [!code-csharp[ProjectN#10](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat3.cs#10)]

  Typ `InnerType` nie jest znany do serializatora, ponieważ elementy członkowskie klasy bazowej nie są przenoszone podczas serializacji.

- <xref:System.Runtime.Serialization.DataContractSerializer> i <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> nie można serializować klasy lub struktury implementującej interfejs <xref:System.Collections.Generic.IEnumerable%601>. Na przykład następujące typy nie mogą serializować lub deserializować:

- <xref:System.Xml.Serialization.XmlSerializer> nie może serializować następującej wartości obiektu, ponieważ nie zna dokładnego typu obiektu do serializacji:

- nie można serializować lub deserializować <xref:System.Xml.Serialization.XmlSerializer>, jeśli typ serializowanego obiektu jest <xref:System.Xml.XmlQualifiedName>.

- Wszystkie serializatory (<xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>i <xref:System.Xml.Serialization.XmlSerializer>) nie generują kodu serializacji dla <xref:System.Xml.Linq.XElement?displayProperty=nameWithType> typu lub dla typu, który zawiera <xref:System.Xml.Linq.XElement>. Wyświetlają one błędy czasu kompilacji.

- Następujące konstruktory typów serializacji nie gwarantują działania zgodnie z oczekiwaniami:

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.DataContractSerializerSettings%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Xml.XmlDictionaryString%2CSystem.Xml.XmlDictionaryString%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.Json.DataContractJsonSerializerSettings%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.String%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlRootAttribute%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%2CSystem.Type%5B%5D%2CSystem.Xml.Serialization.XmlRootAttribute%2CSystem.String%29?displayProperty=nameWithType>

- <xref:System.Xml.Serialization.XmlSerializer> nie może wygenerować kodu dla typu, który ma metody przypisane do żadnego z następujących atrybutów:

  - <xref:System.Runtime.Serialization.OnSerializingAttribute>

  - <xref:System.Runtime.Serialization.OnSerializedAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializingAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializedAttribute>

- <xref:System.Xml.Serialization.XmlSerializer> nie honoruje <xref:System.Xml.Serialization.IXmlSerializable> niestandardowego interfejsu serializacji. Jeśli masz klasę, która implementuje ten interfejs, <xref:System.Xml.Serialization.XmlSerializer> traktuje typ zwykłego starego obiektu CLR (POCO) i serializować tylko jego właściwości publiczne.

- Serializacja prostego obiektu <xref:System.Exception> nie działa dobrze z <xref:System.Runtime.Serialization.DataContractSerializer> i <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.

<a name="VS"></a>

## <a name="visual-studio-differences"></a>Różnice w programie Visual Studio

**Wyjątki i debugowanie**

Gdy uruchamiasz Aplikacje skompilowane przy użyciu .NET Native w debugerze, wyjątki pierwszej szansy są włączone dla następujących typów wyjątków:

- <xref:System.MemberAccessException>

- <xref:System.TypeAccessException>

**Tworzenie aplikacji**

Użyj narzędzi kompilacji x86, które są używane domyślnie przez program Visual Studio. Nie zalecamy korzystania z narzędzi MSBuild AMD64, które znajdują się w folderze C:\Program Files (x86) \MSBuild\12.0\bin\amd64; może to spowodować problemy z kompilacją.

**Profilery**

- Profiler procesora CPU programu Visual Studio i Profiler pamięci XAML nie wyświetlają poprawnie kodu "tylko mój kod".

- Profiler pamięci XAML nie wyświetla prawidłowo danych sterty zarządzanej.

- Program profilujący procesora nie zidentyfikuje prawidłowo modułów i wyświetla nazwy funkcji poprzedzone prefiksem.

**Projekty biblioteki testów jednostkowych**

Włączanie .NET Native w bibliotece testów jednostkowych dla projektu aplikacji ze sklepu Windows nie jest obsługiwane i powoduje, że kompilacja nie powiedzie się.

## <a name="see-also"></a>Zobacz także

- [Wprowadzenie](getting-started-with-net-native.md)
- [Dokumentacja pliku konfiguracji dyrektyw środowiska uruchomieniowego (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Omówienie programu .NET dla aplikacji do sklepu Windows](https://docs.microsoft.com/previous-versions/windows/apps/br230302%28v=vs.140%29)
- [Obsługa programu .NET Framework dla aplikacji ze Sklepu Windows i środowiska wykonawczego systemu Windows](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
