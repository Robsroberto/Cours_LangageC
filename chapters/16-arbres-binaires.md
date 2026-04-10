# Les Arbres Binaires en C

## 1. Qu'est-ce qu'un arbre ?

Un **arbre** est une structure hiérarchique de nœuds. Dans un **arbre binaire**, chaque nœud a au plus **deux enfants** : gauche et droite.

```
          10
         /  \
        5    15
       / \     \
      3   7    20
```

**Vocabulaire :**
- **Racine** : nœud sans parent (ici 10)
- **Feuille** : nœud sans enfants (3, 7, 20)
- **Hauteur** : nombre de niveaux (ici 3)
- **Sous-arbre** : arbre enraciné à un nœud quelconque

---

## 2. Structure

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Noeud {
    int valeur;
    struct Noeud *gauche;
    struct Noeud *droit;
} Noeud;
```

---

## 3. Créer un nœud

```c
Noeud* creer_noeud(int val) {
    Noeud *n   = (Noeud*) malloc(sizeof(Noeud));
    n->valeur  = val;
    n->gauche  = NULL;
    n->droit   = NULL;
    return n;
}
```

---

## 4. Arbre Binaire de Recherche (ABR)

Dans un **ABR**, pour chaque nœud :
- toutes les valeurs du sous-arbre **gauche** sont **inférieures**
- toutes les valeurs du sous-arbre **droit** sont **supérieures**

### Insertion (récursive)

```c
Noeud* inserer(Noeud *racine, int val) {
    if (racine == NULL) return creer_noeud(val);

    if (val < racine->valeur)
        racine->gauche = inserer(racine->gauche, val);
    else if (val > racine->valeur)
        racine->droit  = inserer(racine->droit, val);
    // val == racine->valeur : doublons ignorés

    return racine;
}
```

### Recherche

```c
Noeud* rechercher(Noeud *racine, int val) {
    if (racine == NULL || racine->valeur == val)
        return racine;

    if (val < racine->valeur)
        return rechercher(racine->gauche, val);
    else
        return rechercher(racine->droit, val);
}
```

---

## 5. Parcours (traversals)

### Infixe : Gauche - Racine - Droite

Donne les valeurs **triées** dans un ABR.

```c
void infixe(Noeud *r) {
    if (r == NULL) return;
    infixe(r->gauche);
    printf("%d ", r->valeur);
    infixe(r->droit);
}
```

### Préfixe : Racine - Gauche - Droite

Utile pour copier ou sérialiser l'arbre.

```c
void prefixe(Noeud *r) {
    if (r == NULL) return;
    printf("%d ", r->valeur);
    prefixe(r->gauche);
    prefixe(r->droit);
}
```

### Suffixe : Gauche - Droite - Racine

Utile pour libérer l'arbre ou calculer des expressions.

```c
void suffixe(Noeud *r) {
    if (r == NULL) return;
    suffixe(r->gauche);
    suffixe(r->droit);
    printf("%d ", r->valeur);
}
```

---

## 6. Utilitaires

```c
// Hauteur de l'arbre
int hauteur(Noeud *r) {
    if (r == NULL) return 0;
    int hg = hauteur(r->gauche);
    int hd = hauteur(r->droit);
    return 1 + (hg > hd ? hg : hd);
}

// Nombre de nœuds
int compter(Noeud *r) {
    if (r == NULL) return 0;
    return 1 + compter(r->gauche) + compter(r->droit);
}

// Libérer l'arbre
void liberer(Noeud *r) {
    if (r == NULL) return;
    liberer(r->gauche);
    liberer(r->droit);
    free(r);
}
```

---

## 7. Programme complet

```c
int main() {
    Noeud *arbre = NULL;

    int vals[] = {10, 5, 15, 3, 7, 20, 1};
    int n = 7;
    for (int i = 0; i < n; i++)
        arbre = inserer(arbre, vals[i]);

    printf("Infixe  : "); infixe(arbre);   printf("\n"); // 1 3 5 7 10 15 20
    printf("Préfixe : "); prefixe(arbre);  printf("\n"); // 10 5 3 1 7 15 20
    printf("Suffixe : "); suffixe(arbre);  printf("\n"); // 1 3 7 5 20 15 10

    printf("Hauteur : %d\n", hauteur(arbre));  // 4
    printf("Noeuds  : %d\n", compter(arbre));  // 7

    Noeud *f = rechercher(arbre, 7);
    printf("7 trouvé : %s\n", f ? "oui" : "non");

    liberer(arbre);
    return 0;
}
```
