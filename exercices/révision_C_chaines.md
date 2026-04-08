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

# Chapitre : Révision Langage C : Chaine de Caractéres
- ### Introduction aux Chaînes de Caractères
- ### Déclaration de Chaînes de Caractères
- ### Caractère de Fin de Chaîne (NUL)
- ### Accès aux Caractères d'une Chaîne
- ### Fonctions de Manipulation de Chaînes
- ### TP
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

## Par Robert DIASSÉ

---
## Introduction aux Chaînes de Caractères

En programmation, une chaîne de caractères est une séquence de caractères, tels que des lettres, des chiffres, des symboles, et des espaces, qui sont utilisés pour représenter du texte. En langage C, les chaînes de caractères sont gérées sous forme de tableaux de caractères (`char`).

## Déclaration de Chaînes de Caractères
En C, les chaînes de caractères sont déclarées comme des tableaux de caractères, suivies d'une séquence de caractères entre guillemets. Voici comment vous déclarez une chaîne de caractères :
```C
char maChaine[] = "Bonjour, monde!";
```
Exemple:
```C
#include <stdio.h>

int main() {
    char maChaine[] = "Bonjour, monde!";
    printf("Ma chaîne : %s\n", maChaine);
    return 0;
}

```

`char maChaine[] = "Bonjour, monde!";` : Cette ligne déclare une variable de tableau de caractères (`char`) appelée `maChaine` et y assigne la chaîne de caractères "Bonjour, monde!". La chaîne est délimitée par des guillemets doubles.

`printf("Ma chaîne : %s\n", maChaine);` : Cette ligne affiche la valeur de `maChaine` à l'écran à l'aide de la fonction `printf`. Le format `%s` est utilisé pour indiquer que vous souhaitez afficher une chaîne de caractères, et maChaine est fournie comme argument pour être affichée. Le `\n` à la fin crée une nouvelle ligne (retour à la ligne) pour que la sortie suivante apparaisse sur une nouvelle ligne.

---

## Caractère de Fin de Chaîne (NUL)
Toutes les chaînes de caractères en C se terminent par un caractère spécial appelé le caractère de fin de chaîne (NUL), représenté par '\0'. Ce caractère indique la fin de la chaîne de caractères et est automatiquement ajouté lorsque vous initialisez une chaîne de caractères entre guillemets.

```C
#include <stdio.h>

int main() {
    char chaine[] = "Exemple";
    int longueur = 0;

    while (chaine[longueur] != '\0') {
        longueur++;
    }

    printf("Longueur de la chaîne : %d\n", longueur);

    return 0;
}

```
`while (chaine[longueur] != '\0') {` : Ceci est une boucle `while` qui itère tant que le caractère courant de la chaîne n'est pas le caractère nul ('\0'). En d'autres termes, il parcourt la chaîne caractère par caractère jusqu'à ce qu'il atteigne la fin de la chaîne.

`longueur++;` : À chaque itération de la boucle, la variable longueur est incrémentée de 1, ce qui compte le nombre de caractères dans la chaîne.

---

## Accès aux Caractères d'une Chaîne

L'accès aux chaînes de caractères en C est basé sur un tableau de caractères (tableau de type `char`).

exemple 

```c
#include <stdio.h>

int main() {
    char maChaine[] = "Bonjour";
    printf("Premier caractère : %c\n", maChaine[0]);
    printf("Deuxième caractère : %c\n", maChaine[1]);
    return 0;
}

```
`printf("Premier caractère : %c\n", maChaine[0]); `: Cette ligne utilise la fonction `printf` pour afficher le premier caractère de la chaîne `maChaine`. Le `%c` dans la chaîne de format indique que nous affichons un caractère. `maChaine[0]` fait référence au premier caractère de la chaîne (ici, 'B').

`printf("Deuxième caractère : %c\n", maChaine[1]);`: Cette ligne est similaire à la précédente, mais elle affiche le deuxième caractère de la chaîne maChaine (ici, 'o').

---

## Fonctions de Manipulation de Chaînes

1. **`strcpy` (Copy String)** :
   -  Copie le contenu d'une chaîne source dans une chaîne de destination.
   - `char* strcpy(char* destination, const char* source);`

2. **`strcat` (Concatenate Strings)** :
   -  Concatène (ajoute) une chaîne source à la fin d'une chaîne de destination.
   -  `char* strcat(char* destination, const char* source);`

3. **`strlen` (String Length)** :
   -  Renvoie la longueur (le nombre de caractères) d'une chaîne de caractères, excluant le caractère nul (`'\0'`).
   -  `size_t strlen(const char* str);`

4. **`strcmp` (String Compare)** :
   -  Compare deux chaînes de caractères et renvoie un entier négatif, nul ou positif en fonction de la comparaison.
   -  `int strcmp(const char* str1, const char* str2);`

5. **`strchr` (String Character)** :
   -  Recherche un caractère donné dans une chaîne et renvoie un pointeur vers la première occurrence de ce caractère.
   -  `char* strchr(const char* str, int character);`

6. **`strstr` (String Search)** :
   -  Recherche une sous-chaîne donnée dans une chaîne et renvoie un pointeur vers la première occurrence de la sous-chaîne.
   -  `char* strstr(const char* haystack, const char* needle);`

7. **`strtok` (String Token)** :
   -  Divise une chaîne en "jetons" en utilisant un délimiteur spécifié.
   -  `char* strtok(char* str, const char* delimiters);`

8. **`strncpy` (Copy N Characters from String)** :
   -  Copie les N premiers caractères d'une chaîne source dans une chaîne de destination.
   -  `char* strncpy(char* destination, const char* source, size_t num);`

9. **`sprintf` (String Print Formatted)** :
   -  Permet de formater et d'écrire des données dans une chaîne au lieu de les afficher à l'écran.
   -  `int sprintf(char* str, const char* format, ...);`

10. **`snprintf` (String Print Formatted with Size)** :
    -  Similaire à `sprintf`, mais limite la taille de la chaîne résultante pour éviter les débordements de mémoire.
    -  `int snprintf(char* str, size_t size, const char* format, ...);`

Ces fonctions sont très utiles pour effectuer des opérations courantes sur les chaînes de caractères en C, telles que la copie, la concaténation, la recherche, la comparaison, la division et le formatage. Assurez-vous de lire la documentation et de prendre en compte les limites de la mémoire lors de l'utilisation de ces fonctions pour éviter les débordements de mémoire.

---

## Noté Bien 
En langage C, il existe plusieurs fonctions pour afficher et récupérer des chaînes de caractères. Les deux principales fonctions pour ces tâches sont `printf` pour afficher et `scanf` pour récupérer des chaînes.

### Afficher des Chaînes de Caractères :

1. **`printf`** :
   - **Description** : Utilisée pour afficher des données formatées à la console.
   - **Utilisation** : `int printf(const char *format, ...);`

   - **Exemple :**
     ```c
     char chaine[] = "Bonjour";
     printf("La chaîne est : %s\n", chaine);
     ```

2. **`puts`** :
   - **Description** : Utilisée pour afficher une chaîne suivie d'un saut de ligne.
   - **Utilisation** : `int puts(const char *str);`

   - **Exemple :**
     ```c
     char chaine[] = "Bonjour";
     puts(chaine);
     ```

### Récupérer des Chaînes de Caractères :

1. **`scanf`** :
   - **Description** : Utilisée pour lire des données formatées depuis l'entrée standard (souvent le clavier).
   - **Utilisation** : `int scanf(const char *format, ...);`

   - **Exemple :**
     ```c
     char chaine[100];
     printf("Entrez une chaîne : ");
     scanf("%s", chaine);
     ```

2. **`gets`** :
   - **Description** : Utilisée pour lire une ligne de texte depuis l'entrée standard (déconseillée en raison de problèmes de sécurité).
   - **Utilisation** : `char *gets(char *str);`

   - **Exemple :**
     ```c
     char chaine[100];
     printf("Entrez une chaîne : ");
     gets(chaine); // Déconseillée en raison de problèmes de sécurité
     ```

3. **`fgets`** :
   - **Description** : Utilisée pour lire une ligne de texte depuis un flux (souvent l'entrée standard) avec une limite de caractères.
   - **Utilisation** : `char *fgets(char *str, int size, FILE *stream);`

   - **Exemple :**
     ```c
     char chaine[100];
     printf("Entrez une chaîne : ");
     fgets(chaine, sizeof(chaine), stdin);
     ```

### Différences Importantes :

- **Problèmes de Sécurité :**
  - `gets` est déconseillée en raison de problèmes de sécurité, car elle ne vérifie pas la taille du tampon de destination, ce qui peut entraîner des dépassements de mémoire.

- **Gestion des Espaces :**
  - `scanf` lit les chaînes jusqu'à rencontrer un espace, ce qui peut être problématique pour la saisie de phrases complètes. Pour lire une phrase entière avec des espaces, il est souvent préférable d'utiliser `fgets`.

- **Ajout de Nouvelles Lignes :**
  - `printf` ajoute automatiquement une nouvelle ligne à la fin de la sortie, alors que `puts` ajoute également une nouvelle ligne mais n'accepte pas de formatage.

En résumé, `printf` et `puts` sont principalement utilisées pour afficher des chaînes, tandis que `scanf`, `gets` et `fgets` sont utilisées pour récupérer des chaînes. Choisissez la fonction en fonction de vos besoins spécifiques et prenez en compte les problèmes de sécurité associés à certaines fonctions.

---

## TP
1- Écrire un programme qui demande à l'utilisateur de saisir une chaîne de caractères, puis affiche sa longueur et enfin copie cette chaîne dans une autre variable.

2- Écrire un programme qui compare deux chaînes de caractères saisies par l'utilisateur et indique si elles sont égales ou non.

3-Écrire un programme qui demande à l'utilisateur de saisir une phrase et une sous-chaîne, puis indique si la sous-chaîne est présente dans la phrase.

4- Écrire un programme qui demande à l'utilisateur de saisir une phrase, puis découper la phrase en mots. Affichez chaque mot sur une nouvelle ligne.

5- Écrire un programme qui demande à l'utilisateur de saisir une phrase et un caractère, trouver la première occurrence du caractère dans la phrase. Affichez la position du caractère.