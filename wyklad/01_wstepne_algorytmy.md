# Algorytmy omówione na poprzednich przedmiotach

## Merge Sort

Dzielimy tablice na połowe i rekurencyjnie wywołujemy dla nich funkcje. Następnie obie połówki posortowane już połówki scalamy, przechodząc po tablicy i pokolei porównując elementy.

Złożoność merge sorta można oszacować poniższym równaniem rekurencyjnym:

$T(n) = 2T(n/2) + O(n) = O(nlog(n))$

## Algorytm Euklidesa

Wersja iteracyjna:

```
def NWD(a, b):
	while b != 0:
		pom = b
		b = a % b
		a = pom
    return a;
```

Wersja rekurencyjna:

```

def NWD(a, b):
    if b != 0:
        return NWD(b, a % b)
    else:
        return a

```

## DFS i BFS

```
def DFS_step(G, visited, u):
    visited[u] = True
    for v in G[u]:
        if not visited[v]:
            DFS_step(G, visited, v)

def DFS(G):
    # mozna zamiast robić tablice visited zapalać bity
    # dla poszególnych wierzchołków w strukturze
    visited = [False for u in G]
    for u in G:
        if not visited[u]:
            DFS_step(G, visited, u)
```

```
def BFS(G, start):
    visited = [False for u in G]
    Q = kolejka FIFO

    Q.push(start)

    while Q:
        u = Q.pop()
        visited[u] = True
        for v in G[u]:
            if not visited[v]:
                Q.push(v)
```

## Algorytm Forda-Fulkersona

## Maszyna RAM
