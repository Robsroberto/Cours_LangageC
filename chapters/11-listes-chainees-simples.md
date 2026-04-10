# Les Listes Chaînées Simples en C

## 1. Pourquoi les listes chaînées ?

Les tableaux ont une taille fixe connue à la compilation. Les **listes chaînées** permettent d'ajouter et supprimer des éléments dynamiquement, sans décaler la mémoire.

Chaque **nœud** contient une **valeur** et un **pointeur** vers le nœud suivant.

```
[10 | •]→[25 | •]→[8 | •]→[NULL]
```

---

## 2. Définir la structure d'un nœud

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Noeud {
    int valeur;
    struct Noeud *suivant;
} Noeud;
```

---

## 3. Créer un nœud

```c
Noeud* creer_noeud(int val) {
    Noeud *n = (Noeud*) malloc(sizeof(Noeud));
    if (!n) { printf("Erreur malloc\n"); exit(1); }
    n->valeur  = val;
    n->suivant = NULL;
    return n;
}
```

---

## 4. Insertion

### En tête de liste

```c
void inserer_tete(Noeud **tete, int val) {
    Noeud *n   = creer_noeud(val);
    n->suivant = *tete;
    *tete      = n;
}
```

### En queue de liste

```c
void inserer_queue(Noeud **tete, int val) {
    Noeud *n = creer_noeud(val);
    if (*tete == NULL) { *tete = n; return; }

    Noeud *c = *tete;
    while (c->suivant != NULL)
        c = c->suivant;
    c->suivant = n;
}
```

---

## 5. Affichage

```c
void afficher(Noeud *tete) {
    while (tete != NULL) {
        printf("%d → ", tete->valeur);
        tete = tete->suivant;
    }
    printf("NULL\n");
}
```

---

## 6. Recherche

```c
Noeud* chercher(Noeud *tete, int val) {
    while (tete != NULL) {
        if (tete->valeur == val) return tete;
        tete = tete->suivant;
    }
    return NULL;
}
```

---

## 7. Suppression

```c
void supprimer(Noeud **tete, int val) {
    if (*tete == NULL) return;

    // Nœud en tête
    if ((*tete)->valeur == val) {
        Noeud *tmp = *tete;
        *tete = (*tete)->suivant;
        free(tmp);
        return;
    }

    // Nœud ailleurs
    Noeud *c = *tete;
    while (c->suivant != NULL) {
        if (c->suivant->valeur == val) {
            Noeud *tmp   = c->suivant;
            c->suivant   = tmp->suivant;
            free(tmp);
            return;
        }
        c = c->suivant;
    }
}
```

---

## 8. Libérer toute la liste

```c
void liberer(Noeud **tete) {
    Noeud *c = *tete;
    while (c != NULL) {
        Noeud *tmp = c;
        c = c->suivant;
        free(tmp);
    }
    *tete = NULL;
}
```

---

## 9. Programme complet

```c
int main() {
    Noeud *liste = NULL;

    inserer_queue(&liste, 10);
    inserer_queue(&liste, 25);
    inserer_queue(&liste, 8);
    inserer_tete(&liste, 5);

    afficher(liste);
    // 5 → 10 → 25 → 8 → NULL

    supprimer(&liste, 25);
    afficher(liste);
    // 5 → 10 → 8 → NULL

    Noeud *trouve = chercher(liste, 10);
    printf("Trouvé : %s\n", trouve ? "oui" : "non");

    liberer(&liste);
    return 0;
}
```
