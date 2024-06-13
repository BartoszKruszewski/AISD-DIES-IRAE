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