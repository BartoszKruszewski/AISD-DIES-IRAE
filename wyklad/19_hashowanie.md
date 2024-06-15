# Hashowanie

Hashowanie pozwala na realizowanie operacji słownikowych w czasie stałym dla małego uniwersum kluczy.

## Funkcje hashujące

Funkcja hashująca pozwala na mapowanie kluczy na komórki tablicy.

$h: U \rarr \{0, \dots, m - 1\}$

Dobra funkcja hashująca powinna spełniać warunek:

$\forall_{j = 0, \dots, m - 1} \sum_{k:h(k) = j} P(k) = \frac{1}{m}$

Przykładowe funkcje hashujące:

$h(k) = k \mod m$

Dla tej funkcji wybór $m$ jest dość istotny. Dla $m$ będących potęgami liczby $2$. Dla $m = 2^p$ $h(k)$ będzie odpowiadało liczbie zapisanej na $p$ najmniej znaczących bitach liczby $k$. Najmniej znaczące bity liczby będą często się powtarzać oraz będą się rozkładać nierównomiernie.

$h(k) = \lfloor m(kA - \lfloor kA \rfloor ) \rfloor$

W tym przypadku $m$ będące potęgą $2$ jest porządane, przez szybkość mnożenia. W tym przypadku nie wpływa to na równomierność rozkładu. Wybór stałej $A$ jest bardziej znaczący w praktyce wybiera się liczbę $(\sqrt{5} - 1)/2 \approx 0.6180339887$. Jest to "małe" $\phi$, czyli mniejszy pierwiastek ciągu Fibonacciego.

Jeżeli dla kluczy $x$ oraz $y$ wystąpi $h(x) = h(y)$ mówimy o **kolizji**. Jest wiele sposób rozwiązywania kolizji.

Współczynnik wypełnienia talbicy oznaczamy jako $\alpha$. Z reguły $\alpha = \frac{n}{m}$.

## Słownik "z nawlekaniem"

W takim słowniku, w tablicy hashowanej pamiętamy wskaźniki na pierwszy element listy. W razie wystąpienia kolizji dodajemy kolejny element do listy.

Oczekiwany koszt odwołania do takiego słownika to $\Theta(1 + \alpha)$.

## Hashowanie otwarte

W tym przypadku nie pamiętamy wskaźników na listy, a wartości zapamiętujemy bezpośrednio w tablicy. Wielkość talicy może wymagać zwiększenia w trakcie działania algorytmu. Wtedy redefiniujemy funkcje hashującą dla zwiękoszonego $m$ oraz przepisujemy elementy tablicy.

W przypadku wystąpienia kolizji zapisujemy wartość w innej komórce, sposób wyznaczania następnej komórki po napotkaniu kolizji, deifniuje funkcja hashująca.

Oznaczamy jako $h'(k)$ podstawową funkcję hashującą oraz $i$ jako liczbę komórek, w których przy danej próbie napotkaliśmy kolizję.

Metoda liniowa:

$h(k, i) = (h'(k) + i) \mod m$

Metoda kwadratowa:

$h(k, i) = (h'(k) + c_1 * i + c_2 * i^2) \mod m$

gdzie $c_1$ oraz $c_2$ to stałe.

Podwójne hashowanie:

$h(k, i) = (h_1(k) + i * h_2(k)) \mod m$

Najlepsze efekty daje podwójne hashowanie. W pozostałych metodach powstają "zlepki", czyli zwarte obszary tablicy obniżające równomierność rozłożenia kluczy.

Oczekiwana liczba prób w poszukiwaniu zakończonym niepowodzeniem jest $\le \frac{1}{1 - \alpha}$.

Oczekiwana liczba prób w poszukiwaniu zakończonym sukcesem jest  $\le \frac{1}{\alpha} ln \frac{1}{1 - \alpha}$.

## Hashowanie uniwersalne

Dla każdej funkcji hashującej istnieją dane, dla których czas działania słownika będzie wolny. Może istnieć sytuacja, której wszystkie dane będą miały identyczny hash. Żeby temu zapobiec będziemy losować funkcję hashującą z rodziny funkcji.

Rodzina funkcji hasujących $H$ jest uniwersalna jeżeli:

$\forall_{x, y \in U ; x \ne y} |\{h \in H: h(x) = h(y) \}| \le \frac{|H|}{m}$

Dla takiej rodziny średnia liczba kolizji jest mniejsza niż 1.

Przykład 1:

$h_a(x) = \sum_{i = 0}^{r} a_i x_i \mod m$

gdzie $m$ jest liczbą pierwszą, $|U| < m^{r + 1}$, $a$ jest liczba z przediału $[0, m^{r + 1}]$. Natomiast $<a_1, \dots, a_n>$ oraz $<x_1, \dots, x_n>$ to reprezentacje liczb $a$ oraz $x$ w systemie m-arnym.

Przykład 2:

$h_{ab}(x) = ((ax + b) \mod p ) \mod m$

gdzie $p$ to liczba pierwsza większa niż uniwersum kluczy, $m$ to wielkość tablicy, $a \in Z_p^*$, $b \in Z_p$

## Słownik statyczny

Słownik statyczny zakłada, że nie będą wykonywane operacje *insert* oraz *delete*, natomiast chcemy, żeby koszt operacji *find* był deterministycznie stały, oraz żeby oczekiwany czas konstrukcji struktury był wielomianowy.