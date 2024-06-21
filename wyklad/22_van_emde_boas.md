# Van Emde Boas

Oznaczamy nazwę struktury jako $vEB$

## Założenia

Ta struktura danych działa dobrze dla danych z niewielkiego uniwersum liczb całkowitych. Struktura pozwala wykonywać operacje insert, delete, find, succ, pre, min, max w czasie $O(log{log{u}})$, gdzie $u$ to rozmiar uniwersum.

## Budowa

Struktura wykorzystuje rekurencyjnie wektory charakterystyczne, czyli tablice wartości boolowskich dla których wartość $1$ na indeksie $i$ oznacza, że struktura zawiera liczbę $i$, $0$ wpp.

Na każdym poziomie rekurencji struktura ma $\sqrt{u}$ podtablic, gdzie każda jest $vEB$, oraz tablic podsumowującą wszystkie podtablice, która również jest $vEB$.

Tablica podsumowująca zawiera $1$ na indeksie $i$, jeżeli i-ta podtablica ma w sobie jakiekolwiek $1$ (taki duży **OR**). Dzięki temu możemy pomijać puste obszary tablicy podczas wyszukiwania $succ$.

Do odnoszenia się do elementów struktury będziemy używać oznaczeń:

- V.cluster[i] (i-ta podtablica)
- V.summary (tablica podsumowująca)
- high(x) (indeks podtablicy w jakiej znajduje się x)
- low(x) (indeks elementu x w swojej podtablicy)
- V.min / V.max (min i max w danym drzewie)

## Wyliczanie high oraz low

$high(x) = \lfloor x/\sqrt{u} \rfloor$

$low(x) = x \mod \sqrt{u}$

Zauważmy, że high(x) odpowiada liczbie zapisanej na wyższej połowie bitów x, natomiast low(x) na niższej.

Dzięki temu można wyliczać high oraz low za pomocą przesunięc bitowych, co jest bardzo szybkie.

Odwołanie się do elementu można zrobić za pomocą:

$index(i, j) = i * \sqrt{u} + j$

## Operacja Succ

1. Znajdujemy odpowiednią podtablicę
2. Sprawdzamy, czy element jest mniejszy niż max podtablicy
   - jeżeli tak to znaczy, że jego następnik jest w tej podtablicy
   - jeżeli nie musimy szukać w innych podtablicach
3. Jeżeli szukamy w innych podtablicach, to znajdujemy następnik wśród podsumowań podtablic. Będzie on wskazywał na pierwszą podtablicę, która ma jakikolwiek element.
4. Następna podtablica zawiera tylko elementy większe od x, więc wystarczy wziąć min z tej podtablicy, a będzie ono następnikiem.

```
def succ(V, x):
    i = high(x)
    if low(x) < V.cluster[i].max:
        j = succ(V.cluster[i], low(x))
    else:
        i = succ(V.summary, high(x))
        j = V.cluster[i].min
    return index(i, j)
```

# Insert

Dodając do $vEB$ musimy zaktualizować wartość podtablicy oraz tablicy podsumowującej. Zauważmy, że tablica podsumowująca podczas dodawania elementu można zostać zmieniona tylko z 0 na 1 dla indeksu podtablicy w jakiej znajduje się dodawany element. Taka zmiana występuje tylko wtedy, kiedy wartość w tablicy była równa 0, czyli podtablica była pusta.

Musimy umieć wykrywać czy tablica jest pusta w czasie stałym. Możemy to zrobić sprawdzając, czy min zostało już ustawione.

```
def empty(V):
    return V.min == None
```

Dodawanie do pustego drzewa też jest leniwe, czyli zapamietujemy wartość w min oraz max, która zostanie przeniesiona przy kolejnych wywołaniach:

```
def empty_insert(V, x):
    V.min = x
    V.max = x
```

1. Sprawdz czy podtablica jest pusta
2. Jeżeli tak to dodaj element do podtablicy (szybko) oraz zaktualizuj tablice podsumowującą
3. Jeżeli nie to nie trzeba modyfikować tablicy podsumowującej, więć zmodyfikuj tylko podtablice

Dodatkowo aktualizujemy wartości min oraz max.

```
def insert(V, x):
    if empty(V):
        empty_insert(V, x)
    else:
        if x < V.min:
            swap(x, V.min)
        if x > V.max:
            V.max = x
        if empty(V.cluster[high(x)]):
            insert(V.summary, high(x))
            empty_insert(V, x)
        else:
            insert(V.cluster[high(x)], low(x))
```

## Złożoność

Ponieważ dla każdej instrukcji zachodzi tylko jedno wywołanie rekurencyjnie albo dla jej tablicy podsumowującej albo dla pojedyńczej podtablicy, które mają $\sqrt{n}$ elementów, a pozostałe instrukcje wykonują się w czasie stałym, to złożoność wszystkich operacji można opisać następująco:

$T(n) = T(\sqrt{n}) + O(1)$

Załóżmy, że $n = 2^{2^k}$

$T(n) = T(\sqrt{2^{2^k}}) + O(1) = T(2^{2^{k - 1}}) + O(1) = T(2^{2^0}) + k * O(1) = T(2) + O(k) = O(k)$

Wiemy, że $n = 2^{2^k}$, więc $log_2{n} = 2^k$, więc $log_2{log_2{n}} = k$, więc $T(n) = O(log_2{log_2{n}})$
