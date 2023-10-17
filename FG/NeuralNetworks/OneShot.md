# Trenowanie sieci neuronowej One-Shot

## Co to
Sieć One-Shot to taka, która klasyfikuje dane wejściowe do klasy, którą zna z jednego tylko wektora wejściowego. Gdy pokażemy takiej jedno zdjęcie dowolnego, nieznanego dotąd przedmiotu ta powinna być w stanie powiedzieć, czy na kolejnym zdjęciu znajduje się ten sam przedmiot, czy nie.

## Trenowanie
Proces trenowania konwolucyjnej sieci neuronowej One-Shot polega na dwóch krokach:
## Verification
W tym kroku trenujemy wyłącznie część konwolucyjną sieci do tego, by wykrywała poprawnie cechy obiektów. Wykorzystujemy do tego technikę `Triplet Loss`. Polega ona na przygotowaniu trójek danych:
- baseline input
- positive input
- negative input
`positive input` powinno być danymi stosunkowo podobnymi do `baseline input`, a `negative input` powinno różnić się od `baseline input`. Celem tej techniki jest sprawienie, by konwolucja zwracała jak najbliższe wektory wyjściowe dla `baseline` i `positive` a wektory wyjściowe `baseline` i `negative` powinny być od siebie różne. W ten sposób sieć uczy się wykrywać cechy obiektów, a nie ich klasy. 

Implementacja tej techniki polega na utworzeniu `Siamese Neural Network` - sieci neuronowej syjamskiej. Ma ona dwa "wejścia" - dwie kopie naszej części konwolucyjnej. Przez jedną z kopii przepuszczamy `base input` a przez drugą `positive` lub `negative`. Porównujemy odległość wyjść obydwu kopii i w przypadku `positive` traktujemy odległość jak `loss` i minimalizujemy ją w procesie uczenia, a w przypadku `negative` traktujemy odległość jak `gain` i maksymalizujemy ją w procesie uczenia.

Wynikiem takiego treningu powinna być część konwolucyjna sieci, która jest w stanie wykrywać cechy obiektów.

## Generalization
W tym kroku dołączamy zwykłą część perceptronową na koniec części konwolucyjnej, trening części konwolucyjnej blokujemy. Podajemy, podobnie, dwa różne obrazy do każdej z kopii sieci konwolucyjnej i przepuszczamy wyjścia przez część perceptronową, która powinna zwracać jedną wartość - prawdopodobieństwo należenia do jednej klasy. W tym kroku nauczanie przypomina już bardzo nauczanie sieci `Transferowej`. Podawane na wejście obrazy powinny być do siebie bardzo podobne, jako, że część konwolucyjna jest już dosyć dobrze wytrenowana. Porównujemy odpowiedź sieci z faktem należenia dwóch wektorów do tej samej klasy, lub nie. Gdy uznamy, że sieć nie robi już postępów, odblokowujemy trenowanie części konwolucyjnej.

## ps
Jako, że proces tak bardzo przypomina dotrenowywanie sieci transferowej do rozpoznawania obiektów, może faktycznie warto z takiej skorzystać i "pożyczyć" wagi do części konwolucyjnej zamiast trenować je od zera.
