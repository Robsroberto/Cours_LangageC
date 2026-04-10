# Les Piles (Stack) en C

## 1. Principe LIFO

Une **pile** suit le principe **LIFO** : *Last In, First Out* — Dernier entré, premier sorti.

Comme une pile d'assiettes : on empile par le haut, on récupère par le haut.

```
Empiler 5  → [5]
Empiler 10 → [10][5]
Empiler 3  → [3][10][5]
Dépiler    →  3   | reste [10][5]
```

**Utilisations** : appels de fonctions (call stack), annulation (Ctrl+Z), évaluation d'expressions, parcours DFS de graphes.

---

## 2. Structure

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Noeud {
    int valeur;
    struct Noeud *suivant;
} Noeud;

typedef struct {
    Noeud *sommet;
    int    taille;
} Pile;
```

---

## 3. Initialiser

```c
void init(Pile *p) {
    p->sommet = NULL;
    p->taille = 0;
}

int est_vide(Pile *p) {
    return p->sommet == NULL;
}
```

---

## 4. Empiler (push)

```c
void empiler(Pile *p, int val) {
    Noeud *n   = (Noeud*) malloc(sizeof(Noeud));
    n->valeur  = val;
    n->suivant = p->sommet;
    p->sommet  = n;
    p->taille++;
}
```

---

## 5. Dépiler (pop)

```c
int depiler(Pile *p) {
    if (est_vide(p)) {
        printf("Pile vide !\n");
        return -1;
    }
    Noeud *tmp = p->sommet;
    int val    = tmp->valeur;
    p->sommet  = tmp->suivant;
    free(tmp);
    p->taille--;
    return val;
}
```

---

## 6. Consulter le sommet (peek)

```c
int peek(Pile *p) {
    if (est_vide(p)) return -1;
    return p->sommet->valeur;
}
```

---

## 7. Affichage

```c
void afficher(Pile *p) {
    Noeud *c = p->sommet;
    printf("Sommet → ");
    while (c != NULL) {
        printf("[%d] ", c->valeur);
        c = c->suivant;
    }
    printf("\n");
}
```

---

## 8. Cas pratique : vérifier les parenthèses

```c
#include <string.h>

int parentheses_ok(char *expr) {
    Pile p;
    init(&p);

    for (int i = 0; expr[i] != '\0'; i++) {
        if (expr[i] == '(') {
            empiler(&p, '(');
        } else if (expr[i] == ')') {
            if (est_vide(&p)) return 0;  // Fermante sans ouvrante
            depiler(&p);
        }
    }
    return est_vide(&p);  // Toutes les ouvrantes ont été fermées
}

int main() {
    printf("%s\n", parentheses_ok("((a+b)*(c-d))") ? "OK" : "Erreur");  // OK
    printf("%s\n", parentheses_ok("((a+b)")         ? "OK" : "Erreur");  // Erreur
    printf("%s\n", parentheses_ok("a+b)")           ? "OK" : "Erreur");  // Erreur
    return 0;
}
```

---

## 9. Programme principal

```c
int main() {
    Pile p;
    init(&p);

    empiler(&p, 5);
    empiler(&p, 10);
    empiler(&p, 3);

    afficher(&p);                          // Sommet → [3] [10] [5]
    printf("Dépilé  : %d\n", depiler(&p)); // 3
    printf("Sommet  : %d\n", peek(&p));    // 10
    printf("Taille  : %d\n", p.taille);    // 2

    afficher(&p);

    return 0;
}
```
