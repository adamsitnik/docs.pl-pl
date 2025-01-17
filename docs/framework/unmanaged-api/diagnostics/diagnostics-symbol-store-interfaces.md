---
title: Interfejsy magazynu symboli diagnostycznych
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- diagnostics symbol store interfaces [.NET Framework]
- interfaces [.NET Framework], diagnostics symbol store
- unmanaged interfaces [.NET Framework], diagnostics symbol store
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: f96987d5-e6a5-478b-ac5e-302e16545cce
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6fca7359888b8b73b2e1cf709ab708d71abf0db6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787897"
---
# <a name="diagnostics-symbol-store-interfaces"></a>Interfejsy magazynu symboli diagnostycznych
W tym temacie opisano niezarządzane interfejsy, które umożliwiają kompilatora do generowania informacji o symbolach do użytku przez debuger.  
  
## <a name="in-this-section"></a>W tej sekcji  
 [IBindingDisplay, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/ibindingdisplay-interface.md)  
 Udostępnia metody, które wyświetlają bieżące informacje o powiązaniu o uruchomionej aplikacji.  
  
 [IDebugAutoAttach, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/idebugautoattach-interface.md)  
 Definiuje interfejs dla automatycznego wywoływane serwer debugera dołączania.  
  
 [INotifyConnection2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/inotifyconnection2-interface.md)  
 Deklaruje metody zarejestrować lub wyrejestrować źródła powiadomień połączenia.  
  
 [INotifySink2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/inotifysink2-interface.md)  
 Deklaruje metody dla obiektu sink powiadomień.  
  
 [INotifySource2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/inotifysource2-interface.md)  
 Deklaruje metody do ustawiania filtrów powiadomień.  
  
 [ISymENCUnmanagedMethod, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-interface.md)  
 Informacje dotyczące funkcji Edytuj i Kontynuuj.  
  
 [ISymUnmanagedAsyncMethod, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethod-interface.md)  
 Ten interfejs jest to uzupełnienie odczytu [ISymUnmanagedAsyncMethodPropertiesWriter, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-interface.md).  
  
 [ISymUnmanagedAsyncMethodPropertiesWriter, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-interface.md)  
 Pozwala na określenie informacji o metodzie async opcjonalne na symbol metody. Należy używać z metodą otwarte (to znaczy między wywołaniami [openmethod — metoda](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openmethod-method.md)i [closemethod — metoda](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closemethod-method.md)).  
  
 [ISymUnmanagedBinder, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder-interface.md)  
 Reprezentuje integrator symboli dla niezarządzanego kodu.  
  
 [ISymUnmanagedBinder2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder2-interface.md)  
 Reprezentuje integrator symboli dla niezarządzanego kodu i rozszerza `ISymUnmanagedBinder` interfejsu.  
  
 [ISymUnmanagedBinder3, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder3-interface.md)  
 Reprezentuje integrator symboli dla niezarządzanego kodu i rozszerza `ISymUnmanagedBinder` interfejsu.  
  
 [ISymUnmanagedConstant, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedconstant-interface.md)  
 Zapewnia dostęp do niezarządzanego stałych.  
  
 [ISymUnmanagedDispose, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddispose-interface.md)  
 Usuwa zasoby niezarządzane.  
  
 [ISymUnmanagedDocument, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)  
 Reprezentuje dokument odwołuje się w magazynie symboli.  
  
 [ISymUnmanagedDocumentWriter, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocumentwriter-interface.md)  
 Udostępnia metody do zapisywania dokumentu odwołuje się w magazynie symboli.  
  
 [ISymUnmanagedENCUpdate, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedencupdate-interface.md)  
 Udostępnia metody dla funkcji Edytuj i Kontynuuj.  
  
 [ISymUnmanagedMethod, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedmethod-interface.md)  
 Reprezentuje metodę w magazynie symboli.  
  
 [ISymUnmanagedNamespace, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagednamespace-interface.md)  
 Reprezentuje obszar nazw.  
  
 [ISymUnmanagedReader, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md)  
 Reprezentuje czytnik symbolu, który zapewnia dostęp do dokumentów, metod i zmiennych w magazynie symboli.  
  
 [ISymUnmanagedReader2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader2-interface.md)  
 Pobiera metodę czytnika symboli podany token metody i numeru wersji edycji i kopiowania.  
  
 [ISymUnmanagedReaderSymbolSearchInfo, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreadersymbolsearchinfo-interface.md)  
 Udostępnia metody, które zawierają informacje o wyszukiwaniu symboli.  
  
 [ISymUnmanagedScope, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedscope-interface.md)  
 Reprezentuje zakresie leksykalnym wewnątrz metody.  
  
 [ISymUnmanagedScope2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedscope2-interface.md)  
 Reprezentuje zakresie leksykalnym wewnątrz metody i rozszerza `ISymUnmanagedScope` interfejs, za pomocą metod, które uzyskać informacje na temat stałe zdefiniowane w zakresie...  
  
 [ISymUnmanagedSourceServerModule, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsourceservermodule-interface.md)  
 Udostępnia dane z serwera źródłowego dla modułu.  
  
 [ISymUnmanagedSymbolSearchInfo, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-interface.md)  
 Udostępnia metody, które zawierają informacje o ścieżce wyszukiwania.  
  
 [ISymUnmanagedVariable, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-interface.md)  
 Reprezentuje zmienną, takie jak parametr, zmienna lokalna lub pola.  
  
 [ISymUnmanagedWriter, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)  
 Reprezentuje edytor symboli i zapewnia metody do definiowania dokumentów, punktów sekwencji, leksykalne zakresy i zmienne.  
  
 [ISymUnmanagedWriter2, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter2-interface.md)  
 Reprezentuje edytor symboli i zapewnia metody do definiowania dokumentów, punktów sekwencji, leksykalne zakresy i zmienne. Rozszerza `ISymUnmanagedWriter` interfejsu.  
  
 [ISymUnmanagedWriter3, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter3-interface.md)  
 Reprezentuje edytor symboli i zapewnia metody do definiowania dokumentów, punktów sekwencji, leksykalne zakresy i zmienne. Rozszerza `ISymUnmanagedWriter` interfejsu.  
  
 [ISymUnmanagedWriter4, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter4-interface.md)  
 ISymUnmanagedWriter4, interfejs  
  
 [ISymUnmanagedWriter5, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter5-interface.md)  
 ISymUnmanagedWriter5, interfejs  
  
## <a name="related-sections"></a>Sekcje pokrewne  
 [Wyliczenia magazynu symboli diagnostycznych](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-enumerations.md)  
  
 [Struktury magazynu symboli diagnostycznych](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-structures.md)  
  
 [Debugowanie](../../../../docs/framework/unmanaged-api/debugging/index.md)
