# Preliminaria

## Mnożenie "po rosyjsku"

Mając dane liczby x oraz y, jedną z nich dzielimy całkowicie przez 2 aż uzyskamy 1. Równolegle mnożymy drugą liczbę przez 2. Reszty z dzielenia pierwszej liczby zapisujmy obok wyników dzieleń i mnożeń. Na koniec dodajemy do siebie te wartości przemnożone przez 2 które mają obok siebie 1.

Przykład:

```
 134 95 1
 268 47 1
 536 23 1
1072 11 1
2144  5 1
4288  2 0
8576  1 1

134 + 268 + 536 + 1072 + 2144 + 8576 = 12 730 = 134 * 95
```

Algorytm:

```
def russian_mult(x, y):
    s = 0
    while y > 1:
        s += x * (y % 2)
        y //= 2
        x *= 2
    return s
```

## Kryterium jednorodne i logarytmiczne

Kryterium jednorodne przyjmuje koszt operacji maszyny RAM za jednostkowy.
Kryterium logarytmiczne przyjmuje koszt operacji jako suma długośći bitowej operandów.

Przykład:
Koszt operacji $x = 4 + 8$ to:
W kryterium jednorodnym: 1
W kryterium logarytmicznym: 3 + 4 = 7

Analiza mnożenia po rosyjku z użyciem kryterium logarytmicznego:

Oznaczmy jako a oraz b liczby bitów liczb x i y.
Koszt każdej iteracji pętli to:

- mnożenie i dzielenie przez 2, czyli przesunięcie bitowe o 1 (koszt 2 \* 1 = 2)
- policzenie modulo 2 to odczytanie ostatniego bitu liczby (koszt 1)
- mnożenie przez 1 lub 0 to przepisanie liczby lub nie, więć można to zastąpić skokiem warunkowym połączonym z odczytaniem ostatniego bitu liczby (koszt uwzględniony w poprzenium podpunkcie)
- dodanie liczby do sumy (koszt to aktualna długość bitowa sumy + aktualne a)

Aktualna suma przed dodaniem x, jest zawsze mniejsza od x, ponieważ x zwiększa się dwukrotnie w każdej iteracji. Więc możemy oszacować z góry aktualną długość bitową sumy przez długość bitową x, czyli a.
Pętla wykona się b razy, ponieważ dzielimy liczbę przez 2, aż osiągniemy 1.

Sumując koszt:

$\sum*{i = 1}^{b} 3 + 2 * (a + i) = 3b + 2a + 2 * sum*{i = 1}^{b} i = 3 * b + 2 * a * b + \frac{b(b - 1)}{2}$

Standardowy algorytm mnożenia ma złożoność:
$a * b + 2 * a * b = 3 * a * b$

## Notacje rzędów funkcji $\Omega$, $\Theta$, $O$

## Algorytm wyliczania ciagu rekurencyjnego za pomocą potęgowania macierzy

Mając podaną zależność rekurencyjną:

$a_{n + m + 1} = \beta_1 * a_{n} + \beta_2 * a_{n + 1} + \dots + \beta_m * a_{n + m}$

Oraz wartości początkowe:

$a_1 = s_1, a_2 = s_2, \dots, a_m = s_m$

Możemy utworzyć funkcje kroku rekurencyjnego:

$f(x_1, x_2, \dots, x_m) = (x_2, x_3, \dots, x_m, \beta_1 * x_1 + \beta_2 * x_2 + \dots + \beta_m * x_m)$

Zauważmy, że poniższa funkcja może być przedstawiona jako przekształcenie liniowe.

Wtedy macierz takiego przekształcenia będzie równa:

$$
\left(\begin{array}{cc}
0 & 1 & 0 & \dots & 0\\
0 & 0 & 1 & \dots & 0\\
\dots & \dots & \dots & \dots & \dots\\
0 & 0 & 0 & \dots & 1 \\
\beta_1 & \beta_2 & \beta_3 & \dots & \beta_m\\
\end{array}\right)
$$

Zauważmy, że:

$$
\left(\begin{array}{cc}
0 & 1 & 0 & \dots & 0\\
0 & 0 & 1 & \dots & 0\\
\dots & \dots & \dots & \dots & \dots\\
0 & 0 & 0 & \dots & 1 \\
\beta_1 & \beta_2 & \beta_3 & \dots & \beta_m\\
\end{array}\right)
\left(\begin{array}{cc}
a_n \\
a_{n + 1} \\
\dots \\
a_{n + m - 1}  \\
a_{n + m} \\
\end{array}\right)
=
\left(\begin{array}{cc}
a_{n + 1} \\
a_{n + 2} \\
\dots \\
a_{n + m}  \\
a_{n + m + 1} \\
\end{array}\right)
$$

Wtedy, żeby wyliczyć odpowiedni wyraz ciągu wystarczy podnieść macierz do odpowiedniej potęgi oraz przemnożyć ją przez wektor wartości początkowych. Na koniec trzeba jeszcze przemnożyć macierz przez wektor "wyciągający" konkretny element ciągu z wektora wynikowego.:

$$
a_{n + m} =
\left(\begin{array}{cc}
0 & 1 & 0 & \dots & 0\\
0 & 0 & 1 & \dots & 0\\
\dots & \dots & \dots & \dots & \dots\\
0 & 0 & 0 & \dots & 1 \\
\beta_1 & \beta_2 & \beta_3 & \dots & \beta_m\\
\end{array}\right)^n
\left(\begin{array}{cc}
s_1 \\
s_2 \\
\dots \\
s_{m - 1}  \\
s_{m} \\
\end{array}\right)
\left(\begin{array}{cc}
0 & 0 & \dots & 1
\end{array}\right)
$$
