# AISD DIES IRAE

*Sztuka prztrwania przedmiotu "Algorytmy i Struktury Danych" w założeniu szybko, łatwo i przyjemnie, a w praktyce nie.*

# Spis tematów

0. [Algorytmy omówione na poprzednich przedmiotach](#Algorytmy-omówione-na-poprzednich-przedmiotach)
1. [Preliminaria](#Preliminaria)
2. [Kopce](#Kopce)
3. [Algorytmy zachłanne](#Algorytmy-zachłanne)
4. [Dziel i zwyciężaj](#Dziel-i-zwyciężaj)
5. [Sieci przełączników](#Sieci-przełączników)
6. [Programowanie dynamiczne](#Programowanie-dynamiczne)
7. [Dolne granice](#Dolne-granice)
8. [Sortowania](#Sortowania)
9. [Selekcja](#Selekcja)
10. [Drzewa AVL](#Drzewa-AVL)
11. [Drzewa czerwono-czarne](#Drzewa-czerwono-czarne)
12. [B-drzewa](#B-drzewa)
13. [Kopce Dwumianowe](#Kopce-Dwumianowe)
14. [Kopce Fibonacciego](#Kopce-Fibonacciego)
15. [Drzewa Splay](#Drzewa-Splay)
16. [Drzewce](#Drzewce)
17. [Union Find](#Union-Find)
18. [Hashowanie](#Hashowanie)
19. [Wyszukiwanie wzorca](#Wyszukiwanie-wzorca)
20. [FFT](#FFT)
21. [Van Emde Boas](#Van-Emde-Boas)

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

## Algorytm Prima
## Algorytm Kruskala
## Algorytm Boruvki
## Algorytm Djikstry
## Szeregowanie zadań
## Pokrycie zbioru

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
## Liniowe drzewa decyzyjne
## Redukcje
## Gra z adwersarzem

# Sortowania (głównie Quicksort)

## Izomorfizm drzew
## Quicksort
## Counting sort
## Bucket sort
## Radix sort

# Selekcja

## Algorytm deterministyczny
## Algorytm Hoare'a
## Lazy Select

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