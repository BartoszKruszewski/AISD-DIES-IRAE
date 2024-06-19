# B-drzewa

## Opis 

B-drzewa to drzewa przeszukiwań mające określoną arność. Drzewa mają od $B/2$ do $B$ kluczy w wierzchołku (wyjątkiem jest korzeń, który może mieć mniej). Wierzchołek może mieć do $B + 1$ dzieci. Klucze są posortowane i tworzą przedziały dla każdego dziecka. Dzięku temu podczas przeszukiwania wiemy, do którego dziecka należy przejść. B-drzewa dodatkowo wymuszają położenie wszystkich liści na tym samym poziomie. 

## Insert

Dodajemy wierzchołek do liścia. Jeżeli liść zostaje przepełniony to wtedy rozdzielamy klucze. Środkowy klucz trafia do ojca liścia. Kluze większe do niego idą do nowo utworzonego prawego brata liścia, a mniejsze zostają w liściu. Jeżeli ojciec liścia zostanie przepełniony podczas insertu, to powtarzamy proces rekurencyjnie dla ojca.

## Delete

Usuwanie, wartości w liściach, może powodować obniżenie ilości ich kluczy poniżej minimum. Wtedy zabieramy klucze od brata, jednocześnie zamieniając je z separatorem u ojca, żeby zachować kolejność drzewa. Jeżeli u brata również spowodowałoby to zejście poniżej minimum to łączymy oba liście w jeden, razem z ich separatorem od ojca.

Jeżeli usuwawamy wartość będącą separatorem, to musimy najpierw znaleźć nowy separator. Zabieramy go z minimum lewego lub maksimum prawego syna. Jeżeli spowoduje to problemy z minimalną liczbą kluczy u któregoś z synów to problem rozwiązujemy jak w przypadku usuwania klucza z liścia.

## Efektywność

Takie rozwiązanie sprawdza się bardzo dobrze dla dużych baz danych, gdzie czas pobierania bloku danych do pamięci znacznie przewyższa czas operacji na pamięci wewnętrznej. Wtedy przeszukanie wierzchołka, nawet z duża arnością zabiera mniej czasu niż pobranie wartości kolejnego wierzchołka.

## Złożoność

Wysokość drzewa nie przekracza $log_t \frac{n + 1}{2}$, gdzie $n$ to ilość kluczy, a $t$ to maksymalna arność wierzchołka.

Złożoność powyższcyh operacji na B-drzewie wynosi $O(h)$ operacji dyskowych (tych wolnych), oraz $O(t * h)$ pozostałych operacji, $t$ to maksymalna arność wierzchołka, a $h$ to wysokość drzewa. 



