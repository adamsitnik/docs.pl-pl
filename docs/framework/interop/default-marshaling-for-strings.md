---
title: Organizowanie domyślne dotyczące ciągów
ms.date: 03/20/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings, interop marshaling
- interop marshaling, strings
ms.assetid: 9baea3ce-27b3-4b4f-af98-9ad0f9467e6f
ms.openlocfilehash: 49f2d871a42db484e20f0bfc35634a0e8b959c2e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73123552"
---
# <a name="default-marshaling-for-strings"></a>Organizowanie domyślne dotyczące ciągów

Klasy <xref:System.String?displayProperty=nameWithType> i <xref:System.Text.StringBuilder?displayProperty=nameWithType> mają podobne zachowanie organizowania.

Ciągi są organizowane jako typ `BSTR` stylu COM lub jako ciąg zakończony znakiem null (tablica znaków, która kończy się znakiem null). Znaki w ciągu mogą być organizowane jako Unicode (domyślnie w systemach Windows) lub ANSI.

## <a name="strings-used-in-interfaces"></a>Ciągi używane w interfejsach

W poniższej tabeli przedstawiono opcje kierowania dla typu danych ciągu, które są organizowane jako argumenty metody do kodu niezarządzanego. Atrybut <xref:System.Runtime.InteropServices.MarshalAsAttribute> zawiera kilka <xref:System.Runtime.InteropServices.UnmanagedType> wartości wyliczenia do kierowania ciągów do interfejsów COM.

|Typ wyliczenia|Opis niezarządzanego formatu|
|----------------------|-------------------------------------|
|`UnmanagedType.BStr` (wartość domyślna)|Styl COM `BSTR` ze wstępnie ustaloną długością i znakami Unicode.|
|`UnmanagedType.LPStr`|Wskaźnik do tablicy znaków ANSI zakończonych znakiem null.|
|`UnmanagedType.LPWStr`|Wskaźnik do tablicy znaków Unicode zakończonych wartością null.|

Ta tabela ma zastosowanie do <xref:System.String>. W przypadku <xref:System.Text.StringBuilder>Jedyne dozwolone opcje to `UnmanagedType.LPStr` i `UnmanagedType.LPWStr`.

Poniższy przykład przedstawia ciągi zadeklarowane w interfejsie `IStringWorker`.

```csharp
public interface IStringWorker
{
    void PassString1(string s);
    void PassString2([MarshalAs(UnmanagedType.BStr)] string s);
    void PassString3([MarshalAs(UnmanagedType.LPStr)] string s);
    void PassString4([MarshalAs(UnmanagedType.LPWStr)] string s);
    void PassStringRef1(ref string s);
    void PassStringRef2([MarshalAs(UnmanagedType.BStr)] ref string s);
    void PassStringRef3([MarshalAs(UnmanagedType.LPStr)] ref string s);
    void PassStringRef4([MarshalAs(UnmanagedType.LPWStr)] ref string s);
}
```

```vb
Public Interface IStringWorker
    Sub PassString1(s As String)
    Sub PassString2(<MarshalAs(UnmanagedType.BStr)> s As String)
    Sub PassString3(<MarshalAs(UnmanagedType.LPStr)> s As String)
    Sub PassString4(<MarshalAs(UnmanagedType.LPWStr)> s As String)
    Sub PassStringRef1(ByRef s As String)
    Sub PassStringRef2(<MarshalAs(UnmanagedType.BStr)> ByRef s As String)
    Sub PassStringRef3(<MarshalAs(UnmanagedType.LPStr)> ByRef s As String)
    Sub PassStringRef4(<MarshalAs(UnmanagedType.LPWStr)> ByRef s As String)
End Interface
```

Poniższy przykład pokazuje odpowiedni interfejs opisany w bibliotece typów.

```cpp
interface IStringWorker : IDispatch
{
    HRESULT PassString1([in] BSTR s);
    HRESULT PassString2([in] BSTR s);
    HRESULT PassString3([in] LPStr s);
    HRESULT PassString4([in] LPWStr s);
    HRESULT PassStringRef1([in, out] BSTR *s);
    HRESULT PassStringRef2([in, out] BSTR *s);
    HRESULT PassStringRef3([in, out] LPStr *s);
    HRESULT PassStringRef4([in, out] LPWStr *s);
};
```

## <a name="strings-used-in-platform-invoke"></a>Ciągi używane w wywołaniu platformy

Wywołanie platformy kopiuje argumenty ciągu, konwertując z formatu .NET Framework (Unicode) na format niezarządzany platformy. Ciągi są niezmienne i nie są kopiowane z pamięci niezarządzanej do pamięci zarządzanej, gdy wywołanie zwraca wartość.

W poniższej tabeli wymieniono opcje kierowania dla ciągów, które są organizowane jako argumenty metody wywołania wywołania platformy. Atrybut <xref:System.Runtime.InteropServices.MarshalAsAttribute> zawiera kilka <xref:System.Runtime.InteropServices.UnmanagedType> wartości wyliczenia do organizowania ciągów.

|Typ wyliczenia|Opis niezarządzanego formatu|
|----------------------|-------------------------------------|
|`UnmanagedType.AnsiBStr`|Styl COM `BSTR` ze wstępnie ustaloną długością i znakami ANSI.|
|`UnmanagedType.BStr`|Styl COM `BSTR` ze wstępnie ustaloną długością i znakami Unicode.|
|`UnmanagedType.LPStr` (wartość domyślna)|Wskaźnik do tablicy znaków ANSI zakończonych znakiem null.|
|`UnmanagedType.LPTStr`|Wskaźnik do tablicy zakończonych znakiem NULL znaków zależnych od platformy.|
|`UnmanagedType.LPUTF8Str`|Wskaźnik do tablicy kodowanej za pomocą wartości NULL znaków zakodowanych w formacie UTF-8.|
|`UnmanagedType.LPWStr`|Wskaźnik do tablicy znaków Unicode zakończonych wartością null.|
|`UnmanagedType.TBStr`|Styl COM `BSTR` ze wstępnie ustaloną długością i znakami zależnymi od platformy.|
|`VBByRefStr`|Wartość, która umożliwia Visual Basic .NET, aby zmienić ciąg w kodzie niezarządzanym i mieć wyniki odzwierciedlone w kodzie zarządzanym. Ta wartość jest obsługiwana tylko w przypadku wywołania platformy. Jest to wartość domyślna w Visual Basic dla ciągów `ByVal`.|

Ta tabela ma zastosowanie do <xref:System.String>. W przypadku <xref:System.Text.StringBuilder>Jedyne dozwolone opcje to `LPStr`, `LPTStr`i `LPWStr`.

W poniższej definicji typu przedstawiono poprawne użycie `MarshalAsAttribute` dla wywołań wywołania platformy.

```csharp
class StringLibAPI
{
    [DllImport("StringLib.dll")]
    public static extern void PassLPStr([MarshalAs(UnmanagedType.LPStr)] string s);
    [DllImport("StringLib.dll")]
    public static extern void PassLPWStr([MarshalAs(UnmanagedType.LPWStr)] string s);
    [DllImport("StringLib.dll")]
    public static extern void PassLPTStr([MarshalAs(UnmanagedType.LPTStr)] string s);
    [DllImport("StringLib.dll")]
    public static extern void PassLPUTF8Str([MarshalAs(UnmanagedType.LPUTF8Str)] string s);
    [DllImport("StringLib.dll")]
    public static extern void PassBStr([MarshalAs(UnmanagedType.BStr)] string s);
    [DllImport("StringLib.dll")]
    public static extern void PassAnsiBStr([MarshalAs(UnmanagedType.AnsiBStr)] string s);
    [DllImport("StringLib.dll")]
    public static extern void PassTBStr([MarshalAs(UnmanagedType.TBStr)] string s);
}
```

```vb
Class StringLibAPI
    Public Declare Auto Sub PassLPStr Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.LPStr)> s As String)
    Public Declare Auto Sub PassLPWStr Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.LPWStr)> s As String)
    Public Declare Auto Sub PassLPTStr Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.LPTStr)> s As String)
    Public Declare Auto Sub PassLPUTF8Str Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.LPUTF8Str)> s As String)
    Public Declare Auto Sub PassBStr Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.BStr)> s As String)
    Public Declare Auto Sub PassAnsiBStr Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.AnsiBStr)> s As String)
    Public Declare Auto Sub PassTBStr Lib "StringLib.dll" (
        <MarshalAs(UnmanagedType.TBStr)> s As String)
End Class
```

## <a name="strings-used-in-structures"></a>Ciągi używane w strukturach

Ciągi są prawidłowymi elementami członkowskimi struktur; jednak bufory <xref:System.Text.StringBuilder> są nieprawidłowe w strukturach. W poniższej tabeli przedstawiono opcje organizowania dla <xref:System.String> typ danych, gdy typ jest zorganizowany jako pole. Atrybut <xref:System.Runtime.InteropServices.MarshalAsAttribute> zawiera kilka <xref:System.Runtime.InteropServices.UnmanagedType> wartości wyliczenia, które umożliwiają kierowanie ciągów do pola.

|Typ wyliczenia|Opis niezarządzanego formatu|
|----------------------|-------------------------------------|
|`UnmanagedType.BStr`|Styl COM `BSTR` ze wstępnie ustaloną długością i znakami Unicode.|
|`UnmanagedType.LPStr` (wartość domyślna)|Wskaźnik do tablicy znaków ANSI zakończonych znakiem null.|
|`UnmanagedType.LPTStr`|Wskaźnik do tablicy zakończonych znakiem NULL znaków zależnych od platformy.|
|`UnmanagedType.LPUTF8Str`|Wskaźnik do tablicy kodowanej za pomocą wartości NULL znaków zakodowanych w formacie UTF-8.|
|`UnmanagedType.LPWStr`|Wskaźnik do tablicy znaków Unicode zakończonych wartością null.|
|`UnmanagedType.ByValTStr`|Tablica znaków o stałej długości; typ tablicy jest określany przez zestaw znaków struktury zawierającej.|

Typ `ByValTStr` jest używany w przypadku wbudowanych tablic znaków o stałej długości, które pojawiają się w obrębie struktury. Inne typy są stosowane do odwołań do ciągów zawartych w strukturach, które zawierają wskaźniki do ciągów.

`CharSet` argument <xref:System.Runtime.InteropServices.StructLayoutAttribute>, który jest stosowany do struktury zawierającej, określa format znaków ciągów w strukturach. Następujące przykładowe struktury zawierają odwołania do ciągów i ciągi śródwierszowe oraz znaki ANSI, Unicode i. Reprezentacja tych struktur w bibliotece typów jest pokazana w poniższym C++ kodzie:

```cpp
struct StringInfoA
{
    char *  f1;
    char    f2[256];
};

struct StringInfoW
{
    WCHAR * f1;
    WCHAR   f2[256];
    BSTR    f3;
};

struct StringInfoT
{
    TCHAR * f1;
    TCHAR   f2[256];
};
```

Poniższy przykład pokazuje, jak używać <xref:System.Runtime.InteropServices.MarshalAsAttribute> do definiowania tej samej struktury w różnych formatach.

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
struct StringInfoA
{
    [MarshalAs(UnmanagedType.LPStr)] public string f1;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 256)] public string f2;
}

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
struct StringInfoW
{
    [MarshalAs(UnmanagedType.LPWStr)] public string f1;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 256)] public string f2;
    [MarshalAs(UnmanagedType.BStr)] public string f3;
}

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct StringInfoT
{
    [MarshalAs(UnmanagedType.LPTStr)] public string f1;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 256)] public string f2;
}
```

```vb
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Ansi)> _
Structure StringInfoA
    <MarshalAs(UnmanagedType.LPStr)> Public f1 As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _
    Public f2 As String
End Structure

<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Unicode)> _
Structure StringInfoW
    <MarshalAs(UnmanagedType.LPWStr)> Public f1 As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _
    Public f2 As String
<MarshalAs(UnmanagedType.BStr)> Public f3 As String
End Structure

<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Auto)> _
Structure StringInfoT
    <MarshalAs(UnmanagedType.LPTStr)> Public f1 As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _
    Public f2 As String
End Structure
```

## <a name="fixed-length-string-buffers"></a>Bufory ciągów o stałej długości

W pewnych okolicznościach bufor znaków o stałej długości musi być przekazywać do kodu niezarządzanego w celu manipulowania. Po prostu przekazanie ciągu nie działa w tym przypadku, ponieważ element wywoływany nie może modyfikować zawartości przekazywanego buforu. Nawet jeśli ciąg jest przekazywane przez odwołanie, nie ma możliwości zainicjowania buforu do danego rozmiaru.

Rozwiązanie to przekazanie <xref:System.Text.StringBuilder> bufora jako argumentu zamiast <xref:System.String>. `StringBuilder` można wycofać i zmodyfikować przez element wywoływany, pod warunkiem, że nie przekracza on pojemności `StringBuilder`. Można go również zainicjować na stałą długość. Na przykład jeśli zainicjujesz bufor `StringBuilder` do pojemności `N`, organizator udostępnia bufor o rozmiarze (`N`+ 1). Konta + 1 dla faktu, że niezarządzany ciąg ma terminator o wartości null, podczas gdy `StringBuilder` nie.

Na przykład funkcja interfejsu API systemu Windows [`GetWindowText`](/windows/desktop/api/winuser/nf-winuser-getwindowtextw) (zdefiniowana w *Winuser. h*) wymaga, aby obiekt wywołujący przeszedł bufor znaków o stałej długości, do którego funkcja zapisuje tekst okna. `LpString` wskazuje buforem przydzielonym przez obiekt wywołujący `nMaxCount`rozmiarem. Obiekt wywołujący oczekuje na przydzielenie buforu i ustawienie argumentu `nMaxCount` na rozmiar przydzielonego buforu. W poniższym przykładzie pokazano deklarację funkcji `GetWindowText`, zgodnie z definicją w *Winuser. h*.

```cpp
int GetWindowText(
    HWND hWnd,        // Handle to window or control.
    LPTStr lpString,  // Text buffer.
    int nMaxCount     // Maximum number of characters to copy.
);
```

`StringBuilder` można wycofać i zmodyfikować przez element wywoływany, pod warunkiem, że nie przekracza on pojemności `StringBuilder`. Poniższy przykład kodu demonstruje, jak `StringBuilder` można zainicjować o stałej długości.

```csharp
using System;
using System.Runtime.InteropServices;
using System.Text;

internal static class NativeMethods
{
    [DllImport("User32.dll")]
    internal static extern void GetWindowText(IntPtr hWnd, StringBuilder lpString, int nMaxCount);
}

public class Window
{
    internal IntPtr h;        // Internal handle to Window.
    public String GetText()
    {
        StringBuilder sb = new StringBuilder(256);
        NativeMethods.GetWindowText(h, sb, sb.Capacity + 1);
        return sb.ToString();
    }
}
```

```vb
Imports System.Text

Friend Class NativeMethods
    Friend Declare Auto Sub GetWindowText Lib "User32.dll" _
        (hWnd As IntPtr, lpString As StringBuilder, nMaxCount As Integer)
End Class

Public Class Window
    Friend h As IntPtr ' Friend handle to Window.
    Public Function GetText() As String
        Dim sb As New StringBuilder(256)
        NativeMethods.GetWindowText(h, sb, sb.Capacity + 1)
        Return sb.ToString()
   End Function
End Class
```

## <a name="see-also"></a>Zobacz także

- [Domyślne zachowanie marshalingu](default-marshaling-behavior.md)
- [Marshaling ciągów](marshaling-strings.md)
- [Typy kopiowalne i niekopiowalne](blittable-and-non-blittable-types.md)
- [Atrybuty kierunkowe](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100))
- [Kopiowanie i przypinanie](copying-and-pinning.md)
