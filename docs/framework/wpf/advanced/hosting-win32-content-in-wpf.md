---
title: Hosting zawartości Win32 w WPF
ms.date: 03/30/2017
helpviewer_keywords:
- interoperability [WPF], tutorials
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 3cc8644a-34f3-4082-9ddc-77623e4df2d8
ms.openlocfilehash: 3b6e30a612c87880121c227c85c4bd6a7ef31f40
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/25/2019
ms.locfileid: "72920233"
---
# <a name="hosting-win32-content-in-wpf"></a>Hosting zawartości Win32 w WPF

## <a name="prerequisites"></a>Wymagania wstępne

Zobacz [WPF i Win32 — współdziałanie](wpf-and-win32-interoperation.md).

## <a name="a-walkthrough-of-win32-inside-windows-presentation-framework-hwndhost"></a>Przewodnik po Win32 wewnątrz struktury prezentacji systemu Windows (HwndHost)

Aby ponownie użyć [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] zawartości w aplikacjach [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], użyj <xref:System.Windows.Interop.HwndHost>, która jest formantem, który sprawia, że elementy HWND wyglądają jak [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] zawartość. Podobnie jak <xref:System.Windows.Interop.HwndSource>, <xref:System.Windows.Interop.HwndHost> jest prosta do użycia: pochodzi z <xref:System.Windows.Interop.HwndHost> i Implementuj metody `BuildWindowCore` i `DestroyWindowCore`, a następnie Utwórz wystąpienie <xref:System.Windows.Interop.HwndHost> klasy pochodnej i umieść ją w aplikacji [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].

Jeśli logika [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] jest już spakowana jako kontrolka, to `BuildWindowCore` implementacja jest nieco większa niż wywołanie `CreateWindow`. Na przykład, aby utworzyć formant LISTBOX [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] w C++:

```cpp
virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {
    HWND handle = CreateWindowEx(0, L"LISTBOX",
    L"this is a Win32 listbox",
    WS_CHILD | WS_VISIBLE | LBS_NOTIFY
    | WS_VSCROLL | WS_BORDER,
    0, 0, // x, y
    30, 70, // height, width
    (HWND) hwndParent.Handle.ToPointer(), // parent hwnd
    0, // hmenu
    0, // hinstance
    0); // lparam

    return HandleRef(this, IntPtr(handle));
}

virtual void DestroyWindowCore(HandleRef hwnd) override {
    // HwndHost will dispose the hwnd for us
}
```

Ale Załóżmy, że kod [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] nie jest całkowicie zawarty? Jeśli tak, możesz utworzyć okno dialogowe [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] i osadzić jego zawartość w większej [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacji. Przykład pokazuje to w programie Visual Studio i C++, chociaż jest to również możliwe w innym języku lub w wierszu polecenia.

Zacznij od prostego okna dialogowego, które jest kompilowane do projektu C++ dll.

Następnie wprowadź okno dialogowe do większego [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacji:

- Kompiluj bibliotekę DLL jako zarządzaną (`/clr`)

- Przekształcanie okna dialogowego w kontrolkę

- Definiowanie klasy pochodnej <xref:System.Windows.Interop.HwndHost> przy użyciu metod `BuildWindowCore` i `DestroyWindowCore`

- Zastąp metodę `TranslateAccelerator`, aby obsłużyć klawisze dialogu

- Zastąp metodę `TabInto`, aby obsługiwać tabulację

- Zastąp metodę `OnMnemonic`, aby obsługiwała

- Utwórz wystąpienie podklasy <xref:System.Windows.Interop.HwndHost> i umieść ją w prawym [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elemencie

### <a name="turn-the-dialog-into-a-control"></a>Przekształcanie okna dialogowego w kontrolkę

Okno dialogowe można przekształcić w podrzędny element HWND przy użyciu stylów WS_CHILD i DS_CONTROL. Przejdź do pliku zasobów (. RC), w którym zdefiniowano okno dialogowe, a następnie Znajdź początek definicji okna dialogowego:

```text
IDD_DIALOG1 DIALOGEX 0, 0, 303, 121
STYLE DS_SETFONT | DS_MODALFRAME | DS_FIXEDSYS | WS_POPUP | WS_CAPTION | WS_SYSMENU
```

Zmień drugi wiersz na:

```text
STYLE DS_SETFONT | WS_CHILD | WS_BORDER | DS_CONTROL
```

Ta akcja nie powoduje całkowitego spakowania jej w celu samodzielnego sterowania; nadal musisz wywoływać `IsDialogMessage()`, aby [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] mogli przetwarzać niektóre komunikaty, ale zmiana kontrolki zapewnia prostą metodę umieszczania tych kontrolek wewnątrz innego elementu HWND.

## <a name="subclass-hwndhost"></a>HwndHost podklasy

Zaimportuj następujące przestrzenie nazw:

```cpp
namespace ManagedCpp
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Input;
    using namespace System::Windows::Media;
    using namespace System::Runtime::InteropServices;
```

Następnie Utwórz klasę pochodną <xref:System.Windows.Interop.HwndHost> i Zastąp metody `BuildWindowCore` i `DestroyWindowCore`:

```cpp
public ref class MyHwndHost : public HwndHost, IKeyboardInputSink {
    private:
        HWND dialog;

    protected:
        virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {
            InitializeGlobals();
            dialog = CreateDialog(hInstance,
                MAKEINTRESOURCE(IDD_DIALOG1),
                (HWND) hwndParent.Handle.ToPointer(),
                (DLGPROC) About);
            return HandleRef(this, IntPtr(dialog));
        }

        virtual void DestroyWindowCore(HandleRef hwnd) override {
            // hwnd will be disposed for us
        }
```

W tym miejscu użyjesz `CreateDialog`, aby utworzyć okno dialogowe, które jest naprawdę formantem. Ponieważ jest to jedna z pierwszych metod wywoływanych wewnątrz biblioteki DLL, należy również wykonać kilka standardowych [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] inicjacji, wywołując funkcję, która zostanie zdefiniowana później, o nazwie `InitializeGlobals()`:

```cpp
bool initialized = false;
    void InitializeGlobals() {
        if (initialized) return;
        initialized = true;

        // TODO: Place code here.
        MSG msg;
        HACCEL hAccelTable;

        // Initialize global strings
        LoadString(hInstance, IDS_APP_TITLE, szTitle, MAX_LOADSTRING);
        LoadString(hInstance, IDC_TYPICALWIN32DIALOG, szWindowClass, MAX_LOADSTRING);
        MyRegisterClass(hInstance);
```

### <a name="override-translateaccelerator-method-to-handle-dialog-keys"></a>Zastąp metodę TranslateAccelerator, aby obsłużyć klawisze dialogu

Jeśli ten przykład został uruchomiony teraz, zobaczysz kontrolkę okna dialogowego, która wyświetla, ale zignorujesz wszystkie przetwarzanie klawiatury, które powoduje okno dialogowe funkcjonalne. Teraz należy zastąpić implementację `TranslateAccelerator` (która pochodzi z `IKeyboardInputSink`, interfejsu, który <xref:System.Windows.Interop.HwndHost> implementuje). Ta metoda jest wywoływana, gdy aplikacja odbiera PRZETŁUMACZYŁA i WM_SYSKEYDOWN.

```cpp
#undef TranslateAccelerator
        virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,
            ModifierKeys modifiers) override
        {
            ::MSG m = ConvertMessage(msg);

            // Win32's IsDialogMessage() will handle most of our tabbing, but doesn't know
            // what to do when it reaches the last tab stop
            if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {
                HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
                HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
                TraversalRequest^ request = nullptr;

                if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {
                    // this code should work, but there’s a bug with interop shift-tab in current builds
                    request = gcnew TraversalRequest(FocusNavigationDirection::Last);
                }
                else if (!GetKeyState(VK_SHIFT) && GetFocus() == lastTabStop) {
                    request = gcnew TraversalRequest(FocusNavigationDirection::Next);
                }

                if (request != nullptr)
                    return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);

            }

            // Only call IsDialogMessage for keys it will do something with.
            if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {
                switch (m.wParam) {
                    case VK_TAB:
                    case VK_LEFT:
                    case VK_UP:
                    case VK_RIGHT:
                    case VK_DOWN:
                    case VK_EXECUTE:
                    case VK_RETURN:
                    case VK_ESCAPE:
                    case VK_CANCEL:
                        IsDialogMessage(dialog, &m);
                        // IsDialogMessage should be called ProcessDialogMessage --
                        // it processes messages without ever really telling you
                        // if it handled a specific message or not
                        return true;
                }
            }

            return false; // not a key we handled
        }
```

Jest to wiele kodu w jednej części, dzięki czemu można użyć bardziej szczegółowych wyjaśnień. Najpierw kod wykorzystujący C++ i C++ makra; należy pamiętać, że istnieje już makro o nazwie`TranslateAccelerator`, które jest zdefiniowane w Winuser. h:

```cpp
#define TranslateAccelerator  TranslateAcceleratorW
```

Upewnij się, że zdefiniowano metodę `TranslateAccelerator`, a nie metodę `TranslateAcceleratorW`.

Podobnie istnieje zarówno niezarządzana MSG Winuser. h, jak i zarządzana struktura `Microsoft::Win32::MSG`. Można odróżnić dwa z nich przy użyciu operatora C++`::`.

```cpp
virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,
    ModifierKeys modifiers) override
{
    ::MSG m = ConvertMessage(msg);
}

Both MSGs have the same data, but sometimes it is easier to work with the unmanaged definition, so in this sample you can define the obvious conversion routine:

```cpp
::MSG ConvertMessage(System::Windows::Interop::MSG% msg) {
    ::MSG m;
    m.hwnd = (HWND) msg.hwnd.ToPointer();
    m.lParam = (LPARAM) msg.lParam.ToPointer();
    m.message = msg.message;
    m.wParam = (WPARAM) msg.wParam.ToPointer();

    m.time = msg.time;

    POINT pt;
    pt.x = msg.pt_x;
    pt.y = msg.pt_y;
    m.pt = pt;

    return m;
}
```

Wróć do `TranslateAccelerator`. Podstawowa zasada polega na wywołaniu funkcji [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] `IsDialogMessage` w celu uzyskania możliwie największej ilości pracy, ale `IsDialogMessage` nie ma dostępu do niczego poza oknem dialogowym. Jako karta użytkownika w oknie dialogowym, gdy karta jest uruchamiana poza ostatnią kontrolką w naszym oknie dialogowym, należy ustawić fokus na [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] część, wywołując `IKeyboardInputSite::OnNoMoreStops`.

```cpp
// Win32's IsDialogMessage() will handle most of the tabbing, but doesn't know
// what to do when it reaches the last tab stop
if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {
    HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
    HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
    TraversalRequest^ request = nullptr;

    if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {
        request = gcnew TraversalRequest(FocusNavigationDirection::Last);
    }
    else if (!GetKeyState(VK_SHIFT) && GetFocus() ==  lastTabStop) { {
        request = gcnew TraversalRequest(FocusNavigationDirection::Next);
    }

    if (request != nullptr)
        return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);
}
```

Na koniec Wywołaj `IsDialogMessage`. Ale jeden z obowiązków metody `TranslateAccelerator` jest informujący [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] o tym, czy zostały obsłużone naciśnięcie klawisza. Jeśli go nie obsłuży, zdarzenie wejściowe może tunelować i bąbelkować przez resztę aplikacji. Tutaj zobaczysz Quirk obsługi messange z klawiatury i charakteru architektury wejściowej w [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]. Niestety `IsDialogMessage` nie zwraca w żaden sposób, czy obsługuje określone naciśnięcie klawisza. Nawet gorszy, wywoła `DispatchMessage()` na naciśnięciach klawiszy, które nie powinny obsłużyć!  W związku z tym trzeba będzie odwrócić `IsDialogMessage`i wywołać ją tylko dla kluczy, które są obsługiwane przez Ciebie:

```cpp
// Only call IsDialogMessage for keys it will do something with.
if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {
    switch (m.wParam) {
        case VK_TAB:
        case VK_LEFT:
        case VK_UP:
        case VK_RIGHT:
        case VK_DOWN:
        case VK_EXECUTE:
        case VK_RETURN:
        case VK_ESCAPE:
        case VK_CANCEL:
            IsDialogMessage(dialog, &m);
            // IsDialogMessage should be called ProcessDialogMessage --
            // it processes messages without ever really telling you
            // if it handled a specific message or not
            return true;
    }
```

### <a name="override-tabinto-method-to-support-tabbing"></a>Zastąp metodę TabInto w celu obsługi tabulacji

Teraz, po zaimplementowaniu `TranslateAccelerator`, użytkownik może umieścić kartę w obszarze okna dialogowego i wylogować się z niego do większej [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacji. Jednak użytkownik nie może powracać do okna dialogowego. Aby rozwiązać ten problem, Zastąp `TabInto`:

```cpp
public:
    virtual bool TabInto(TraversalRequest^ request) override {
        if (request->FocusNavigationDirection == FocusNavigationDirection::Last) {
            HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
            SetFocus(lastTabStop);
        }
        else {
            HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
            SetFocus(firstTabStop);
        }
        return true;
    }
```

Parametr `TraversalRequest` informuje o tym, czy akcja karty jest tabulatorem, czy klawiszem Shift.

### <a name="override-onmnemonic-method-to-support-mnemonics"></a>Przesłoń metodę do obsługi symboli

Obsługa klawiatury jest niemal ukończona, ale nie ma jednego z nich — nie działa. Jeśli użytkownik naciśnie klawisze ALT-F, fokus Nowak nie Przeskocz do pola edycji imię i nazwisko:. Dlatego należy zastąpić metodę `OnMnemonic`:

```cpp
virtual bool OnMnemonic(System::Windows::Interop::MSG% msg, ModifierKeys modifiers) override {
    ::MSG m = ConvertMessage(msg);

    // If it's one of our mnemonics, set focus to the appropriate hwnd
    if (msg.message == WM_SYSCHAR && GetKeyState(VK_MENU /*alt*/)) {
        int dialogitem = 9999;
        switch (m.wParam) {
            case 's': dialogitem = IDOK; break;
            case 'c': dialogitem = IDCANCEL; break;
            case 'f': dialogitem = IDC_EDIT1; break;
            case 'l': dialogitem = IDC_EDIT2; break;
            case 'p': dialogitem = IDC_EDIT3; break;
            case 'a': dialogitem = IDC_EDIT4; break;
            case 'i': dialogitem = IDC_EDIT5; break;
            case 't': dialogitem = IDC_EDIT6; break;
            case 'z': dialogitem = IDC_EDIT7; break;
        }
        if (dialogitem != 9999) {
            HWND hwnd = GetDlgItem(dialog, dialogitem);
            SetFocus(hwnd);
            return true;
        }
    }
    return false; // key unhandled
};
```

Dlaczego nie należy wywoływać `IsDialogMessage` tym miejscu?  Ten sam problem należy wykonać co wcześniej — musisz mieć możliwość poinformowania [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] kodzie, czy kod obsłużył naciśnięcie klawisza, a nie `IsDialogMessage`. Występuje również drugi problem, ponieważ `IsDialogMessage` odmawia przetworzenia elementu, jeśli priorytetowy element HWND nie znajduje się w oknie dialogowym.

### <a name="instantiate-the-hwndhost-derived-class"></a>Tworzenie wystąpienia klasy pochodnej HwndHost

Teraz, gdy cała obsługa klucza i karty jest na miejscu, możesz umieścić <xref:System.Windows.Interop.HwndHost> w większej [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplikacji. Jeśli główna aplikacja jest zapisywana w [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], najprostszym sposobem umieszczenia jej w odpowiednim miejscu jest pozostawienie pustego elementu <xref:System.Windows.Controls.Border>, w którym ma zostać umieszczony <xref:System.Windows.Interop.HwndHost>. W tym miejscu utworzysz <xref:System.Windows.Controls.Border> o nazwie `insertHwndHostHere`:

```xaml
<Window x:Class="WPFApplication1.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Windows Presentation Framework Application"
    Loaded="Window1_Loaded"
    >
    <StackPanel>
        <Button Content="WPF button"/>
        <Border Name="insertHwndHostHere" Height="200" Width="500"/>
        <Button Content="WPF button"/>
    </StackPanel>
</Window>
```

Następnie wszystko to, co pozostanie, aby znaleźć dobre miejsce w sekwencji kodu, aby utworzyć wystąpienie <xref:System.Windows.Interop.HwndHost> i połączyć je z <xref:System.Windows.Controls.Border>. W tym przykładzie umieścisz go wewnątrz konstruktora dla klasy pochodnej <xref:System.Windows.Window>:

```csharp
public partial class Window1 : Window {
    public Window1() {
    }

    void Window1_Loaded(object sender, RoutedEventArgs e) {
        HwndHost host = new ManagedCpp.MyHwndHost();
        insertHwndHostHere.Child = host;
    }
}
```

Dzięki temu:

![Zrzut ekranu z uruchomioną aplikacją WPF.](./media/hosting-win32-content-in-wpf/windows-presentation-foundation-application.png)

## <a name="see-also"></a>Zobacz także

- [WPF i Win32 — współdziałanie](wpf-and-win32-interoperation.md)
