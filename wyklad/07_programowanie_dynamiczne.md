# Programowanie dynamiczne

## Filozfia programowania dynamicznego
## Najtańsze przejście po tablicy 
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
Tworzymy tabelę dp[i][w], w której każdy element reprezentuje maksymalną wartość, jaką można uzyskać, mając plecak o pojemności w i rozważając i pierwszych przedmiotów.
```
knapsack(weights, values, W):
    n = length(weights)
    
    dp = array of size (n+1)x(W+1) initialized to 0

    for i from 1 to n:
        for w from 0 to W:
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], dp[i-1][w-weights[i-1]] + values[i-1])
            else:
                dp[i][w] = dp[i-1][w]

    return dp[n][W]
```

### Wyjaśnienie

1. Tworzymy **tablicę dp** o rozmiarze **(n+1)×(W+1)**, gdzie n i m są długościami sekwencji X i Y, odpowiednio. Wszystkie elementy tablicy są **inicjalizowane na 0**.
1. Iterujemy przez przedmioty (i od 1 do n) i przez możliwe pojemności plecaka (w od 0 do W). Dla każdego przedmiotu i pojemności, **sprawdzamy, czy możemy dodać dany przedmiot do plecaka**. 
    - Jeśli tak, ustawiamy wartość w tabeli jako maksymalną wartość między **wartością bez dodawania przedmiotu a wartością z dodaniem przedmiotu**.
    - w przeciwnym przypadku ustawiamy wartość na tą **bez dodania tego przedmiotu**.
1. Maksymalna wartość, jaką można uzyskać, znajduje się w **dp[n][W]**.

### Analiza:
- **Czasowa**: O(n×W), gdzie n to liczba przedmiotów, a W to pojemność plecaka.
- **Pamięciowa**: O(n×W) ze względu na tablicę DP.

## Problem sumy podzbiorów (Subset Sum Problem)
## Problem wyznaczania optymalnej kolejności mnożenia macierzy (Matrix Chain Multiplication Problem) 
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