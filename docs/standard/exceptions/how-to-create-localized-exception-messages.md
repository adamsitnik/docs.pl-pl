---
title: 'Instrukcje: tworzenie wyjątków zdefiniowanych przez użytkownika z zastosowaniem zlokalizowanych komunikatów o wyjątkach'
description: Dowiedz się, jak tworzyć zdefiniowane przez użytkownika wyjątki przy użyciu zlokalizowanych komunikatów o wyjątkach
author: Youssef1313
ms.date: 09/13/2019
ms.openlocfilehash: 453e332541628770932da2a6802fdcaee5211a84
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73141526"
---
# <a name="how-to-create-user-defined-exceptions-with-localized-exception-messages"></a>Instrukcje: tworzenie wyjątków zdefiniowanych przez użytkownika z zastosowaniem zlokalizowanych komunikatów o wyjątkach

W tym artykule opisano sposób tworzenia wyjątków zdefiniowanych przez użytkownika, które są dziedziczone z podstawowej klasy <xref:System.Exception> ze zlokalizowanymi komunikatami o wyjątkach przy użyciu zestawów satelickich.

## <a name="create-custom-exceptions"></a>Tworzenie wyjątków niestandardowych

Platforma .NET zawiera wiele różnych wyjątków, których można użyć. Jednak w niektórych przypadkach, gdy żaden z nich nie spełnia Twoich potrzeb, można utworzyć własne wyjątki niestandardowe.

Załóżmy, że chcesz utworzyć `StudentNotFoundException`, który zawiera właściwość `StudentName`.
Aby utworzyć wyjątek niestandardowy, wykonaj następujące kroki:

1. Utwórz klasę z możliwością serializacji, która dziedziczy po <xref:System.Exception>. Nazwa klasy powinna kończyć się znakiem "Exception":

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception { }
    ```

1. Dodaj konstruktory domyślne:

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception
    {
        public StudentNotFoundException() { }

        public StudentNotFoundException(string message)
            : base(message) { }

        public StudentNotFoundException(string message, Exception inner)
            : base(message, inner) { }
    }
    ```

1. Zdefiniuj wszelkie dodatkowe właściwości i konstruktory:

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception
    {
        public string StudentName { get; }

        public StudentNotFoundException() { }

        public StudentNotFoundException(string message)
            : base(message) { }

        public StudentNotFoundException(string message, Exception inner)
            : base(message, inner) { }

        public StudentNotFoundException(string message, string studentName)
            : this(message)
        {
            StudentName = studentName;
        }
    }
    ```

## <a name="create-localized-exception-messages"></a>Tworzenie zlokalizowanych komunikatów o wyjątkach

Utworzono wyjątek niestandardowy i można go zgłosić w dowolnym miejscu przy użyciu kodu w następujący sposób:

```csharp
throw new StudentNotFoundException("The student cannot be found.", "John");
```

Problem z poprzednim wierszem to, że `"The student cannot be found."` jest tylko stałym ciągiem. W zlokalizowanej aplikacji chcesz mieć różne komunikaty w zależności od kultury użytkownika.
[Zestawy satelickie](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md) to dobry sposób na to. Zestaw satelicki to plik dll, który zawiera zasoby dla określonego języka. Po poproszeniu określonych zasobów w czasie wykonywania środowisko CLR znajdzie ten zasób w zależności od kultury użytkownika. Jeśli nie odnaleziono zestawu satelickiego dla tej kultury, używane są zasoby domyślnej kultury.

Aby utworzyć zlokalizowane komunikaty o wyjątkach:

1. Utwórz nowy folder o nazwie *resources* , aby przechowywać pliki zasobów.
1. Dodaj do niego nowy plik zasobów. Aby to zrobić w programie Visual Studio, kliknij prawym przyciskiem myszy folder w **Eksplorator rozwiązań**, a następnie wybierz pozycję **Dodaj** > **nowy element** > **plik zasobów**. Nazwij plik *ExceptionMessages. resx*. Jest to domyślny plik zasobów.
1. Dodaj parę nazwa/wartość dla komunikatu o wyjątku, jak pokazano na poniższej ilustracji:

   ![Dodaj zasoby do domyślnej kultury](media/add-resources-to-default-culture.jpg)

1. Dodaj nowy plik zasobów dla języka francuskiego. Nadaj mu nazwę *ExceptionMessages.fr-fr. resx*.
1. Ponownie Dodaj parę nazwa/wartość dla komunikatu o wyjątku, ale z wartością francuską:

   ![Dodawanie zasobów do kultury fr-FR](media/add-resources-to-fr-culture.jpg)

1. Po skompilowaniu projektu folder wyjściowy kompilacji powinien zawierać folder *fr-fr* z plikiem *dll* , który jest zestawem satelickim.
1. Należy zgłosić wyjątek z kodem podobnym do następującego:

    ```csharp
    var resourceManager = new ResourceManager("FULLY_QIALIFIED_NAME_OF_RESOURCE_FILE", Assembly.GetExecutingAssembly());
    throw new StudentNotFoundException(resourceManager.GetString("StudentNotFound"), "John");
    ```

  > [!NOTE]
  > Jeśli nazwa projektu jest `TestProject` a plik zasobów *ExceptionMessages. resx* znajduje się w folderze *resources* projektu, w pełni kwalifikowana nazwa pliku zasobów jest `TestProject.Resources.ExceptionMessages`.

## <a name="see-also"></a>Zobacz także

- [Jak utworzyć wyjątki zdefiniowane przez użytkownika](how-to-create-user-defined-exceptions.md)
- [Tworzenie zestawów satelickich dla aplikacji klasycznych](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
- [Base (C# odwołanie)](../../csharp/language-reference/keywords/base.md)
- [This (C# odwołanie)](../../csharp/language-reference/keywords/this.md)
