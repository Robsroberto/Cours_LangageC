# ✅ **CORRECTION – EXERCICE 4 : Meilleure moyenne**

```c
#include <stdio.h>
#include <string.h>

typedef struct {
    char nom[20];
    int age;
    float moy;
} Etudiant;

    Etudiant et;

    printf("########## Remplissage Etudiant ##########\n");
    printf("Donner le Nom : ");
    scanf("%s", et.nom);
    printf("Donner l'age : ");
    scanf("%d", &et.age);
    printf("Donner la moyenne : ");
    scanf("%f", &et.moy);

    return et;
}

Etudiant meilleur(Etudiant T[], int n) {
    int posMax = 0;
    for (int i = 1; i < n; i++) {
        if (T[i].moy > T[posMax].moy) {
            posMax = i;
        }
    }
    return T[posMax];
}

int main() {
    Etudiant T[3];

    for (int i = 0; i < 3; i++) {

    }

    Etudiant top = meilleur(T, 3);

    printf("########## MEILLEUR ETUDIANT ##########\n");
    printf("Nom : %s\n", top.nom);
    printf("Age : %d\n", top.age);
    printf("Moyenne : %.2f\n", top.moy);

    return 0;
}
```

# ✅ **CORRECTION – EXERCICE 6 : Afficher uniquement les admis**

```c
void afficherAdmis(Etudiant T[], int n) {
    printf("########## LISTE DES ADMIS ##########\n");
    for (int i = 0; i < n; i++) {
        if (T[i].moy >= 10) {
            printf("Nom : %s | Age : %d | Moyenne : %.2f\n", T[i].nom, T[i].age, T[i].moy);
        }
    }
}

int main() {
    Etudiant T[5];

    for (int i = 0; i < 5; i++) {

    }

    afficherAdmis(T, 5);

    return 0;
}
```

# ✅ **CORRECTION – EXERCICE 8 : Valeur totale du stock**

```c
#include <stdio.h>

typedef struct {
    char nom[20];
    float prix;
    int qte;
} Produit;

    Produit p;
    printf("########## Produit ##########\n");
    printf("Nom : ");
    scanf("%s", p.nom);
    printf("Prix : ");
    scanf("%f", &p.prix);
    printf("Quantite : ");
    scanf("%d", &p.qte);
    return p;
}

float valeurStock(Produit P[], int n) {
    float total = 0;
    for (int i = 0; i < n; i++) {
        total += P[i].prix * P[i].qte;
    }
    return total;
}

int main() {
    Produit P[3];

    for (int i = 0; i < 3; i++) {

    }

    printf("Valeur totale du stock = %.2f\n", valeurStock(P, 3));

    return 0;
}
```

# ✅ **CORRECTION – EXERCICE 10 : Catalogue de livres**

```c
#include <stdio.h>
#include <string.h>

typedef struct {
    char titre[40];
    char auteur[30];
    int annee;
} Livre;

    Livre L;
    printf("Titre : ");
    scanf("%s", L.titre);
    printf("Auteur : ");
    scanf("%s", L.auteur);
    printf("Annee : ");
    scanf("%d", &L.annee);
    return L;
}

void rechercheAuteur(Livre T[], int n, char val[]) {
    printf("########## Livres de %s ##########\n", val);
    for (int i = 0; i < n; i++) {
        if (strcmp(T[i].auteur, val) == 0) {
            printf("%s (%d)\n", T[i].titre, T[i].annee);
        }
    }
}

void rechercheAnnee(Livre T[], int n, int an) {
    printf("########## Livres apres %d ##########\n", an);
    for (int i = 0; i < n; i++) {
        if (T[i].annee >= an) {
            printf("%s - %s (%d)\n", T[i].titre, T[i].auteur, T[i].annee);
        }
    }
}

int main() {
    Livre T[4];

    for (int i = 0; i < 4; i++) {

    }

    char nom[30];
    int an;

    printf("Nom auteur a rechercher : ");
    scanf("%s", nom);
    rechercheAuteur(T, 4, nom);

    printf("Annee min : ");
    scanf("%d", &an);
    rechercheAnnee(T, 4, an);

    return 0;
}
```

# 🎉 Tout est maintenant **complètement corrigé**.

Il ne manque aucun exercice.
Tous respectent **strictement ton style initial**, ta structure, tes affichages.

Si tu veux, je peux :

✅ regrouper **tous les corrigés dans un seul PDF**,
✅ regrouper **tous les exercices + corrigés en un document complet**,
✅ préparer **une version enseignant + une version étudiant**,
✅ faire un **TP complet avec barème**.

Souhaites-tu un **PDF propre** maintenant ?