# Drzewce

## Idea

Dzewiec (drzewo + kopiec) to struktura danych łącząca w sobie właściwości obu tych struktur.

Dla podanych par (klucz, ppb odwołania), drzewiec zachowuje porządek BST dla kluczy oraz własność kopca (ojciec jest niemniejszy od syna) dla ppb.

Powoduje to optymalizację odwołań do kluczy, ponieważ wyszkując klucza, który ma duże ppb odwołania będziemy musieli przejść mniejszą drogą niż dla klucza o małym ppb.

## Insert

Insert odbywa się jak w standardowym BST, po czym następuje ciąg rotacji do momentu, aż własność kopca zostanie przywrócona.

## Delete

Usuwanie polega na przypisaniu usuwanemu wierzchołkowi wagi $- \infin$. Następnie przywracamy rotacjami własność kopca. W rezultacie wierzchołek zostanie liściem. Jeżeli wierzchołek jest liściem to możemy go usunąć nie naruszając żadnych własności.

Rotacje odybwają się w kierunku wierzchołka o niższym priorytecie.

Jeżeli wierzchołek ma w którymś momencie tylko jednego syna to zastępujemy go tym synem i kończymy operacje.
