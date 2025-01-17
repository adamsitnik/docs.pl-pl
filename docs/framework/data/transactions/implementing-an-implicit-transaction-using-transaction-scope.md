---
title: Implementowanie transakcji niejawnej przy użyciu zakresu transakcji
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49d1706a-1e0c-4c85-9704-75c908372eb9
ms.openlocfilehash: e3af361f4268e9a83efe4d28547dc95fc242633e
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040200"
---
# <a name="implementing-an-implicit-transaction-using-transaction-scope"></a>Implementowanie transakcji niejawnej przy użyciu zakresu transakcji
Klasa <xref:System.Transactions.TransactionScope> zapewnia prosty sposób oznaczania bloku kodu, który uczestniczy w transakcji, bez konieczności korzystania z samej transakcji. Zakres transakcji można wybrać i automatycznie zarządzać otoczenia transakcji. Ze względu na łatwość użycia i wydajność zaleca się użycie klasy <xref:System.Transactions.TransactionScope> podczas tworzenia aplikacji transakcji.  
  
 Ponadto nie trzeba jawnie zarejestrować zasobów w ramach transakcji. Wszelkie <xref:System.Transactions> Menedżera zasobów (takich jak SQL Server 2005) można wykryć istnienie otoczenia transakcji utworzone przez zakres i automatycznie zarejestrować.  
  
## <a name="creating-a-transaction-scope"></a>Tworzenie zakresu transakcji  
 Poniższy przykład pokazuje proste użycie klasy <xref:System.Transactions.TransactionScope>.  
  
 [!code-csharp[TransactionScope#1](../../../../samples/snippets/csharp/VS_Snippets_Remoting/TransactionScope/cs/ScopeWithSQL.cs#1)]
 [!code-vb[TransactionScope#1](../../../../samples/snippets/visualbasic/VS_Snippets_Remoting/TransactionScope/vb/ScopeWithSQL.vb#1)]  
  
 Zakres transakcji jest uruchamiany po utworzeniu nowego obiektu <xref:System.Transactions.TransactionScope>.  Jak pokazano w przykładzie kodu, zaleca się utworzenie zakresów z instrukcją `using`. Instrukcja `using` jest dostępna zarówno w C# , jak i w Visual Basic i działa jak blok`try`...`finally`, aby upewnić się, że zakres jest prawidłowo usunięty.  
  
 Podczas tworzenia instancji <xref:System.Transactions.TransactionScope>, Menedżer transakcji określa, która transakcja wziąć udział w. Po określeniu zakresu zawsze uczestniczy w danej transakcji. Decyzja opiera się na dwa czynniki: Określa, czy transakcja otoczenia jest obecny i ma wartość `TransactionScopeOption` parametr w konstruktorze. Transakcja otoczenia jest transakcji, w którym wykonuje kodu. Odwołanie do transakcji otoczenia można uzyskać przez wywołanie metody statyczne klasy <xref:System.Transactions.Transaction.Current%2A?displayProperty=nameWithType> właściwości <xref:System.Transactions.Transaction> klasy. Więcej informacji na temat sposobu użycia tego parametru znajduje się w sekcji [Zarządzanie przepływem transakcji przy użyciu usługi TransactionScopeOption](#ManageTxFlow) w tym temacie.  
  
## <a name="completing-a-transaction-scope"></a>Wykonywanie zakresu transakcji  
 Gdy aplikacja ukończy wszystkie zadania, które chce wykonać w transakcji, należy wywołać metodę <xref:System.Transactions.TransactionScope.Complete%2A?displayProperty=nameWIthType> tylko raz, aby poinformować Menedżera transakcji, że jest on akceptowalny do zatwierdzenia transakcji. Dobrze jest bardzo na wstrzymanie wywołanie <xref:System.Transactions.TransactionScope.Complete%2A> jako ostatnią instrukcję w `using` bloku.  
  
 Wywołanie tej metody przerywa transakcję, ponieważ Menedżer transakcji interpretuje ją jako błąd systemu lub równoważy wyjątek zgłoszony w zakresie transakcji. Jednak wywołanie tej metody nie gwarantuje, że transakcji będzie zatwierdzone. Jest tylko sposób informowania menedżera transakcji Twój status. Po wywołaniu <xref:System.Transactions.TransactionScope.Complete%2A> metody jest już dostępne otoczenia transakcji przy użyciu <xref:System.Transactions.Transaction.Current%2A> właściwości i próby podjęły spowodują wyjątek.  
  
 Jeśli <xref:System.Transactions.TransactionScope> obiektu początkowo utworzona transakcja występuje rzeczywista praca z Zatwierdzanie transakcji przez Menedżera transakcji po ostatni wiersz kodu w `using` bloku. Jeśli nie utworzył transakcji, zatwierdzanie występuje zawsze, gdy <xref:System.Transactions.CommittableTransaction.Commit%2A> jest wywoływana przez właściciela <xref:System.Transactions.CommittableTransaction> obiektu. W tym momencie Menedżer transakcji wywołuje menedżerów zasobów i informuje je o zatwierdzeniu lub wycofaniu, w zależności od tego, czy metoda <xref:System.Transactions.TransactionScope.Complete%2A> została wywołana w obiekcie <xref:System.Transactions.TransactionScope>.  
  
 `using` Instrukcji zapewnia, że <xref:System.Transactions.TransactionScope.Dispose%2A> metody <xref:System.Transactions.TransactionScope> obiektu jest wywoływana, nawet jeśli wystąpi wyjątek. <xref:System.Transactions.TransactionScope.Dispose%2A> Metody oznacza koniec zakresu transakcji. Wyjątki, które mogą występować po wywołaniu tej metody nie może mieć wpływ na transakcji. Ta metoda również przywraca otoczenia transakcji jej poprzedniego stanu.  
  
 Element <xref:System.Transactions.TransactionAbortedException> jest generowany, jeśli zakres tworzy transakcji, a transakcja została przerwana. Element <xref:System.Transactions.TransactionInDoubtException> jest generowany, gdy Menedżer transakcji nie może podjąć decyzję zatwierdzania. Nie wyjątku, jeśli transakcja została zatwierdzona.  
  
## <a name="rolling-back-a-transaction"></a>Wycofywanie transakcji  
 Jeśli chcesz wycofać transakcji, nie należy wywołać <xref:System.Transactions.TransactionScope.Complete%2A> metody w zakresie transakcji. Na przykład można zgłosić wyjątek w zakresie. Transakcji, w których uczestniczy w zostaną wycofane.  
  
## <a name="ManageTxFlow"></a>Zarządzanie przepływem transakcji przy użyciu TransactionScopeOption  
 Zakres transakcji może być zagnieżdżony przez wywołanie metody, która używa <xref:System.Transactions.TransactionScope> z metody, która używa własnego zakresu, podobnie jak w przypadku metody `RootMethod` w poniższym przykładzie.  
  
```csharp  
void RootMethod()
{
    using(TransactionScope scope = new TransactionScope())
    {
        /* Perform transactional work here */
        SomeMethod();
        scope.Complete();
    }
}

void SomeMethod()
{
    using(TransactionScope scope = new TransactionScope())
    {
        /* Perform transactional work here */
        scope.Complete();
    }
}
```  
  
 Zakres transakcji wierzchu nosi nazwę zakres głównego.  
  
 <xref:System.Transactions.TransactionScope> Udostępnia kilka przeciążenia konstruktorów, które akceptują wyliczenie typu <xref:System.Transactions.TransactionScopeOption>, definiujący transakcyjnych zachowanie zakresu.  
  
 Element <xref:System.Transactions.TransactionScope> obiekt zawiera trzy pozycje:  
  
- Dołącz do otoczenia transakcji lub Utwórz nową, jeśli nie istnieje.  
  
- Można nowego zakresu głównego, oznacza to, że uruchomić nowej transakcji i skonfigurować danej transakcji można nowej transakcji otoczenia w zakresie własnej.  
  
- Nie w ogóle brać udział w transakcji. Z tego względu nie ma żadnej otoczenia transakcji.  
  
 Jeśli zakres jest utworzone za pomocą elementów <xref:System.Transactions.TransactionScopeOption.Required>i transakcja otoczenia jest obecna, zakres sprzężenia danej transakcji. Jeśli z drugiej strony, nie ma żadnej transakcji otoczenia, następnie zakres tworzy nową transakcję i stają się zakres głównego. Jest to wartość domyślna. Gdy <xref:System.Transactions.TransactionScopeOption.Required> jest używany, kod w zakresie nie jest konieczne działają inaczej, czy jest to główny lub po prostu dołączenie do otoczenia transakcji. Powinna ona działać tak samo w obu przypadkach.  
  
 Jeśli zakres jest utworzone za pomocą elementów <xref:System.Transactions.TransactionScopeOption.RequiresNew>, zawsze jest zakres głównego. Rozpoczyna się nowej transakcji, a jego transakcji staje się nowe otoczenia transakcji w zakresie.  
  
 Jeśli zakres jest utworzone za pomocą elementów <xref:System.Transactions.TransactionScopeOption.Suppress>, nigdy nie bierze udział w transakcji, niezależnie od tego, czy transakcja otoczenia jest obecny. Zakres utworzone za pomocą elementów wartość ta zawsze ma `null` jako jego otoczenia transakcji.  
  
 Powyższych opcji przedstawiono w poniższej tabeli.  
  
|TransactionScopeOption|Otoczenia transakcji|Zakres uczestniczy|  
|----------------------------|-------------------------|-----------------------------|  
|Wymagane|Nie|Nowa transakcja (będzie główny)|  
|Wymagane nowe|Nie|Nowa transakcja (będzie główny)|  
|Pomiń|Nie|Nie transakcji|  
|Wymagane|Tak|Otoczenia transakcji|  
|Wymagane nowe|Tak|Nowa transakcja (będzie główny)|  
|Pomiń|Tak|Nie transakcji|  
  
 Gdy <xref:System.Transactions.TransactionScope> obiektu sprzężenia istniejącej transakcji otoczenia, usuwania obiektu zakres nie może kończyć się transakcji, chyba że zakres przerywa transakcję. Jeśli otoczenia transakcji został utworzony przez zakres głównego, tylko wtedy, gdy zakres główny jest usunięty, nie <xref:System.Transactions.CommittableTransaction.Commit%2A> jest wywoływana w transakcji. Jeśli transakcja została utworzona ręcznie, zakończenia transakcji, gdy jest to zostało przerwane lub przydzielonej przez jej twórcę.  
  
 Poniższy przykład pokazuje obiekt <xref:System.Transactions.TransactionScope>, który tworzy trzy obiekty zagnieżdżonych zakresów, z których każde zostanie utworzone z inną <xref:System.Transactions.TransactionScopeOption> wartością.  
  
```csharp  
using(TransactionScope scope1 = new TransactionScope())
//Default is Required
{
    using(TransactionScope scope2 = new TransactionScope(TransactionScopeOption.Required))
    {
        //...
    }

    using(TransactionScope scope3 = new TransactionScope(TransactionScopeOption.RequiresNew))   
    {
        //...  
    }
  
    using(TransactionScope scope4 = new TransactionScope(TransactionScopeOption.Suppress))
    {
        //...  
    }
}
```  
  
 W przykładzie przedstawiono blok kodu bez żadnej otaczającej transakcji tworzącej nowy zakres (`scope1`) z <xref:System.Transactions.TransactionScopeOption.Required>. Zakres `scope1` jest zakresem głównego, ponieważ tworzy nową transakcję (transakcji A) i sprawia, że transakcja A otoczenia transakcji. `Scope1`następnie tworzy trzy więcej obiektów, każdy z inną <xref:System.Transactions.TransactionScopeOption> wartość. Na przykład `scope2` jest tworzony przy użyciu <xref:System.Transactions.TransactionScopeOption.Required>, a ponieważ istnieje otoczenia transakcji, przyłączana jest pierwsza transakcja utworzona przez `scope1`. Należy pamiętać, że `scope3` zakres główny nowej transakcji, a `scope4` ma ma otoczenia transakcji.  
  
 Chociaż często używane wartości domyślne i większość <xref:System.Transactions.TransactionScopeOption> jest <xref:System.Transactions.TransactionScopeOption.Required>, inne wartości ma unikatowy z przeznaczeniem.  

### <a name="non-transactional-code-inside-a-transaction-scope"></a>Kod nietransakcyjny wewnątrz zakresu transakcji

 <xref:System.Transactions.TransactionScopeOption.Suppress>jest przydatne, gdy chcesz zachować operacji wykonywanych przez sekcję kodu, a nie chcesz przerwać otoczenia transakcji, jeśli operacje kończą się niepowodzeniem. Na przykład, gdy chcesz wykonać operacje rejestrowania lub inspekcji lub Kiedy chcesz opublikować zdarzenia dla subskrybentów, niezależnie od tego, czy otoczenia transakcji zatwierdzeń lub przerwań. Ta wartość umożliwia posiadanie sekcji kodu nietransakcyjnej wewnątrz zakresu transakcji, jak pokazano w poniższym przykładzie.  
  
```csharp  
using(TransactionScope scope1 = new TransactionScope())
{
    try
    {
        //Start of non-transactional section
        using(TransactionScope scope2 = new
            TransactionScope(TransactionScopeOption.Suppress))  
        {  
            //Do non-transactional work here  
        }  
        //Restores ambient transaction here
   }
   catch {}  
   //Rest of scope1
}
```  
  
### <a name="voting-inside-a-nested-scope"></a>Głosowanie wewnątrz zagnieżdżonej zakresu  
 Chociaż zagnieżdżony zakres może dołączyć do otoczenia transakcji zakresu głównego, wywoływania <xref:System.Transactions.TransactionScope.Complete%2A> w zakresie zagnieżdżone nie ma wpływu na zakres głównego. Tylko wtedy, gdy wszystkie zakresy z zakresu głównego do ostatni zakres zagnieżdżonych głosowania można zatwierdzić transakcji, będzie można zatwierdzić transakcji. Nie wywołuje metody <xref:System.Transactions.TransactionScope.Complete%2A> w zakresie zagnieżdżonych będzie miała wpływ na zakres głównego zgodnie z otoczenia transakcja zostanie natychmiast przerwane.  
  
## <a name="setting-the-transactionscope-timeout"></a>Ustawienie limitu czasu elementu TransactionScope  
 Niektóre z przeciążenia konstruktorów z <xref:System.Transactions.TransactionScope> akceptować wartości typu <xref:System.TimeSpan>, używany do sterowania limit czasu transakcji. Upłynął limit czasu ustawioną wartość zero oznacza nieskończony limit czasu. Nieskończony limit czasu przydaje się głównie na potrzeby debugowania, gdy chcesz wyizolować problem w logiki biznesowej przez krokowe wykonywanie kodu, a użytkownik nie chce transakcji, które można debugować limitu czasu podczas próby zlokalizowania problemu. Ostrożność bardzo przy użyciu wartości nieskończony limit czasu we wszystkich innych przypadkach, ponieważ zastępuje zabezpiecza przed zakleszczenia transakcji.  
  
 Zwykle ustawiana <xref:System.Transactions.TransactionScope> limitu czasu w celu wartości innej niż domyślny w obu przypadkach. Pierwszy jest podczas opracowywania, gdy chcesz przetestować sposób, w jaki aplikacja obsługuje przerwane transakcje. Przez ustawienie limitu czasu małej wartości (na przykład jeden milisekund), spowodować transakcji nie powiedzie się i w związku z tym można obserwować obsługę kodu błędu. Drugi przypadek, w którym można ustawić wartość jest mniejsza niż domyślna wartość limitu czasu jest, jeśli uważasz, że zakres polega konfliktu zasobów, co spowoduje zakleszczenia. W takim przypadku chcesz przerwać transakcji, jak najszybciej i nie czeka na domyślna wartość limitu czasu wygaśnięcia.  
  
 Gdy zakres sprzężenia otoczenia transakcji, ale określa limit czasu mniejsze niż ma ustawioną wartość transakcji otoczenia, nowe, krótszy limit czasu jest wymuszane na <xref:System.Transactions.TransactionScope> obiektu i zakres musi kończyć się w czasie zagnieżdżonych określonym lub transakcja jest automatycznie przerwana. Jeśli limit czasu zagnieżdżony zakres jest więcej niż otoczenia transakcji, ustawienie nie działa.  
  
## <a name="setting-the-transactionscope-isolation-level"></a>Ustawienie poziomu izolacji elementu TransactionScope  
 Niektóre z przeciążenia konstruktorów z <xref:System.Transactions.TransactionScope> zaakceptować struktury typu <xref:System.Transactions.TransactionOptions> określa poziom izolacji, oprócz wartość limitu czasu. Domyślnie transakcji wykonuje z ustawioną poziom izolacji <xref:System.Transactions.IsolationLevel.Serializable>. Wybranie innego niż poziom izolacji <xref:System.Transactions.IsolationLevel.Serializable> jest najczęściej używana w systemach intensywnie korzysta z odczytu. Wymaga to pełny opis przetwarzania interpretacją i semantyka transakcja współbieżności problemy związane z i skutków spójności systemu transakcji.  
  
 Ponadto nie wszystkie menedżerów zasobów obsługuje wszystkie poziomy izolacji i może zdecydować się do wzięcia udziału w transakcji na wyższym poziomie niż skonfigurowane.  
  
 Każdy poziom izolacji poza <xref:System.Transactions.IsolationLevel.Serializable> się niespójność wynikające z innych transakcji dostęp do tych samych informacji. Różnica między izolacji różne poziomy w ten sposób do odczytu i zapisu blokady są używane. Blokada może zostać pociągnięty tylko wtedy, gdy transakcji uzyskuje dostęp do danych w Menedżerze zasobów lub może zostać pociągnięty do momentu transakcji nie zostanie przekazana lub zostało przerwane. Jest lepsze przepustowości, ten ostatni w celu zachowania spójności. Dwa rodzaje blokady i dwa rodzaje operacji (odczyt/zapis) dostarcza cztery poziomy izolacji podstawowe. Aby uzyskać więcej informacji, zobacz <xref:System.Transactions.IsolationLevel>.  
  
 Po użyciu zagnieżdżone <xref:System.Transactions.TransactionScope> obiektów, wszystkie zakresy zagnieżdżonych musi być skonfigurowany do użycia dokładnie ten sam poziom izolacji, aby dołączyć otoczenia transakcji. Jeśli zagnieżdżonych <xref:System.Transactions.TransactionScope> obiektu próbuje dołączyć otoczenia transakcji, jeszcze określa poziom izolacji różnych <xref:System.ArgumentException> zgłaszany.  
  
## <a name="interop-with-com"></a>Usługę międzyoperacyjną z modelu COM +  
 Podczas tworzenia nowego <xref:System.Transactions.TransactionScope> wystąpienie, można użyć <xref:System.Transactions.EnterpriseServicesInteropOption> wyliczenia w jednym z konstruktorów do określenia sposobu interakcji z modelu COM +. Aby uzyskać więcej informacji na ten temat, zobacz [współdziałanie z usługami przedsiębiorstwa i transakcjami modelu COM+](interoperability-with-enterprise-services-and-com-transactions.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Transactions.Transaction.Clone%2A>
- <xref:System.Transactions.TransactionScope>
