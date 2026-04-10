# Les Listes Doublement Chaînées en C

## 1. Principe

Chaque nœud possède **deux pointeurs** : vers le suivant ET vers le précédent. On peut parcourir la liste dans les deux sens.

```
NULL ← [5 | •|•] ↔ [10 | •|•] ↔ [8 | •|NULL]
```

---

## 2. Structure du nœud

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Noeud {
    int valeur;
    struct Noeud *suivant;
    struct Noeud *precedent;
} Noeud;
```

---

## 3. Créer un nœud

```c
Noeud* creer_noeud(int val) {
    Noeud *n     = (Noeud*) malloc(sizeof(Noeud));
    n->valeur    = val;
    n->suivant   = NULL;
    n->precedent = NULL;
    return n;
}
```

---

## 4. Insertion

### En tête

```c
void inserer_tete(Noeud **tete, int val) {
    Noeud *n   = creer_noeud(val);
    n->suivant = *tete;
    if (*tete != NULL) (*tete)->precedent = n;
    *tete = n;
}
```

### En queue

```c
void inserer_queue(Noeud **tete, int val) {
    Noeud *n = creer_noeud(val);
    if (*tete == NULL) { *tete = n; return; }

    Noeud *c = *tete;
    while (c->suivant != NULL) c = c->suivant;
    c->suivant   = n;
    n->precedent = c;
}
```

---

## 5. Affichage dans les deux sens

```c
void afficher_avant(Noeud *tete) {
    printf("→ ");
    while (tete != NULL) {
        printf("%d ", tete->valeur);
        tete = tete->suivant;
    }
    printf("\n");
}

void afficher_arriere(Noeud *tete) {
    if (tete == NULL) return;
    while (tete->suivant != NULL) tete = tete->suivant;

    printf("← ");
    while (tete != NULL) {
        printf("%d ", tete->valeur);
        tete = tete->precedent;
    }
    printf("\n");
}
```

---

## 6. Suppression

```c
void supprimer(Noeud **tete, int val) {
    Noeud *c = *tete;
    while (c != NULL) {
        if (c->valeur == val) {
            if (c->precedent) c->precedent->suivant = c->suivant;
            else              *tete = c->suivant;
            if (c->suivant)   c->suivant->precedent = c->precedent;
            free(c);
            return;
        }
        c = c->suivant;
    }
}
```

---

## 7. Programme complet

```c
int main() {
    Noeud *liste = NULL;

    inserer_queue(&liste, 10);
    inserer_queue(&liste, 20);
    inserer_queue(&liste, 30);
    inserer_tete(&liste, 5);

    afficher_avant(liste);    // → 5 10 20 30
    afficher_arriere(liste);  // ← 30 20 10 5

    supprimer(&liste, 20);
    afficher_avant(liste);    // → 5 10 30

    return 0;
}
```

---

## Comparaison Liste simple vs Double

| Opération | Liste simple | Liste double |
|-----------|-------------|--------------|
| Parcours avant | ✅ | ✅ |
| Parcours arrière | ❌ | ✅ |
| Suppression efficace | Cherche le prec. | Pointeur direct |
| Mémoire par nœud | 1 pointeur | 2 pointeurs |
