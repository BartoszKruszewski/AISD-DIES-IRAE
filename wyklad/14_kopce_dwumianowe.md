# Kopce Dwumianowe

# Idea

Główną ideą stojąca za kopcami dwumianowymi jest implementacja złączalnych kolejek priorytetowych. Dla standardowego kopca binarnego operacja ta może być wykonana w czasie $O(n + m)$. Dla kopców dwumianowych będziemy chcieli uzyskać czas $O(log(n) + logn(m))$.

## Drzewa dwumianowe

Struktura wykorzystywaną w kopcach dwumianowych są drzewa dwumianowe.

Definicja drzew dwumianowych:

- drzewo stopnia $0$ to pojedyńczy wierzchołek
- drzewo stopnia $k$ to dwa połączone drzewa $k - 1$ stopnia

Łączenie drzew to podczepienie korzenia jednego drzewa pod korzeń drugiego drzewa. Tworząc drzewa $minimum$ chcemy, żeby wierzchołek o mniejszym kluczu był rodzicem wierzchołka o większym kluczu.

Własnośći drzew dwumianowym:

- korzeń o stopniu $k$ ma dokładnie $k$ dzieci
- drzewo o stopniu $k$ ma dokładnie $2^k$ wierzchołków oraz wysokośc $(k + 1)$
- dzieci korzenia o stopniu $k$ są korzeniami drzew dwumianowych o stopniach $(k - 1), (k - 2), \dots, 0$

## Kopce dwumianowe

Kopiec dwumianowy to las drzew dwumianowych.

Definicja kopca dwumianowego:

- las drzew dwumianowych (minimum lub maksimum)
- może być co najwyżej $1$ drzewo dwumianowe stopnia $k$ (to jest dla zabalansowania, dwa drzewa dwumianowe stopnia $k$ zawsze można połączyć w jedno stopnia $k + 1$)

Wskaźniki na poszczególne drzewa można przechowywać w tablicy.

## Operajce

### Union

Union polega na zrobieniu "dodawania binarnego" na tablicach wskaźników. Oznaczamy jako $0$ lub $1$ na k-tej pozycji tablicy obecność lub brak drzewa o stopniu $k$. Jeżeli w obu tabliach występuje drzewo o tym samym stopniu to łączymy je otrzymując drzewo o stopniu jeden większym. Łączenie można potraktować jako propagację w dodawaniu.

W kopcu dwumianowym jest maksymalnie $log(n)$ drzew dwumianowych, ponieważ kopiec k-tego stopnia ma $2^k$ wierzchołków, więc maksymalny stopień wierzchołka to $log(n)$ ($2^{log(n)} = n$). Co za tym idzie pesymistycznie zostanie wykonane $O(log(n) + log(m))$ łączeń, każde w czasie $O(1)$. Łącznie daje to złożoność $O(log(n) + log(m))$.

### Insert

Insert to po prostu union obecnego kopca dwumianowego z kopcem zawierającym jeden wierzchołek, który chcemy dodać. Złożoność to $O(log(n) + log(1)) = O(log(n))$

### Find-min

W podstawowej implementacji, należy przeszukać korzenie wszystkich drzew, ponieważ struktura nic nie zapewnia o powiązaniach pomiędzy nimi. Więc czas to $O(log(n))$. Dodając dodatkowy wskaźnik na minimum, aktualizowany przy insercie, co jest standardową modyfikacją dla struktury, możemy uzyskać czas $O(1)$.

### Delete-min

Wykonujemy Findmin. Następnie usuwamy element. Dzieci usunięte wierzchołka to drzewa dwumianowe. Tworzymy kopiec dwumianowy zawierający te drzewa i wykonujemy Union. Złożoność to $O(log(n) + log(n)) = O(log(n))$

## Implementacja leniwa

W tej implementacji po wykonaniu Insert oraz Union tracimy strukturę kopca dwumianowego, ale operacje są wykonywane bez "dodawania binarnego" drzew. Przez to mają koszt $O(1)$. Struktutra kopca dwumianowego zostaje dopiero przywrócona przy wykonaniu operacji $Delete-min$. Może ona mieć opesymistyczny koszt $O(n)$, natomiast przy analizie zamortyzowanej koszt to $O(log(n))$.
