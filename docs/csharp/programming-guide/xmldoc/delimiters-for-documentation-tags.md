---
title: Ograniczniki tagów dokumentacji — C# Przewodnik programowania
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- XML [C#], delimiters
- /** */ delimiters for C# documentation tags
- /// delimiter for C# documentation
ms.assetid: 9b2bdd18-4f5c-4c0b-988e-fb992e0d233e
ms.openlocfilehash: 17594e557df922c1c512b4d643cd85ac76ea5a81
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72523497"
---
# <a name="delimiters-for-documentation-tags-c-programming-guide"></a>Ograniczniki znaczników dokumentacji (Przewodnik programowania w języku C#)
Użycie komentarzy w dokumencie XML wymaga ograniczników wskazujących kompilatorowi, w którym rozpoczyna się i kończą komentarz dokumentacji. Do tagów dokumentacji XML można używać następujących rodzajów ograniczników:  
  
 `///`  
 Ogranicznik pojedynczej linii. Jest to formularz, który jest wyświetlany w przykładach dokumentacji i używany przez szablony C# projektu wizualnego. Jeśli występuje znak spacji po ograniczniku, ten znak nie jest uwzględniany w danych wyjściowych XML.  
  
> [!NOTE]
> Środowisko IDE programu Visual Studio ma funkcję o nazwie edytowanie komentarzy inteligentnych, która automatycznie wstawia > \<summary i \</Summary > tagów i przenosi kursor w tych tagach po wpisaniu ogranicznika `///` w edytorze kodu. Tę funkcję można włączać lub wyłączać w [oknie dialogowym Opcje](/visualstudio/ide/reference/options-text-editor-csharp-advanced).  
  
 `/** */`  
 Ograniczniki wielowierszowe.  
  
 Istnieją pewne reguły formatowania, które należy stosować w przypadku używania ograniczników `/** */`.  
  
- W wierszu zawierającym ogranicznik `/**`, jeśli pozostała część wiersza jest białym znakiem, wiersz nie jest przetwarzany dla komentarzy. Jeśli pierwszy znak po ograniczniku `/**` jest białym znakiem, oznacza to, że odstęp jest ignorowany, a pozostała część wiersza jest przetwarzana. W przeciwnym razie cały tekst wiersza po przekroczeniu ogranicznika `/**` jest przetwarzany jako część komentarza.  
  
- W wierszu zawierającym ogranicznik `*/`, jeśli występuje tylko białe miejsce do ogranicznika `*/`, ten wiersz jest ignorowany. W przeciwnym razie tekst w wierszu do ogranicznika `*/` jest przetwarzany jako część komentarza, zgodnie z regułami dopasowywania wzorców opisanymi w następującym punkcie.  
  
- Dla linii po tej, która rozpoczyna się od ogranicznika `/**`, kompilator szuka wspólnego wzorca na początku każdego wiersza. Wzorzec może składać się z opcjonalnego odstępu i gwiazdki (`*`), po którym następuje bardziej opcjonalny odstęp. Jeśli kompilator odnajdzie wspólny wzorzec na początku każdego wiersza, który nie zaczyna się od ogranicznika `/**` lub ogranicznika `*/`, zignoruje ten wzorzec dla każdego wiersza.  
  
 Poniższe przykłady ilustrują te reguły.  
  
- Jedyną częścią poniższego komentarza, który zostanie przetworzony, jest wiersz zaczynający się od `<summary>`. Trzy formaty tagów dają te same Komentarze.  
  
    ```csharp  
    /** <summary>text</summary> */   
  
    /**   
    <summary>text</summary>   
    */   
  
    /**   
     * <summary>text</summary>   
    */  
    ```  
  
- Kompilator identyfikuje wspólny wzorzec "*" na początku drugiego i trzeciego wiersza. Wzorzec nie jest uwzględniony w danych wyjściowych.  
  
    ```csharp  
    /**   
     * <summary>   
     * text </summary>*/   
    ```  
  
- Kompilator nie znalazł wspólnego wzorca w poniższym komentarzu, ponieważ drugi znak w trzecim wierszu nie jest gwiazdką. W związku z tym cały tekst w drugim i trzecim wierszu jest przetwarzany w ramach komentarza.  
  
    ```csharp  
    /**   
     * <summary>   
       text </summary>  
    */   
    ```  
  
- Kompilator nie znalazł wzorca w poniższym komentarzu z dwóch przyczyn. Najpierw liczba spacji przed gwiazdką nie jest spójna. Sekunda, piąta linia zaczyna się od karty, która nie jest zgodna z spacjami. W związku z tym cały tekst z wierszy od dwóch do pięciu jest przetwarzany jako część komentarza.  
  
    ```csharp  
    /**   
      * <summary>   
      * text   
     *  text2   
        *  </summary>   
    */   
    ```  
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Komentarze dokumentacji XML](./index.md)
- [-doc (C# opcje kompilatora)](../../language-reference/compiler-options/doc-compiler-option.md)
- [Komentarze dokumentacji XML](./index.md)
