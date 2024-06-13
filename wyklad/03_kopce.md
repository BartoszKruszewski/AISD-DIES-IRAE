# Kopce

### Defincja

Kopce to drzewa binarne, zachowujące dwa warunki:
- klucz w wierzchołku jest **nie mniejszy** od kluczy w jego potomkach
- jest **"prawie pełne"** (liście występują tylko, na ostanim lub przedostatnim poziomie, te na przedostatnim są "wyrównane do lewej")

### Implementacja

Kopce pamiętane są w tablicach. Dla wierzchołka pod indeksem $i$:
- jego ojciec ma indeks $\lfloor i / 2 \rfloor$
- jego dzieci mają indeksy $2i$ oraz $2i + 1$

Przywracanie warunku kopca, odbywa się za pomocą procedur $przesuń-niżej$ oraz $przesuń-wyżej$.


```
def przesuń-niżej(K, i):
    k = i
    do:
        # zamiana j-tego elementu z większym dzieckiem
        j = k
        if 2j <= n and K[2j] > K:
            k = 2j
        if 2j < n and K[2j + 1] > K:
            k = 2j + 1
        swap(K[j], K[k])
    while j != k
    # przerywamy kiedy, już nie trzeba robić zamiany

```

### Szybkie budowanie kopca

Kopiec można budować od góry albo od dołu (od liści). Od dołu jest szybciej i działa to w $O(n)$.

Złożoność procedury $przesuń-niżej(i)$ to wysokość poddrzewa elementu o indeksie $i$. Z każdą warstwą licząc od dołu liczba wierzchołków dla których procedura powinna zostać wywołana maleje dwukrotnie. Zaczynamy od wartwy drugiej od dołu, ponieważ najniższa na początku jest już ustawiona poprawnie. 

Rozpisując sumę operacji:

$1 * \lfloor n/2 \rfloor + 2 *  \lfloor n/4 \rfloor + 3 *  \lfloor n/8 \rfloor + \ldots + log_2(n) * 1 = \sum_{i = 0}^{log(n)} \frac{i * n}{2^i} \le 2n = O(n)$

### Heapsort

Algorytm Heapsort działa w czasie $O(nlog(n))$. Dla każdego z $n$ elementów, wypisujemy go, a następnie usuwamy z góry kopca. Dziurę pozostałą po elemencie przesuwamy na dół kopca, żeby można było wstawić w nią ostatni element z kopca. Następnie przesuwamy element w górę (procedurą $przesuń-wyżej$, analogiczną do $przesuń-niżej$), żeby zachować warunek kopca.

Łączny czas to:

$n * (log(n) + log(n)) = 2nlog(n) = O(nlog(n))$

### Kolejka priorytetowa

Kopiec świetnie nadaje się do realizowania operacji kolejki priorytetowej:

- insert $O(1)$
- find-min $O(log(n))$
- delete-min $O(log(n))$