## 🔹 1. `inventaire.h` – **Fichier d'en-tête**
Ce fichier contient :
- La **structure `Produit`**
- Les **constantes**
- Les **prototypes** des fonctions

```c
#ifndef INVENTAIRE_H
#define INVENTAIRE_H

#define MAX_PRODUITS 100
#define TAILLE_NOM 50

typedef struct {
    int code;
    char nom[TAILLE_NOM];
    float prix;
    int quantite;
} Produit;

// Fonctions
void ajouterProduit(Produit tab[], int *nbProduits);
void rechercherProduit(Produit tab[], int nbProduits);
void afficherInventaire(Produit tab[], int nbProduits);
void mettreAJourProduit(Produit tab[], int nbProduits);
void supprimerProduit(Produit tab[], int *nbProduits);
void genererRapport(Produit tab[], int nbProduits);

#endif
```

---

## 🔹 2. `inventaire.c` – **Implémentation des fonctions**
Ce fichier contient toutes les **fonctions déclarées dans l'en-tête**. Voici un exemple simplifié de chaque :

```c
#include <stdio.h>
#include <string.h>
#include "inventaire.h"

void ajouterProduit(Produit tab[], int *nbProduits) {
    if (*nbProduits >= MAX_PRODUITS) {
        printf("Inventaire plein.\n");
        return;
    }

    Produit p;
    int existe = 0;

    printf("Code produit : ");
    scanf("%d", &p.code);
    
    // Vérifier unicité du code
    for (int i = 0; i < *nbProduits; i++) {
        if (tab[i].code == p.code) {
            existe = 1;
            break;
        }
    }

    if (existe) {
        printf("Ce code existe déjà.\n");
        return;
    }

    printf("Nom produit : ");
    scanf(" %[^\n]", p.nom);
    printf("Prix unitaire : ");
    scanf("%f", &p.prix);
    printf("Quantité : ");
    scanf("%d", &p.quantite);

    tab[*nbProduits] = p;
    (*nbProduits)++;
    printf("Produit ajouté.\n");
}

void rechercherProduit(Produit tab[], int nbProduits) {
    int choix, code;
    char nom[TAILLE_NOM];
    int trouve = 0;

    printf("Rechercher par : 1. Code | 2. Nom : ");
    scanf("%d", &choix);

    if (choix == 1) {
        printf("Entrez le code : ");
        scanf("%d", &code);
        for (int i = 0; i < nbProduits; i++) {
            if (tab[i].code == code) {
                printf("Code: %d, Nom: %s, Prix: %.2f, Qté: %d\n", tab[i].code, tab[i].nom, tab[i].prix, tab[i].quantite);
                trouve = 1;
                break;
            }
        }
    } else {
        printf("Entrez le nom : ");
        scanf(" %[^\n]", nom);
        for (int i = 0; i < nbProduits; i++) {
            if (strcmp(tab[i].nom, nom) == 0) {
                printf("Code: %d, Nom: %s, Prix: %.2f, Qté: %d\n", tab[i].code, tab[i].nom, tab[i].prix, tab[i].quantite);
                trouve = 1;
            }
        }
    }

    if (!trouve)
        printf("Produit non trouvé.\n");
}

void afficherInventaire(Produit tab[], int nbProduits) {
    printf("\n=== Inventaire ===\n");
    for (int i = 0; i < nbProduits; i++) {
        printf("Code: %d | Nom: %s | Prix: %.2f | Qté: %d\n",
            tab[i].code, tab[i].nom, tab[i].prix, tab[i].quantite);
    }
}

void mettreAJourProduit(Produit tab[], int nbProduits) {
    int code;
    int trouve = 0;

    printf("Code du produit à modifier : ");
    scanf("%d", &code);

    for (int i = 0; i < nbProduits; i++) {
        if (tab[i].code == code) {
            printf("Nouveau prix : ");
            scanf("%f", &tab[i].prix);
            printf("Nouvelle quantité : ");
            scanf("%d", &tab[i].quantite);
            printf("Produit mis à jour.\n");
            trouve = 1;
            break;
        }
    }

    if (!trouve)
        printf("Produit non trouvé.\n");
}

void supprimerProduit(Produit tab[], int *nbProduits) {
    int code, index = -1;

    printf("Code du produit à supprimer : ");
    scanf("%d", &code);

    for (int i = 0; i < *nbProduits; i++) {
        if (tab[i].code == code) {
            index = i;
            break;
        }
    }

    if (index != -1) {
        for (int i = index; i < *nbProduits - 1; i++) {
            tab[i] = tab[i + 1];
        }
        (*nbProduits)--;
        printf("Produit supprimé.\n");
    } else {
        printf("Produit non trouvé.\n");
    }
}

void genererRapport(Produit tab[], int nbProduits) {
    float total = 0.0;
    for (int i = 0; i < nbProduits; i++) {
        total += tab[i].prix * tab[i].quantite;
    }
    printf("Valeur totale du stock : %.2f\n", total);
}
```

---

## 🔹 3. `main.c` – **Point d’entrée avec le menu**
Ce fichier contient :
- Le menu principal
- L'appel des fonctions

```c
#include <stdio.h>
#include "inventaire.h"

int main() {
    Produit inventaire[MAX_PRODUITS];
    int nbProduits = 0;
    int choix;

    do {
        printf("\n=== Gestion d'Inventaire ===\n");
        printf("1. Ajouter un produit\n");
        printf("2. Rechercher un produit\n");
        printf("3. Afficher l'inventaire\n");
        printf("4. Mettre à jour un produit\n");
        printf("5. Supprimer un produit\n");
        printf("6. Générer un rapport\n");
        printf("7. Quitter\n");
        printf("Choix : ");
        scanf("%d", &choix);

        switch (choix) {
            case 1: ajouterProduit(inventaire, &nbProduits); break;
            case 2: rechercherProduit(inventaire, nbProduits); break;
            case 3: afficherInventaire(inventaire, nbProduits); break;
            case 4: mettreAJourProduit(inventaire, nbProduits); break;
            case 5: supprimerProduit(inventaire, &nbProduits); break;
            case 6: genererRapport(inventaire, nbProduits); break;
            case 7: printf("Au revoir !\n"); break;
            default: printf("Option invalide.\n");
        }

    } while (choix != 7);

    return 0;
}
```

---

## 📌 Compilation
Tu peux compiler avec une seule commande :
```bash
gcc main.c inventaire.c -o inventaire
./inventaire
```

---

## 📦 Bonus
Tu veux que je t’aide à ajouter :
- La **sauvegarde automatique** dans un fichier ?
- La **lecture à partir d’un fichier existant** au démarrage ?
- Une **version avec menu interactif plus graphique (ncurses)** ?

Dis-moi ce que tu veux ajouter pour aller plus loin 👨‍🏫