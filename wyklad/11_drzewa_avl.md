# Drzewa AVL

## Opis problemu
***Drzewo AVL*** zdefiniowane jest jako samobalansujące się drzewo wyszukiwań binarnych **(BST)**, w którym **współczynnik równowagi** każdego węzła jest nie większy niz jeden.

***Współczynnikiem równowagi*** węzła nazywamy różnicę między **wysokością** lewego i prawego poddrzewa tego węzła.

![Drzewo AVL](/Materiały/Drzewo%20AVL.png)
## Obracanie poddrzew w drzewie AVL
Aby zachować **równowagę** oraz **strukturę drzewa wyszukiwań binarnych**, drzewo AVL będzie się obracać w jeden z 4 sposobów:

### ***(Left Rotation)***
Jeżeli po dodaniu węzła do prawego syna (C) prawego poddrzewa (B) drzewo jest niezbalansowane, wykonujemy rotację w **lewo**

![Left Rotation](/src/Drzewa%20AVL%20Left%20Rotation.png)

### ***(Right Rotation)***
Jeżeli po dodaniu węzła do lewego syna (C) lewego poddrzewa (B) drzewo jest niezbalansowane, wykonujemy rotację w **prawo**

![Right Rotation](/src/Drzewa%20AVL%20Right%20Rotation.png) 

### ***(Left-Right Rotation)***
Jeżeli po dodaniu węzła do prawego syna (B) lewego poddrzewa (A) drzewo jest niezbalansowane, wykonujemy wpierw obrót w **lewo**, a potem w **prawo**

![Left right Rotation](/src/Drzewa%20AVL%20Left-Right%20Rotation.png) 

### ***(Right-Left Rotation)***
Jeżeli po dodaniu węzła do lewego syna (B) prawego poddrzewa (C) drzewo jest niezbalansowane, wykonujemy wpierw obrót w **prawo**, a potem w **lewo**

![Right Left Rotation](/src/drzewa%20AVL%20Right-Left%20Rotation.png)

## Zalety drzew AVL
1. **Wysokość drzewa** AVL jest zawsze **O(logn)**, gdzie n to liczba węzłów w drzewie. Dzięki temu operacje wyszukiwania, wstawiania i usuwania mają złożoność czasową **O(logn)**.
1. Dzięki automatycznemu wyważaniu po każdej operacji **wstawiania** lub **usuwania**, drzewa AVL unikają najgorszego przypadku związanego z **drzewami binarnymi**, które mogą stać się **silnie niezrównoważone**.
1. Rotacje wykorzystywane do balansowania drzewa są szybkie i efektywne.
1. Drzewa AVL zawsze są zbalansowane, co oznacza, że zawwsze **współczynnik równowagi** jest nie większy niż 1. To ograniczenie gwarantuje, że operacje będą miały optymalną złożoność czasową.