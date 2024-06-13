# Selekcja

Problem polega na wyborze k-tego co do wielkości elementu ciągu.

## Szczególne przypadki

- $k = 1$: dolna i górna granica: $n - 1$
- $k = 2$: dolna i górna granica: $n - 2 + \lceil log(n) \rceil$

## Algorytm deterministyczny

```
def selection(k, T):
    p = jakiś element z T
    U = elementy mniejsze od p
    if k <= |U|:
        return selection(k, U)
    else:
        return selection(k - |U|, T / U)
```

Żeby zapewnić optymalny podział na podzbiory, należy użyc funkcji pseudomed od wyznaczania $p$. Funkcja ta dzieli zbiór na rozłączne 5-cio elementowe podzbiory, liczy medianę każdego z nich, a następnie liczy medianę wyliczonych median.

```
def pseudomed(T):
    Podziel T na rozłączne 5-cio elementowe podzbiory Ci
    S = {mediana(Ci) for Ci}
    return selection(|S| / 2, S)
```

Przy takiej implementacji algorytm działa w czasie $O(n)$.

## Algorytm Hoare'a

Działa trochę jak zrandomizowany Quicksort, ponieważ p wybieramy losowo. Oczekiwany czas działania algorytmu to $O(n)$.

## Algorytm Lazy Select

```
def lazy_selection(k, T):
    R = losowa próbka wielkości n^(3/4) zbioru S
    sort(R)
    x = k * n^(-1/4)
    L = R[x - n^(1/2)]
    H = R[x + n^(1/2)]
    P = elementy z S z przedziału <L, H>
    r = liczba elementów mniejszych od L
    if r < k < r + |P| and |P| < 4n^(3/4) + 2:
        sort(P)
        return P[k - r + 1]
    else:
        powtórz algorytm jeszcze raz
```

Z prawdopodobieństwem $1 - O(\frac{1}{\sqrt[4]{n}})$ Lazy Select wykona jedną iterację.
Wtedy czas działania algorytmu to $O(n^{3/4} * log(n))$.