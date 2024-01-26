# BMS - Battery Management System
System zarządzania bateriami (BMS) są systemami elektronicznymi, które zarzjądzają akumulatorem w celu ochrony go przed pracą z parametrami poza wartościami zalecanymi (SOA - Safe Operating Area), monitorowanie jego stanu, obliczanie różnego rodzaju wartości i ich monitorowanie.

## Monitorowanie
- napięć
    - całkowitego
    - indywidualnych ogniw
- temperatury
    - średniej
    - płynu chłodzącego
    - indywidualnych ogniw
- przepływu płynu chłodzącego
- prądu
    - wpływającego
    - wypływającego
- zdrowia ogniw
- zbalansowania

BMS może obliczać też różne dodatkowe wartości służące do oceny stanu ogniw.
Niektóre BMS-y mogą komunikować się przez różnego rodzaju magistrale (np. CAN), jednak te operujące na niskich napięciach są zazwyczaj pozbawiane tej funkcji.

## Ochrona
- przed przeładowaniem lub nadmiernym rozładowaniem
- przed nadmiernym prądem ładowania lub rozładowania
- przed nadmiernym napięciem ładowania
- przed zbyt niskim napięciem rozładowywania
- przed zbyt niską lub zbyt wysoką temperaturą

## Sposoby balansowania
- strata energii -> obciążenie jest podłączane pod bardziej naładowane ogniwa przez co nadwyżka naładowania względem innych ogniw jest wydzielana w postaci ciepła. Tak robi PRAKTYCZNIE KAŻDY BMS. Nazywane to jest też aktywnym typem balansowania lub "bypass balancing".
- poprzeze przerzucanie energii z bardziej naładowanych ogniw na te mniej naładowane
- zmniejszenie prądu ładowania do takiego, który nie uszkodzi już naładowanych ogniw, ale pozwoli nadal ładować pozostałe - nie dotyczy ogniw opartych o lit, przy nich nawet mały prąd ładowania może uszkadzać już naładowane ogniwa

## Typy BMS
- regulatory pasywne -> jeżeli napięcie ogniwa osiąga określony poziom to prąd ładowania "omija" to ogniwo
- regulatory aktywne -> włączanie i wyłączanie obciążenia, by osiągnąć zbalansowanie. Mogą brać pod uwagę nie tylko samo napięcie, ale ogólnie SoC (State of Charge) obliczany w bardziej skomplikowany sposób
- pełny BMS -> raportuje stany ogniw na wyświetlaczu i chroni baterię

Nieco inne rozróżnienie proponuje wiki na stronie reddit.com/AskElectronics/wiki/batteries
- Gdy BMS otwiera "power switch", by zabezpieczyć ogniwo przed pracą poza SOA (safe operating area) to jest to "protector BMS"
- Istnieją też "balancer BMS", które mówią tylko jakiemuś zewnętrznemu układowi, by zmienił charakterystykę ładowania lub jego zaprzestał
Opisywany power switch to układ składający się z 2 MOSFET-ów. Pierwszy z nich jest wyłączany, gdy bateria jest pusta, ale nadal pozwala na ładowanie. Natomiast drugi MOSFET jest wyłączony, gdy bateria jest pełna, ale nadal pozwala na rozładowywanie.

W ramach protector BMS można wymienić również dwa rodzaje, układy z:
- jednym portem -> służy on jednocześnie do ładowania lub rozładowywania
- dwoma portami -> jeden z nich służy wyłącznie do ładowania, a drugi wyłącznie do podłączenia obciążenia

```
                  charger ----+---- load
                              |
              ----------------------------------
             |            Main port             |
             |                                  |
             |              BMS                 | 
             |                                  |
             |           Cells port             |
              ----------------------------------
                   |    |    |    |    |
                   *-||-*-||-*-||-*-||-*
```
*BMS z jednym portem*

```
 charger+ -------------------+------------------------ load+
                             |
              ----------------------------------
             |               B+                 |
             |                                  |
 charger- -- |charge port   BMS   discharge port| ---- load-
             | C-                            B- |
             |           Cells port             |
              ----------------------------------
                   |    |    |    |    |
                   *-||-*-||-*-||-*-||-*
```
*BMS z dwoma portami*

## Topologie BMS
- zcentralizowany -> pojedynczy kontroler połączony z baterią wiązką przewodów
- rozproszony -> płytka BMS przy każdym ogniwie połączona jednym przewodem z kontrolerem
- modułowy -> istnieje kilka skomunikowanych ze sobą kontrolerów - każdy kontroluje po kilka ogniw

## Stosowanie BMS
Użycie BMS jest __konieczne__ przy korzystaniu z baterii litowo-jonowych..

## Źródła:
https://www.reddit.com/r/AskElectronics/wiki/batteries/#wiki_li-ion_bms
Internet
Wikipedia
