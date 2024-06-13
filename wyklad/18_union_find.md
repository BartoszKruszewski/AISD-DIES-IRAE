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