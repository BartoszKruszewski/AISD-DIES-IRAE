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