# AISD DIES IRAE

*Sztuka prztrwania przedmiotu "Algorytmy i Struktury Danych" w założeniu szybko, łatwo i przyjemnie, a w praktyce nie.*

# Spis tematów

0. [Algorytmy omówione na poprzednich przedmiotach](/wyklad/01_wstepne_algorytmy.md)
1. [Preliminaria](/wyklad/02_preliminaria.md)
2. [Kopce](/wyklad/03_kopce.md)
3. [Algorytmy zachłanne](/wyklad/04_algorytmy_zachlanne.md)
4. [Dziel i zwyciężaj](/wyklad/05_dziel_i_zwyciezaj.md)
5. [Sieci przełączników](/wyklad/06_sieci_przelacznikow.md)
6. [Programowanie dynamiczne](/wyklad/07_programowanie_dynamiczne.md)
7. [Dolne granice](/wyklad/08_dolne_granice.md)
8. [Sortowania](/wyklad/09_sortowania.md)
9. [Selekcja](/wyklad/10_selekcja.md)
10. [Drzewa AVL](/wyklad/11_drzewa_avl.md)
11. [Drzewa czerwono-czarne](/wyklad/12_drzewa_czerwono_czarne.md)
12. [B-drzewa](/wyklad/13_b_drzewa.md)
13. [Kopce Dwumianowe](/wyklad/14_kopce_dwumianowe.md)
14. [Kopce Fibonacciego](/wyklad/15_kopce_fibonacciego.md)
15. [Drzewa Splay](/wyklad/16_drzewa_splay.md)
16. [Drzewce](/wyklad/17_drzewce.md)
17. [Union Find](/wyklad/18_union_find.md)
18. [Hashowanie](/wyklad/19_hashowanie.md)
19. [Wyszukiwanie wzorca](/wyklad/20_wyszukiwanie_wzorca.md)
20. [FFT](/wyklad/21_fft.md)
21. [Van Emde Boas](/wyklad/22_van_emde_boas.md)

# Algorytmy omówione na poprzednich przedmiotach

## Merge Sort
## Algorytm Euklidesa
## DFS i BFS
## Algorytm Forda-Fulkersona
## Maszyna RAM

# Preliminaria

## Mnożenie "po rosyjsku"
## Kryterium jednorodne i logarytmiczne
## Notacje rzędów funkcji $\Omega$, $\Theta$, $O$

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

# Algorytmy zachłanne

## Wydawanie reszty

Mając podany zbiór nominałów, chcemy wydać konkretną kwotę za ich pomocą, używając jak najmniej monet. Strategia zachłanna zakłada wydawanie zawsze najwięszkego nominału mieszącego się w kwocie jaka pozostała nam do wydania.

Algorytm ten nie zawsze zwraca rozwiązanie optymalne, a dla niektórych danych może zwrócić nawet niepoprawne.

## Algorytmy znajdowania MST (Minimalne drzewo rozpinające) 

MST to zbiór krawędzi z grafu, które tworzą drzewo (graf spójny, acykliczny) o minimalnej wadze krawędzi.

### Algorytm Kruskala

Dodajemy do rozwiązania krawędź o najmniejszej wadze, jeżeli nie powoduje to powstania cyklu w rozwiązaniu. Krawędzie dodajemy, aż dodanie jakiejkolwiek krawiędzi będzie powodowało cykl.

### Algorytm Prima

Wybieramy losowo wierzchołek. Dodajemy do rozwiązania krawędź incydentną z nim o najmniejszej wadze. Następnie dodajemy do rozwiązania krawędź, z jeszcze niewybranych krawędzi incydentną z aktualnym rozwiązaniem (tylko jednym końcem), która ma najmniejszą wagę. Powtarzamy, aż wszystkie pozostałe krawędzie będą incydentne oboma końcami z rozwiązaniem.

### Algorytm Boruvki

Dla każdego wierzchołka, dodajemy do rozwiązania najkrótszą incydentą z nim krawędź. Tak powstałe spójne składowe oznaczamy traktujemy jako superwierzchołki i powtarzamy algorytm dla tworzonego przez nie grafu. Powtarzamy, aż zostanie jedna spójna składowa.

## Szeregowanie zadań

### Wariant podstawowy

Musimy ustalić kolejność wykonywania zadań, tak żeby czas oczekiwania zadań w systemie był najkrótszy.

Wykorzystujemy strategię zachłanną ustawiając zadania w kolejności rosnącej względem ich długości.
Wtedy najszybciej zmniejszamy liczbę równolegle czekających zadań.

### Wariant z terminami

Każdy proces wykonujemy się jedną jednostkę czasu. Każdy proces ma termin wykonania oraz nagrodę za wykonanie go w terminie. Chcemy wybrać taki podzbiór procesów, żeby suma zdobytych nagród była maksymalna.

*do dokończenia*

## Pokrycie zbioru

Dla rodziny zbiorów oraz ich kosztów, musimy znaleźć najtańszą podrodzinę tych zbiorów, która pokryje uniwersum.

Problem jest $NP-trudny$, ale zamiast tego można zastosować algorytm aproksymacyjny. Wybieramy zbiór, który najtaniej pokrywa elementy. 

Określamy to wzorem:

$cne(S_i) = \frac{c(S_i)}{|S_i/C|}$

gdzie $C$ to zbiór dotychczas pokrytych elementów.

Do rozwiązania wybieramy zbiór z minimalnym $cne$.

Koszt powyższego algorytmu jest nie większy niż $log(n) * OPT$

$Koszt(ALG) = \sum_{i = 1}^{n} c(e_i) \le \sum_{i = 1}^{n} \frac{OPT}{n - i + 1} = OPT * \sum_{i = 1}^{n} \frac{1}{n - i + 1} = OPT * log(n)$ 

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

# Sieci przełączników

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

# Dolne granice

## Drzewa decyzyjne

### Intuicja

Model obliczeń, w którym jedynymi operacjami na ciągu wejściowym są porównania. Jedno drzewo decyzyjne odpowiada działaniu algorytmu dla danych o konkretnym rozmiarze przez co jest skończone. Chcąc uzyskać dowolność w rozmiarze danych możemy rozważyć rodzinę drzew decyzyjnych.

### Reprezentacja

- wierzchołki wewnętrzne: porównania
- liście: wyniki
- krawędzie: obliczenia pomiędzy porównaniami

### Dolna granica dla problemu sortowania

Utwórzmy drzewo decyzyjne dla ciągu $n$ liczb. Ilość możliwych wyników, więc też liści to liczba permutacji ciągu wejściowego, czyli $n!$. Drzewo binarne o $n!$ liściach ma wysokość $\ge log_2(n!)$. 

Oszacujmy to ze wzoru **Stirlinga** $n! \ge (n/e)^n$:
$log_2(n!) \ge log_2((n/e)^n) = n * (log_2(n) - log_2(e)) = \Omega(n * log(n))$. 

## Liniowe drzewa decyzyjne

### Intuicja

Model jest rozszerzeniem klasycznych drzew decyzyjnych. Te drzewa są trynarne, a porównywać będziemy kombinacje liniowe elementów ciągu wejściowego w trzech relacjach: $<0$, $>0$, $=0$.

### Dolna granica dla problemu różności elementów

Problem polega na stwierdzeniu, czy wszystkie elementy ciągu wejściowego są parami różne.

*do dokończenia*

## Redukcje

Redukcje pozwalają stwierdzić, że jakiś problem jest co najmniej tak trudny jak inny problem.

### Redukcja z problemu sortowania do problemu znajdowania otoczki wypukłej

Musimy używając algorytmu znajdowania otoczki wypukłej oraz używając operacji o złożonośći mniejszej niż ten algorytm, rozwiązać problem sortowania.

1. Dla danych ${x_1, ..., x_n}$, weźmy $S = \{(x_1, x_1^2), ..., (x_n, x_n^2)\}$
2. Znajdujemy otoczkę wypukłą dla punktów $S$ i zapisujemy ją jako $A$.
3. Weźmy pierwsze współrzędne punktów z $A$, będą one posortowane.

Punkty $S$ tworzyły parabole, czyli figurę wypukłą, więc wszystkie trafią do wyniku. Punkty na otoczce wypukłej są zwracane w kolejności w jakiej powinny zostać połączone. Dla paraboli, będzie to posortowany ciąg.

Ponieważ problem sortowania jest $\Omega(nlog(n))$ to problem znajdowania otoczki wypukłej też musi być co najmniej $\Omega(nlog(n))$. Inaczej zaprzeczałby dolnej granicy problemu sortowania.

## Gra z adwersarzem

### Intuicja

Gra z adwersarzem, polega na "odwróceniu ról". Algorytm, którego czas chcemy oszacować nie zna zbioru danych na jakich będzie operował. Adwersarz będzie podawał dane, ale będzie opracowywał strategię podawania danych, żeby przekroczyć dolną granicę, którą chcemy udowodnić. Algorytm będzie starał się tak działać, że uzyskać najmniejszy możliwy czas. Naszym celem jest udowodnić, że istnieje wygrawająca strategia dla adwersarza.

### Dolna granica dla jednoczesnego znajdowania min oraz max

Chcemy udowodnić, że dolna granica dla tego problemu to $\lceil \frac{3}{2}n-2 \rceil$ porównań.

Cel gry:
- algorytm: znalezienie min i max, w mniej niż $\lceil \frac{3}{2}n-2 \rceil$ porównań
- adwersarz: zmuszenie algorytmu do zadania co najmniej $\lceil \frac{3}{2}n-2 \rceil$ porównań

Ruchy:
- algorytm: zapytanie porównujące dwa elementy
- adwersarz: odpowiedź na to pytanie (zawsze musi zgodna z prawdą)

Musimy pokazać, że istnieje strategia zawsze wygrywająca dla adwersarza.

Strategia:

Dzielimy elementy na cztery zbiory:
- $A$ (jeszcze nie porównane elementy)
- $B$ (elementy, które były większe w porównaniu i jeszcze ani razu nie były mniejsze)
- $C$ (elementy, które były mniejsze w porównaniu i jeszcze ani razu nie były większe)
- $D$ (elementy, które wygrały i przegrały)

Zauważmy, że adwersarz może zwiększać wartości elementów z $B$ i zmiejszać wartości elementów z $C$, ponieważ nadal będą one zgodne z już udzielonymi odpowiedziami

Adwersarz może zapewnić, że wszystkie elementy z $A$ oraz $D$ będą mniejsze od elementów z $B$ i większe od elementów z $C$.

Obserwacje:
- jedno porównanie usuwa max 2 elementy z $A$
- dodanie elementu do $D$ wymaga jednego porównania
- porównania, których bierze udział element z $A$, nie zwiększają $D$ 

Dopóki $A$ jest niepusty lub $B$ lub $C$ zawierają więcej niż jeden element, algorytm nie może udzielić poprawnej odpowiedzi.

Na opróżnienie zbioru A, potrzeba $\lceil n/2 \rceil$ porównań. Następnie potrzeba $n - 2$ porównań na przesłanie elementów z $B$ i $C$ do $D$. Razem to $\lceil \frac{3}{2}n-2 \rceil$ porównań.

# Sortowania (głównie Quicksort)

## Właściowości sortowań

### Stabilność

Sortowanie jest stabilne jeżeli elementy o równej wartości klucza, po sortowaniu zachowują względem siebie pierwotny porządek.

### Sortowanie w miejscu

Algorytm sortuje w miejscu, jeżeli nie zużywa dodatkowej pamięci proporcjonalnej do wielkości danych.

## Quicksort

### Intuicja

Quicksort przypomina Merge sorta, z tą różnicą, że podział tablicy odbywa się względem pivota. Jest to wybierany w określony sposób element, względem którego tablice dzielone są na dwie części. Jedna zawiera elementy mniejsze od pivota a druga większe.

### Algorytm

Wybieramy pivota, następnie przestawiamy elemenety za pomocą procedury partiotion, żeby elementy na lewo od pivota były mniejsze od niego, a na prawo od pivota były od niego większe. Następnie dla tak powstałych dwóch części tablicy wywołujemy quicksorta rekurencyjnie.

Koszt procedury partition to $\Theta(r - p)$, czyli długość przestawianego przedziału. 

```
def quick_sort(A, p, r):
    if r - p jest małe:
        insert_sort(A)
    else:
        choose_pivot(A, p, r)
        q = partition(A, p, r)
        quick_sort(A, p, q)
        quick_sort(A, q + 1, r)
```

```
def partition(A, p, r):
    x = A[p]
    i = p - 1
    j = r + 1
    while i < j:
        while A[j] > x:
            j -= 1
        while A[i] < x:
            i += 1
        if i < j:
            swap(A[i], A[j])
        else:
            return j
```

### Wybór Pivota

- mediana: czas działania algorytmu wynosi $\Theta(nlog(n))$, ale stała ukryta pod $\Theta$ jest bardzo duża
- metoda deterministyczna (pierwszy element): nierównomierne podziały dla uporządkowanych danych, pesymistycznie czas działania to $O(n^2)$
- wybór zrandomizowany: czas oczekiwany $\Theta(nlog(n))$, pesymistyczny $O(n^2)$, ale jest mało prawdopodobny. Ta metoda nie jest wrażliwa na złośliwe dane
- mediana z małej próbki: podobnie jak wybór zrandomizowany

### Analiza złożoności

Weźmy zmienna losową $X_{ij}$, która przyjmuje wartość $1$, jeśli quicksort porównał elementy $y_i$ oraz $y_j$, i wartość $0$ wpp. Niech $X = \sum_{i = 1}^{n - 1} \sum_{j = i + 1}^{n} X_{ij}$. Wtedy $X$ oznacza liczbę porównań jakich dokonał quicksort.

$E(X) = E(\sum_{i = 1}^{n - 1} \sum_{j = i + 1}^{n} X_{ij}) = \sum_{i = 1}^{n - 1} \sum_{j = i + 1}^{n} E(X_{ij})$

Do porównania elementów $y_i$ oraz $y_j$ nie dojdzie kiedy będą porównywane elementy spoza zbioru $y_i, ..., y_j$. Jeżeli pivotem zostanie $y_i$ lub $y_j$ to dojdzie do porównania, natomiast dla pozostałych elementów z tego zbioru elementy $y_i$ i $y_j$ nie zostaną porównane, ale znajdą się w innych zbiorach, więc nie zostaną porównane ponownie. Więc szansa to $2$ wybory ze zbioru $y_i, ..., y_j$. Stąd:

$E(X_{ij}) = P(X_{ij} = 1) = \frac{2}{j - i + 1}$

Podstawiając:

$E(X) = \sum_{i = 1}^{n - 1} \sum_{j = i + 1}^{n} \frac{2}{j - i + 1} = 2nln(n) + \Theta(n)$

## Counting sort

Counting przyjmuje jako dane tylko liczby całkowite z przedziału $<1, k>$ i nie bazuje na standardowym modelu porównań wykorzystywanym w sortowaniach.

Idea opiera się na policzeniu $c[x]$ oznaczające liczbę elementów tablicy niewiększych od x. Następnie wystarczy dodać element $x$ na miejsce $c[x]$

```
def counting_sort(A, k)

    B = [] * n
    for i = 1 ... k:
        c[i] = 0

    # każdy element jest niewiększy od siebie samego
    for j = 1 ... n:
        c[A[j]] += 1

    # elementy niewiększe od i są też niewiększe od i - 1
    for i = 2 ... k:
        c[i] += c[i − 1]

    # wpisywanie elementów na odpowiednie miejsce
    for j = n ... 1:
        B[c[A[j]]] = A[j]

        # jeżeli jakiś element będzie równy aktualnemu A[j],
        # to zostanie wpisany na mniejsce poprzedzające A[j]
        c[A[j]] −= 1

    return B
```

Counting sort działa w czasie $\Theta(n + k)$ i jest stabilny.

## Bucket sort

Sortowanie kubełkowe działa dobrze dla danych będących losowymi liczbami rzeczywistymi z przedziału $<0, 1>$ o rozkładzie jednostajnym.

Idea opiera się o podział przedziału $<0, 1>$ na $n$ odcinków i obliczaniu w czasie stałym do jakiego odcinka należy wartość. Następnie taką wartość dodajemy do kubełka reprezentującego odcinek. Następnie należy posortować kubełki (oczekiwana wielkość kubełków jest bardzo mało, jest $n$ kubełków na $n$ punktów). Na koniec wystarczy skleić ze sobą kubełki.

```
def bucket_sort(A):
    for i = 0 ... n − 1:
        B[i] = []
    for i = 1 ... n:
        B[floor(n * A[i])].append(A[i])
    for i = 0 ... n − 1:
        select_sort(B[i])
    return B[0] + B[1] + , ..., + B[n − 1]
```

Niech $X_i$ oznacza liczbę elementów w i-tym kubełku. $X_i$ ma rozkład dwumianowy z ppb sukcesu $1/n$. Niech $Y_i$ oznacza liczbę porównań podczas sortowania i-tego kubełka. Używamy do tego select-sorta, więc $Y_i = X_i^2$

Wiemy, że:
$E(X_i) = n * p = n * 1/n = 1$
$V(X_i) = n * p * (1 - p)= 1 - 1/n$

Podstawmy pod wzór na wariancję:
$V(X_i) = E(X_i^2) - (E(X_i))^2$
$E(X_i^2) = V(X_i) + (E(X_i))^2$
$E(X_i^2) = 1 - 1/n + 1 = 2 - 1/n$
$E(Y_i) = E(X_i^2) = 2 - 1/n$

Weźmy $Y = \sum_{i = 0}^{n - 1} Y_i$. Wtedy $Y$ oznacza liczbę porównań w całym bucket-sort.  

$E(Y) = E(\sum_{i = 0}^{n - 1} Y_i) = \sum_{i = 0}^{n - 1} E(Y_i) = n * (2 - 1/n) = 2n - 1 = \Theta(n)$

Więc oczekiwany czas działania bucket-sorta to $\Theta(n)$.

## Radix sort

Radix sort oznacza sortowanie leksykograficzne. Ciąg S jest wcześniejszy leksykograficznie od T, jeżeli S jest prefiksem T, lub jeżeli na pierwszej różniącej się pozycji ma wcześniejszy element względem ustalonego alfabetu.

### Ciagi słów jednakowej długości

Tutaj wystaczy stabilnie posortować elementy po każdym elemencie zaczynając od ostatniego.

```
def radix_sort(T):
    for i = |T[0]| ... 0:
        stable_sort(T, key = lambda A: A[i])
```

Używając Counting Sorta, złożoność tego algorytmu będzie wynosić $O((n + |\Sigma|) * d)$. Gdzie $|\Sigma|$ to wielkość alfabetu, natomiast $d$ to długość słów. Jeżeli potraktujemy $d$ jako stałą, a $|\Sigma| = O(n)$ to złożnośc algorytmu wyniesie $O(n)$.

### Ciągi słów różnej długości

Można zastosować uzupełnienie słów o pusty znak i wtedy posortować, natomiast taka metoda jest nieefektywna.

Oznaczmy jako $l_i$ długość i-tego słowa. Wtedy:

$l_{total} = \sum_{i = 1}^{n} l_i$

Chcemy uzyskać algorytm, który ma złożoność $O(|\Sigma| + l_{total})$.

```
B[l] - zawiera wszystkie l-te litery słow uprządkowane niemalejąco
S[l] - zawiera wszystkie slowa o długości l
Q[a] - zawiera kolejkę słów, której l-tą literą jest a

for l = lmax ... 1:
    while S[l] != []:
        slowo = S[l].pop()
        Q[slowo[l]].push(slowo)
    for a in B[l]:
        res += Q[a]
```

Listę $B$ można utoworzyć poprzez radix_sort dla słów tej samej długośći dla listy par $<l, a>$, gdzie $a$ to l-ta litera jakiegoś słowa. Robimy to w czasie $O(l_{total})$.
Utworzenie $S$ to policzenie liter i dodanie słów do odpowiedniego kubełka, czyli $O(l_{total})$. Pętla while wykona się proporcjonanie do ilości słów, a wewnętrzna pętla for proporcjonalnie do ilości liter. Czyli razem $O(l_{total})$.

## Izomorfizm drzew

### Intuicja

Dwa grafy są izomorficzne, jeżeli istnieje bijekcja (przeetykietowanie) wierzchołków jednego grafu w wierzchołki drugiego grafu, takie że jeżeli wierzchołki w pierwszym grafie łączyła krawędź to w drugim też będzie. Intuicyjnie oznacza to, że grafy mają taką strukturę, niezależną od wartości wierzchołków.

### Izomorfizm grafów, a izomorfizm drzew

Problem rozstrzygnięcia czy dwa grafy są izomorficzne jest w klasie NP, zatomiast nie wiadomo, czy jest NP-zupełny. Natomiast ograniczając się do wyłącznie do drzew problem izomorfizmu grafu można rozwiązać w czasie $O(n)$.

### Algorytm AHU (Aho, Hopcroft, Ullman)

Algorytm polega zakodowaniu drzew jako jednoznacznie definiujące ich strukturę ciągi nawiasów, a następnie porównanie czy ciągi są takie same.

Enkodowanie dla poddrzewa to jego zakodowane poddrzewa, w posortowanej kolejności, żeby zachować jednoznaczność, otoczone nawiasami.

```
def encode(node):
    if node is None:
        return ""

    labels = [encode(v) for v in node.children]
    sort(labels)

    return "(" + str(labels) + ")"
```

Dla drzew nieukorzenionych należy znaleźć ich wierzchołki centralne i dla nich wywołać enkodowanie.

```
def tree_isomorphism(T1, T2):
    centers1 = tree_centers(T1)
    centers2 = tree_centers(T2)

    encoded1 = encode(centers1[0])

    for center in centers2:
        encoded2 = encode(center)
        if encoded1 == encoded2:
            return True
    return False
```

Złożoność algorytmu jest równa $O(n * m * log(m))$, gdzie $n$ to liczba wierzchołków, a $m$ to arność drzewa. Wynika to stąd, że dla każdego wierzchołka wykonamy sortowanie ciągu o długości równej co najwyżej arności drzewa. Przyjmując $m$ jako stałą, złożoność algorytmu wynosi $O(n)$.


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

# Drzewa AVL

## Opis problemu
***Drzewo AVL*** zdefiniowane jest jako samobalansujące się drzewo wyszukiwań binarnych **(BST)**, w którym **współczynnik równowagi** każdego węzła jest nie większy niz jeden.

***Współczynnikiem równowagi*** węzła nazywamy różnicę między **wysokością** lewego i prawego poddrzewa tego węzła.

![Drzewo AVL](/Materiały/Drzewo%20AVL.png)
## Obracanie poddrzew w drzewie AVL
Aby zachować **równowagę** oraz **strukturę drzewa wyszukiwań binarnych**, drzewo AVL będzie się obracać w jeden z 4 sposobów:

### ***(Left Rotation)***
Jeżeli po dodaniu węzła do prawego syna (C) prawego poddrzewa (B) drzewo jest niezbalansowane, wykonujemy rotację w **lewo**

![Left Rotation](/Materiały/Drzewa%20AVL%20Left%20Rotation.png)

### ***(Right Rotation)***
Jeżeli po dodaniu węzła do lewego syna (C) lewego poddrzewa (B) drzewo jest niezbalansowane, wykonujemy rotację w **prawo**

![Right Rotation](/Materiały/Drzewa%20AVL%20Right%20Rotation.png) 

### ***(Left-Right Rotation)***
Jeżeli po dodaniu węzła do prawego syna (B) lewego poddrzewa (A) drzewo jest niezbalansowane, wykonujemy wpierw obrót w **lewo**, a potem w **prawo**

![Left right Rotation](/Materiały/Drzewa%20AVL%20Left-Right%20Rotation.png) 

### ***(Right-Left Rotation)***
Jeżeli po dodaniu węzła do lewego syna (B) prawego poddrzewa (C) drzewo jest niezbalansowane, wykonujemy wpierw obrót w **prawo**, a potem w **lewo**

![Right Left Rotation](/Materiały/drzewa%20AVL%20Right-Left%20Rotation.png)

## Zalety drzew AVL
1. **Wysokość drzewa** AVL jest zawsze **O(logn)**, gdzie n to liczba węzłów w drzewie. Dzięki temu operacje wyszukiwania, wstawiania i usuwania mają złożoność czasową **O(logn)**.
1. Dzięki automatycznemu wyważaniu po każdej operacji **wstawiania** lub **usuwania**, drzewa AVL unikają najgorszego przypadku związanego z **drzewami binarnymi**, które mogą stać się **silnie niezrównoważone**.
1. Rotacje wykorzystywane do balansowania drzewa są szybkie i efektywne.
1. Drzewa AVL zawsze są zbalansowane, co oznacza, że zawwsze **współczynnik równowagi** jest nie większy niż 1. To ograniczenie gwarantuje, że operacje będą miały optymalną złożoność czasową.

# Drzewa czerwono-czarne

## Opis problemu
***Drzewo Czerwono - Czarne*** to rodzaj **zrównoważonego drzewa wyszukiwań binarnych**, które wykorzystuje zestaw reguł do utrzymania równowagi, zapewniając **logarytmiczną** złożoność czasową dla operacji takich jak **insert**, **delete** i **find**, niezależnie od początkowego kształtu drzewa.

![Drzewo czerwono-czarne](/Materiały/Drzewo%20czerwono-czarne.png)

***Drzewa Czerwono - Czarne*** balansują się wykorzystując prosty **schemat kodowania kolorami** w celu dostosowania drzewa po każdej modyfikacji.

Intuicyjnie, można sobie wyobrazić drzewo czerwono-czarne jako drzewo, które jest **nieco bardziej elastyczne** w porównaniu do drzewa AVL, pozwalając na nieco większe odchylenia od idealnej równowagi, ale nadal **ograniczające te odchylenia** w sposób kontrolowany.

## Właściwości Drzew Czerwono - Czarncyh
1. **Kolor węzła** : Każdy węzeł jest czerwony lub czarny .
1. **Właściwość korzenia** : Korzeń drzewa jest zawsze czarny .
1. **Właściwość koloru czerwonego** : Węzły czerwone nie mogą mieć czerwonych dzieci (nie ma dwóch kolejnych czerwonych węzłów na żadnej ścieżce).
1. **Właściwość koloru czarnego** : każda ścieżka od węzła do potomnych węzłów zerowych (liście) ma tę samą liczbę czarnych węzłów.
1. **Właściwość liścia** : Wszystkie liście (węzły NIL) są czarne.

Te właściwości zapewniają, że **najdłuższa ścieżka** od korzenia do dowolnego liścia nie jest dłuższa niż dwukrotność najkrótszej ścieżki, zachowując równowagę drzewa i wydajną pracę.

# B-drzewa

# Drzewa Splay			

# Drzewce

# Kopce Dwumianowe

# Kopce Fibonacciego

# Union Find

### Opis problemu

Union-Find jest strukturą danych służącą do zarządzania dynamicznie zmieniającymi się zbiorami elementów. Algorytm ten pozwala efektywnie wykonywać dwie główne operacje:

- Union: Łączenie dwóch zbiorów w jeden.
- Find: Znajdowanie reprezentanta (lidera) zbioru, do którego należy dany element.

### Reprezentacja zbiorów
Każdy zbiór jest reprezentowany przez drzewo, gdzie każdy węzeł wskazuje na swojego rodzica. Korzeń drzewa jest reprezentantem zbioru. Początkowo każdy element jest w swoim własnym zbiorze i jest korzeniem samego siebie.

### Operacje
- ***Find*** polega na znalezieniu **korzenia drzewa**, do którego należy dany element. Aby to zrobić, przechodzimy od danego elementu w górę drzewa, aż dojdziemy do korzenia.
- ***Union*** polega na połączeniu dwóch zbiorów. Najpierw znajdujemy **reprezentantów obu zbiorów**, a następnie łączymy jeden z tych zbiorów z drugim. Można to zrobić, ustawiając korzeń jednego drzewa jako dziecko korzenia drugiego drzewa.

### Optymalizacje
- **Kompresja ścieżki** (Path Compression): Podczas wykonywania operacji find, każdemu węzłowi na ścieżce do korzenia przypisujemy bezpośrednio korzeń, co przyspiesza przyszłe operacje find.
- **Złączenie według rangi** (Union by Rank): Przy łączeniu dwóch drzew, mniejsze drzewo (pod względem głębokości) jest przyłączane do korzenia większego drzewa, co zapobiega powstawaniu zbyt głębokich drzew.

### Złożoność czasowa
- Dzięki zastosowaniu **kompresji ścieżki** i **złączenia według rangi**, czas wykonywania każdej operacji find i union jest bardzo efektywny.
- Amortyzowana złożoność czasowa każdej operacji to niemal stała **O(α(n))**, gdzie α jest bardzo wolno rosnącą funkcją inwersji **Ackermanna**, która jest mniejsza niż 5 dla wszelkich praktycznych zastosowań.

# Hashowanie

## Funkcje hashujące
## Słownik "z nawlekaniem"
## Hashowanie otwarte
## Hashowanie uniwersalne
## Schematy urnowe
## Słownik statyczny

# Wyszukiwanie wzorca

## Algorytm Karpa-Rabina
## Automaty skończone
## Algorytm KMP (Knuth-Morris-Pratt)
## Algorytm Boyera-Moore'a
## Algorytm Shift-AND
## Algorytm KMR (Karpa-Millera-Rosenberga)

# FFT
# Van Emde Boas

# Lista 0
## Macierzowe obliczanie ciągów rekurencyjnych
## Szybkie potęgowanie
## Sprawdzanie kto czy wierzchołek jest potomkiem innego wierzchołka

# Lista 1
## Wielkość i średnica drzewa binarnego
## Kopiec min-max
## Znajdowanie pierwszego porządku topologicznego
## Liczba sensownych dróg w grafie
## Najdłuższa droga w DAG (Directed acyclic graph)
## Ile elementów 2 razy większych od innych możemy usunąć?
## Okno pokrywające wszystkie listy

# Lista 2
## Maksymalny zbiór nieprzecinających się odcinków
## Znajdowanie ułamka egipskiego
## Wydawanie reszty liczbami Fibonacciego
## "Atrakcyjność kliencka"
## Kolorowanie k-ścieżek w drzewie
## Należenie krawędzi do MST
## Obwód drzewa
## Ciąg operacji swap zamiany permutacji $\pi$ w $\sigma$
## Scieżka Hamiltona dla grafów skierowanych
## Scieżka Hamiltona w grafie gdzie wierzchołki mają conajmniej $\frac{n}{2}$ sąsiadów
## Dowód poprawności Dijkstry

# Lista 3
## Szacowanie równania rekurencyjnego
## Widoczność prostych
## Kwadrat liczby za pomocą Karatsuby
## Znajdowanie otoczki wypukłej za pomocą dziel i zwyciężaj
## Minimum lokalne w drzewie z minimalną liczbą odsłonięć
## Liczba wierzchołków oddalonych o stałą
## Liczba inwersji w permutacji
## Sieć przełączników

# Lista 4
## Drugie najtańsze przejście po tablicy
## Sprawdzanie przynależnośći słowa do gramatyki w postaci Chomskiego
## Najkrótszy Superciąg
## Szukanie elementów mniejszych niż k, przy minimalnej liczbie zapytań.
## LCS w liniowej pamięci (sztuczka Hirschberg'a)
## Niezależny podzbiór wierzchołków z max wagą
## LCS ze wzorcem
## Problem 3-podziału
## LCIS (Longest common increasing subsequence)
## LIS oraz liczba LIS'ów

# Lista 5
## Dowód, że otoczka wypułka nie może być rozwiązana w modelu drzew decyzyjnych
## Dolna granica dla 3SUM
## 3SUM
## Redukcja 3SUM do współliniowości 3 punktów
## Dolna granica porównań dla scalania ciągów
## Redukcja 3SAT do 3D-matching
## Dolna granica dla znajdowania największego i drugiego największego elementu

# Lista 6
## Nierekurencyjny Quicksort w miejscu
## Izomorfizm drzew nieukorzenionych
## Szacowania złożonośći algorytmu Hoare'a metodą Fredmana
## Drzewa lewicowe
## Przekształcanie BST w dowolne inne BST za pomocą rotacji
## Split drzew AVL
## Struktura danych do mindiff
## Struktura danych do sum-of-even
## Optymalizacja pamięci w drzewach AVL

# Lista 7
## Ciąg operacji Union, Find w strukturze drzewiastej
## Ciąg operacji Insert, DeleteMin, Min
## Ciąg instrukcji Link i Depth na lesie rozłącznych drzew
## Find podłączające wierzchołek pod jego dziadka
## "Osuszanie sąsiedztwa zalanych domów"

# Lista 8
## Znajdowanie optymalnego BST
## Znajdowanie pary najbliżej położonych punktów za pomocą grida i hashowania
## Oczekiwana liczba pustych list w słowniku
## Analiza zamortyzowana kosztu operacji dla kopca Fibonacciego
## Czas tworzenia słownika stałego
## Oczekiwana liczba prób do trafienia w słowniku z hashowaniem otwartym

# Lista 9
## Obsługa "wild card'a" we wzorcu
## Określenie czy T jest przesunięciem cyklicznym T'
## Obliczenie funkcji przejść automatu dla wzorca
## Szukanie kolorowania czerwono-czarnego dla drzewa binarnego
