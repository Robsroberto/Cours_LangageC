- ### Tableau
- ### Matrice
- ### Structure
- ### Fonction
- ### TP
       

## Structures
Les structures permettent de regrouper plusieurs variables de types différents sous un même nom. Elles sont utiles pour créer des objets personnalisés.

Syntaxe :

```C
struct Nom_De_Structure {
    type champ1;
    type champ2;
    // ...
};

```
Exemple :
```C
struct Personne {
    char nom[50];
    int age;
};

```
Une structure nommée "Personne" est créée, avec un champ "nom" de type chaîne de caractères et un champ "age" de type entier.

Exercice:
Créez une structure pour représenter un livre avec des champs comme le titre, l'auteur et l'année de publication.
Solutions:
```C
#include <stdio.h>

// Définir la structure pour représenter un livre
struct Livre {
    char titre[100];
    char auteur[100];
    int anneePublication;
};

int main() {
    // Créer une instance de la structure Livre
    struct Livre monLivre;

    // Remplir les champs de la structure
    printf("Entrez le titre du livre : ");
    scanf("%s", monLivre.titre);
    printf("Entrez l'auteur du livre : ");
    scanf("%s", monLivre.auteur);
    printf("Entrez l'année de publication du livre : ");
    scanf("%d", &monLivre.anneePublication);

    // Afficher les champs de la structure
    printf("Détails du livre :\n");
    printf("Titre : %s\n", monLivre.titre);
    printf("Auteur : %s\n", monLivre.auteur);
    printf("Année de publication : %d\n", monLivre.anneePublication);

    return 0;
}

```

Exemples:
- fonction
```C
#include <stdio.h>

// Définition d'une fonction qui calcule la somme de deux entiers
int addition(int a, int b) {
    return a + b;
}

int main() {
    //Appel de la fonction addition
    //stockage valeur de retour dan sresultat
    int resultat = addition(5, 3);
    //affichage du resultat
    printf("Résultat de l'addition : %d\n", resultat);
    return 0;
}

```
- procédure
```C
#include <stdio.h>

// Définition d'une procédure qui affiche un message de salutation
void saluer() {
    printf("Bonjour, cher utilisateur!\n");
}

int main() {
    saluer(); // Appel de la procédure de salutation
    return 0;
}

```

Exercices:
Écrivez une fonction en langage C qui calcule la somme des entiers de 1 à n, où n est un paramètre de la fonction. Ensuite, appelez cette fonction avec n = 10 et affichez le résultat.
Solution
```C
#include <stdio.h>

// Définition de la fonction de calcul de la somme des entiers de 1 à n
int sommeDesEntiers(int n) {
    int somme = 0;
    for (int i = 1; i <= n; i++) {
        somme += i;
    }
    return somme;
}

int main() {
    int n = 10;
    int resultat = sommeDesEntiers(n);
    printf("Somme des entiers de 1 à %d : %d\n", n, resultat);
    return 0;
}

```

Écrivez une procédure en langage C qui affiche les n premiers termes de la suite de Fibonacci. Ensuite, appelez cette procédure avec n = 8 et affichez les termes de la suite.
Solution:
```C
#include <stdio.h>

// Définition d'une procédure pour afficher les n premiers termes de la suite de Fibonacci
void afficherSuiteFibonacci(int n) {
    int premier = 0, deuxieme = 1, suivant;

    printf("Suite de Fibonacci : ");
    for (int i = 0; i < n; i++) {
        if (i <= 1) {
            suivant = i;
        } else {
            suivant = premier + deuxieme;
            premier = deuxieme;
            deuxieme = suivant;
        }
        printf("%d ", suivant);
    }
    printf("\n");
}

int main() {
    int n = 8;
    afficherSuiteFibonacci(n);
    return 0;
}

```
## TP

- Écrivez un programme en C qui effectue la multiplication de deux matrices carrées 3x3. Les valeurs des matrices peuvent être initialisées dans le code.

- Déclarez une structure en C pour représenter un étudiant avec des champs tels que le nom, la note moyenne et l'âge. Créez un tableau de trois étudiants et affichez leurs informations.

- Écrivez une fonction en C qui calcule la factorielle d'un entier donné en tant que paramètre. Ensuite, appelez cette fonction avec une valeur et affichez le résultat.

- Écrivez une procédure en C qui affiche la table de multiplication pour un nombre donné. Appelez cette procédure avec un nombre et affichez la table de multiplication.