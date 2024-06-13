# Dziel i zwyciężaj

## Schemat ogólny
## Master's Theorem
Master's Theorem jest narzędziem służącym do analizowania złożoności czasowej algorytmów rekurencyjnych, zwłaszcza tych, które można wyrazić za pomocą rekurencji postaci:
$$T(n)=aT(\frac{n}{b})+f(n)$$
gdzie $f(n) = O(n^d)$, Master's Theorem daje nam trzy przypadki:

1. dla d > $log{_b}{a}$ 
   
   $$T(n) = O(n^d)$$

2. dla d = $log{_b}{a}$
   $$T(n) = O(n^d log{_2}{n})$$

3. dla d < $log{_b}{a}$
   $$T(n) = O(n^{\log{_b} {a}})$$

### Wyjaśnienie
- Gdy d > $log{_b}{a}$, **funkcja f(n)** dominuje i określa asymptotyczną złożoność czasową.
- Gdy d = $log{_b}{a}$, zarówno **rekurencyjna część, jak i funkcja f(n)** mają taki sam wpływ na złożoność, co dodaje czynnik logarytmiczny.
- Gdy d < $log{_b}{a}$, **rekurencyjna część** dominuje i określa asymptotyczną złożoność czasową.

Opisuje nam to czy więcej pracy wykonujemy przez rekurencyjne wywołania funkcji, czy też więcej pracy zajmuje rozwiązanie podproblemu (funkcja f(n) wywołana w przypadku bazowym)
### Przykład (Mergesort)
Rekurencja algorytmu mergesort dana jest funkcją 
$$T(n)=2T(\frac{n}{2})+O(n)$$
gdzie
$$a = 2, b = 2, d = 1$$
w tym przypadku $d = log{_b}{a}$, więc złożoność Mergesort'a to 
$$T(n) = O(n^d log{_2}{n}) = O(nlog{_2}{n})$$

### Przykład 1 (Mergesort)
Rekurencja algorytmu mergesort dana jest funkcją 
$$T(n)=2T(\frac{n}{2})+O(n)$$
gdzie
$$a = 2, b = 2, d = 1$$
w tym przypadku $d = log{_b}{a}$, więc złożoność Mergesort'a to 
$$T(n) = O(n^d log{_2}{n}) = O(nlog{_2}{n})$$

## Binsearch
## Równoczesne wyszukiwanie min i max w zbiorze
## Mergesort
## Wyszukiwanie pary najbliżej położonych punktów
## Algorytm Karatsuby