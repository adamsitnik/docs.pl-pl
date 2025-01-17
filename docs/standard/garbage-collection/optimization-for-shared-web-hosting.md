---
title: Optymalizacja udostępnionej usługi hostingu sieci Web
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, Web hosting
- garbage collection, optimizing
- garbage collection, shared Web hosting
ms.assetid: be98c0ab-7ef8-409f-8a0d-cb6e5b75ff20
ms.openlocfilehash: 07a100e2cd6aaff2b54b99144c9d762c8979fb47
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140273"
---
# <a name="optimization-for-shared-web-hosting"></a>Optymalizacja udostępnionej usługi hostingu sieci Web
Jeśli jesteś administratorem serwera, który jest udostępniany przez hosting kilku małych witryn sieci Web, możesz zoptymalizować wydajność i zwiększyć pojemność lokacji, dodając następujące ustawienie `gcTrimCommitOnLowMemory` do węzła `runtime` w pliku aspnet. config w katalogu .NET :  
  
 `<gcTrimCommitOnLowMemory enabled="true|false"/>`  
  
> [!NOTE]
> To ustawienie jest zalecane tylko w scenariuszach hostingu w sieci Web.  
  
 Ponieważ moduł wyrzucania elementów bezużytecznych zachowuje pamięć dla przyszłych przydziałów, jego zatwierdzone miejsce może być większe niż to, co jest absolutnie wymagane. Można zmniejszyć to miejsce do czasu, gdy występuje duże obciążenie pamięci systemowej. Zmniejszenie ilości tego zajmowanego miejsca zwiększa wydajność i zwiększa możliwości hostowania większej liczby lokacji.  
  
 Gdy ustawienie `gcTrimCommitOnLowMemory` jest włączone, moduł zbierający elementy bezużyteczne szacuje obciążenie pamięci systemowej i przechodzi do trybu przycinania, gdy obciążenie osiągnie 90%. Utrzymuje tryb przycinania do momentu spadku obciążenia poniżej 85%.  
  
 Gdy warunki zezwalają, Moduł wyrzucania elementów bezużytecznych może zdecydować, że ustawienie `gcTrimCommitOnLowMemory` nie będzie pomocne dla bieżącej aplikacji i nie zostanie zignorowane.  
  
## <a name="example"></a>Przykład  
 Poniższy fragment kodu XML pokazuje, jak włączyć ustawienie `gcTrimCommitOnLowMemory`. Elipsy wskazują inne ustawienia, które mogą znajdować się w węźle `runtime`.  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <runtime>  
    . . .  
    <gcTrimCommitOnLowMemory enabled="true"/>  
    </runtime>  
    . . .  
</configuration>  
```  
  
## <a name="see-also"></a>Zobacz także

- [Odzyskiwanie pamięci](../../../docs/standard/garbage-collection/index.md)
