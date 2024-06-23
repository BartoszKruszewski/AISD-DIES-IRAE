# Programowanie dynamiczne

## Filozfia programowania dynamicznego

## Najtańsze przejście po tablicy

## Opis problemu

Problem Najtańszego Przejścia po Tablicy polega na znalezieniu ścieżki z pierwszej tablicy do ostatniej, której suma wartości jest minimalna. Możemy przemieszczać się jak na poniższym obrazku w każdym kroku. Podejście dynamiczne jest idealne do tego problemu, ponieważ możemy stopniowo obliczać minimalny koszt dotarcia do każdego pola, bazując na wcześniej obliczonych wartościach.

![Możliwe ruchy](/src/Szukanie%20min%20ścieżki.png)

## Podejście dynamiczne

Definiujemy tablicę dp o wymiarach $$m*n$$, gdzie m i n to wymiary bazowej tablicy kosztów taką, że dp[i][j] określa koszt minimalnej ścieżki prowadzącej do komórki (i, j).

```
minPathSum(grid):
    m = number of rows in grid
    n = number of columns in grid

    dp = array of size m x n

    dp[0][0] = grid[0][0]

    for i from 1 to m-1:
        dp[i][0] = dp[i-1][0] + grid[i][0]

    for i from 1 to m-1:
        for j from 1 to n-1:
            dp[i][j] = min(dp[i-1][j-1], dp[i][j-1], dp[i+1][j-1]) + grid[i][j]

    return dp
```

### Wyjaśnienie

1. Inicjalizacja

   - Tworzymy tablicę dp o tych samych wymiarach co grid, aby przechowywać **minimalne koszty dotarcia do każdego pola**.
   - Koszt dotarcia do każdej komórki w pierwszej kolumnie to koszt tej komórki.

1. Dla każdego pola (i, j), koszt dotarcia do niego to minimalny koszt dotarcia do jednego z następujących pól dp[i-1][j-1], dp[i][j-1] oraz dp[i+1][j-1] plus koszt wejścia na pole (i, j) czyli grid[i][j].

### Analiza Złożoności

- **Czasowa**: O(m×n), ponieważ każdy element tablicy grid jest odwiedzany dokładnie raz.
- **Pamięciowa**: O(m×n) z powodu użycia tablicy dp o tych samych wymiarach co grid.

## LCS (Longest Common Subsequence)

### Opis problemu

Algorytm **LCS** znajduje najdłuższą wspólną podsekwencję (kolejność elementów musi być zachowana, ale niekoniecznie muszą być one sąsiadujące) dwóch sekwencji. Intuicyjnie, LCS pomaga zidentyfikować podobieństwa pomiędzy dwiema sekwencjami.

### Podejście dynamiczne

Podstawowy pomysł jest taki, aby zdefiniować tablicę 2D dp, gdzie dp[i][j] oznacza długość LCS dla pierwszych i znaków w sekwencji X i pierwszych j znaków w sekwencji Y.

```
LCS(X, Y):
    n = length(X)
    m = length(Y)

    dp = array of size (n+1)x(m+1) initialized to 0

    for i from 1 to n:
        for j from 1 to m:
            if X[i-1] == Y[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[n][m]
```

### Wyjaśnienie

1. Tworzymy **tablicę dp** o rozmiarze **(n+1)×(m+1)**, gdzie n i m są długościami sekwencji X i Y, odpowiednio. Wszystkie elementy tablicy są **inicjalizowane na 0**.
1. Iterujemy przez sekwencje X i Y przy użyciu dwóch zagnieżdżonych pętli.
   - Jeśli znaki **X[i−1] i Y[j−1] są równe**, to **dp[i][j]** jest zwiększone o 1 w stosunku do **dp[i−1][j−1]**.
   - W przeciwnym razie, wartość **dp[i][j]** jest **maksymalną wartością z dp[i−1][j] lub dp[i][j−1]**.
1. Po zakończeniu iteracji, długość najdłuższej wspólnej podsekwencji będzie znajdować się w **dp[n][m]**.

## Analiza

- **Czasowa**: $O(m*n)$ gdzie m i n to długości dwóch ciągów wejściowych.
- **Pamięciowa**: $O(m*n)$ ze względu na tablicę dp.

## LIS (Longest Increasing Subsequnce)

## Problem plecakowy (Knapsack Problem)

### Opis problemu

Problem plecakowy polega na **maksymalizacji wartości** przedmiotów umieszczonych w plecaku, przy czym **waga tych przedmiotów nie może przekroczyć** określonej pojemności plecaka. Każdy przedmiot ma określoną wagę i wartość. Celem jest wybranie podzbioru przedmiotów, aby ich łączna wartość była **jak największa, bez przekraczania pojemności plecaka**.

### Podejście dynamiczne

Tworzymy tabelę dp[w], w której każdy element reprezentuje maksymalną wartość, jaką można uzyskać, mając plecak o pojemności w.
Zauważmy, że dla każej pojemnośći w jakieś ułożenie będzie maksymalne, oraz że takie ułożenie po wyciągnięciu jednego elementu, będzie maksymalne dla pojemności w pomniejszonej o wage wyciagnietego elementu. Wystarczy dla każdej wagi sprawdzić jaki to będzie element i wziąć maksymalną osiąganą wteyd wartość.

```
def knapsack(weights, values, W):
    n = length(weights)
    dp = [0] * W

    for w = 1 ... W:
        for i = 0 ... n:
            if weight[i] <= w:
                dp[w] = max(dp[w], dp[w - weights[i]] + values[i])

    return dp[W]

```

Złożoność to $O(nW)$. Zauważmy, że jest to złożoność pseudowielomianowa, ponieważ W nie jest wartość opisującą wielkość danych wejściowych.

## Problem sumy podzbiorów (Subset Sum Problem)

## Problem wyznaczania optymalnej kolejności mnożenia macierzy (Matrix Chain Multiplication Problem)

Koszt pomnożenia macierzy o wymiarach $a \times b$ oraz $b \times c$ wynosi $O(abc)$.

Dostajemy jako dane ciąg $d_0 \dots d_n$, wymiary i-tej macierzy to $d_{i-1} \times d_i$.

Użyjemy programowania dynamicznego do obliczenia najmniejszego kosztu mnożenia macierzy, a następnie odtworzymy ciąg operacji.

Zauważmy, że znając koszt mnożenia ciągów macierzy $M_i, \dots, M_k$ oraz $M_{k + 1}, \dots, M_j$, wiemy że koszt wymnożenia powstałych przez nich macierzy to $d_{i - 1} * d_k * d*j$. Jeżeli te koszty były optymalne to wtedy suma tych kosztów będzie optymalna na przedziale $[i, j]$.

```
m[i][j] = min((m[i][k] + m[k + 1][j] + d[i-1] * d[k] * d[j]) for k = i ... j)
```

Dodatkowo w tablicy $p$ możemy zapisywać dla jakich argumentów k wartośc $m_{ij}$ była optymalna. Pozwoli to na szybkie odtworzenie rozwiązania.

```
def matrix_mult(d):
    m = [1..n, 1..n]
    p = [1..n, 1..n]

    for i = 1 ... n:
        m[i][i] = 0
    for s = 1 ... n − 1:
        for i = 1 ... n − s:
            j = i + s
            for k = i ... j:
                opt = m[i][k] + m[k + 1][j] + d[i − 1] * d[k] * d[j]
                if opt < m[i][j]:
                    m[i][j] = opt
                    p[i][j] = k
    return p
```

Przy odtwarzaniu zaczynamy od $p[0][n]$, czyli całego przedziału. Wartość zapisana tam, będzie wyznaczać $k$ dla optymlanego podziału, więc dzielimy macierze na dwie grupy wzgledem tej wartości i dajemy w nawiasy. Proces powtarzamy rekurencyjnie dla obu tak powstałych grup, tylko indesy dla tablicy p będą granicami przedziału tych grup.

## Algorytm Forda-Bellmana

### Opis problemu

Algorytm Bellmana-Forda służy do znajdowania najkrótszych ścieżek **z jednego źródłowego** wierzchołka **do wszystkich innych wierzchołków** w grafie z wagami krawędzi, które mogą być ujemne. Algorytm działa na zasadzie **relaksacji krawędzi**, powtarzając ten proces wielokrotnie, aby poprawić oszacowanie najkrótszych ścieżek. Bellman-Ford może również wykrywać cykle o ujemnej wadze.

### Podejście dynamiczne

Definiujemy dynamiczną tablicę distance, gdzie distance[v] oznacza odległość wierzchołka **v** od wierzchołka **source**.

```
BellmanFord(graph, source):
    distance = array of size |V|, initialized to INF
    distance[source] = 0

    for i from 1 to |V| - 1:
        for each edge (u, v) with weight w in graph:
            if distance[u] + w < distance[v]:
                distance[v] = distance[u] + w

    return distance
```

### Wyjaśnienie

1. Ustawiamy odległości od wierzchołka źródłowego do wszystkich innych wierzchołków na nieskończoność (INF), a odległość do samego źródła na 0.

1. Powtarzamy V−1 razy (gdzie V to liczba wierzchołków w grafie). Dla każdej krawędzi (u, v) z wagą w, jeśli obecna odległość do v jest większa niż odległość do u plus waga krawędzi (u, v), aktualizujemy odległość do v.

### Analiza złożoności

- **Czasowa**: O(V×E), gdzie V to liczba wierzchołków, a E to liczba krawędzi. Algorytm wykonuje V−1 iteracji relaksacji wszystkich E krawędzi.

- **Pamięciowa**: O(V), ponieważ przechowujemy tablicę odległości z jednym wpisem dla każdego wierzchołka.

## Algorytm Warshalla-Floyda

### Opis problemu

Algorytm Floyda-Warshalla służy do **znajdowania najkrótszych ścieżek pomiędzy wszystkimi parami wierzchołków** w grafie. Jest to algorytm dynamicznego programowania, który iteracyjnie poprawia szacunki odległości, uwzględniając coraz większą liczbę możliwych węzłów pośrednich.

### Podejście dynamiczne

tworzymy tabelę dist[i][j], która określa długość najkrótszej ścieżki pomiędzy wierzchołkami i oraz j. Zamysł algorytmu polega na tym, aby dla każdej pary wierzchołków i, j sprawdzić czy poprowadzenie ścieżki przez wierzchołek k zmniejsza długość ścieżki pomiędzy nimi.

```
floydWarshall(graph):
    n = length(graph)
    dist = array of size n x n

    for i from 0 to n-1:
        for j from 0 to n-1:
            dist[i][j] = graph[i][j]

    for k from 0 to n-1:
        for i from 0 to n-1:
            for j from 0 to n-1:
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

    return dist
```

### Wyjaśnienie

1. **dist** jest macierzą odległości początkowo ustawioną tak samo jak macierz wejściowa **graph**, gdzie graph[i][j] zawiera wagę krawędzi między wierzchołkami i oraz j. Jeśli nie ma **bezpośredniej krawędzi między i a j**, graph[i][j] powinno być ustawione na nieskończoność.
1. Iteracja Głównej pętli
   - Algorytm iteracyjnie rozpatruje każdy wierzchołek **k** jako możliwy wierzchołek pośredni na ścieżce z i do j.
   - **Dla każdej pary wierzchołków** i i j, sprawdza, czy przejście przez k daje krótszą ścieżkę niż bezpośrednie połączenie.
   - Jeśli **dist[i][j] > dist[i][k] + dist[k][j]**, aktualizuje dist[i][j] do wartości dist[i][k] + dist[k][j].
1. Po zakończeniu pętli dist[i][j] zawiera najkrótszą odległość między wierzchołkami i i j.

### Analiza

- **Czasowa**: $O(n^3)$, gdzie n to liczba wierzchołków. Wynika to z trzech zagnieżdżonych pętli iterujących przez wierzchołki grafu.

- **Pamięciowa**: $O(n^2)$ ze względu na macierz dist.

## Przynależność do języka bezkontekstowego (membership in a context-free language)

## Drzewa rozpinające drabin

## Problemy NP(NP-trudność, NP-zupełność, redukcje)
