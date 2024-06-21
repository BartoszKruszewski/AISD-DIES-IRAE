# Drzewa czerwono-czarne

## Opis problemu

**_Drzewo Czerwono - Czarne_** to rodzaj **zrównoważonego drzewa wyszukiwań binarnych**, które wykorzystuje zestaw reguł do utrzymania równowagi, zapewniając **logarytmiczną** złożoność czasową dla operacji takich jak **insert**, **delete** i **find**, niezależnie od początkowego kształtu drzewa.

![Drzewo czerwono-czarne](/src/Drzewo%20czerwono-czarne.png)

**_Drzewa Czerwono - Czarne_** balansują się wykorzystując prosty **schemat kodowania kolorami** w celu dostosowania drzewa po każdej modyfikacji.

Intuicyjnie, można sobie wyobrazić drzewo czerwono-czarne jako drzewo, które jest **nieco bardziej elastyczne** w porównaniu do drzewa AVL, pozwalając na nieco większe odchylenia od idealnej równowagi, ale nadal **ograniczające te odchylenia** w sposób kontrolowany.

## Właściwości Drzew Czerwono - Czarncyh

1. **Kolor węzła** : Każdy węzeł jest czerwony lub czarny .
1. **Właściwość korzenia** : Korzeń drzewa jest zawsze czarny .
1. **Właściwość koloru czerwonego** : Węzły czerwone nie mogą mieć czerwonych dzieci (nie ma dwóch kolejnych czerwonych węzłów na żadnej ścieżce).
1. **Właściwość koloru czarnego** : każda ścieżka od węzła do potomnych węzłów zerowych (liście) ma tę samą liczbę czarnych węzłów.
1. **Właściwość liścia** : Wszystkie liście (węzły NIL) są czarne.

Te właściwości zapewniają, że **najdłuższa ścieżka** od korzenia do dowolnego liścia nie jest dłuższa niż dwukrotność najkrótszej ścieżki, zachowując równowagę drzewa i wydajną pracę.

## Operacja insert

Podczas operacji insert wstawiamy wierzchołek jak do standardowego BST w czasie $O(log(n))$, a następnie przywracamy balans. Wierzchołek w momencie wstawienia kolorujemy na czerwono. Mogą wystąpić trzy sytuacje:

1. Wujek wierzchołka jest czerwony

Dziadka kolorujemy na czerowono (bo był czarny), a wujka i ojca na czarno. Następną rotację wywołyjemy dla dziadka wierzchołka.

```
z.p.p.color = RED
z.p.p.r.color = BLACK
z.p = color = BLACK
z = z.p.p
```

2. Wujek wierzchołka jest czarny (wierzchołek jest prawym synem swojego ojca)

Robimy rotacje ojca w lewo.
Otrzymujemy wtedy przypadek 3 dla byłego ojca wierzchołka.

```
z = z.p
rotate-left(z)
```

3. Wujek wierzchołka jest czarny (wierzchołek jest lewym synem swojego ojca)

Dziadka malujemy na czerwono, ojca na czarno i robimy rotacje dziadka w prawo.

```
z.p.p.color = RED
z.p = BLACK
rotate-right(z.p.p)
```

Wykonujemy operacje aż dojdziemy do korzenia.

## Złożoność

Maksymalnie wykonamy operacje naprawiania porządku dla wierzchołków na ścieżce. Wykonujemy je w czasie stałym, więc złożoność całego inserta to $O(log(n))$.
