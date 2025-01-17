---
title: Obsługa SqlClient dla wysokiej dostępności, odzyskiwania po awarii
ms.date: 03/30/2017
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.openlocfilehash: b51c3cb1eb3c8726b7de007a1c1519eae0733392
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791612"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>Obsługa SqlClient dla wysokiej dostępności, odzyskiwania po awarii
W tym temacie omówiono obsługę SqlClient (dodano w .NET Framework 4,5) w celu uzyskania wysokiej dostępności i odzyskiwania po awarii — Zawsze włączone grupy dostępności.  Dodano funkcję Zawsze włączone grupy dostępności do SQL Server 2012. Aby uzyskać więcej informacji na temat Zawsze włączone grupy dostępności, zobacz SQL Server Books Online.  
  
 W właściwości Connection można teraz określić odbiornik grupy dostępności (wysokiej dostępności, odzyskiwania po awarii) lub SQL Server 2012 wystąpienia klastra trybu failover. Jeśli aplikacja SqlClient jest połączona z bazą danych AlwaysOn, która przejdzie w tryb failover, oryginalne połączenie zostanie przerwane, a aplikacja musi otworzyć nowe połączenie, aby kontynuować pracę po przejściu w tryb pracy awaryjnej.  
  
 Jeśli nie łączysz się z odbiornikiem grupy dostępności lub wystąpieniem klastra trybu failover w systemie SQL Server 2012, a wiele adresów IP jest skojarzonych z nazwą hosta, klient SqlClient będzie sekwencyjnie powtarzać wszystkie adresy IP skojarzone z wpisem DNS. Może to być czasochłonne, jeśli pierwszy adres IP zwrócony przez serwer DNS nie jest powiązany z żadną kartą interfejsu sieciowego. Podczas nawiązywania połączenia z odbiornikiem grupy dostępności lub wystąpieniem klastra trybu failover z systemem SQL Server 2012 klient ponowi próbę nawiązania połączenia ze wszystkimi adresami IP równolegle i w przypadku pomyślnego nawiązania połączenia. podejmował.  
  
> [!NOTE]
> Zwiększenie limitu czasu połączenia i wdrożenie logiki ponawiania połączenia spowoduje zwiększenie prawdopodobieństwa, że aplikacja będzie łączyć się z grupą dostępności. Ponadto, ponieważ połączenie może zakończyć się niepowodzeniem ze względu na przejście w tryb failover, należy wdrożyć logikę ponawiania połączenia, ponawianie próby połączenia, dopóki nie nastąpi ponowne połączenie.  
  
 Następujące właściwości połączenia zostały dodane do usługi SqlClient w .NET Framework 4,5:  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
 Można programowo modyfikować te słowa kluczowe parametrów połączenia przy użyciu:  
  
1. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
2. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  

> [!NOTE]
> Ustawienie `MultiSubnetFailover`niejestwymagane wprzypadku.NETFramework4.6.1lubnowszychwersji.`true`
  
## <a name="connecting-with-multisubnetfailover"></a>Łączenie z usługą MultiSubnetFailover  
 Zawsze określaj `MultiSubnetFailover=True` podczas nawiązywania połączenia z odbiornikiem grupy dostępności SQL Server 2012 lub z wystąpieniem klastra trybu failover z systemem SQL Server 2012. `MultiSubnetFailover`Włącza szybszą pracę w trybie failover dla wszystkich grup dostępności i wystąpienia klastra trybu failover w SQL Server 2012 i znacznie skraca czas pracy w trybie failover dla topologii zawsze włączonych dla jednej i kilku podsieci. Podczas pracy w trybie failover z obsługą wielopodsieci klient próbuje równolegle nawiązywania połączeń. Podczas przełączania do trybu failover w podsieci program będzie agresywnie ponawiać próbę połączenia TCP.  
  
 Właściwość `MultiSubnetFailover` Connection wskazuje, że aplikacja jest wdrażana w grupie dostępności lub wystąpieniu klastra trybu failover w systemie SQL Server 2012, a klient SqlClient podejmie próbę nawiązania połączenia z bazą danych w podstawowym wystąpieniu SQL Server, próbując Połącz się ze wszystkimi adresami IP. Gdy `MultiSubnetFailover=True` jest określony dla połączenia, klient ponawia próbę nawiązania połączenia TCP szybciej niż domyślne interwały ponownej transmisji protokołu TCP systemu operacyjnego. Umożliwia to szybsze Ponowne nawiązywanie połączenia po przejściu do trybu failover grupy dostępności AlwaysOn lub funkcji AlwaysOn klastra trybu failover i ma zastosowanie zarówno do grup dostępności, jak i dla jednej podsieci i wystąpień klastra trybu failover.  
  
 Aby uzyskać więcej informacji na temat słów kluczowych parametrów połączenia w <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>SqlClient, zobacz.  
  
 Określanie `MultiSubnetFailover=True` , czy nawiązywanie połączenia z elementem innym niż odbiornik grupy dostępności lub wystąpienie klastra trybu failover w SQL Server 2012 może skutkować negatywnym wpływem na wydajność i nie jest obsługiwane.  
  
 Skorzystaj z poniższych wskazówek, aby nawiązać połączenie z serwerem w grupie dostępności lub wystąpieniu klastra trybu failover SQL Server 2012:  
  
- Użyj właściwości `MultiSubnetFailover` Connection podczas nawiązywania połączenia z pojedynczą podsiecią lub z jedną podsiecią. spowoduje to zwiększenie wydajności obu tych wartości.  
  
- Aby nawiązać połączenie z grupą dostępności, należy określić odbiornik grupy dostępności dla grupy dostępności jako serwer w parametrach połączenia.  
  
- Połączenie z wystąpieniem SQL Server skonfigurowanym za pomocą więcej niż 64 adresów IP spowoduje błąd połączenia.  
  
- Nie ma to żadnego zastosowania w przypadku `MultiSubnetFailover` aplikacji, która używa właściwości Connection, na podstawie typu uwierzytelniania: Uwierzytelnianie SQL Server, uwierzytelnianie Kerberos lub uwierzytelnianie systemu Windows.  
  
- Zwiększ wartość `Connect Timeout` , aby uwzględnić czas pracy w trybie failover i zmniejszyć liczbę ponownych prób połączenia aplikacji.  
  
- Transakcje rozproszone nie są obsługiwane.  
  
 Jeśli Routing tylko do odczytu nie obowiązuje, połączenie z pomocniczą lokalizacją repliki zakończy się niepowodzeniem w następujących sytuacjach:  
  
1. Jeśli pomocnicza lokalizacja repliki nie jest skonfigurowana do akceptowania połączeń.  
  
2. Jeśli aplikacja używa `ApplicationIntent=ReadWrite` programu (omówione poniżej) i pomocnicza lokalizacja repliki jest skonfigurowana do dostępu tylko do odczytu.  
  
 <xref:System.Data.SqlClient.SqlDependency>nie jest obsługiwane w replikach pomocniczych tylko do odczytu.  
  
 Połączenie zakończy się niepowodzeniem, jeśli dla repliki podstawowej skonfigurowano odrzucanie obciążeń tylko do odczytu, a `ApplicationIntent=ReadOnly`parametry połączenia zawierają.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Uaktualnianie do korzystania z klastrów wielopodsieci z poziomu dublowania baz danych  
 Błąd połączenia (<xref:System.ArgumentException>) nastąpi, `MultiSubnetFailover` Jeśli w `Failover Partner` parametrach połączenia znajdują się słowa kluczowe i połączenia, `MultiSubnetFailover=True` lub jeśli używany jest protokół inny niż TCP. Błąd (<xref:System.Data.SqlClient.SqlException>) również występuje, gdy `MultiSubnetFailover` jest używany, a SQL Server zwraca odpowiedź partnera trybu failover, wskazującą, że jest częścią pary dublowania bazy danych.  
  
 W przypadku uaktualniania aplikacji SqlClient, która obecnie używa dublowania baz danych do scenariusza z obsługą kilku podsieci, należy `Failover Partner` usunąć Właściwość połączenia i zastąpić `MultiSubnetFailover` ją ustawieniem `True` ustawionym na i zastąpić nazwę serwera w parametry połączenia z odbiornikiem grupy dostępności. Jeśli parametry połączenia korzystają `Failover Partner` z i `MultiSubnetFailover=True`, sterownik wygeneruje błąd. Jeśli jednak parametry połączenia korzystają `Failover Partner` z i `MultiSubnetFailover=False` (lub `ApplicationIntent=ReadWrite`), aplikacja będzie używać funkcji dublowania baz danych.  
  
 Sterownik zwróci błąd, jeśli używana jest funkcja dublowania bazy danych w podstawowej bazie danych w sieci AG, a `MultiSubnetFailover=True` jeśli jest używana w parametrach połączenia, które łączą się z podstawową bazą danych, a nie z odbiornikiem grupy dostępności.  
  
## <a name="specifying-application-intent"></a>Określanie zamiaru aplikacji  
 Gdy `ApplicationIntent=ReadOnly`klient zażąda odczytu obciążenia podczas nawiązywania połączenia z włączoną funkcją AlwaysOn. Serwer będzie wymuszać zamiar w czasie połączenia oraz w instrukcji USE DATABASE, ale tylko do bazy danych zawsze włączone.  
  
 `ApplicationIntent` Słowo kluczowe nie działa ze starszymi bazami danych tylko do odczytu.  
  
 Baza danych może zezwalać na odczyt obciążeń lub nie zezwalać na nie. (W tym celu należy wykonać `ALLOW_CONNECTIONS` klauzulę `PRIMARY_ROLE` `SECONDARY_ROLE`instrukcji języka Transact-SQL).  
  
 `ApplicationIntent` Słowo kluczowe jest używane do włączania routingu tylko do odczytu.  
  
## <a name="read-only-routing"></a>Routing tylko do odczytu  
 Routing tylko do odczytu to funkcja, która umożliwia zapewnienie dostępności repliki tylko do odczytu bazy danych. Aby włączyć routing tylko do odczytu:  
  
1. Należy nawiązać połączenie z odbiornikiem grupy dostępności zawsze włączone.  
  
2. Słowo kluczowe parametrów `ReadOnly` połączeniamusibyć`ApplicationIntent` ustawione na wartość.  
  
3. Aby włączyć routing tylko do odczytu, Grupa dostępności musi być skonfigurowana przez administratora bazy danych.  
  
 Istnieje możliwość, że wiele połączeń przy użyciu routingu tylko do odczytu nie wszystkie nawiązują połączenie z tą samą repliką tylko do odczytu. Zmiany w synchronizacji bazy danych lub zmiany w konfiguracji routingu serwera mogą spowodować połączenia klientów z różnymi replikami tylko do odczytu. Aby upewnić się, że wszystkie żądania tylko do odczytu łączą się z tą samą repliką tylko do odczytu, nie przekazuj `Data Source` odbiornika grupy dostępności do słowa kluczowego parametrów połączenia. Zamiast tego należy określić nazwę wystąpienia tylko do odczytu.  
  
 Routing tylko do odczytu może trwać dłużej niż łączenie z serwerem podstawowym, ponieważ tylko do odczytu jest nawiązywane połączenie z serwerem podstawowym, a następnie szuka najlepszego dostępnego dodatkowego elementu pomocniczego. W związku z tym należy zwiększyć limit czasu logowania.  
  
## <a name="see-also"></a>Zobacz także

- [Funkcje Serwera SQL i ADO.NET](sql-server-features-and-adonet.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
