---
title: Kopiowanie zestawów w tle
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], shadow copying
- application domains, shadow copying assemblies
- shadow copying assemblies
ms.assetid: de8b8759-fca7-4260-896b-5a4973157672
ms.openlocfilehash: 40a1b5062d45b7b540af7058b82b77c664070d2e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73119776"
---
# <a name="shadow-copying-assemblies"></a>Kopiowanie zestawów w tle

Kopiowanie w tle umożliwia aktualizowanie zestawów, które są używane w domenie aplikacji, aby można było je aktualizować bez wyładowywania domeny aplikacji. Jest to szczególnie przydatne w przypadku aplikacji, które muszą być stale dostępne, takich jak Lokacje ASP.NET.

> [!IMPORTANT]
> Kopiowanie w tle nie jest obsługiwane w aplikacjach [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].

Środowisko uruchomieniowe języka wspólnego blokuje plik zestawu podczas ładowania zestawu, więc nie można zaktualizować pliku do momentu, gdy zestaw nie zostanie zwolniony. Jedynym sposobem zwolnienia zestawu z domeny aplikacji jest zwolnienie domeny aplikacji, więc w normalnych warunkach nie można zaktualizować zestawu na dysku do momentu, gdy wszystkie domeny aplikacji korzystające z niego nie zostały zwolnione.

Gdy domena aplikacji jest skonfigurowana do kopiowania plików w tle, zestawy ze ścieżki aplikacji są kopiowane do innej lokalizacji i ładowane z tej lokalizacji. Kopia jest zablokowana, ale oryginalny plik zestawu jest odblokowany i można go zaktualizować.

> [!IMPORTANT]
> Jedyne zestawy, które mogą być kopiowane w tle, są przechowywane w katalogu aplikacji lub jego podkatalogach, określone przez <xref:System.AppDomainSetup.ApplicationBase%2A> i <xref:System.AppDomainSetup.PrivateBinPath%2A> właściwości podczas konfigurowania domeny aplikacji. Zestawy przechowywane w globalnej pamięci podręcznej zestawów nie są kopiowane w tle.

Ten artykuł zawiera następujące sekcje:

- W przypadku [włączania i używania kopiowania w tle](#EnablingAndUsing) opisano podstawowe użycie i opcje, które są dostępne do kopiowania w tle.

- [Wydajność uruchamiania](#StartupPerformance) zawiera opis zmian wprowadzonych w funkcji kopiowania w tle w .NET Framework 4 w celu zwiększenia wydajności uruchamiania oraz przywracania wcześniejszych wersji.

- [Przestarzałe metody](#ObsoleteMethods) opisują zmiany wprowadzone we właściwościach i metodach kontrolujących kopiowanie w tle w .NET Framework 2,0.

<a name="EnablingAndUsing"></a>

## <a name="enabling-and-using-shadow-copying"></a>Włączanie i korzystanie z kopiowania w tle

Właściwości klasy <xref:System.AppDomainSetup> można użyć w następujący sposób, aby skonfigurować domenę aplikacji do kopiowania w tle:

- Włącz kopiowanie w tle, ustawiając właściwość <xref:System.AppDomainSetup.ShadowCopyFiles%2A> na wartość ciągu `"true"`.

  Domyślnie to ustawienie powoduje, że wszystkie zestawy w ścieżce aplikacji mają być kopiowane do pamięci podręcznej pobierania przed ich załadowaniem. Jest to ta sama pamięć podręczna obsługiwana przez środowisko uruchomieniowe języka wspólnego do przechowywania plików pobranych z innych komputerów, a środowisko uruchomieniowe języka wspólnego automatycznie usuwa pliki, gdy nie są już potrzebne.

- Opcjonalnie można ustawić niestandardową lokalizację dla skopiowanych plików w tle za pomocą właściwości <xref:System.AppDomainSetup.CachePath%2A> i właściwości <xref:System.AppDomainSetup.ApplicationName%2A>.

  Ścieżka bazowa dla lokalizacji jest tworzona przez połączenie właściwości <xref:System.AppDomainSetup.ApplicationName%2A> z właściwością <xref:System.AppDomainSetup.CachePath%2A> jako podkatalogiem. Zestawy są kopiowane w tle do podkatalogów tej ścieżki, a nie do samej ścieżki podstawowej.

  > [!NOTE]
  > Jeśli właściwość <xref:System.AppDomainSetup.ApplicationName%2A> nie jest ustawiona, właściwość <xref:System.AppDomainSetup.CachePath%2A> zostanie zignorowana, a zostanie użyta pamięć podręczna pobierania. Nie zgłoszono żadnego wyjątku.

  Jeśli określisz lokalizację niestandardową, użytkownik jest odpowiedzialny za czyszczenie katalogów i skopiowanych plików, gdy nie są już potrzebne. Nie są usuwane automatycznie.

  Istnieje kilka przyczyn, dla których warto ustawić lokalizację niestandardową dla skopiowanych plików w tle. Możesz chcieć ustawić lokalizację niestandardową dla skopiowanych plików w tle, jeśli aplikacja generuje dużą liczbę kopii. Pamięć podręczna pobierania jest ograniczona rozmiarem, a nie przez okres istnienia, więc jest możliwe, że środowisko uruchomieniowe języka wspólnego podejmie próbę usunięcia pliku, który jest nadal używany. Kolejną przyczyną ustawienia niestandardowej lokalizacji jest to, że użytkownicy korzystający z aplikacji nie mają dostępu do zapisu w lokalizacji katalogu używanej przez środowisko uruchomieniowe języka wspólnego na potrzeby pamięci podręcznej pobierania.

- Opcjonalnie Ogranicz zestawy, które są kopiowane w tle za pomocą właściwości <xref:System.AppDomainSetup.ShadowCopyDirectories%2A>.

  Po włączeniu kopiowania w tle dla domeny aplikacji domyślną wartością jest skopiowanie wszystkich zestawów w ścieżce aplikacji — czyli w katalogach określonych przez <xref:System.AppDomainSetup.ApplicationBase%2A> i <xref:System.AppDomainSetup.PrivateBinPath%2A> właściwości. Można ograniczyć kopiowanie do wybranych katalogów, tworząc ciąg zawierający tylko te katalogi, które mają być kopiowane w tle, i przypisując ciąg do właściwości <xref:System.AppDomainSetup.ShadowCopyDirectories%2A>. Oddziel katalogi średnikami. Jedynymi zestawami, które są kopiowane w tle, są te, które znajdują się w wybranych katalogach.

  > [!NOTE]
  > Jeśli nie przypiszesz ciągu do właściwości <xref:System.AppDomainSetup.ShadowCopyDirectories%2A> lub jeśli ustawisz tę właściwość na `null`, wszystkie zestawy w katalogach określonych przez <xref:System.AppDomainSetup.ApplicationBase%2A> i <xref:System.AppDomainSetup.PrivateBinPath%2A> właściwości są kopiowane w tle.

  > [!IMPORTANT]
  > Ścieżki katalogów nie mogą zawierać średników, ponieważ średnik jest znakiem ogranicznika. Brak znaku ucieczki dla średników.

<a name="StartupPerformance"></a>

## <a name="startup-performance"></a>Startowa wydajność

Gdy domena aplikacji, która korzysta z kopiowania w tle, rozpocznie się, występuje opóźnienie, a zestawy w katalogu aplikacji są kopiowane do katalogu kopii w tle lub zweryfikowane, jeśli znajdują się już w tej lokalizacji. Przed .NET Framework 4 wszystkie zestawy zostały skopiowane do katalogu tymczasowego. Każdy zestaw został otwarty w celu zweryfikowania nazwy zestawu i zweryfikowania silnej nazwy. Każdy zestaw został sprawdzony, aby sprawdzić, czy został on ostatnio zaktualizowany niż kopia w katalogu kopii w tle. Jeśli tak, zostało ono skopiowane do katalogu kopii w tle. Na koniec kopie tymczasowe zostały odrzucone.

Począwszy od .NET Framework 4, domyślnym zachowaniem uruchamiania jest bezpośrednie porównanie daty i godziny pliku każdego zestawu w katalogu aplikacji z datą i godziną kopiowania w katalogu kopii w tle. Jeśli zestaw został zaktualizowany, jest kopiowany przy użyciu tej samej procedury jak we wcześniejszych wersjach .NET Framework; w przeciwnym razie zostanie załadowana kopia w katalogu kopii w tle.

Wynikowe zwiększenie wydajności jest największe dla aplikacji, w których zestawy nie zmieniają się często, a zmiany zwykle występują w małym podzestawie zestawów. Jeśli większość zestawów w aplikacji często zmienia się, nowe domyślne zachowanie może spowodować regresję wydajności. Można przywrócić zachowanie uruchamiania poprzednich wersji .NET Framework przez dodanie [elementu\<shadowCopyVerifyByTimestamp >](../configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md) do pliku konfiguracji, z `enabled="false"`.

<a name="ObsoleteMethods"></a>

## <a name="obsolete-methods"></a>Metody przestarzałe

Klasa <xref:System.AppDomain> ma kilka metod, takich jak <xref:System.AppDomain.SetShadowCopyFiles%2A> i <xref:System.AppDomain.ClearShadowCopyPath%2A>, których można użyć do kontrolowania kopiowania w tle w domenie aplikacji, ale zostały oznaczone jako przestarzałe w .NET Framework wersji 2,0. Zalecanym sposobem skonfigurowania domeny aplikacji do kopiowania w tle jest użycie właściwości klasy <xref:System.AppDomainSetup>.

## <a name="see-also"></a>Zobacz także

- <xref:System.AppDomainSetup.ShadowCopyFiles%2A?displayProperty=nameWithType>
- <xref:System.AppDomainSetup.CachePath%2A?displayProperty=nameWithType>
- <xref:System.AppDomainSetup.ApplicationName%2A?displayProperty=nameWithType>
- <xref:System.AppDomainSetup.ShadowCopyDirectories%2A?displayProperty=nameWithType>
- [\<element > shadowCopyVerifyByTimestamp](../configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md)
