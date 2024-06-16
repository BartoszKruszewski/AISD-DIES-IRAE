# Kopce Fibonacciego

## Idea

Chcemy zachowywać właściowośći kopców dwumianowych, ale dodatkowo chcemy móc wykonać operacje $decrease-key$ w czasie stałym.

## Operacja Cut

Operacja Cut odcinka wybrany wierzchołek i dołącza go operacją union do tablicy drzew. Dodatkowo oznacza ojca odciętego wierzchołka. W sytuacji, w której ojciec wierzchołka już wcześniej był oznaczony to funkcja jest wywoływana rekurencyjnie dla ojca.

Można wykazać, że zamortyzowany czas działania operacji cut jest $O(1)$.

## Operacja Decrease-key

```
def decrease_key(p, delta):
    p.value -= delta
    if p.value > p.father.value:
        cut(p)
```

## Operacja Delete-min

Identycznie jak w wersji Lazy kopców dwumianowych łączymy poodcinane przez inne operacje drzewa. Tym razem jednak nie łączymy ich w drzewa dwumianowe, tylko po prostu podłączamy pod siebie drzewa, których korzenie mają identyczną liczbę synów.

W momencie dołączania i-tego syna do korzenia, korzeń musiał mieć $(i - 1)$ synów. Co za tym idzie dołączany syn też miał $(i - 1)$, ponieważ łączymy korzenie o tej samej liczbie synów. Korzeń mógł stracić co najwyżej jednego syna, bo inaczej zostałby odcięty przez cut, więc ma co najmniej $(i - 2)$ synów. Więc liczba wierzchołków w całym poddrzewie to korzeń oraz podrzewa po minimum $(i - 2)$ synów dla i-tego syna, czyli $1 + \sum_{j = 0}^{i - 2} F_j$, gdzie $F_j$ to j-ta liczba Fibonacciego. Razem sumuje się to do $F_i$ liczby Fibonacciego. Stąd liczba wierzchołków w drzewie o korzeniu z $k$ synami jest nie mniejsza niż $\phi^k$. Więc w lesie jest nie więcej niż $log_{\phi}(n) = O(log(n))$ drzew. Więc czas działania Delete-min jest $log_{\phi}(n) = O(log(n))$.
