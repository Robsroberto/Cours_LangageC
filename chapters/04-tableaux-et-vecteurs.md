# Tableaux et Tableaux Dynamiques en C

## 1. Qu'est-ce qu'un tableau ?

Un **tableau** est une collection de variables du même type, stockées de façon contiguë en mémoire. On accède à chaque élément via un **indice** (commençant à 0).

```c
int notes[5];       // tableau de 5 entiers
float prix[10];     // tableau de 10 flottants
char lettres[26];   // tableau de 26 caractères
```

---

## 2. Déclaration et initialisation

```c
// Déclaration + initialisation directe
int notes[5] = {14, 17, 12, 19, 10};

// Taille automatique déduite
int notes[] = {14, 17, 12, 19, 10};  // taille = 5

// Initialisation à zéro
int tab[100] = {0};

// Déclaration puis affectation élément par élément
int tab[3];
tab[0] = 10;
tab[1] = 20;
tab[2] = 30;
```

---

## 3. Parcourir un tableau

```c
#include <stdio.h>

int main() {
    int notes[] = {14, 17, 12, 19, 10};
    int n = 5;

    for (int i = 0; i < n; i++) {
        printf("notes[%d] = %d\n", i, notes[i]);
    }
    return 0;
}
```

---

## 4. Calculs courants sur un tableau

```c
#include <stdio.h>

int main() {
    int tab[] = {5, 12, 3, 18, 7, 14, 9};
    int n = 7;
    int somme = 0, min = tab[0], max = tab[0];

    for (int i = 0; i < n; i++) {
        somme += tab[i];
        if (tab[i] < min) min = tab[i];
        if (tab[i] > max) max = tab[i];
    }

    printf("Somme   : %d\n", somme);
    printf("Moyenne : %.2f\n", (float)somme / n);
    printf("Min     : %d\n", min);
    printf("Max     : %d\n", max);
    return 0;
}
```

---

## 5. Tableaux à deux dimensions (matrices)

```c
#include <stdio.h>

int main() {
    int mat[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%3d", mat[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

**Multiplication de matrices :**

```c
void multiplier(int A[3][3], int B[3][3], int C[3][3]) {
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++) {
            C[i][j] = 0;
            for (int k = 0; k < 3; k++)
                C[i][j] += A[i][k] * B[k][j];
        }
}
```

---

## 6. Tableaux dynamiques avec malloc

Un **tableau dynamique** est alloué à l'exécution quand on ne connaît pas la taille à l'avance.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;
    printf("Combien d'éléments ? ");
    scanf("%d", &n);

    // Allocation dynamique
    int *tab = (int*) malloc(n * sizeof(int));
    if (tab == NULL) {
        printf("Erreur d'allocation !\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        printf("tab[%d] = ", i);
        scanf("%d", &tab[i]);
    }

    for (int i = 0; i < n; i++)
        printf("%d ", tab[i]);
    printf("\n");

    // Libération mémoire - OBLIGATOIRE
    free(tab);
    return 0;
}
```

---

## 7. Redimensionner : realloc

```c
int *tab = (int*) malloc(3 * sizeof(int));
tab[0] = 10; tab[1] = 20; tab[2] = 30;

// Agrandir à 5 éléments
tab = (int*) realloc(tab, 5 * sizeof(int));
tab[3] = 40; tab[4] = 50;

free(tab);
```

---

## 8. Tri à bulles

```c
void tri_bulles(int tab[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (tab[j] > tab[j + 1]) {
                int temp    = tab[j];
                tab[j]      = tab[j + 1];
                tab[j + 1]  = temp;
            }
        }
    }
}
```

---

## Résumé

| Concept | Syntaxe |
|---------|---------|
| Déclaration statique | `int tab[N];` |
| Accès | `tab[i]` |
| Tableau 2D | `int mat[L][C];` |
| Dynamique | `malloc(n * sizeof(type))` |
| Redimensionner | `realloc(ptr, nouvelle_taille)` |
| Libérer | `free(ptr)` |

> Toujours libérer la mémoire allouée avec `malloc` ou `realloc` !
