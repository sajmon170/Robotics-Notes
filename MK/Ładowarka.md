# Ładowarka
Przez ładowarkę rozumiem układ umożliwiający ładowanie układu podłączany do sieci elektrycznej, czyli jest to system składający się z zasilacza oraz przetwornicy CC/CV.
Zasilacz pozwala zamianę prądu z przemiennego na stały oraz zmniejszenie napięcia, a przetwornica step-down na dalsze zmniejszenie napięcia oraz zapewnienie ograniczenia prądu ładowania (tak w praktyce działa CC/CV).

## Przetwornice step-up i step-down
Są to takie przetwornice, które odpowiednio podwyższają napięcie względem wejściwego lub je obniżają. Istnieją też przetwornice, które w zależności od warunków pełnią obie te funkcje, by ostatecznie na wyjściu pojawiło się ustalone napięcie.

## Przetwornica CC/CV
Przetwornica taka pozwala, zazwyczaj za pomocą potencjometrów montażowych, na zmianę napięcia wyjściowego oraz na zmianę maksymalnego prądu wyjściowego.
Ograniczenia są zazwyczaj wykonywane poprzez przełączanie za pomocą tranzystorów, dzięki czemu generowane straty w postaci ciepła są bardzo małe (a w szczególności dużo mniejsze od różnicy napięcia wejściowego od wyjściowego).

## Ładowanie CC/CV
1. Początkową fazą ładowania jest faza constant current, czyli taka podczas której prąd ładowania jest stały i zmienia się napięcie (rośnie). Przetwornica CC/CV musi ograniczać ten prąd, ponieważ w innym wypadku bateria pobrałaby zbyt duży, co mogłoby doprowadzić co jej uszkodzenia (prawdopodobnie w gwałtowny sposób np. wybuchu czy zapalenia).
2. Gdy bateria dostatecznie się naładuje jej opór wzrasta do takiego poziomu, że ogranicza to przepływający przez nią prąd - wówczas kończy się faza constant current i rozpoczyna się faza constant voltage. W fazie constant voltage napięcie pozostaje na stałym poziomie, a zmniejsza się jedynie prąd.
3. *W momencie osiągnięcia zbyt małego poziomu prądu ładującego układ BMS powinien odciąć ładowanie tak by nie uszkodzić ogniw litowo-jonowych.

## Źródła:
https://www.reddit.com/r/AskElectronics/wiki/batteries/#wiki_li-ion_bms
https://www.youtube.com/watch?v=AJoudtXLsHc
https://www.youtube.com/watch?v=Z0zRkfVpU6c
