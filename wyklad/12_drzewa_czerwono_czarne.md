# Drzewa czerwono-czarne

## Opis problemu
***Drzewo Czerwono - Czarne*** to rodzaj **zrównoważonego drzewa wyszukiwań binarnych**, które wykorzystuje zestaw reguł do utrzymania równowagi, zapewniając **logarytmiczną** złożoność czasową dla operacji takich jak **insert**, **delete** i **find**, niezależnie od początkowego kształtu drzewa.

![Drzewo czerwono-czarne](/src/Drzewo%20czerwono-czarne.png)

***Drzewa Czerwono - Czarne*** balansują się wykorzystując prosty **schemat kodowania kolorami** w celu dostosowania drzewa po każdej modyfikacji.

Intuicyjnie, można sobie wyobrazić drzewo czerwono-czarne jako drzewo, które jest **nieco bardziej elastyczne** w porównaniu do drzewa AVL, pozwalając na nieco większe odchylenia od idealnej równowagi, ale nadal **ograniczające te odchylenia** w sposób kontrolowany.

## Właściwości Drzew Czerwono - Czarncyh
1. **Kolor węzła** : Każdy węzeł jest czerwony lub czarny .
1. **Właściwość korzenia** : Korzeń drzewa jest zawsze czarny .
1. **Właściwość koloru czerwonego** : Węzły czerwone nie mogą mieć czerwonych dzieci (nie ma dwóch kolejnych czerwonych węzłów na żadnej ścieżce).
1. **Właściwość koloru czarnego** : każda ścieżka od węzła do potomnych węzłów zerowych (liście) ma tę samą liczbę czarnych węzłów.
1. **Właściwość liścia** : Wszystkie liście (węzły NIL) są czarne.

Te właściwości zapewniają, że **najdłuższa ścieżka** od korzenia do dowolnego liścia nie jest dłuższa niż dwukrotność najkrótszej ścieżki, zachowując równowagę drzewa i wydajną pracę.