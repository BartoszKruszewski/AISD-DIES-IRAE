# Preliminaria

## Mnożenie "po rosyjsku"
## Kryterium jednorodne i logarytmiczne
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