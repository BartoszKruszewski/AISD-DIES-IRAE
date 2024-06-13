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
