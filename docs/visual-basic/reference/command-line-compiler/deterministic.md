---
title: -deterministic
ms.date: 04/11/2018
helpviewer_keywords:
- deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
ms.openlocfilehash: 6a83b636dd83534788f3a38971e0fef2919314f5
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005630"
---
# <a name="-deterministic"></a>-deterministic

Powoduje, że kompilator tworzy zestaw, którego bajty w bajtach są identyczne w kompilacjach dla identycznych danych wejściowych.

## <a name="syntax"></a>Składnia

```console
-deterministic
```

## <a name="remarks"></a>Uwagi

Domyślnie dane wyjściowe kompilatora z danego zestawu danych wejściowych są unikatowe, ponieważ kompilator dodaje sygnaturę czasową i identyfikator GUID, który jest generowany na podstawie liczb losowych. Opcja `-deterministic` służy do tworzenia *deterministycznego zestawu*, który jest identyczny z zawartością binarną w kompilacjach, o ile dane wejściowe pozostają takie same.

Kompilator traktuje następujące dane wejściowe na potrzeby ustalenia:

- Sekwencja parametrów wiersza polecenia.
- Zawartość pliku odpowiedzi kompilatora. rsp.
- Dokładna wersja używanego kompilatora oraz zestawy, do których się odwołuje.
- Bieżąca ścieżka katalogu.
- Zawartość binarna wszystkich plików jawnie przekazana do kompilatora bezpośrednio lub pośrednio, w tym:
  - Pliki źródłowe
  - Przywoływane zestawy
  - Moduły, do których istnieją odwołania
  - Resources
  - Plik klucza o silnej nazwie
  - pliki odpowiedzi @
  - Analizatory
  - Zestaw reguł
  - Dodatkowe pliki, które mogą być używane przez analizatory
- Bieżąca kultura (dla języka, w którym są generowane diagnostyczne i komunikaty o wyjątkach).
- Domyślne kodowanie (lub bieżącą stronę kodową), Jeśli kodowanie nie jest określone.
- Istnienie, nieistnienie i zawartość plików na ścieżkach wyszukiwania kompilatora (na przykład przez `/lib` lub `/recurse`).
- Platforma CLR, na której jest uruchomiony kompilator.
- Wartość `%LIBPATH%`, która może wpływać na ładowanie zależności analizatora.

Gdy źródła są dostępne publicznie, można użyć deterministycznej kompilacji do ustalenia, czy plik binarny jest kompilowany z zaufanego źródła. Może być również przydatna w systemie ciągłej kompilacji, aby określić, czy należy wykonać kroki kompilacji, które są zależne od zmian w pliku binarnym.

## <a name="see-also"></a>Zobacz także

- [Kompilator wiersza polecenia Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [Przykłady kompilacji — wiersze poleceń](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
