---
title: Testowanie aplikacji ASP.NET Core MVC
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Testowanie aplikacji ASP.NET Core MVC
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 9bc97efdda44ca4dfa4a583c32e9e55c9502d975
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73089693"
---
# <a name="test-aspnet-core-mvc-apps"></a>Testowanie aplikacji ASP.NET Core MVC

> *"Jeśli nie podoba Ci się testowanie jednostkowe produktu, najprawdopodobniej nie chcesz przetestować go."*
 > \_-Anonymous-

Oprogramowanie dowolnej złożoności może zakończyć się niepowodzeniem na nieoczekiwanych sposobach w reakcji na zmiany. W ten sposób testowanie po wprowadzeniu zmian jest wymagane dla wszystkich, ale najbardziej prostych (lub najmniej krytycznych) aplikacji. Testowanie ręczne to najwolniejsze, najmniej niezawodne, najbardziej kosztowne rozwiązanie do testowania oprogramowania. Niestety, jeśli aplikacje nie mają być weryfikowalne, może to być tylko dostępne. Aplikacje, które zostały wykonane zgodnie z zasadami architektury określonymi w [rozdziale 4](architectural-principles.md) , powinny być weryfikowalne jednostkowe, a aplikacje ASP.NET Core obsługują również zautomatyzowaną integrację i testowanie funkcjonalne.

## <a name="kinds-of-automated-tests"></a>Rodzaje testów automatycznych

Istnieje wiele rodzajów zautomatyzowanych testów dla aplikacji oprogramowania. Najprostszym, najniższym poziomem testu jest test jednostkowy. Na nieco wyższym poziomie istnieją testy integracji i testy funkcjonalne. Inne rodzaje testów, takie jak testy interfejsu użytkownika, testy obciążeniowe, testy obciążeniowe i testy dymu, wykraczają poza zakres tego dokumentu.

### <a name="unit-tests"></a>Testy jednostkowe

Test jednostkowy testów pojedynczej części logiki aplikacji. Jeden z nich może jeszcze bardziej opisać, wyświetlając niektóre z tych rzeczy. Test jednostkowy nie testuje, w jaki sposób kod współpracuje z zależnościami lub infrastrukturą — to są testy integracji. Test jednostkowy nie przetestuje struktury kodu, w którym jest on pisany — należy zastanowić się, że działa lub, jeśli okaże się, że nie, należy zgłosić błąd i napisać obejście problemu. Test jednostkowy jest całkowicie wykonywany w pamięci i w procesie. Nie komunikuje się z systemem plików, siecią lub bazą danych. Testy jednostkowe powinny tylko testować kod.

Testy jednostkowe, na mocy których testuje tylko jedną jednostkę kodu bez zależności zewnętrznych, powinny być wykonywane bardzo szybko. Z tego względu powinno być możliwe uruchamianie zestawów testów dla setek testów jednostkowych w ciągu kilku sekund. Uruchamiaj je często, najlepiej przed każdym wypchnięciem do udostępnionego repozytorium kontroli źródła i z pewnością przy każdej zautomatyzowanej kompilacji na serwerze kompilacji.

### <a name="integration-tests"></a>Testy integracji

Chociaż dobrym pomysłem jest Hermetyzowanie kodu, który współdziała z infrastrukturą, taką jak bazy danych i systemy plików, nadal będziesz mieć część tego kodu i prawdopodobnie chcesz go przetestować. Ponadto należy sprawdzić, czy warstwy kodu działają w oczekiwany sposób, gdy zależności aplikacji są w pełni rozwiązane. Jest to odpowiedzialność za testy integracji. Testy integracji są znacznie wolniejsze i trudniejsze do skonfigurowania niż testy jednostkowe, ponieważ często zależą od zewnętrznych zależności i infrastruktury. W tym celu należy unikać testowania, które mogą być testowane przy użyciu testów jednostkowych w testach integracji. Jeśli można testować dany scenariusz z testem jednostkowym, należy przetestować go z testem jednostkowym. Jeśli nie jest to możliwe, rozważ użycie testu integracji.

Testy integracji często mają bardziej skomplikowane ustawienia i usuwania procedury niż testy jednostkowe. Na przykład test integracji, który przechodzi względem rzeczywistej bazy danych, będzie wymagał metody przywrócenia bazy danych do znanego stanu przed każdym uruchomieniem testu. Po dodaniu nowych testów, a produkcyjny schemat bazy danych, te skrypty te zależą od rozmiaru i złożoności. W wielu dużych systemach nie ma praktycznego uruchamiania pełnych zestawów testów integracji na stacjach roboczych deweloperów przed zaewidencjonowaniem zmian w udostępnionej kontroli źródła. W takich przypadkach testy integracji mogą być uruchamiane na serwerze kompilacji.

### <a name="functional-tests"></a>Testy funkcjonalne

Testy integracji są napisywane od perspektywy dewelopera, aby sprawdzić, czy niektóre składniki systemu działają prawidłowo. Testy funkcjonalne są zapisywane z perspektywy użytkownika i sprawdzają poprawność systemu w zależności od wymagań. Poniższy fragment przedstawia przydatną funkcję analogową do rozważania, jak należy wziąć pod uwagę testy funkcjonalne w porównaniu z testami jednostkowymi:

> "Wiele razy rozwój systemu jest likened do budynku w domu. Chociaż ta wartość analogiczna nie jest poprawna, możemy ją rozłożyć na potrzeby ustalenia różnicy między testami jednostkowymi i funkcjonalnymi. Testy jednostkowe są analogiczne do Inspektora konstrukcyjnego odwiedzającego witrynę konstrukcyjną domu. Koncentruje się na różnych systemach wewnętrznych, fundamentach, ramkach, elektrycznych, wodociągowych i tak dalej. Gwarantuje (testy), że części domu będą działały prawidłowo i bezpiecznie, czyli spełniają kod budynku. Testy funkcjonalne w tym scenariuszu są analogiczne do Homeowner odwiedzania tej samej lokacji konstrukcja. Przyjęto założenie, że systemy wewnętrzne będą działać odpowiednio, że Inspektor budynku wykonuje jego zadanie. Homeowner koncentruje się na tym, co będzie wyglądać na żywo w tym domu. Ma ona wpływ na wygląd domu, czy różne pokoje są wygodne, czy najlepiej odpowiadają potrzebom rodziny, czy w systemie Windows jest dobrym miejscem, aby przechwycić rano Sun. Homeowner wykonuje testy funkcjonalne w domu. Ma perspektywę użytkownika. Inspektor budowlany przeprowadza testy jednostkowe w domu. Ma perspektywę konstruktora ".

Źródło: [testowanie jednostkowe i testy funkcjonalne](https://www.softwaretestingtricks.com/2007/01/unit-testing-versus-functional-tests.html)

Fond się powiedzieć "jako Deweloperzy, ale kończymy się niepowodzeniem na dwa sposoby: możemy utworzyć niewłaściwy element lub stworzyć niewłaściwy element". Testy jednostkowe gwarantują, że tworzysz to prawo; testy funkcjonalne zapewniają, że tworzysz odpowiednie rzeczy.

Ponieważ testy funkcjonalne działają na poziomie systemu, mogą wymagać pewnego stopnia automatyzacji interfejsu użytkownika. Podobnie jak w przypadku testów integracji, zazwyczaj działają one również w przypadku niektórych rodzajów infrastruktury testowej. Sprawia to wolniejsze i bardziej kruchy niż testy jednostkowe i integracji. Należy mieć tylko tyle testów funkcjonalnych, ile trzeba mieć pewność, że system zachowuje się, gdy użytkownicy oczekują.

### <a name="testing-pyramid"></a>Piramida testowania

Fowlera Martin na temat ostrosłupa testowego, którego przykład przedstawiono na rysunku 9-1.

![Piramida testowania](./media/image9-1.png)

**Rysunek 9-1**. Piramida testowania

Różne warstwy ostrosłupa i ich względne rozmiary reprezentują różne rodzaje testów oraz liczbę elementów, które należy napisać dla aplikacji. Jak widać, zalecenie ma mieć dużą podstawę testów jednostkowych, które są obsługiwane przez niższą warstwę testów integracji, z jeszcze mniejszą warstwą testów funkcjonalnych. Każda warstwa powinna mieć idealny tylko testy, które nie mogą być wykonywane odpowiednio na niższej warstwie. Zadbaj o to, aby określić, jakiego rodzaju testu potrzebujesz w konkretnym scenariuszu.

### <a name="what-to-test"></a>Co należy przetestować

Typowy problem dla deweloperów, którzy są niedoświadczeni z pisaniem zautomatyzowanych testów, jest tworzony z przeznaczeniem do przetestowania. Dobrym punktem początkowym jest Testowanie logiki warunkowej. Wszędzie tam, gdzie masz metodę z zachowaniem, które zmienia się w zależności od instrukcji warunkowej (if-else, Switch itp.), powinna być dostępna co najmniej kilka testów, które potwierdzają poprawne zachowanie określonych warunków. Jeśli kod zawiera warunki błędu, warto napisać co najmniej jeden test dla "silnej ścieżki" przez kod (bez błędów) i co najmniej jeden test dla "ścieżki sad" (z błędami lub nietypowymi wynikami), aby potwierdzić, że aplikacja działa zgodnie z oczekiwaniami w przypadku błędów. Na koniec spróbuj skupić się na testowaniu rzeczy, które mogą się nie powieść, zamiast skupić się na metrykach, takich jak pokrycie kodu. Większa ilość pokrycia kodu jest lepsza niż mniej, ogólnie. Jednak zapisanie kilku dodatkowych testów bardzo złożonej i krytycznej dla firmy jest zwykle lepszym sposobem korzystania z czasu niż podczas pisania testów dla właściwości samodzielnych, co pozwala ulepszyć metryki pokrycia kodu testowego.

## <a name="organizing-test-projects"></a>Organizowanie projektów testowych

Projekty testowe mogą być zorganizowane, jednak najlepiej sprawdzają się. Dobrym pomysłem jest oddzielenie testów według typu (test jednostkowy, test integracji) i ich testowanie (według projektu, według przestrzeni nazw). Czy ta separacja składa się z folderów w ramach pojedynczego projektu testowego lub wielu projektów testowych, stanowi decyzję projektową. Jeden projekt jest najprostszy, ale w przypadku dużych projektów z wieloma testami lub w celu łatwiejszego uruchamiania różnych zestawów testów można chcieć mieć kilka różnych projektów testowych. Wiele zespołów organizuje projekty testowe na podstawie testowanego projektu, co w przypadku aplikacji z więcej niż kilkoma projektami może spowodować powstanie dużej liczby projektów testowych, szczególnie w przypadku, gdy te dane są nadal dzielone zgodnie z typem testów w każdym projekcie. Podejście do kompromisu polega na tym, że jeden projekt dla każdego rodzaju testu, na aplikację, z folderami w projektach testowych, ma wskazywać testowany projekt (i klasę).

Typowym podejściem jest organizowanie projektów aplikacji w folderze "src" i projektów testowych aplikacji w ramach równoległego folderu "Tests". Można utworzyć dopasowane foldery rozwiązań w programie Visual Studio, jeśli okaże się to przydatne w tej organizacji.

![Testowanie organizacji w rozwiązaniu](./media/image9-2.png)

**Rysunek 9-2**. Testowanie organizacji w rozwiązaniu

Możesz użyć niezależnej platformy testowej. Środowisko xUnit Framework działa prawidłowo i jest zapisywana wszystkie ASP.NET Core i EF Core testy. Możesz dodać projekt testu xUnit w programie Visual Studio przy użyciu szablonu pokazanego na rysunku 9-3 lub interfejsu wiersza polecenia przy użyciu polecenia dotnet New xUnit.

![Dodawanie projektu testowego xUnit w programie Visual Studio](./media/image9-3.png)

**Rysunek 9-3**. Dodawanie projektu testowego xUnit w programie Visual Studio

### <a name="test-naming"></a>Nazwa testu

Należy nazwać testy w spójny sposób, z nazwami wskazującymi, co każdy test wykonuje. Jednym z metod, które mam doskonałe sukces, jest nazwa klasy testowej zgodnie z klasą i metodą, które są testowane. Powoduje to wykonanie wielu małych klas testowych, ale wyraźnie czyści, do czego każdy test jest odpowiedzialny. Przy użyciu nazwy klasy testowej skonfigurowanej do identyfikacji klasy i metody do przetestowania, nazwa metody testowej może służyć do określenia testowanego zachowania. Powinno to obejmować oczekiwane zachowanie oraz wszelkie dane wejściowe lub założeń, które powinny spowodować takie zachowanie. Przykładowe nazwy testów:

- `CatalogControllerGetImage.CallsImageServiceWithId`

- `CatalogControllerGetImage.LogsWarningGivenImageMissingException`

- `CatalogControllerGetImage.ReturnsFileResultWithBytesGivenSuccess`

- `CatalogControllerGetImage.ReturnsNotFoundResultGivenImageMissingException`

Zmiana tego podejścia spowoduje zakończenie każdej klasy testowej o nazwie "powinien" i nieco modyfikuje intensywność:

- `CatalogControllerGetImage`**powinna**`.`**wywoływania**`ImageServiceWithId`

- `CatalogControllerGetImage`**powinna**`.`**dziennika**`WarningGivenImageMissingException`

Niektóre zespoły szukają drugiego podejścia do nazewnictwa, chociaż nieco bardziej pełne. W każdym przypadku spróbuj użyć konwencji nazewnictwa, która zapewnia wgląd w działanie testowe, dzięki czemu w przypadku niepowodzenia co najmniej jednego testu, jest oczywiste z nazw, których przypadki zakończyły się niepowodzeniem. Unikaj niejasnego nazewnictwa testów, takich jak ControllerTests. TEST1, ponieważ nie są one wyświetlane w wynikach testu.

Jeśli przestrzegasz konwencji nazewnictwa, takiej jak powyżej, która tworzy wiele małych klas testowych, dobrym pomysłem jest dalsze organizowanie testów przy użyciu folderów i przestrzeni nazw. Rysunek 9-4 przedstawia jedno podejście do organizowania testów według folderu w kilku projektach testowych.

![Organizowanie klas testowych według folderu na podstawie testowanej klasy](./media/image9-4.png)

**Rysunek 9-4.** Organizowanie klas testowych według folderu na podstawie testowanej klasy.

Oczywiście, jeśli określona Klasa aplikacji ma wiele metod do przetestowania (i w ten sposób wiele klas testowych), warto je umieścić w folderze odpowiadającym klasie aplikacji. Ta organizacja nie różni się od sposobu, w jaki można organizować pliki w folderach w innym miejscu. Jeśli masz więcej niż trzy lub cztery powiązane pliki w folderze zawierającym wiele innych plików, często warto przenieść je do własnego podfolderu.

## <a name="unit-testing-aspnet-core-apps"></a>Testowanie jednostkowe ASP.NET Core aplikacji

W dobrze zaprojektowanej aplikacji ASP.NET Core większość złożoności i logiki biznesowej będzie hermetyzowana w jednostkach firmy i w różnych usługach. Sama aplikacja MVC ASP.NET Core, z jej kontrolerami, filtrami, modele widoków i widokami, powinna wymagać bardzo kilku testów jednostkowych. Większość funkcjonalności danej akcji leży poza samą metodą akcji. Testowanie, czy Routing działa prawidłowo, czy globalna obsługa błędów, nie można efektywnie skutecznie z testem jednostkowym. Analogicznie, wszelkie filtry, w tym Walidacja modelu i filtry uwierzytelniania i autoryzacji, nie mogą być testowane jednostkowo. Bez tych źródeł zachowania większość metod działania powinna być bardzo mała, co pozwala na ich przetestowanie do usług, które mogą być testowane niezależnie od kontrolera, który z nich korzysta.

Czasami konieczne będzie Refaktoryzacja kodu w celu przetestowania go jednostkowo. Często polega to na identyfikowaniu abstrakcji i korzystaniu z iniekcji zależności w celu uzyskania dostępu do abstrakcji kodu, który chcesz przetestować, zamiast kodowania bezpośrednio względem infrastruktury. Rozważmy na przykład prostą metodę akcji do wyświetlania obrazów:

```csharp
[HttpGet("[controller]/pic/{id}")]
public IActionResult GetImage(int id)
{
    var contentRoot = _env.ContentRootPath + "//Pics";
    var path = Path.Combine(contentRoot, id + ".png");
    Byte[] b = System.IO.File.ReadAllBytes(path);
    return File(b, "image/png");
}
```

Testowanie jednostkowe tej metody jest utrudnione w zależności od `System.IO.File`, której używa do odczytu z systemu plików. Możesz przetestować to zachowanie, aby upewnić się, że działa zgodnie z oczekiwaniami, ale jest to test integracji z rzeczywistymi plikami. Warto zauważyć, że nie można testować jednostkowo trasy tej metody — zobaczysz, jak to zrobić z testem funkcjonalnym wkrótce.

Jeśli nie można bezpośrednio przetestować zachowania systemu plików i nie można przetestować trasy, co to jest? Ponadto po refaktoryzacji w celu przeprowadzenia testów jednostkowych można wykryć niektóre przypadki testowe i brakujące zachowanie, takie jak obsługa błędów. Co robią metoda po znalezieniu pliku? Co należy zrobić? W tym przykładzie metoda refaktoryzacji wygląda następująco:

```csharp
[HttpGet("[controller]/pic/{id}")]
public IActionResult GetImage(int id)
{
    byte[] imageBytes;
    try
    {
        imageBytes = _imageService.GetImageBytesById(id);
    }
    catch (CatalogImageMissingException ex)
    {
        _logger.LogWarning($"No image found for id: {id}");
        return NotFound();
    }
    return File(imageBytes, "image/png");
}
```

Rejestratory \_i \_imageService są wprowadzane jako zależności. Teraz można sprawdzić, czy ten sam identyfikator, który jest przesyłany do metody akcji jest przekazana do \_imageService i że wynikowe bajty są zwracane w ramach FileResult. Możesz również sprawdzić, czy rejestrowanie błędów odbywa się zgodnie z oczekiwaniami, i czy wynik NotFound jest zwracany, jeśli brakuje obrazu, przy założeniu, że jest to ważne zachowanie aplikacji (czyli nie tylko kod tymczasowy dodany przez dewelopera w celu zdiagnozowania problemu). Rzeczywista logika pliku została przeniesiona do oddzielnej usługi implementacji i została uzupełniona, aby zwracała wyjątek specyficzny dla aplikacji w przypadku brakujących plików. Tę implementację można przetestować niezależnie przy użyciu testu integracji.

W większości przypadków należy użyć globalnych programów obsługi wyjątków na kontrolerach, więc ilość logiki w nich powinna być minimalna i prawdopodobnie nie być testowana. Większość testów akcji kontrolera należy wykonywać przy użyciu testów funkcjonalnych i klasy `TestServer` opisanej poniżej.

## <a name="integration-testing-aspnet-core-apps"></a>Testowanie integracji ASP.NET Core aplikacje

Większość testów integracji w aplikacjach ASP.NET Core należy przetestować usługi i inne typy implementacji zdefiniowane w projekcie infrastruktury. Można na przykład [sprawdzić, czy EF Core pomyślnie zaktualizować i pobrać dane, których oczekujesz](https://docs.microsoft.com/ef/core/miscellaneous/testing/) od klas dostępu do danych znajdujących się w projekcie infrastruktury. Najlepszym sposobem, aby sprawdzić, czy projekt ASP.NET Core MVC działa prawidłowo, jest testami funkcjonalnymi uruchamianymi względem aplikacji działającej na hoście testowym.

## <a name="functional-testing-aspnet-core-apps"></a>Testowanie funkcjonalne ASP.NET Core aplikacji

W przypadku aplikacji ASP.NET Core Klasa `TestServer` sprawia, że testy funkcjonalne są dość łatwe do zapisu. `TestServer` można skonfigurować przy użyciu `WebHostBuilder` bezpośrednio (jak zwykle w przypadku aplikacji) lub z typem `WebApplicationFactory` (dostępnym od wersji 2,1). Należy spróbować dokładnie dopasować hosta testowego do hosta produkcyjnego, aby testy były wykonywane podobnie jak w przypadku aplikacji w środowisku produkcyjnym. Klasa `WebApplicationFactory` jest przydatna do konfigurowania ContentRoot TestServer, który jest używany przez ASP.NET Core do lokalizowania zasobów statycznych, takich jak widoki.

Możesz utworzyć proste testy funkcjonalne, tworząc klasę testową implementującą IClassFixture\<WebApplicationFactory\<> >, gdzie namiot jest klasą początkową aplikacji sieci Web. W tym miejscu, armatura testowa może utworzyć klienta przy użyciu metody "ServiceClient" fabryki:

```cs
public class BasicWebTests : IClassFixture<WebApplicationFactory<Startup>>
{
    protected readonly HttpClient _client;

    public BaseWebTest(WebApplicationFactory<Startup> factory)
    {
        _client = factory.CreateClient();
    }

    // write tests that use _client
}
```

Często podczas każdego przebiegu testowego należy wykonać dodatkową konfigurację lokacji, na przykład w celu skonfigurowania aplikacji do używania magazynu danych w pamięci, a następnie wypełniania aplikacji za pomocą danych testowych. W tym celu należy utworzyć własną podklasę WebApplicationFactory\<> i zastąpić jej metodę ConfigureWebHost. Poniższy przykład pochodzi z projektu eShopOnWeb FunctionalTests i jest używany jako część testów w głównej aplikacji sieci Web.

```cs
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Mvc.Testing;
using Microsoft.EntityFrameworkCore;
using Microsoft.eShopWeb.Infrastructure.Data;
using Microsoft.eShopWeb.Infrastructure.Identity;
using Microsoft.eShopWeb.Web;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using System;

namespace Microsoft.eShopWeb.FunctionalTests.Web.Controllers
{
    public class CustomWebApplicationFactory<TStartup>
    : WebApplicationFactory<Startup>
    {
        protected override void ConfigureWebHost(IWebHostBuilder builder)
        {
            builder.ConfigureServices(services =>
            {
                // Create a new service provider.
                var serviceProvider = new ServiceCollection()
                    .AddEntityFrameworkInMemoryDatabase()
                    .BuildServiceProvider();

                // Add a database context (ApplicationDbContext) using an in-memory
                // database for testing.
                services.AddDbContext<CatalogContext>(options =>
                {
                    options.UseInMemoryDatabase("InMemoryDbForTesting");
                    options.UseInternalServiceProvider(serviceProvider);
                });

                services.AddDbContext<AppIdentityDbContext>(options =>
                {
                    options.UseInMemoryDatabase("Identity");
                    options.UseInternalServiceProvider(serviceProvider);
                });

                // Build the service provider.
                var sp = services.BuildServiceProvider();

                // Create a scope to obtain a reference to the database
                // context (ApplicationDbContext).
                using (var scope = sp.CreateScope())
                {
                    var scopedServices = scope.ServiceProvider;
                    var db = scopedServices.GetRequiredService<CatalogContext>();
                    var loggerFactory = scopedServices.GetRequiredService<ILoggerFactory>();

                    var logger = scopedServices
                        .GetRequiredService<ILogger<CustomWebApplicationFactory<TStartup>>>();

                    // Ensure the database is created.
                    db.Database.EnsureCreated();

                    try
                    {
                        // Seed the database with test data.
                        CatalogContextSeed.SeedAsync(db, loggerFactory).Wait();
                    }
                    catch (Exception ex)
                    {
                        logger.LogError(ex, $"An error occurred seeding the " +
                            "database with test messages. Error: {ex.Message}");
                    }
                }
            });
        }
    }
}
```

Testy mogą korzystać z tego niestandardowego WebApplicationFactory przy użyciu go do tworzenia klienta, a następnie do wykonywania żądań do aplikacji przy użyciu tego wystąpienia klienta. Aplikacja będzie zawierać dane, które mogą być używane jako część zatwierdzeń testu. Poniższy test sprawdza, czy Strona główna aplikacji eShopOnWeb jest poprawnie załadowana i zawiera listę produktów, która została dodana do aplikacji w ramach danych inicjatora.

```cs
using Microsoft.eShopWeb.FunctionalTests.Web.Controllers;
using Microsoft.eShopWeb.Web;
using System.Net.Http;
using System.Threading.Tasks;
using Xunit;

namespace Microsoft.eShopWeb.FunctionalTests.WebRazorPages
{
    public class HomePageOnGet : IClassFixture<CustomWebApplicationFactory<Startup>>
    {
        public HomePageOnGet(CustomWebApplicationFactory<Startup> factory)
        {
            Client = factory.CreateClient();
        }

        public HttpClient Client { get; }

        [Fact]
        public async Task ReturnsHomePageWithProductListing()
        {
            // Arrange & Act
            var response = await Client.GetAsync("/");
            response.EnsureSuccessStatusCode();
            var stringResponse = await response.Content.ReadAsStringAsync();

            // Assert
            Assert.Contains(".NET Bot Black Sweatshirt", stringResponse);
        }
    }
}
```

Ten test funkcjonalny wykonuje pełny ASP.NET Core stos aplikacji MVC/Razor Pages, w tym wszystkie oprogramowanie pośredniczące, filtry, powiązania itp., które mogą być stosowane. Sprawdza, czy dana trasa ("/") zwraca oczekiwany kod stanu sukcesu i dane wyjściowe HTML. Nie konfiguruje prawdziwy serwer sieci Web, dlatego pozwala uniknąć większości brittleness, które używają rzeczywistego serwera sieci Web do testowania (na przykład problemy z ustawieniami zapory). Testy funkcjonalne uruchamiane względem TestServer są zwykle wolniejsze niż testy integracji i jednostkowe, ale są znacznie szybsze niż testy, które byłyby wykonywane przez sieć, do testowego serwera sieci Web. Należy użyć testów funkcjonalnych, aby upewnić się, że stos frontonu aplikacji działa zgodnie z oczekiwaniami. Te testy są szczególnie przydatne w przypadku znalezienia duplikatów na kontrolerach lub stronach i poprawnego duplikowania przez dodanie filtrów. W idealnym przypadku ten Refaktoryzacja nie zmienia zachowania aplikacji, a zestaw testów funkcjonalnych sprawdzi, czy jest to przypadek.

> ### <a name="references--test-aspnet-core-mvc-apps"></a>References — testowanie ASP.NET Core aplikacji MVC
>
> - **Testowanie w ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/testing/>
> - **Konwencja nazewnictwa testów jednostkowych**  
>   <https://ardalis.com/unit-test-naming-convention>
> - **Testowanie EF Core**  
>   <https://docs.microsoft.com/ef/core/miscellaneous/testing/>

>[!div class="step-by-step"]
>[Poprzedni](work-with-data-in-asp-net-core-apps.md)
>[Następny](development-process-for-azure.md)
