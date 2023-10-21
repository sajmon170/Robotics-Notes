# Przetwornica DC/DC

Obniżanie napięcia przez przetwornice polega na przełączaniu napięcia, czyli naprzemiennym wyłączaniu i włączaniu go. Jest to efektywny sposób na zmniejszenie strat. Musi to następować odpowiednio szybko, aby nie zakłócało to pracy naszego układu.

## Elementy przetwornicy i ich zadania

Kondensatory — filtracja

Cewki (przynajmniej jedna) — magazynowanie energii podczas zasilania, oddawanie jej po odłączeniu.

Tranzystor MOSFET — przełącznik

Dioda krzemowa — kontrola prądów płynących w
obwodzie we właściwym kierunku

Układ scalony/sterownik
## Podział przetwornic.

Możemy wyróżnić układy step-down(buck) obniżające napięcie, step-up(boost) zwiększające napięcie oraz układy które, w zależności od wejścia dostosowują tryb pracy(buck-boost).
Istnieją także rzadziej stosowane przetwornice zmieniające polaryzację (odwrócenie biegunów), wykorzystywane w układach o zasilaniu symetrycznym.

## Zmiana wartości napięcia a moc
**Przykład idealny:**

Raspberry 5.1 V \* 3.0 A = 15.3 W

4 \* 18650 szeregowo (4 \* 3.7 V) \* xA = 15.3 W, x = 1.034A

**Przykład z uwzględnieniem sprawności:**

Dla sprawności 90%

15.3 W / 0.9 = 17 W

4 \* 18650 szeregowo (4 \* 3.7 V) \* xA = 17 W, x = 1.149 A

Sprawność przetwornicy zależy od aktualnych warunków pracy.

## Uwagi ogólne

Ze względu na to, że przetwornica jest układem impulsowym, generuje zakłócenia. W przypadku układów wrażliwych na zmiany napięcia trzeba stosować stabilizatory liniowe, które redukują wpływ impulsów zasilających. Silniki, jak i Raspberry Pi nie wymagają takich układów.

W przypadku użycia baterii warto tutaj zaznaczyć, że spadki napięcia podczas rozładowywania baterii i duże obciążenie może przysparzać problemów, dlatego należy zawsze mieć zapas. Dobrym wyborem może być przetwornica buck-boost.
