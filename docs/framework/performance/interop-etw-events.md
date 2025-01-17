---
title: Zdarzenia ETW międzyoperacyjności
ms.date: 03/30/2017
helpviewer_keywords:
- interop events [.NET Framework]
- ETW, interop events (CLR)
ms.assetid: eb6eac2e-45f4-4923-a32c-38f203da66df
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 787c6221b651a53dbb932a5a9d0edea123e1d97d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046435"
---
# <a name="interop-etw-events"></a>Zdarzenia ETW międzyoperacyjności
<a name="top"></a>Zdarzenia międzyoperacyjności przechwytują informacje o generacji i buforowaniu klasy języka pośredniego firmy Microsoft (MSIL).  
  
 Ta kategoria obejmuje następujące zdarzenia:  
  
- [Zdarzenie ILStubGenerated](#ilstubgenerated_event)  
  
- [ILStubCacheHit Event](#ilstubcachehit_event)  
  
<a name="ilstubgenerated_event"></a>   
## <a name="ilstubgenerated-event"></a>Zdarzenie ILStubGenerated  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom. (Aby uzyskać więcej informacji, zobacz [słowa kluczowe i poziomy ETW CLR](clr-etw-keywords-and-levels.md)).  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`InteropKeyword` (0x2000)|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-----------|--------------|-----------------|  
|`ILStubGenerated`|88|Wygenerowało procedurę pośredniczącą MSIL.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|ModuleID|win: UInt16|Identyfikator modułu.|  
|StubMethodID|win: UInt64|Identyfikator metody zastępczej.|  
|StubFlags|win: UInt64|Flagi dla elementu zastępczego:<br /><br /> 0x1 — odwrotna współdziałanie.<br /><br /> 0x2 — międzyoperacyjność COM.<br /><br /> 0x4-stub wygenerowane przez program NGen. exe.<br /><br /> 0x8 — delegat.<br /><br /> 0x10 — argument zmiennej.<br /><br /> 0x20 — niezarządzany wywoływany.|  
|ManagedInteropMethodToken|win: UInt32|Token dla zarządzanej metody międzyoperacyjnego.|  
|ManagedInteropMethodNameSpace|win: UnicodeString|Przestrzeń nazw zarządzanej metody międzyoperacyjnego.|  
|ManagedInteropMethodName|win: UnicodeString|Nazwa zarządzanej metody międzyoperacyjnego.|  
|ManagedInteropMethodSignature|win: UnicodeString|Sygnatura zarządzanej metody międzyoperacyjnego.|  
|NativeMethodSignature|win: UnicodeString|Podpis metody natywnej.|  
|StubMethodSignature|win: UnicodeString|Sygnatura metody zastępczej.|  
|StubMethodILCode|win: UnicodeString|Kod MSIL dla metody zastępczej.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
 [Powrót do początku](#top)  
  
<a name="ilstubcachehit_event"></a>   
## <a name="ilstubcachehit-event"></a>ILStubCacheHit Event  
 W poniższej tabeli przedstawiono słowo kluczowe i poziom.  
  
|Słowo kluczowe do podniesienia zdarzenia|Poziom|  
|-----------------------------------|-----------|  
|`InteropKeyword` (0x2000)|Informacyjny (4)|  
  
 W poniższej tabeli przedstawiono informacje o zdarzeniu.  
  
|Zdarzenie|Identyfikator zdarzenia|Wywoływane, gdy|  
|-----------|--------------|-----------------|  
|`ILStubCacheHit`|89|Dostęp do pamięci podręcznej MSIL został uzyskany.|  
  
 W poniższej tabeli przedstawiono dane zdarzenia.  
  
|Nazwa pola|Typ danych|Opis|  
|----------------|---------------|-----------------|  
|ModuleID|win: UInt16|Identyfikator modułu.|  
|StubMethodID|win: UInt64|Identyfikator metody zastępczej.|  
|ManagedInteropMethodToken|win: UInt32|Token dla zarządzanej metody międzyoperacyjnego.|  
|ManagedInteropMethodNameSpace|win: UnicodeString|Przestrzeń nazw zarządzanej metody międzyoperacyjnego.|  
|ManagedInteropMethodName|win: UnicodeString|Nazwa zarządzanej metody międzyoperacyjnego.|  
|ManagedInteropMethodSignature|win: UnicodeString|Sygnatura zarządzanej metody międzyoperacyjnego.|  
|ClrInstanceID|win: UInt16|Unikatowy identyfikator wystąpienia CLR lub CoreCLR.|  
  
 [Powrót do początku](#top)  
  
## <a name="see-also"></a>Zobacz także

- [Zdarzenia CLR ETW](clr-etw-events.md)
