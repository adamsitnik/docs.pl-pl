---
title: 'Wskazówki: tworzenie formantu złożonego za pomocą Visual C#'
ms.date: 03/30/2017
dev_langs:
- CSharp
helpviewer_keywords:
- custom controls [C#]
- user controls [Windows Forms], creating with Visual C#
- UserControl class [Windows Forms], walkthroughs
- user controls [C#]
- custom controls [Windows Forms], creating
ms.assetid: f88481a8-c746-4a36-9479-374ce5f2e91f
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c1d9be77550b1255a24120c68f20d25640e0ebdf
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2019
ms.locfileid: "73460631"
---
# <a name="walkthrough-author-a-composite-control-with-c"></a>Przewodnik: Tworzenie kontrolki złożonej za pomocą języka C\#

Kontrolki złożone zapewniają metodę, za pomocą której można tworzyć i ponownie używać niestandardowych interfejsów graficznych. Formant złożony jest zasadniczo składnikiem z reprezentacją wizualną. W związku z tym może składać się z co najmniej jednego Windows Forms kontrolek, składników lub bloków kodu, który może zwiększyć funkcjonalność, sprawdzając dane wejściowe użytkownika, modyfikując właściwości wyświetlania lub wykonując inne zadania wymagane przez autora. Kontrolki złożone mogą być umieszczane na Windows Forms w taki sam sposób jak w przypadku innych kontrolek. W pierwszej części tego przewodnika utworzysz prostą kontrolkę złożoną o nazwie `ctlClock`. W drugiej części przewodnika rozszerzono funkcjonalność `ctlClock` przez dziedziczenie.

## <a name="create-the-project"></a>Tworzenie projektu

Podczas tworzenia nowego projektu należy określić jego nazwę, aby ustawić główną przestrzeń nazw, nazwę zestawu i nazwę projektu, i upewnić się, że składnik domyślny będzie w poprawnej przestrzeni nazw.

### <a name="to-create-the-ctlclocklib-control-library-and-the-ctlclock-control"></a>Aby utworzyć bibliotekę kontrolek ctlClockLib i formant ctlClock

1. W programie Visual Studio Utwórz nowy projekt **biblioteki formantów Windows Forms** i nadaj mu nazwę **ctlClockLib**.

     Nazwa projektu, `ctlClockLib`, również jest domyślnie przypisana do głównej przestrzeni nazw. Główna przestrzeń nazw służy do kwalifikowania nazw składników w zestawie. Na przykład jeśli dwa zestawy zapewniają składniki o nazwie `ctlClock`, można określić składnik `ctlClock` przy użyciu `ctlClockLib.ctlClock.`

2. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **UserControl1.cs**, a następnie kliknij polecenie **Zmień nazwę**. Zmień nazwę pliku na `ctlClock.cs`. Kliknij przycisk **tak** po wyświetleniu monitu, jeśli chcesz zmienić nazwy wszystkich odwołań do elementu kodu "UserControl1".

    > [!NOTE]
    > Domyślnie formant złożony dziedziczy z klasy <xref:System.Windows.Forms.UserControl> dostarczonej przez system. Klasa <xref:System.Windows.Forms.UserControl> zapewnia funkcje wymagane przez wszystkie kontrolki złożone i implementuje standardowe metody i właściwości.

3. W menu **plik** kliknij polecenie **Zapisz wszystko** , aby zapisać projekt.

## <a name="add-windows-controls-and-components-to-the-composite-control"></a>Dodawanie formantów i składników systemu Windows do kontrolki złożonej

Interfejs wizualny jest istotną częścią formantu złożonego. Ten interfejs wizualny jest implementowany przez dodanie jednego lub większej liczby kontrolek systemu Windows do powierzchni projektanta. Poniższa prezentacja zawiera kontrolki systemu Windows w kontrolce złożonej i pisanie kodu w celu zaimplementowania funkcji.

### <a name="to-add-a-label-and-a-timer-to-your-composite-control"></a>Aby dodać etykietę i czasomierz do kontrolki złożonej

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlClock.cs**, a następnie kliknij pozycję **Projektant widoków**.

2. W **przyborniku**rozwiń węzeł **formanty wspólne** , a następnie kliknij dwukrotnie pozycję **etykieta**.

     Kontrolka <xref:System.Windows.Forms.Label> o nazwie `label1` jest dodawana do kontrolki na powierzchni projektanta.

3. W projektancie kliknij pozycję **Label1**. W okno Właściwości ustaw następujące właściwości.

    |Właściwość|Zmień na|
    |--------------|---------------|
    |**Nazwa**|`lblDisplay`|
    |**Tekst**|`(blank space)`|
    |**TextAlign**|`MiddleCenter`|
    |**Font. size**|`14`|

4. W **przyborniku**rozwiń węzeł **składniki** , a następnie kliknij dwukrotnie przycisk **czasomierz**.

     Ponieważ <xref:System.Windows.Forms.Timer> jest składnikiem, nie ma żadnej wizualizacji w czasie wykonywania. W związku z tym nie jest wyświetlany z kontrolkami na powierzchni projektanta, ale raczej w **projektancie składników** (zasobnik u dołu powierzchni projektanta).

5. W **projektancie składników**kliknij pozycję **Timer1**, a następnie ustaw właściwość <xref:System.Windows.Forms.Timer.Interval%2A> na `1000` i Właściwość <xref:System.Windows.Forms.Timer.Enabled%2A> na `true`.

     Właściwość <xref:System.Windows.Forms.Timer.Interval%2A> kontroluje częstotliwość, z którą <xref:System.Windows.Forms.Timer> składnik. Za każdym razem, gdy `timer1` takty, uruchamia kod w zdarzeniu `timer1_Tick`. Interwał reprezentuje liczbę milisekund między taktami.

6. W **projektancie składników**kliknij dwukrotnie pozycję **Timer1** , aby przejść do zdarzenia `timer1_Tick` `ctlClock`.

7. Zmodyfikuj kod w taki sposób, aby wyglądał jak Poniższy przykład kodu. Zmień modyfikator dostępu z `private` na `protected`.

    ```csharp
    protected void timer1_Tick(object sender, System.EventArgs e)
    {
        // Causes the label to display the current time.
        lblDisplay.Text = DateTime.Now.ToLongTimeString();
    }
    ```

     Ten kod spowoduje, że bieżący czas będzie pokazywany w `lblDisplay`. Ponieważ interwał `timer1` został ustawiony na `1000`, to zdarzenie będzie wykonywane co tysiąc milisekund, co oznacza zaktualizowanie bieżącego czasu co sekundę.

8. Zmodyfikuj metodę, aby można było ją zastąpić za pomocą słowa kluczowego `virtual`. Aby uzyskać więcej informacji, zobacz sekcję "dziedziczenie z kontrolki użytkownika" poniżej.

    ```csharp
    protected virtual void timer1_Tick(object sender, System.EventArgs e)
    ```

9. W menu **plik** kliknij polecenie **Zapisz wszystko** , aby zapisać projekt.

## <a name="add-properties-to-the-composite-control"></a>Dodawanie właściwości do kontrolki złożonej

Kontrolka zegara hermetyzuje obecnie formant <xref:System.Windows.Forms.Label> i składnik <xref:System.Windows.Forms.Timer>, z których każdy ma własny zestaw właściwości. Chociaż poszczególne właściwości tych kontrolek nie będą dostępne dla kolejnych użytkowników kontrolki, można utworzyć i uwidocznić właściwości niestandardowe przez napisanie odpowiednich bloków kodu. Poniższa procedura obejmuje dodanie do kontrolki właściwości, które umożliwiają użytkownikowi zmianę koloru tła i tekstu.

### <a name="to-add-a-property-to-your-composite-control"></a>Aby dodać właściwość do kontrolki złożonej

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlClock.cs**, a następnie kliknij pozycję **Wyświetl kod**.

     Zostanie otwarty **Edytor kodu** dla kontrolki.

2. Znajdź instrukcję `public partial class ctlClock`. Poniżej otwierającego nawiasu klamrowego (`{)`wpisz poniższy kod.

    ```csharp
    private Color colFColor;
    private Color colBColor;
    ```

     Te instrukcje tworzą zmienne prywatne, które będą używane do przechowywania wartości właściwości, które mają zostać utworzone.

3. Wprowadź lub wklej następujący kod poniżej deklaracji zmiennych z kroku 2.

    ```csharp
    // Declares the name and type of the property.
    public Color ClockBackColor
    {
        // Retrieves the value of the private variable colBColor.
        get
        {
            return colBColor;
        }
        // Stores the selected value in the private variable colBColor, and
        // updates the background color of the label control lblDisplay.
        set
        {
            colBColor = value;
            lblDisplay.BackColor = colBColor;
        }
    }
    // Provides a similar set of instructions for the foreground color.
    public Color ClockForeColor
    {
        get
        {
            return colFColor;
        }
        set
        {
            colFColor = value;
            lblDisplay.ForeColor = colFColor;
        }
    }
    ```

     Poprzedni kod tworzy dwie niestandardowe właściwości, `ClockForeColor` i `ClockBackColor`, dostępne dla kolejnych użytkowników tej kontrolki. Instrukcje `get` i `set` zapewniają przechowywanie i pobieranie wartości właściwości, a także kodu do implementacji funkcji odpowiednich dla właściwości.

4. W menu **plik** kliknij polecenie **Zapisz wszystko** , aby zapisać projekt.

## <a name="test-the-control"></a>Testowanie kontrolki

Formanty nie są aplikacjami autonomicznymi; muszą być hostowane w kontenerze. Przetestuj zachowanie w czasie wykonywania formantu i wykonuj jego właściwości za pomocą **kontenera testów UserControl**. Aby uzyskać więcej informacji, zobacz [jak: testowanie zachowania elementu UserControl w czasie wykonywania](how-to-test-the-run-time-behavior-of-a-usercontrol.md).

### <a name="to-test-your-control"></a>Aby przetestować kontrolkę

1. Naciśnij klawisz **F5** , aby skompilować projekt i uruchomić formant w **kontenerze Test UserControl**.

2. W siatce właściwości kontenera testów Znajdź Właściwość `ClockBackColor`, a następnie wybierz właściwość, aby wyświetlić paletę kolorów.

3. Wybierz kolor, klikając go.

   Kolor tła kontrolki zmieni się na wybrany kolor.

4. Użyj podobnej sekwencji zdarzeń, aby sprawdzić, czy właściwość `ClockForeColor` działa zgodnie z oczekiwaniami.

   W tej sekcji i w powyższych sekcjach pokazano, jak można łączyć składniki i formanty systemu Windows z kodem i opakowaniem, aby zapewnić niestandardowe funkcje w formie złożonego formantu. Wiesz już, jak uwidocznić właściwości w kontrolce złożonej oraz jak przetestować swój formant po jego zakończeniu. W następnej sekcji dowiesz się, jak utworzyć Dziedziczony formant złożony przy użyciu `ctlClock` jako podstawy.

## <a name="inherit-from-a-composite-control"></a>Dziedzicz z kontrolki złożonej

W poprzednich sekcjach przedstawiono sposób łączenia formantów, składników i kodu systemu Windows z kontrolkami złożonymi do wielokrotnego użytku. Formant złożony może być teraz używany jako podstawa, na której można skompilować inne kontrolki. Proces wyprowadzania klasy z klasy bazowej nosi nazwę *dziedziczenia*. W tej sekcji utworzysz formant złożony o nazwie `ctlAlarmClock`. Ta kontrolka będzie wyprowadzana z jej formantu nadrzędnego, `ctlClock`. Dowiesz się, jak zwiększyć funkcjonalność `ctlClock`, zastępując metody nadrzędne i dodając nowe metody i właściwości.

Pierwszym krokiem tworzenia dziedziczonej kontrolki jest uzyskanie jej z elementu nadrzędnego. Ta akcja tworzy nową kontrolkę, która ma wszystkie właściwości, metody i charakterystyki graficzne kontrolki nadrzędnej, ale może również stanowić podstawę do dodania nowych lub zmodyfikowanych funkcji.

### <a name="to-create-the-inherited-control"></a>Aby utworzyć Dziedziczony formant

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlClockLib**, wskaż polecenie **Dodaj**, a następnie kliknij pozycję **Kontrola użytkownika**.

     Zostanie otwarte okno dialogowe **Dodaj nowy element** .

2. Wybierz szablon **dziedziczonej kontrolki użytkownika** .

3. W polu **Nazwa** wpisz `ctlAlarmClock.cs`, a następnie kliknij przycisk **Dodaj**.

     Zostanie wyświetlone okno dialogowe **Selektor dziedziczenia** .

4. W obszarze **Nazwa składnika**kliknij dwukrotnie pozycję **ctlClock**.

5. W **Eksplorator rozwiązań**Przeglądaj bieżące projekty.

    > [!NOTE]
    > Plik o nazwie **ctlAlarmClock.cs** został dodany do bieżącego projektu.

### <a name="add-the-alarm-properties"></a>Dodaj właściwości alarmu

Właściwości są dodawane do dziedziczonej kontrolki w taki sam sposób, w jaki są dodawane do kontrolki złożonej. Teraz użyjesz składni deklaracji właściwości, aby dodać dwie właściwości do kontrolki: `AlarmTime`, w której będzie przechowywana wartość daty i czasu alarmu, a `AlarmSet`, która wskazuje, czy alarm jest ustawiony.

#### <a name="to-add-properties-to-your-composite-control"></a>Aby dodać właściwości do kontrolki złożonej

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlAlarmClock**, a następnie kliknij pozycję **Wyświetl kod**.

2. Znajdź instrukcję `public class`. Należy zauważyć, że formant dziedziczy po `ctlClockLib.ctlClock`. Poniżej otwierającego nawiasu klamrowego (`{)` instrukcji wpisz poniższy kod.

    ```csharp
    private DateTime dteAlarmTime;
    private bool blnAlarmSet;
    // These properties will be declared as public to allow future
    // developers to access them.
    public DateTime AlarmTime
    {
        get
        {
            return dteAlarmTime;
        }
        set
        {
            dteAlarmTime = value;
        }
    }
    public bool AlarmSet
    {
        get
        {
            return blnAlarmSet;
        }
        set
        {
            blnAlarmSet = value;
        }
    }
    ```

### <a name="add-to-the-graphical-interface-of-the-control"></a>Dodaj do interfejsu graficznego formantu

Formant dziedziczony ma interfejs wizualny, który jest identyczny z kontrolką, z której dziedziczy. Posiada te same kontrolki elementów, jak jej kontrolki nadrzędne, ale właściwości kontrolek elementów nie będą dostępne, chyba że zostały one jawnie ujawnione. Można dodać do interfejsu graficznego dziedziczonego formantu złożonego w taki sam sposób, jak w przypadku dowolnej kontrolki złożonej. Aby kontynuować dodawanie do interfejsu wizualizacji zegara alarmu, należy dodać kontrolkę etykieta, która będzie Flash, gdy alarm jest dźwiękowy.

#### <a name="to-add-the-label-control"></a>Aby dodać kontrolkę etykieta

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlAlarmClock**, a następnie kliknij pozycję **Projektant widoków**.

     Projektant dla `ctlAlarmClock` otwiera się w oknie głównym.

2. Kliknij część ekranu kontrolki i Wyświetl okno Właściwości.

    > [!NOTE]
    > Wszystkie właściwości są wyświetlane, są wygaszone. Oznacza to, że te właściwości są natywne dla `lblDisplay` i nie można ich modyfikować ani uzyskiwać do nich dostępu w okno Właściwości. Domyślnie formanty zawarte w kontrolce złożonej są `private`, a ich właściwości nie są dostępne w żaden sposób.

    > [!NOTE]
    > Jeśli chcesz, aby użytkownicy formantu złożonego mieli dostęp do swoich wewnętrznych kontrolek, zadeklaruj je jako `public` lub `protected`. Umożliwi to Ustawianie i modyfikowanie właściwości kontrolek zawartych w kontrolce złożonej przy użyciu odpowiedniego kodu.

3. Dodaj kontrolkę <xref:System.Windows.Forms.Label> do formantu złożonego.

4. Za pomocą myszy przeciągnij kontrolkę <xref:System.Windows.Forms.Label> bezpośrednio poniżej pola wyświetlania. W okno Właściwości ustaw następujące właściwości.

    |Właściwość|Ustawienie|
    |--------------|-------------|
    |**Nazwa**|`lblAlarm`|
    |**Tekst**|**Uruchomienia!**|
    |**TextAlign**|`MiddleCenter`|
    |**Widać**|`false`|

### <a name="add-the-alarm-functionality"></a>Dodawanie funkcji alarmu

W poprzednich procedurach dodano właściwości i kontrolkę, która spowoduje włączenie funkcji alarmu w formancie złożonym. W ramach tej procedury dodasz kod w celu porównania bieżącego czasu z czasem alarmu i, jeśli są one takie same, do nabłysku alarmu. Zastępując `timer1_Tick` metodę `ctlClock` i dodając do niej dodatkowy kod, będzie można zwiększyć możliwości `ctlAlarmClock` przy zachowaniu wszystkich nieodłącznych funkcji `ctlClock`.

#### <a name="to-override-the-timer1_tick-method-of-ctlclock"></a>Aby zastąpić metodę timer1_Tick ctlClock

1. W **edytorze kodu**znajdź instrukcję `private bool blnAlarmSet;`. Bezpośrednio poniżej, Dodaj następującą instrukcję.

    ```csharp
    private bool blnColorTicker;
    ```

2. W **edytorze kodu**Znajdź zamykający nawias klamrowy (`})` na końcu klasy. Tuż przed nawiasem klamrowym Dodaj następujący kod.

    ```csharp
    protected override void timer1_Tick(object sender, System.EventArgs e)
    {
        // Calls the Timer1_Tick method of ctlClock.
        base.timer1_Tick(sender, e);
        // Checks to see if the alarm is set.
        if (AlarmSet == false)
            return;
        else
            // If the date, hour, and minute of the alarm time are the same as
            // the current time, flash an alarm.
        {
            if (AlarmTime.Date == DateTime.Now.Date && AlarmTime.Hour ==
                DateTime.Now.Hour && AlarmTime.Minute == DateTime.Now.Minute)
            {
                // Sets lblAlarmVisible to true, and changes the background color based on
                // the value of blnColorTicker. The background color of the label
                // will flash once per tick of the clock.
                lblAlarm.Visible = true;
                if (blnColorTicker == false)
                {
                    lblAlarm.BackColor = Color.Red;
                    blnColorTicker = true;
                }
                else
                {
                    lblAlarm.BackColor = Color.Blue;
                    blnColorTicker = false;
                }
            }
            else
            {
                // Once the alarm has sounded for a minute, the label is made
                // invisible again.
                lblAlarm.Visible = false;
            }
        }
    }
    ```

     Dodanie tego kodu wykonuje kilka zadań. Instrukcja `override` kieruje formant do użycia tej metody zamiast metody, która była dziedziczona z kontrolki podstawowej. Gdy ta metoda jest wywoływana, wywołuje metodę, która zastąpi przez wywołanie instrukcji `base.timer1_Tick`, co zapewnia, że wszystkie funkcje wbudowane w pierwotnej kontrolce są odtwarzane w tym formancie. Następnie uruchamia dodatkowy kod w celu uwzględnienia funkcji alarmu. Migająca kontrolka etykieta zostanie wyświetlona, gdy wystąpi alarm.

     Kontrola zegara alarmu jest niemal ukończona. Jedyną czynnością, która pozostanie, jest zaimplementowanie sposobu jej wyłączenia. W tym celu należy dodać kod do metody `lblAlarm_Click`.

#### <a name="to-implement-the-shutoff-method"></a>Aby zaimplementować metodę ShutOff

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlAlarmClock.cs**, a następnie kliknij pozycję **Projektant widoków**.

     Zostanie otwarty projektant.

2. Dodaj przycisk do kontrolki. Ustaw właściwości przycisku w następujący sposób.

    |Właściwość|Wartość|
    |--------------|-----------|
    |**Nazwa**|`btnAlarmOff`|
    |**Tekst**|**Wyłącz alarm**|

3. W projektancie kliknij dwukrotnie pozycję **btnAlarmOff**.

     **Edytor kodu** zostanie otwarty w wierszu `private void btnAlarmOff_Click`.

4. Zmodyfikuj tę metodę, tak aby była podobna do poniższego kodu.

    ```csharp
    private void btnAlarmOff_Click(object sender, System.EventArgs e)
    {
        // Turns off the alarm.
        AlarmSet = false;
        // Hides the flashing label.
        lblAlarm.Visible = false;
    }
    ```

5. W menu **plik** kliknij polecenie **Zapisz wszystko** , aby zapisać projekt.

### <a name="use-the-inherited-control-on-a-form"></a>Używanie dziedziczonej kontrolki w formularzu

Można testować Dziedziczony formant w taki sam sposób, w jaki przetestowano kontrolkę klasy bazowej, `ctlClock`: naciśnij klawisz **F5** , aby skompilować projekt i uruchomić formant w **kontenerze testów UserControl**. Aby uzyskać więcej informacji, zobacz [jak: testowanie zachowania elementu UserControl w czasie wykonywania](how-to-test-the-run-time-behavior-of-a-usercontrol.md).

Aby można było użyć formantu, musisz go hostować w formularzu. Podobnie jak w przypadku standardowej kontroli złożonej, Dziedziczony formant złożony nie może być autonomiczny i musi być hostowany w formie lub w innym kontenerze. Ponieważ `ctlAlarmClock` ma większą głębię funkcjonalności, wymagany jest dodatkowy kod do przetestowania. Ta procedura polega na napisaniu prostego programu w celu przetestowania funkcjonalności `ctlAlarmClock`. Napisz kod, aby ustawić i wyświetlić Właściwość `AlarmTime` `ctlAlarmClock`i przetestować jej funkcje.

#### <a name="to-build-and-add-your-control-to-a-test-form"></a>Aby skompilować i dodać formant do formularza testowego

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **ctlClockLib**, a następnie kliknij pozycję **Kompiluj**.

2. Dodaj nowy projekt **aplikacji systemu Windows** do rozwiązania i nadaj mu nazwę **test**.

3. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy węzeł **odwołania** dla projektu testowego. Kliknij przycisk **Dodaj odwołanie** , aby wyświetlić okno dialogowe **Dodawanie odwołania** . Kliknij kartę z etykietą **projekty**. Projekt `ctlClockLib` zostanie wyświetlony na liście **Nazwa projektu**. Kliknij dwukrotnie projekt, aby dodać odwołanie do projektu testowego.

4. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **test**, a następnie kliknij polecenie **Kompiluj**.

5. W **przyborniku**rozwiń węzeł **składniki ctlClockLib** .

6. Kliknij dwukrotnie pozycję **ctlAlarmClock** , aby dodać kopię `ctlAlarmClock` do formularza.

7. W **przyborniku**Znajdź i kliknij dwukrotnie pozycję **DateTimePicker** , aby dodać do formularza formant <xref:System.Windows.Forms.DateTimePicker>, a następnie Dodaj kontrolkę <xref:System.Windows.Forms.Label>, klikając dwukrotnie pozycję **etykieta**.

8. Użyj myszy, aby ustawić kontrolki w wygodnym miejscu w formularzu.

9. Ustaw właściwości tych kontrolek w następujący sposób.

    |formant|Właściwość|Wartość|
    |-------------|--------------|-----------|
    |`label1`|**Tekst**|`(blank space)`|
    ||**Nazwa**|`lblTest`|
    |`dateTimePicker1`|**Nazwa**|`dtpTest`|
    ||**Formatowanie**|<xref:System.Windows.Forms.DateTimePickerFormat.Time>|

10. W projektancie kliknij dwukrotnie pozycję **dtpTest**.

     **Edytor kodu** zostanie otwarty w celu `private void dtpTest_ValueChanged`.

11. Zmodyfikuj kod w taki sposób, aby wyglądał następująco.

    ```csharp
    private void dtpTest_ValueChanged(object sender, System.EventArgs e)
    {
        ctlAlarmClock1.AlarmTime = dtpTest.Value;
        ctlAlarmClock1.AlarmSet = true;
        lblTest.Text = "Alarm Time is " +
            ctlAlarmClock1.AlarmTime.ToShortTimeString();
    }
    ```

12. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **test**, a następnie kliknij pozycję **Ustaw jako projekt startowy**.

13. W menu **debugowanie** kliknij **Rozpocznij debugowanie**.

     Zostanie uruchomiony program testowy. Należy pamiętać, że bieżący czas jest aktualizowany w kontrolce `ctlAlarmClock` i że czas rozpoczęcia jest pokazywany w kontrolce <xref:System.Windows.Forms.DateTimePicker>.

14. Kliknij <xref:System.Windows.Forms.DateTimePicker>, w którym są wyświetlane minuty godziny.

15. Korzystając z klawiatury, ustaw wartość minut na minutę, która jest większa niż bieżąca godzina pokazana przez `ctlAlarmClock`.

     Czas ustawienia alarmu jest pokazywany w `lblTest`. Poczekaj, aż wyświetlany czas osiągnie czas ustawienia alarmu. Gdy wyświetlany czas osiągnie czas, w którym ustawiono alarm, `lblAlarm` zostanie błysk.

16. Wyłącz alarm, klikając `btnAlarmOff`. Teraz możesz zresetować alarm.

W tym artykule omówiono szereg kluczowych pojęć. Wiesz już, jak utworzyć formant złożony przez połączenie formantów i składników do kontenera kontroli złożonej. Wiesz już, jak dodać właściwości do kontrolki i napisać kod w celu zaimplementowania funkcji niestandardowych. W ostatniej sekcji pokazano, jak zwiększyć funkcjonalność danego formantu złożonego przez dziedziczenie i zmienić funkcjonalność metod hosta, zastępując te metody.

## <a name="see-also"></a>Zobacz także

- [Różne typy kontrolek niestandardowych](varieties-of-custom-controls.md)
- [Instrukcje: wyświetlanie kontrolki w oknie dialogowym Wybierz elementy przybornika](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)
- [Przewodnik: dziedziczenie z kontrolki formularzy Windows Forms za pomocą języka Visual C#](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
