---
title: 'Instrukcje: Wywołaj funkcję systemu Windows, która pobiera typy bez znaku (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Windows functions [Visual Basic], calling
- unsigned data types [Visual Basic]
- UShort data type [Visual Basic], using
- functions [Visual Basic], calling Windows functions
- ULong data type [Visual Basic], using
- UInteger data type [Visual Basic], using
- data types [Visual Basic], using
- unsigned types [Visual Basic]
- data types [Visual Basic], unsigned
- data types [Visual Basic], numeric
- unsigned types [Visual Basic], using
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
ms.openlocfilehash: 97075fb6149ed8c0ce06318d0e5bb6f01b841f30
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053326"
---
# <a name="how-to-call-a-windows-function-that-takes-unsigned-types-visual-basic"></a>Instrukcje: Wywołaj funkcję systemu Windows, która pobiera typy bez znaku (Visual Basic)

Jeśli korzystasz z klasy, modułu lub struktury, która ma elementy członkowskie z niepodpisanymi typami całkowitymi, możesz uzyskać dostęp do tych elementów członkowskich za pomocą Visual Basic.

## <a name="to-call-a-windows-function-that-takes-an-unsigned-type"></a>Aby wywołać funkcję systemu Windows, która ma typ bez znaku

1. Użyj [instrukcji DECLARE](../../../visual-basic/language-reference/statements/declare-statement.md) , aby poinformować Visual Basic bibliotekę, w której znajduje się ta funkcja, jak jej nazwa znajduje się w tej bibliotece, co to jest sekwencja wywoływania i jak konwertować ciągi podczas wywoływania.

2. `UInteger`W instrukcji Użyj ,`ULong` ,`UShort`, lub`Byte` , w zależności od parametru z niepodpisanym typem. `Declare`

3. Zapoznaj się z dokumentacją funkcji systemu Windows, która jest wywoływana, aby znaleźć nazwy i wartości stałych, z których korzysta. Wiele z nich jest zdefiniowanych w pliku WinUser. h.

4. Zadeklaruj niezbędne stałe w kodzie. Wiele stałych systemu Windows to 32-bitowe wartości bez znaku i należy je `As UInteger`zadeklarować.

5. Wywołaj funkcję w zwykły sposób. Poniższy przykład wywołuje funkcję `MessageBox`systemu Windows, która przyjmuje argument liczby całkowitej bez znaku.

    ```vb
    Public Class windowsMessage
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (
            ByVal hWnd As Integer,
            ByVal lpText As String,
            ByVal lpCaption As String,
            ByVal uType As UInteger) As Integer
        Private Const MB_OK As UInteger = 0
        Private Const MB_ICONEXCLAMATION As UInteger = &H30
        Private Const IDOK As UInteger = 1
        Private Const IDCLOSE As UInteger = 8
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION
        Public Function messageThroughWindows() As String
            Dim r As Integer = mb(0, "Click OK if you see this!",
                "Windows API call", c)
            Dim s As String = "Windows API MessageBox returned " &
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"
            Return s
        End Function
    End Class
    ```

     Funkcję `messageThroughWindows` można przetestować przy użyciu następującego kodu.

    ```vb
    Public Sub consumeWindowsMessage()
        Dim w As New windowsMessage
        w.messageThroughWindows()
    End Sub
    ```

    > [!CAUTION]
    > `UInteger` ,`ULong`, ,I`SByte` typy danych nie są częścią [niezależności od języka i składników niezależnych od języka](../../../standard/language-independence-and-language-independent-components.md) (CLS), więc kod zgodny ze specyfikacją CLS nie może zużywać składnika, który z nich korzysta. `UShort`

    > [!IMPORTANT]
    > Wywoływanie kodu niezarządzanego, takiego jak interfejs programowania aplikacji (API) systemu Windows, uwidacznia swój kod na potencjalne zagrożenia bezpieczeństwa.

    > [!IMPORTANT]
    > Wywołanie interfejsu API systemu Windows wymaga uprawnień do kodu niezarządzanego, co może mieć wpływ na wykonywanie w sytuacjach częściowej relacji zaufania. Aby uzyskać więcej informacji, <xref:System.Security.Permissions.SecurityPermission> Zobacz i [uprawnienia dostępu kodu](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h846e9b3(v=vs.100)).

## <a name="see-also"></a>Zobacz także

- [Typy danych](../../../visual-basic/language-reference/data-types/index.md)
- [Integer, typ danych](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [UInteger, typ danych](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)
- [Declare, instrukcja](../../../visual-basic/language-reference/statements/declare-statement.md)
- [Przewodnik: wywoływanie interfejsów API systemu Windows](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
