# Les Listes Circulaires en C

## 1. Principe

Dans une **liste circulaire**, le dernier nœud pointe vers le **premier** au lieu de NULL. La liste forme un cycle fermé.

```
→ [5] → [10] → [8] → [3] → (retour vers 5)
```

**Utilisations** : planification round-robin, buffers circulaires, jeux de plateau, lecteurs musicaux en boucle.

---

## 2. Structure

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Noeud {
    int valeur;
    struct Noeud *suivant;
} Noeud;
```

On garde un pointeur vers la **queue** (dernier nœud). La **tête** est alors `queue->suivant`.

---

## 3. Insertion en fin

```c
void inserer(Noeud **queue, int val) {
    Noeud *n = (Noeud*) malloc(sizeof(Noeud));
    n->valeur = val;

    if (*queue == NULL) {
        n->suivant = n;   // pointe vers lui-même
        *queue = n;
        return;
    }

    n->suivant        = (*queue)->suivant;  // n → ancienne tête
    (*queue)->suivant = n;                  // ancienne queue → n
    *queue            = n;                  // n devient la nouvelle queue
}
```

---

## 4. Affichage

```c
void afficher(Noeud *queue) {
    if (queue == NULL) { printf("Liste vide\n"); return; }

    Noeud *tete = queue->suivant;
    Noeud *c    = tete;
    do {
        printf("%d → ", c->valeur);
        c = c->suivant;
    } while (c != tete);
    printf("(cycle)\n");
}
```

---

## 5. Suppression de la tête

```c
void supprimer_tete(Noeud **queue) {
    if (*queue == NULL) return;

    Noeud *tete = (*queue)->suivant;

    if (tete == *queue) {
        // Un seul élément
        free(*queue);
        *queue = NULL;
        return;
    }

    (*queue)->suivant = tete->suivant;
    free(tete);
}
```

---

## 6. Compter les éléments

```c
int compter(Noeud *queue) {
    if (queue == NULL) return 0;
    int count   = 1;
    Noeud *tete = queue->suivant;
    Noeud *c    = tete->suivant;
    while (c != tete) {
        count++;
        c = c->suivant;
    }
    return count;
}
```

---

## 7. Programme complet

```c
int main() {
    Noeud *queue = NULL;

    inserer(&queue, 5);
    inserer(&queue, 10);
    inserer(&queue, 8);
    inserer(&queue, 3);

    afficher(queue);
    // 5 → 10 → 8 → 3 → (cycle)

    printf("Taille : %d\n", compter(queue));  // 4

    supprimer_tete(&queue);
    afficher(queue);
    // 10 → 8 → 3 → (cycle)

    return 0;
}
```

---

## 8. Simulation Round-Robin

```c
// Chaque processus obtient un tour à tour
void round_robin(Noeud *queue, int tours) {
    if (!queue) return;
    Noeud *c = queue->suivant;  // tête
    for (int i = 0; i < tours; i++) {
        printf("Processus %d s'exécute\n", c->valeur);
        c = c->suivant;
    }
}
```
