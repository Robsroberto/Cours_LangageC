# Les Files (Queue) en C

## 1. Principe FIFO

Une **file** suit le principe **FIFO** : *First In, First Out* — Premier entré, premier sorti.

Comme une file d'attente : on entre par derrière, on sort par devant.

```
Enfiler 5  → [5]
Enfiler 10 → [5][10]
Enfiler 3  → [5][10][3]
Défiler    →  5  | reste [10][3]
```

**Utilisations** : gestion d'impression, file de tâches, parcours BFS de graphes, buffering réseau.

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
    Noeud *tete;   // On retire ici (FIFO)
    Noeud *queue;  // On ajoute ici
    int    taille;
} File;
```

---

## 3. Initialiser

```c
void init(File *f) {
    f->tete   = NULL;
    f->queue  = NULL;
    f->taille = 0;
}

int est_vide(File *f) {
    return f->tete == NULL;
}
```

---

## 4. Enfiler (enqueue)

```c
void enfiler(File *f, int val) {
    Noeud *n   = (Noeud*) malloc(sizeof(Noeud));
    n->valeur  = val;
    n->suivant = NULL;

    if (f->queue == NULL) {
        f->tete = f->queue = n;
    } else {
        f->queue->suivant = n;
        f->queue          = n;
    }
    f->taille++;
}
```

---

## 5. Défiler (dequeue)

```c
int defiler(File *f) {
    if (est_vide(f)) {
        printf("File vide !\n");
        return -1;
    }
    Noeud *tmp = f->tete;
    int val    = tmp->valeur;
    f->tete    = tmp->suivant;
    if (f->tete == NULL) f->queue = NULL;
    free(tmp);
    f->taille--;
    return val;
}
```

---

## 6. Consulter la tête

```c
int tete(File *f) {
    if (est_vide(f)) return -1;
    return f->tete->valeur;
}
```

---

## 7. Affichage

```c
void afficher(File *f) {
    Noeud *c = f->tete;
    printf("Tête → ");
    while (c != NULL) {
        printf("[%d] ", c->valeur);
        c = c->suivant;
    }
    printf("← Queue\n");
}
```

---

## 8. Simulation file de caisse

```c
int main() {
    File caisse;
    init(&caisse);

    // Clients qui arrivent
    enfiler(&caisse, 101);
    enfiler(&caisse, 102);
    enfiler(&caisse, 103);
    enfiler(&caisse, 104);

    printf("File initiale : ");
    afficher(&caisse);

    // Traitement dans l'ordre d'arrivée
    while (!est_vide(&caisse)) {
        printf("Traitement client n°%d\n", defiler(&caisse));
    }

    return 0;
}
```

---

## Pile vs File - Résumé

| | Pile (Stack) | File (Queue) |
|--|--|--|
| Principe | LIFO | FIFO |
| Entrée | sommet | queue |
| Sortie | sommet | tête |
| Opérations | push / pop | enfiler / défiler |
| Usage type | Fonctions, annulation | Impression, BFS |
