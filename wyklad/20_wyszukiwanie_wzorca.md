# Wyszukiwanie wzorca

## Algorytm Karpa-Rabina

## Automaty skończone

## Algorytm KMP (Knuth-Morris-Pratt)

Algotym KMP przyśpiesza naiwny algorytm wyszukiwania wzorca z $O(n * m)$ do $O(n + m)$ za pomocą tablicy prefikso-sufiksów. Oznaczamy taka tablice jako $\pi$. $\pi(k) = x$ oznacza, że w prefiksie wzorca o długości $k$, najdłuższy prefiks tego prefksu, który jest jednocześnie jego sufiksem ma długość $x$. Intuicyjnie $\pi$ mówi nam do którego miejsca we wzorcu należy się cofnąć, po chybieniu. Tablice taką można utworzyć następująco:

1. Tworzymy indeksy $i$ oraz $j$
2. Jeżeli indeksy wskazują na takie same litery we wzorcu to przesuwamy je w prawo i zwiększamy wartość w pi
3. Jeżeli nie to znaczy, że litery są różne, czyli napotkaliśmy pierwszą literę, która nie pasuje. Przestawiamy j na pi ostatniej litery, która pasowała.

```
def make_pi(P):
    n = len(P)
    pi = [0] * n

	i = 1
    j = 0

	while i < n:
		if P[i] == P[j]:
			j += 1
			pi[i] = j
			i += 1
		else:
			if j != 0:
				j = pi[j - 1]
			else:
				lps[i] = 0
				i += 1

    return pi
```

Przechodzimy po wszystkich znakach tekstu. $i$ oznacza indeks znaku tekstu, a $j$ długość dopasownego prefiksu. W momencie w którym mamy pokrycie znaku wzorca ze znakiem tekstu, zwiększamy dopasowany prefiks. Jeżeli nie to cofamy go zgodnie z pi.

```
def kmp(P, T):
    n = len(P)
    m = len(T)

	pi = make_pi

	i = 0
    j = 0
	while (n - i) >= (m - j):
        if j == m:
			return i - j

		if P[j] == T[i]:
			i += 1
			j += 1
        else:
			if j != 0:
				j = pi[j - 1]
			else:
				i += 1

    return -1
```

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
