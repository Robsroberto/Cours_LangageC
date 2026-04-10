- ### Introduction aux Chaînes de Caractères
- ### Déclaration de Chaînes de Caractères
- ### Caractère de Fin de Chaîne (NUL)
- ### Accès aux Caractères d'une Chaîne
- ### Fonctions de Manipulation de Chaînes
- ### TP
       

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

## TP