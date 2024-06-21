# Wyszukiwanie wzorca

## Algorytm Karpa-Rabina

## Automaty skończone

## Algorytm KMP (Knuth-Morris-Pratt)

## Algorytm Boyera-Moore'a

## Algorytm Shift-AND

Dla każdego znaku wzorca tworzymy maskę bitową długości wzorca, gdzie 1 na i-tej pozycji maski dla litery a oznacza, że dla litera a wystepuje na (p - i)-tej pozycji we wzorcu, gdzie p to długość wzorca (odwrócone oznaczanie na której pozycji jest litera).

Używamy $S$ jako wektora stanu. Ma on 1 na i-tej pozycji, jeżeli (m - i)-ty prefix wzorca odwzorowuje aktualny przejrzany suffix tekstu. Jeżeli 1 jest na pozycji 0, to znaczy, że znaleziono dopasowanie.

```
def shift_and(text, pattern):
    t = len(text)
    p = len(pattern)

    m = {l : [0] * p for l in pattern}
    for i in range(p):
        m[pattern[i]][p - i] = 1

    s = 0

    for i in range(t):
        s = ((S << 1) OR 1) AND M[text[i]]
        if s[najstarszy bit] == 1:
            return i - p
```

## Algorytm KMR (Karpa-Millera-Rosenberga)
