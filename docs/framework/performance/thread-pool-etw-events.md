---
title: Zdarzenia ETW puli wątków
ms.date: 03/30/2017
helpviewer_keywords:
- thread pool events [.NET Framework]
- ETW, thread pool events (CLR)
ms.assetid: f2a21e3a-3b6c-4433-97f3-47ff16855ecc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9a96fd4c45113afd2ab918b714bd6e12a429917c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046185"
---
# <a name="thread-pool-etw-events"></a>Zdarzenia ETW puli wątków
<a name="top"></a>Te zdarzenia zbierają informacje o wątkach procesów roboczych i we/wy.  
  
 Istnieją dwie grupy zdarzeń puli wątków:  
  
- [Zdarzenia puli wątków roboczych](#worker), które zawierają informacje o sposobie używania puli wątków przez aplikację oraz o wpływie obciążeń na kontrolę współbieżności.  
  
- [Zdarzenia puli wątków we/wy](#io), które zawierają informacje o wątkach we/wy, które są tworzone, wycofywane lub kończone w puli wątków.  
  
<a name="worker"></a>   
## <a name="worker-thread-pool-events"></a>Zdarzenia puli wątków roboczych  
 Te zdarzenia odnoszą się do puli wątków roboczych środowiska uruchomieniowego i udostępniają powiadomienia dla zdarzeń wątku (na przykład podczas tworzenia lub zatrzymywania wątku). Pula wątków roboczych używa algorytmu adaptacyjnego na potrzeby kontroli współbieżności, gdzie liczba wątków jest obliczana na podstawie zmierzonej przepływności. Zdarzenia puli wątków roboczych mogą służyć do zrozumienia, w jaki sposób aplikacja korzysta z puli wątków, a wpływ niektórych obciążeń na kontrolę współbieżności.  
  
### <a name="threadpoolworkerthreadstart-and-threadpoolworkerthreadstop"></a>ThreadPoolWorkerThreadStart i ThreadPoolWorkerThreadStop  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom dla tych zdarzeń. (Aby uzyskać więcej informacji, zobacz [słowa kluczowe i poziomy ETW CLR](clr-etw-keywords-and-levels.md)).  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-|-|-|  
|`ThreadPoolWorkerThreadStart`|50|Tworzony jest wątek roboczy.|  
|`ThreadPoolWorkerThreadStop`|51|Wątek roboczy został zatrzymany.|  
|`ThreadPoolWorkerThreadRetirementStart`|52|Wątek roboczy jest przeoponą.|  
|`ThreadPoolWorkerThreadRetirementStop`|53|Wycofywany wątek roboczy zostanie ponownie uaktywniony.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|ActiveWorkerThreadCount|win: UInt32|Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.|  
|RetiredWorkerThreadCount|win: UInt32|Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
### <a name="threadpoolworkerthreadadjustment"></a>ThreadPoolWorkerThreadAdjustment  
 Te zdarzenia puli wątków zawierają informacje dotyczące interpretacji i debugowania zachowania algorytmu wstrzykiwania wątku (kontrola współbieżności). Informacje są używane wewnętrznie przez pulę wątków roboczych.  
  
#### <a name="threadpoolworkerthreadadjustmentsample"></a>ThreadPoolWorkerThreadAdjustmentSample  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Opis|  
|-----------|--------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentSample`|54|Odnosi się do kolekcji informacji dla jednej próbki; oznacza to, że pomiar przepływności z pewnym poziomem współbieżności w czasie.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|Kazany|win: Double|Liczba zaawansowania na jednostkę czasu.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
#### <a name="threadpoolworkerthreadadjustmentadjustment"></a>ThreadPoolWorkerThreadAdjustmentAdjustment  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Opis|  
|-----------|--------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentAdjustment`|55|Rejestruje zmianę w kontrolce, gdy algorytm iniekcji wątku (Hill-wspinanie się) określa, że zmiana na poziomie współbieżności jest na miejscu.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|AverageThroughput|win: Double|Średnia przepływność próbki pomiarów.|  
|NewWorkerThreadCount|win: UInt32|Nowa liczba aktywnych wątków roboczych.|  
|Przyczyna|win: UInt32|Przyczyna korekty.<br /><br /> 0x00-rozgrzewania.<br /><br /> 0x01 — inicjowanie.<br /><br /> 0x02 — ruch losowy.<br /><br /> 0x03 — wspinanie się Przenieś.<br /><br /> 0x04 — punkt zmiany.<br /><br /> 0x05-stabilizacja.<br /><br /> 0x06 — przetrzymanie.<br /><br /> 0x07 — Przekroczono limit czasu wątku.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
#### <a name="threadpoolworkerthreadadjustmentstats"></a>ThreadPoolWorkerThreadAdjustmentStats  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Opis|  
|-----------|--------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentStats`|56|Zbiera dane w puli wątków.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|Duration|win: Double|Czas (w sekundach), w którym te statystyki zostały zebrane.|  
|Kazany|win: Double|Średnia liczba zaawansowanych na sekundę w tym interwale.|  
|ThreadWave|win: Double|Zarezerwowane do użytku wewnętrznego.|  
|ThroughputWave|win: Double|Zarezerwowane do użytku wewnętrznego.|  
|ThroughputErrorEstimate|win: Double|Zarezerwowane do użytku wewnętrznego.|  
|AverageThroughputErrorEstimate|win: Double|Zarezerwowane do użytku wewnętrznego.|  
|ThroughputRatio|win: Double|Względne ulepszenie przepływności spowodowane przez różnice w liczbie wątków roboczych w tym interwale.|  
|Confidence|win: Double|Miara ważności pola ThroughputRatio.|  
|NewcontrolSetting|win: Double|Liczba aktywnych wątków roboczych, które będą stanowić podstawę dla przyszłych różnic w aktywnej liczbie wątków.|  
|NewThreadWaveMagnitude|win: UInt16|Wielkość przyszłych wariantów w aktywnej liczbie wątków.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
 [Powrót do początku](#top)  
  
<a name="io"></a>   
## <a name="io-thread-events"></a>Zdarzenia wątku we/wy  
 Te zdarzenia puli wątków występują dla wątków w puli wątków we/wy (porty zakończenia), która jest asynchroniczna.  
  
### <a name="iothreadcreate_v1"></a>IOThreadCreate_V1  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-|-|-|  
|`IOThreadCreate_V1`|44|W puli wątków tworzony jest wątek we/wy.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|Count|win: UInt64|Liczba wątków we/wy, łącznie z nowo utworzonym wątkiem.|  
|NumRetired|win: UInt64|Liczba wycofanych wątków roboczych.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
### <a name="iothreadretire_v1"></a>IOThreadRetire_V1  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-----------|--------------|-----------------|  
|`IOThreadRetire_V1`|46|Wątek we/wy zostaje kandydatem do wycofania.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|Count|win: UInt64|Liczba wątków we/wy pozostałych w puli wątków.|  
|NumRetired|win: UInt64|Liczba wycofanych wątków we/wy.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
### <a name="iothreadunretire_v1"></a>IOThreadUnretire_V1  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-----------|--------------|-----------------|  
|`IOThreadUnretire_V1`|47|Wątek we/wy jest wycofywany ze względu na liczbę operacji we/wy, która dotarła w czasie oczekiwania, gdy wątek stanie się kandydatem wycofania.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|Count|win: UInt64|Liczba wątków we/wy w puli wątków, z uwzględnieniem tego.|  
|NumRetired|win: UInt64|Liczba wycofanych wątków we/wy.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
### <a name="iothreadterminate"></a>IOThreadTerminate  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`ThreadingKeyword`0x10000|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-----------|--------------|-----------------|  
|`IOThreadTerminate`|45|W puli wątków tworzony jest wątek we/wy.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|Count|win: UInt64|Liczba wątków we/wy pozostałych w puli wątków.|  
|NumRetired|win: UInt64|Liczba wycofanych wątków we/wy.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
## <a name="see-also"></a>Zobacz także

- [Zdarzenia CLR ETW](clr-etw-events.md)
