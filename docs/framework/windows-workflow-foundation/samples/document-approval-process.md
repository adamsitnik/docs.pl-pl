---
title: Proces zatwierdzania dokumentu
ms.date: 03/30/2017
ms.assetid: 9b240937-76a7-45cd-8823-7f82c34d03bd
ms.openlocfilehash: 20167cd1c06c2ae57dfe48fd07ab3a0e2adf9927
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038225"
---
# <a name="document-approval-process"></a>Proces zatwierdzania dokumentu

W tym przykładzie pokazano, jak używać wielu funkcji Windows Workflow Foundation (WF) i Windows Communication Foundation (WCF). Razem implementują one scenariusz procesu zatwierdzania dokumentów. Aplikacja kliencka może przesyłać dokumenty do zatwierdzenia i zatwierdzania dokumentów. Istnieje aplikacja Menedżera zatwierdzania ułatwiająca komunikację między klientami i Wymuszanie reguł procesu zatwierdzania. Proces zatwierdzania jest przepływem pracy, który może wykonać kilka typów zatwierdzania. Istnieją działania mające na celu uzyskanie pojedynczego zatwierdzenia, zatwierdzenie kworum (procent zestawu osób zatwierdzających) oraz złożony proces zatwierdzania, który składa się z kworum i pojedynczej zgody w sekwencji.

> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\DocumentApprovalProcess`

## <a name="sample-details"></a>Przykładowe szczegóły

Na poniższej ilustracji przedstawiono przepływ pracy procesu zatwierdzania dokumentów:

![Przepływ pracy procesu zatwierdzania dokumentów](./media/document-approval-process/document-approval-process.jpg)

Z punktu widzenia klienta proces zatwierdzania działa w następujący sposób:

1. Klient subskrybuje użytkownika w systemie procesu zatwierdzania.

2. Klient programu WCF wysyła do usługi WCF hostowanej przez aplikację Menedżer zatwierdzania.

3. Do klienta jest zwracany unikatowy identyfikator użytkownika. Klient może teraz uczestniczyć w procesach zatwierdzania.

4. Po dołączeniu klient może wysłać dokument do zatwierdzenia przy użyciu jednego, kworum lub złożonych procesów zatwierdzania.

5. Kliknięto przycisk w interfejsie klienta, co spowoduje uruchomienie wystąpienia przepływu pracy na hoście usługi przepływu pracy klienta.

6. Przepływ pracy wysyła żądanie zatwierdzenia do aplikacji Menedżera zatwierdzania.

7. Menedżer przepływów pracy uruchamia przepływ pracy na własną stronę, aby reprezentować proces zatwierdzania.

8. Po zakończeniu przepływu pracy zatwierdzania w Menedżerze wyniki są odsyłane do klienta.

9. Klient wyświetla wyniki.

10. Klient może otrzymać żądanie zatwierdzenia i odpowiedzieć na żądanie w dowolnym momencie.

11. Usługa WCF hostowana na kliencie może odebrać żądanie zatwierdzenia od aplikacji Menedżera zatwierdzania.

12. Informacje o dokumencie są prezentowane na kliencie do przeglądu.

13. Użytkownik może zatwierdzić lub odrzucić dokument.

14. Klient WCF jest używany do wysyłania odpowiedzi zatwierdzenia z powrotem do aplikacji Menedżera zatwierdzania.

Z punktu widzenia aplikacji Menedżera zatwierdzania proces zatwierdzania działa w następujący sposób:

1. Klient wnioskuje o uczestnictwo w systemie przetwarzania zatwierdzenia.

2. Usługa WCF w Menedżerze zatwierdzania odbiera żądanie, które jest częścią systemu procesu zatwierdzania.

3. Dla klienta jest generowany unikatowy identyfikator. Informacje o użytkowniku są przechowywane w bazie danych programu.

4. Unikatowy identyfikator jest odsyłany do użytkownika.

5. Odbierane jest żądanie zatwierdzenia. Menedżer zatwierdzania wykonuje proces zatwierdzania.

6. Menedżer zatwierdzania odbiera żądanie zatwierdzenia, rozpoczynając nowy przepływ pracy.

7. W zależności od typu żądania (prostego, kworum lub złożone) wykonywane jest inne działanie.

8. Działania wysyłania i odbierania z korelacją są używane do wysyłania żądania zatwierdzenia do klienta w celu przejrzenia i odebrania odpowiedzi.

9. Wynik przepływu pracy procesu zatwierdzania jest wysyłany do klienta.

## <a name="using-the-sample"></a>Korzystanie z przykładu

##### <a name="to-set-up-the-database"></a>Aby skonfigurować bazę danych

1. W wierszu polecenia programu Visual Studio 2010 otwartym z uprawnieniami administratora przejdź do tego folderu DocumentApprovalProcess i uruchom polecenie Setup. cmd.

##### <a name="to-set-up-the-application"></a>Aby skonfigurować aplikację

1. Za pomocą programu Visual Studio 2010 Otwórz plik rozwiązania DocumentApprovalProcess. sln.

2. Aby skompilować rozwiązanie, naciśnij klawisze CTRL + SHIFT + B.

3. Aby uruchomić rozwiązanie, uruchom aplikację Menedżer zatwierdzania, klikając prawym przyciskiem myszy projekt zatwierdzania w **Eksplorator rozwiązań** a następnie klikając polecenie **Debuguj**->**Uruchom** nowe wystąpienie w menu rozwijanym.

    Poczekaj na dane wyjściowe menedżera, aby poinformować, że jest to gotowe.

##### <a name="to-run-the-single-approval-scenario"></a>Aby uruchomić scenariusz o pojedynczej zatwierdzeniu

1. Otwórz wiersz polecenia z uprawnieniami administratora.

2. Przejdź do katalogu, który zawiera rozwiązanie.

3. Przejdź do folderu ApprovalClient\Bin\Debug i wykonaj dwa wystąpienia programu ApprovalClient. exe.

4. Kliknij przycisk **odkryj**, poczekaj, aż przycisk **Subskrybuj** zostanie włączony.

5. Wpisz dowolną nazwę użytkownika i kliknij przycisk **Subskrybuj**. Dla jednego klienta Użyj `UserType1` i innego typu. `UserType2`

6. `UserType1` W kliencie wybierz typ pojedynczego zatwierdzenia z menu rozwijanego i wpisz nazwę dokumentu i zawartość. Kliknij pozycję **Żądaj zatwierdzenia**.

7. `UserType2` W kliencie zostanie wyświetlony dokument oczekujący na zatwierdzenie. Zaznacz go i naciśnij przycisk Zatwierdź lub Odrzuć. Wyniki powinny być wyświetlane na `UserType1` kliencie.

##### <a name="to-run-the-quorum-approval-scenario"></a>Aby uruchomić Scenariusz zatwierdzania kworum

1. Otwórz wiersz polecenia z uprawnieniami administratora.

2. Przejdź do katalogu, który zawiera rozwiązanie.

3. Przejdź do folderu ApprovalClient\Bin\Debug i wykonaj trzy wystąpienia programu ApprovalClient. exe.

4. Kliknij przycisk **odkryj**, poczekaj, aż przycisk **Subskrybuj** zostanie włączony.

5. Wpisz dowolną nazwę użytkownika i kliknij przycisk **Subskrybuj**. Dla jednego klienta `UserType1` i drugiego typu `UserType2`.

6. `UserType1` W kliencie wybierz typ zatwierdzenia kworum z menu rozwijanego i wpisz nazwę dokumentu i zawartość. Kliknij pozycję **Żądaj zatwierdzenia**. Ta prośba o zaakceptowanie lub odrzucenie dokumentu przez dwóch `UserType2` klientów. Chociaż obydwie `UserType2` klienci muszą reagować, tylko jeden klient musi zatwierdzić dokument do zatwierdzenia.

7. `UserType2` Na klientach zostanie wyświetlony dokument oczekujący na zatwierdzenie. Zaznacz go i naciśnij przycisk Zatwierdź lub Odrzuć. Wyniki powinny być wyświetlane na `UserType1` kliencie.

##### <a name="to-run-the-complex-approval-scenario"></a>Aby uruchomić złożony Scenariusz zatwierdzania

1. Otwórz wiersz polecenia z uprawnieniami administratora.

2. Przejdź do katalogu, który zawiera rozwiązanie.

3. Przejdź do folderu ApprovalClient\Bin\Debug i wykonaj cztery wystąpienia programu ApprovalClient. exe.

4. Kliknij przycisk **odkryj**, poczekaj, aż przycisk **Subskrybuj** zostanie włączony.

5. Wpisz dowolną nazwę użytkownika i kliknij przycisk **Subskrybuj**. Do użycia `UserType1`w przypadku jednego klienta w przypadku dwóch `UserType2`typów użycia i w ostatnim użyciu `UserType3`.

6. `UserType1` W kliencie wybierz typ pojedynczego zatwierdzenia z menu rozwijanego i wpisz nazwę dokumentu i zawartość. Kliknij pozycję **Żądaj zatwierdzenia**.

7. `UserType2` Na klientach zostanie wyświetlony dokument oczekujący na zatwierdzenie. Zaznacz go i naciśnijprzycisk Zatwierdź, dokument jest przesyłany `UserType3` do klienta.

    Jeśli dokument zostanie zatwierdzony przez pierwsze `UserType2` kworum, dokument jest przesyłany `UserType3` do klienta.

8. Zatwierdź lub Odrzuć dokument z `UserType3` klienta. Wyniki powinny być wyświetlane na `UserType1` kliencie.

##### <a name="to-clean-up"></a>Aby oczyścić

1. W wierszu polecenia programu Visual Studio 2010 przejdź do folderu DocumentApprovalProcess i uruchom polecenie Oczyść. cmd.
