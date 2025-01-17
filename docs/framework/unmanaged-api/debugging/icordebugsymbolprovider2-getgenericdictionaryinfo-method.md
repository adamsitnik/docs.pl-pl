---
title: 'ICorDebugSymbolProvider2:: GetGenericDictionaryInfo, Metoda'
ms.date: 03/30/2017
ms.assetid: ba28fe4e-5491-4670-bff7-7fde572d7593
ms.openlocfilehash: c9f7206cac54d64c28eb50d81fea00a6f3c494d4
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73133632"
---
# <a name="icordebugsymbolprovider2getgenericdictionaryinfo-method"></a>ICorDebugSymbolProvider2:: GetGenericDictionaryInfo, Metoda

Pobiera mapę ogólnego słownika.

## <a name="syntax"></a>Składnia

```cpp
HRESULT GetGenericDictionaryInfo(
   [out] ICorDebugMemoryBuffer** ppMemoryBuffer
);
```

## <a name="parameters"></a>Parametry

`ppMemoryBuffer`\
określoną Wskaźnik do adresu obiektu [ICorDebugMemoryBuffer](../../../../docs/framework/unmanaged-api/debugging/icordebugmemorybuffer-interface.md) zawierającego mapę ogólnego słownika. Zobacz sekcję Spostrzeżenia, aby uzyskać więcej informacji.

## <a name="remarks"></a>Uwagi

> [!NOTE]
> Ta metoda jest dostępna tylko z .NET Native.

Mapa składa się z dwóch sekcji najwyższego poziomu:

- [Katalog](#Directory) zawierający względne adresy wirtualne (RVA) wszystkich słowników uwzględnionych w tej mapie.

- [Stos](#Heap) wyrównany do bajtów zawierający informacje o tworzeniu wystąpienia obiektu. Rozpocznie się natychmiast po ostatnim wpisie w katalogu.

<a name="Directory"></a>

## <a name="the-directory"></a>Katalog

Każdy wpis w katalogu odnosi się do przesunięcia wewnątrz sterty; oznacza to, że jest to przesunięcie odnoszące się do początku sterty. Wartość poszczególnych wpisów nie musi być unikatowa. Istnieje możliwość, że wiele wpisów katalogu wskazuje na to samo przesunięcie w stercie.

Część katalogu ogólnego mapowania słownika ma następującą strukturę:

- Pierwsze 4 bajty zawierają liczbę wpisów słownika (czyli liczbę względnych adresów wirtualnych w słowniku). Ta wartość zostanie odwołująca się do tej wartości jako *N*. Jeśli jest ustawiony wysoki bit, wpisy są sortowane według względnych adresów wirtualnych w kolejności rosnącej.

- Wpisy katalogu *N* są następujące. Każdy wpis składa się z 8 bajtów w dwóch segmentach 4-bajtowych:

  - Bajty 0-3: RVA; względny adres wirtualny słownika.

  - Bajty 4-7: przesunięcie; przesunięcie względem początku sterty.

<a name="Heap"></a>

## <a name="the-heap"></a>Sterta

Rozmiar sterty może być obliczany przez czytnik strumienia przez odjęcie długości strumienia od rozmiaru katalogu + 4. Innymi słowy:

```csharp
Heap Size = Stream.Length – (Directory Size + 4)
```

miejsce, w którym rozmiar katalogu jest `N * 8`.

Format każdego elementu informacji o tworzeniu wystąpienia na stercie to:

- Długość tego elementu informacji o tworzeniu wystąpienia w bajtach w skompresowanym formacie metadanych ECMA. Ta wartość wyklucza informacje o długości.

- Liczba typów ogólnych wystąpień wystąpienia lub *T*w formacie skompresowanego metadanych ECMA.

- Typy *T* , każdy reprezentowane w formacie sygnatury typu ECMA.

Włączenie długości dla każdego elementu sterty umożliwia proste sortowanie sekcji katalogu bez wpływu na stertę.

## <a name="requirements"></a>Wymagania

**Platformy:** Zobacz [wymagania systemowe](../../../../docs/framework/get-started/system-requirements.md).

**Nagłówek:** CorDebug. idl, CorDebug. h

**Biblioteka:** CorGuids. lib

**Wersje .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]

## <a name="see-also"></a>Zobacz także

- [ICorDebugSymbolProvider2, interfejs](../../../../docs/framework/unmanaged-api/debugging/icordebugsymbolprovider2-interface.md)
- [Debugowanie, interfejsy](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
