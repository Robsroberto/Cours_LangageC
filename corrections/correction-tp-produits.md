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

## 📦 Bonus
Tu veux que je t’aide à ajouter :
- La **sauvegarde automatique** dans un fichier ?
- La **lecture à partir d’un fichier existant** au démarrage ?
- Une **version avec menu interactif plus graphique (ncurses)** ?

Dis-moi ce que tu veux ajouter pour aller plus loin 👨‍🏫