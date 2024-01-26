# Układ ładujący
Ładowanie baterii Li-ion wymaga nie tylko zastosowania układu [BMS](BMS.md), ale także [ładowarki](Ładowarka.md). Układy te uzupełniają się, ponieważ BMS nie ogranicza w żaden sposób prądu ładowania (robi to ładowarka), a ładowarka nie kontroluje stanu naładowania, zdrowia SOA i innych metryk bezpieczeństwa ogniw (robi to BMS).

## Praktyczna realizacja
- 4 x Ogniwo 18650 o pojemności 3300 mAh i napięciu znamionowym 3,7 V. Łączna pojemność baterii wynosi ok. 50 Wh.
    - Wybór tych konkretnych ogniw polegał na ocenie wymaganej wydajności prądowej obciążenia (czyli między innymi OrangePi + silniczków -> potrzebne co najmniej 6 A przy napięciu ok. 5 V) i taki dobór baterii, by to zapotrzebowanie mogło zostać zaspokojone (warto również wspomnieć, że w ramach układu wykorzystywana jest przetwornica step-down, przez co maksymalny możliwy prąd na wyjściu ulega zwiększeniu - przy zastosowaniu takiej przetwornicy zmniejszanie napięcia oznacza jednocześnie zwiększenie maksymalnej wydajności prądowej)
- Przetwornica CC/CV (tu wpisać dokładnie jaka)
    - Wybór na podstawie parametrów przetwornicy - odpowiedniego zakresu przyjmowanego napięcia wejściowego, a także maksymalnego prądu/napięcia na wyjściu. Przetwornica ta była także polecana przez wielu użytkowników forum elektronicznego elektroda.
    - Prąd ładowania ustawiony na 1,6 A
    - Napięcie ładowania ustawione na 4*4,2 + mała nadwyżka = ok. 17,1 V (o konieczności ustawienia takiego samego lub wyższego niż wymagane napięcia pisano na stronie abcrc - sklepu z elektroniką, gdzie zakupiliśmy przetwornicę)
- BMS - jest to typ "protector BMS", który sam ogranicza w razie potrzeby sposób ładowania lub je odcina. BMS ten nie posiada wyświetlacza, ani żadnego rodzaju magistrali. W ramach posiadanych zabezpieczeń znajduje się m.in. ochrona przed zbyt niskim napięciem rozładowywania lub przed zbyt wysokim napięciem ładowania oraz ochrona przed zbyt niskim prądem ładowania. Dodatkową funkcją jest balansowanie ogniw (w sposób aktywny, tak jak opisywane w [BMS](BMS.md)). Wybrany BMS obsługuje 4 ogniwa połączone szeregowo (o łącznym napięciu znamionowym 14,8 V).
- Zasilacz sieciowy (24 V?)

## Źródła:
https://abc-rc.pl/pl/blog/bms-li-ion-co-to-jest-i-co-trzeba-wiedziec-o-modulach-i-ogniwach-litowych-1540976010.html
można wstawić też inne źródła, linki do produktów
