---
title: 'Punkt końcowy: Przepływ transakcji na sekundę'
ms.date: 03/30/2017
ms.assetid: 0f370ff1-a913-450b-bccb-c279ad165b3d
ms.openlocfilehash: 79f50b6706facd040ec2d325c676f210d5327bf8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61916256"
---
# <a name="endpoint-transactions-flowed-per-second"></a>Punkt końcowy: Przepływ transakcji na sekundę
Nazwa komputera: Przepływ transakcji na sekundę.  
  
## <a name="description"></a>Opis  
 Liczba transakcji przekazane do operacji w tym punkcie końcowym w ciągu sekundy. Ten licznik jest zwiększany ilekroć dowolny identyfikator transakcji znajduje się w wiadomości wysyłane do punktu końcowego.  
  
 Ten licznik jest typ licznika wydajności [PERF_COUNTER_COUNTER](https://go.microsoft.com/fwlink/?LinkID=94649), którego wartość jest obliczana przy użyciu następującej formuły.  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)
