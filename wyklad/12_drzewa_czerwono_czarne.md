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

## Operacja insert

Podczas operacji insert wstawiamy wierzchołek jak do standardowego BST w czasie $O(log(n))$, a następnie przywracamy balans. Wierzchołek w momencie wstawienia kolorujemy na czerwono. Mogą wystąpić cztery sytuacje:

- wierzołek jest korzeniem
- wujek wierzchołka jest czerwony
- wujek wierzchołka jest czarny (wierzchołek tworzy linię ze swoim dziadkiem)
- wujek wierzchołka jest czarny (wierzchołek tworzy trójkąt swoim dziadkiem)

Wykonujemy operacje zależne od którejść z tych sytuacji.
Następnie wykonujemy to samo dla wierzchołka, na ścieżce do korzenia, który narusza własności drzewa.

Maksymalnie wykonamy operacje naprawiania porządku dla wierzchołków na ścieżce. Wykonujemy je w czasie stałym, więc złożoność całego inserta to $O(log(n))$.

### Wierzchołek jest korzeniem

Wtedy wystarczy pokolorować wierzchołek na czarno.

### Wujek wierzchołka jest czerwony

W tej sytuacji kolorujemy ojca oraz wujka na czarno, a dziadka na czerwono.

### Wujek wierzchołka jest czarny (wierzchołek tworzy linię ze swoim dziadkiem)

Robimy rotacje w prawo dla ojca wierzchołka

### Wujek wierzchołka jest czarny (wierzchołek tworzy trójkąt swoim dziadkiem)

Robimy rotacje dziadka wierzchołka w lewo.
Następnie kolorujemy byłego dziadka na czerwono, a ojca na czarno.

