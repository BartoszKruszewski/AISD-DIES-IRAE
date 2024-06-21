# Sieci przełączników

## Przełączniki

Przełącznikiem nazywamy urządzenie, które ma dwa wejścia dwa wyjścia oraz dwa stany:

- 1 stan: przesyła $a_{in} \rarr a_{out}$, $b_{in} \rarr b_{out}$ (przesyłanie na wprost)
- 2 stan: przesyła $a_{in} \rarr b_{out}$, $b_{in} \rarr a_{out}$ (przesyłanie na ukos)

Łącząc przełączniki w sieć, możemy realizować na wyjściu różne permutacje danych wejściowych.

## Zadanie

Zadanie polega na utworzeniu takiej sieci przełączników, żeby poprzez tylko przełączanie stanów przełączników można było uzyskać na wyjściu wszystkie permutacje danych wejściowych.

Kryteriami oceny sieci są:

- liczba przełączników
- głębokość sieci (długość najdłuższej drogiod wejścia do wyjścia)

Im te wartości są mniejsze tym lepiej.

Przez $n$ będziemy oznaczać liczbę wejść sieci.

## Sieć Benesa-Waksmana

![Konstrukcja sieci](/src/06_01.png)

Sieć jest zbudowana w oparciu o zasadzie dziel i zwyciężaj (rekurencyjnie). Budujemy dwie podsieci o $n/2$ wejściach. Wyjścia $a$ wszystkich przełączników podczepiamy do kolejnych wejść pierwszej podsieci, a wejścia $b$ do wejść drugiej podsieci. Wyjścia obu podsieci podłączamy symetrycznie.

## Właściwości

Oznaczmy $n = 2^k$

Liczba przełączników to:

$P(n) = 2 * P(n/2) + n = 2 * (2 * P(n/4) + n/2) + n = 4P(n/4) + n + n = log_2{n} * n$

Głębokość sieci to:

$G(n) = G(2^k) = G(2^{k-1}) + 2 = (log_2{n} - 1) * 2 + 1 = 2 * log_2{n} - 1$

## Dowód poprawności
