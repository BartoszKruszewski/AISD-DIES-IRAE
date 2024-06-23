# FFT

## Problem

Standardowe mnożenie wielomianów, wymaga czasu $O(n^2)$. Chcemy obniżyć ten koszt do $O(nlog{n})$.

## Reprezentacja wielomianu

Wielomian możemy zapisać jako zbiór punktów. Jeżeli punktów przez które przechodzi wielomian będzie więcej niż stopień wielomianu to jednoznacznie definiują one wielomian, ponieważ istnieje tylko jeden wielomian, które będzie przechodził przez tyle punktów jednocześnie.

Przy takiej reprezentacji mnożenie wielomianów $A * B = C$, polega na przemnożeniu dla każdego punktu:

$(x, y_C) = (x, y_A * y_B)$

Co możemy osiągnąć w czasie $n * O(1) = O(n)$.

Natomiast obliczenie wartości takiego wielomianu wymaga interpolacji, która działa w czasie $O(n^2)$

## Idea

Chcemy zamienić reprezentację współczynnikową na punktową, wykonać mnożenie w czasie $O(n)$, a następnie wrócić do reprezentacji do współczynnikowej. Algorytm, który pozwala na taką szybką zamianę reprezentacji to właśnie **FFT** (Fast Fourier Transform).

```
def fast_polynomial_mult(A, B, n):
    A' = fft(A)
    B' = fft(B)

    for i in range(n):
        C'[i] = (A'.x, A'.y * B'.y)

    C = inverted_fft(C')
    return C
```

## Divide and Conquer

Weźmy wielomian w postaci współczynnikowej, gdzie definiujemy go jednoznacznie jako wektor współczynników:

$A(x) = <a_0, a_1, \dots, a_{n - 1}>$

Oznaczmy:

$A_{even}(x) = <a_0, a_2, \dots, >$

$A_{odd}(x) = <a_1, a_3, \dots, >$

Wtedy:

$A(x) = A_{even}(x^2) + x * A_{odd}(x^2)$

Zauważmy, że musimy obliczyć wartość wielomian, dla $x \in X$. Więc dla podwielomianów, dając jako ich argumnet $x^2$ musimy obliczyć $x^2 \in X^2 = \{x^2 | x \in X\}$.

## Dobór zbioru X

Używająć powyższego algorytmu divide and conquer, zmniejszamy przy każdym użyciu $n$ dwukrotnie. Natomiast zbiór dla jakiego musimy wyliczyć punkty ma stała wielkość.

Takie podejście jeżeli zbiory $X$ oraz $X^2$ będą przy każdym kroku rekurencji rozłączne prowadzi do złożonośći $O(n^2)$.

Chcemy doprowadzić do sytuacji, w której zbiór $|X^2| = |X|$. Wtedy złożoność będzie można oszacować jako:

$T(n) = 2 * T(n/2) + O(n) = O(nlog{n})$.

Możemy wykorzystać fakt, że pierwiastki liczby podniesione do kwadratu dają wynikowo tą samą liczbę. Przykład:

$X = \{-1, 1\} \rarr X^2 = \{1\}$

Zauważmy, że chcać wyliczyć zbiór $X^{1/2}$ musimy obliczyć pierwiastki z elementów zbioru $X$. Żeby móc kontunuwać krok rekurencyjny musimy wykorzystać liczby zespolone.

$X^4 = \{1\}$

$X^2 = \{-1, 1\}$

$X^1 = \{-i, i, -1, 1\}$

Więc potrzebujemy umieć szybko policzyć dowolnie dużą ilość pierwiastków zespolonych z $1$.

## Pierwiastki z jedności

Pierwiastki z jedności występują na okręgu jednostkowym na płaszczyźnie liczb zespolonych.

Wzór na n-te pierwiastki z jedności:

$\cos{\theta} + i * \sin{\theta} = e^{i \theta}$

gdzie:

$\theta = 2 \pi * k / n$ dla $k = 0 \dots n - 1$

więc $X = \{e^{i k 2 \pi / n}\ | k = 0 \dots n - 1 \}$

Zauważmy, że:

$(e^{ik 2\pi/n})^2 = e^{i 2k 2\pi/n} = e^{(i 2k 2\pi/n \mod 2\pi)}$

Ponieważ:

$e^{i 2\pi} = 1$

## Kod

```
def fft(A):
    n = len(A)
    if n = 1:
        return A

    nroot = e^(i * 2 * π / n)
    w = 1

    even = fft(A[0::2]) # parzyste elementy A
    odd = fft(A[1::2]) # nieparzyste elementy A

    res = [0] * n

    for k = 0 ... n/2 − 1:
        # obliczamy jednocześnie wartości w punktach -w oraz +w
        # poniewaz wystepuja symetrycznie
        res[k] = even[k] + w * odd[k]
        res[k + (n / 2)] = even[k] − w * odd[k]
        w *= nroot
    return y
```

## Złożoność

Kod zachowuje złożoność:

$T(n) = 2 * T(n/2) + O(n) = O(nlog{n})$.
