---
marp: false
size: 4:3
style: |
  h2, h3, p {
    font-size: 20px;
  }
  li {
    font-size:20px
  }
headingDivider: 1
header: 
paginate: 
footer: Licence 2 Informatique &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ISI (Institut Supérieur D'Informatique) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RD
---

# Chapitre : Révision Langage C
- ### Tableau
- ### Matrice
- ### Structure
- ### Fonction
- ### TP
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

## Par Robert DIASSÉ

---
  ## Tableau
  Les tableaux sont des structures de données qui permettent de stocker plusieurs éléments du même type sous un même nom. Ils sont utilisés pour gérer des collections de données.
  Syntaxe:
```C
  type nom_du_tableau[taille];
```
Exemple
```C
  int tableau[5] = {1, 2, 3, 4, 5};
```
Un tableau d'entiers nommé "tableau" de taille 5 est créé et initialisé avec des valeurs de 1 à 5.
Exercices :

-Créez un tableau de chaînes de caractères et affichez son contenu.
-Calculez la somme des éléments d'un tableau d'entiers.
Solution:
```C
#include <stdio.h>

int main() {
    // Exercice 1 : Créez un tableau de chaînes de caractères et affichez son contenu.
    char *prenoms[] = {"Alice", "Bob", "Charlie", "David", "Eve"};
    printf("Tableau de prenoms :\n");
    for (int i = 0; i < 5; i++) {
        printf("%d : %s\n", i, prenoms[i]);
    }

    // Exercice 2 : Calculez la somme des éléments d'un tableau d'entiers.
    int entiers[] = {1, 2, 3, 4, 5};
    int somme = 0;
    for (int i = 0; i < 5; i++) {
        somme += entiers[i];
    }
    printf("La somme des entiers est : %d\n");

    return 0;
}
```
Exercice :
Créez un tableau de 10 nombres aléatoires entre 1 et 100. Ensuite, trouvez et affichez le plus grand nombre dans ce tableau.
Solutions:
```C
#include <stdio.h>
#include <stdlib.h>

int main() {
    int tableau[10];
    
    // Remplir le tableau avec des nombres aléatoires entre 1 et 100
    for (int i = 0; i < 10; i++) {
        tableau[i] = rand();
    }

    // Trouver le plus grand nombre dans le tableau
    int plusGrand = tableau[0];
    for (int i = 1; i < 10; i++) {
        if (tableau[i] > plusGrand) {
            plusGrand = tableau[i];
        }
    }

    // Afficher le tableau et le plus grand nombre
    printf("Tableau de nombres aléatoires :\n");
    for (int i = 0; i < 10; i++) {
        printf("%d ", tableau[i]);
    }
    printf("\nLe plus grand nombre est : %d\n", plusGrand);

    return 0;
}

```
--
## Matrices

Les matrices sont des tableaux bidimensionnels qui permettent de stocker des données dans des rangées et des colonnes. Elles sont couramment utilisées pour représenter des grilles de données.
Syntaxe :

```C
type nom_de_la_matrice[nb_de_lignes][nb_de_colonnes];

```
Exemple :

```C
int matrice[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

```
Une matrice 3x3 est créée et initialisée avec des valeurs de 1 à 9.

Exercices :

-additionnez deux matrices.
Solutions:
```C
#include <stdio.h>

int main() {
    int lignes, colonnes;

    // Demandez à l'utilisateur la taille des matrices
    printf("Entrez le nombre de lignes des matrices : ");
    scanf("%d", &lignes);
    printf("Entrez le nombre de colonnes des matrices : ");
    scanf("%d", &colonnes;

    int matrice1[lignes][colonnes], matrice2[lignes][colonnes], resultat[lignes][colonnes];

    // Remplissez la première matrice
    printf("Entrez les éléments de la première matrice :\n");
    for (int i = 0; i < lignes; i++) {
        for (int j = 0; j < colonnes; j++) {
            scanf("%d", &matrice1[i][j]);
        }
    }

    // Remplissez la deuxième matrice
    printf("Entrez les éléments de la deuxième matrice :\n");
    for (int i = 0; i < lignes; i++) {
        for (int j = 0; j < colonnes; j++) {
            scanf("%d", &matrice2[i][j]);
        }
    }


    // Additionnez les deux matrices
    for (int i = 0; i < lignes; i++) {
        for (int j = 0; j < colonnes; j++) {
            resultat[i][j] = matrice1[i][j] + matrice2[i][j];
        }
    }

    // Affichez la matrice résultante
    printf("La matrice résultante est :\n");
    for (int i = 0; i < lignes; i++) {
        for (int j = 0; j < colonnes; j++) {
            printf("%d\t", resultat[i][j]);
        }
        printf("\n");
    }

    return 0;
}

```

---

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

---
## Fonctions
- Fonctions

Une fonction est un bloc de code autonome qui effectue une tâche spécifique et renvoie une valeur en sortie. Les fonctions sont principalement utilisées pour effectuer des calculs et des opérations sur les données. Elles peuvent accepter des paramètres en entrée et renvoyer une valeur en sortie.
```C
type_de_retour nom_de_la_fonction(paramètres) {
    // Code de la fonction
    return valeur_de_retour;
}
```
-type_de_retour : Le type de données que la fonction renverra. Cela peut être int, float, void, etc.

-nom_de_la_fonction : Le nom de la fonction.

-paramètres : Les paramètres que la fonction accepte (le cas échéant), séparés par des virgules. Chaque paramètre est composé du type et du nom (par exemple, int x).

-valeur_de_retour : La valeur que la fonction renvoie, de type type_de_retour.

Exemple:
```C
int addition(int a, int b) {
    int somme = a + b;
    return somme;
}

```
Dans cet exemple, nous avons défini une fonction appelée addition. Voici une explication détaillée :

-`int` est le type de retour de la fonction, ce qui signifie que la fonction renverra un résultat de type entier (`int`).

-`addition` est le nom de la fonction.
`int a`, `int b` sont les paramètres d'entrée de la fonction. La fonction attend deux entiers en entrée, que nous nommons a et b.

-À l'intérieur de la fonction, nous avons une instruction qui additionne a et b et stocke le résultat dans une variable locale somme.

-Enfin, nous utilisons return pour renvoyer la valeur de somme en tant que résultat de la fonction.
Lorsque cette fonction est appelée, elle prend deux entiers en entrée, effectue une addition, puis renvoie le résultat en tant qu'entier. Par exemple :
```C
int resultat = addition(5, 3);
```
Ici, `resultat` contiendra la valeur `8`.

- Procédure
Une procédure est similaire à une fonction, mais elle n'a pas de valeur de retour. Elle effectue une série d'instructions sans renvoyer de résultat. Les procédures sont couramment utilisées pour réaliser des actions, des opérations ou des modifications sur les données.
Syntaxe:
```C
void nom_de_la_procedure(paramètres) {
    // Code de la procédure
}
```
-`void` : Le type de retour est void, ce qui signifie que la procédure ne renvoie pas de valeur.
-`nom_de_la_procedure` : Le nom de la procédure.
-`paramètres` : Les paramètres que la procédure accepte (le cas échéant), séparés par des virgules. Chaque paramètre est composé du type et du nom (par exemple, `int x`).
Exemple:
```C
void afficherMessage(char message[]) {
    printf("%s\n", message);
}

```
-`void` est le type de retour de la procédure, ce qui signifie que la procédure n'a pas de valeur de retour.
-`afficherMessage` est le nom de la procédure.
-`char message[]` est un paramètre d'entrée de la procédure. La procédure attend une chaîne de caractères en entrée, que nous nommons message.
-À l'intérieur de la procédure, nous utilisons `printf` pour afficher le contenu de `message`.
Comme il n'y a pas de `return` dans la procédure, elle ne renvoie pas de valeur.

---
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
- Écrivez un programme en C qui demande à l'utilisateur de saisir 5 entiers, les stocke dans un tableau, puis affiche la somme de ces entiers.

- Écrivez un programme en C qui effectue la multiplication de deux matrices carrées 3x3. Les valeurs des matrices peuvent être initialisées dans le code.

- Déclarez une structure en C pour représenter un étudiant avec des champs tels que le nom, la note moyenne et l'âge. Créez un tableau de trois étudiants et affichez leurs informations.

- Écrivez une fonction en C qui calcule la factorielle d'un entier donné en tant que paramètre. Ensuite, appelez cette fonction avec une valeur et affichez le résultat.

- Écrivez une procédure en C qui affiche la table de multiplication pour un nombre donné. Appelez cette procédure avec un nombre et affichez la table de multiplication.