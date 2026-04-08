### Fonctions de Manipulation de Fichiers en C

En langage C, la bibliothèque standard (`<stdio.h>`) fournit plusieurs fonctions pour la manipulation de fichiers. Chacune de ces fonctions a un rôle spécifique dans l'ouverture, la lecture, et l'écriture de fichiers. Voici un aperçu détaillé de certaines de ces fonctions :

#### 1. `fopen` - Ouverture de Fichier

La fonction `fopen` est utilisée pour ouvrir un fichier.

```c
FILE *fichier = fopen("exemple.txt", "r");
```

- **Arguments :**
  - Nom du fichier.
  - Mode d'ouverture (`"r"`, `"w"`, `"a"`, `"rb"`, `"wb"`, `"r+"`, `"w+"`, `"a+"`, etc.).

- **Utilisation :**
  - Ouvre un fichier dans le mode spécifié.

#### 2. `fclose` - Fermeture de Fichier

La fonction `fclose` est utilisée pour fermer un fichier ouvert.

```c
fclose(fichier);
```

- **Arguments :**
  - Pointeur vers le fichier à fermer.

- **Utilisation :**
  - Ferme le fichier précédemment ouvert.

#### 3. `fgetc` - Lecture Caractère par Caractère

La fonction `fgetc` est utilisée pour lire un caractère à la fois depuis un fichier.

```c
int caractere = fgetc(fichier);
```

- **Arguments :**
  - Pointeur vers le fichier.

- **Utilisation :**
  - Lit le caractère suivant dans le fichier.

#### 4. `fputc` - Écriture Caractère par Caractère

La fonction `fputc` est utilisée pour écrire un caractère dans un fichier.

```c
fputc('A', fichier);
```

- **Arguments :**
  - Caractère à écrire.
  - Pointeur vers le fichier.

- **Utilisation :**
  - Écrit un caractère dans le fichier.

#### 5. `fgets` - Lecture de Chaîne de Caractères

La fonction `fgets` est utilisée pour lire une ligne depuis un fichier.

```c
char buffer[100];
fgets(buffer, sizeof(buffer), fichier);
```

- **Arguments :**
  - Buffer pour stocker la ligne lue.
  - Taille du buffer.
  - Pointeur vers le fichier.

- **Utilisation :**
  - Lit une ligne depuis le fichier.

#### 6. `fputs` - Écriture de Chaîne de Caractères

La fonction `fputs` est utilisée pour écrire une chaîne de caractères dans un fichier.

```c
fputs("Hello, fichier!", fichier);
```

- **Arguments :**
  - Chaîne de caractères à écrire.
  - Pointeur vers le fichier.

- **Utilisation :**
  - Écrit une chaîne de caractères dans le fichier.

#### 7. `fread` - Lecture de Bloc de Données

La fonction `fread` est utilisée pour lire un bloc de données depuis un fichier.

```c
char buffer[1024];
size_t taille_lue = fread(buffer, sizeof(char), sizeof(buffer), fichier);
```

- **Arguments :**
  - Buffer pour stocker les données lues.
  - Taille de chaque élément.
  - Nombre d'éléments à lire.
  - Pointeur vers le fichier.

- **Utilisation :**
  - Lit un bloc de données depuis le fichier.

#### 8. `fwrite` - Écriture de Bloc de Données

La fonction `fwrite` est utilisée pour écrire un bloc de données dans un fichier.

```c
char buffer[] = "Donnees a ecrire.";
size_t taille_ecrite = fwrite(buffer, sizeof(char), sizeof(buffer), fichier);
```

- **Arguments :**
  - Buffer contenant les données à écrire.
  - Taille de chaque élément.
  - Nombre d'éléments à écrire.
  - Pointeur vers le fichier.

- **Utilisation :**
  - Écrit un bloc de données dans le fichier.

#### 9. `fprintf` - Écriture Formatée

La fonction `fprintf` est utilisée pour écrire dans un fichier de manière similaire à `printf`.

```c
fprintf(fichier, "Le nombre est : %d", nombre);
```

- **Arguments :**
  - Pointeur vers le fichier.
  - Chaîne de format.
  - Variables à écrire dans le fichier.

- **Utilisation :**
  - Écrit des données formatées dans le fichier.

#### 10. `fscanf` - Lecture Formatée

La fonction `fscanf` est utilisée pour lire depuis un fichier de manière similaire à `scanf`.

```c
int nombre;
fscanf(fichier, "%d", &nombre);
```

- **Arguments :**


  - Pointeur vers le fichier.
  - Chaîne de format.
  - Adresses des variables à remplir.

- **Utilisation :**
  - Lit des données formatées depuis le fichier.

#### 11. `fseek` - Déplacement du Curseur de Lecture/Écriture

La fonction `fseek` est utilisée pour déplacer le curseur de lecture/écriture dans le fichier.

```c
fseek(fichier, 10, SEEK_SET);  // Déplace le curseur à la 10e position depuis le début du fichier
```

- **Arguments :**
  - Pointeur vers le fichier.
  - Offset de déplacement.
  - Position de départ (`SEEK_SET`, `SEEK_CUR`, `SEEK_END`).

- **Utilisation :**
  - Déplace le curseur de lecture/écriture dans le fichier.

#### 12. `rewind` - Retour au Début du Fichier

La fonction `rewind` est utilisée pour ramener le curseur au début du fichier.

```c
rewind(fichier);
```

- **Arguments :**
  - Pointeur vers le fichier.

- **Utilisation :**
  - Ramène le curseur au début du fichier.

#### 13. `feof` - Fin de Fichier Atteinte

La fonction `feof` est utilisée pour vérifier si la fin du fichier a été atteinte.

```c
if (feof(fichier)) {
    // Fin de fichier atteinte
}
```

- **Arguments :**
  - Pointeur vers le fichier.

- **Utilisation :**
  - Vérifie si la fin du fichier a été atteinte.

#### 14. `remove` - Suppression de Fichier

La fonction `remove` est utilisée pour supprimer un fichier.

```c
int resultat = remove("exemple.txt");
```

- **Arguments :**
  - Nom du fichier à supprimer.

- **Utilisation :**
  - Supprime le fichier spécifié.

### Gestion des Erreurs

#### Fonction de Gestion d'Erreur pour la Vérification de Fichier

La fonction suivante peut être utilisée pour vérifier si l'ouverture d'un fichier a réussi et afficher un message d'erreur approprié en cas d'échec.

```c
void gestionErreurFichier(FILE *fichier, const char *nomFichier) {
    if (fichier == NULL) {
        printf("Erreur lors de l'ouverture du fichier %s.\n", nomFichier);
        exit(EXIT_FAILURE);
    }
}
```

- **Arguments :**
  - Pointeur vers le fichier.
  - Nom du fichier (à des fins d'affichage).

- **Utilisation :**
  - Vérifie si l'ouverture du fichier a réussi et affiche un message d'erreur en cas d'échec.

---

Ces explications détaillées, accompagnées d'exemples pratiques, permettront aux étudiants de comprendre pleinement le fonctionnement de chaque fonction de manipulation de fichiers en langage C. Les exercices liés à ces fonctions renforceront leur compréhension pratique.

Bien sûr, voici une explication pour chaque fonction avec les valeurs attendues et leur signification :

### 1. `fopen` - Ouverture de Fichier

- **Valeurs Attendues :**
  - Pointeur vers le fichier (`FILE *`).
  - `NULL` en cas d'échec.

- **Interprétation :**
  - Retourne un pointeur vers la structure de fichier associée au fichier ouvert.
  - `NULL` indique une erreur lors de l'ouverture du fichier.

### 2. `fclose` - Fermeture de Fichier

- **Valeurs Attendues :**
  - `0` en cas de succès.
  - `EOF` en cas d'échec.

- **Interprétation :**
  - `0` indique que la fermeture du fichier a été réalisée avec succès.
  - `EOF` indique une erreur lors de la fermeture du fichier.

### 3. `fgetc` - Lecture de Caractère

- **Valeurs Attendues :**
  - La valeur ASCII du caractère lu.
  - `EOF` en cas de fin de fichier ou d'erreur.

- **Interprétation :**
  - La valeur ASCII du caractère lu.
  - `EOF` indique la fin du fichier ou une erreur de lecture.

### 4. `fputc` - Écriture de Caractère

- **Valeurs Attendues :**
  - La valeur du caractère écrit.
  - `EOF` en cas d'erreur.

- **Interprétation :**
  - La valeur du caractère écrit.
  - `EOF` indique une erreur lors de l'écriture du caractère.

### 5. `fgets` - Lecture de Chaîne de Caractères

- **Valeurs Attendues :**
  - Pointeur vers la chaîne de caractères lue.
  - `NULL` en cas de fin de fichier ou d'erreur.

- **Interprétation :**
  - Pointeur vers la chaîne de caractères lue.
  - `NULL` indique la fin du fichier ou une erreur de lecture.

### 6. `fputs` - Écriture de Chaîne de Caractères

- **Valeurs Attendues :**
  - Non nul en cas de succès.
  - `EOF` en cas d'erreur.

- **Interprétation :**
  - Retourne un nombre non nul en cas de succès.
  - `EOF` indique une erreur lors de l'écriture de la chaîne de caractères.

### 7. `fread` - Lecture de Bloc de Données

- **Valeurs Attendues :**
  - Nombre d'éléments lus avec succès.
  - `0` en cas d'erreur ou de fin de fichier.

- **Interprétation :**
  - Le nombre d'éléments lus avec succès.
  - `0` indique la fin de fichier ou une erreur de lecture.

### 8. `fwrite` - Écriture de Bloc de Données

- **Valeurs Attendues :**
  - Nombre d'éléments écrits avec succès.
  - `0` en cas d'erreur.

- **Interprétation :**
  - Le nombre d'éléments écrits avec succès.
  - `0` indique une erreur lors de l'écriture du bloc de données.

### 9. `fprintf` - Écriture Formatée

- **Valeurs Attendues :**
  - Le nombre total de caractères écrits avec succès.
  - Valeur négative en cas d'erreur.

- **Interprétation :**
  - Le nombre total de caractères écrits avec succès.
  - Valeur négative indique une erreur lors de l'écriture.

### 10. `fscanf` - Lecture Formatée

- **Valeurs Attendues :**
  - Le nombre d'éléments lus avec succès.
  - `EOF` en cas de fin de fichier ou d'erreur.

- **Interprétation :**
  - Le nombre d'éléments lus avec succès.
  - `EOF` indique la fin du fichier ou une erreur de lecture.

### 11. `fseek` - Déplacement du Curseur

- **Valeurs Attendues :**
  - `0` en cas de succès.
  - Valeur non nulle en cas d'erreur.

- **Interprétation :**
  - `0` indique un déplacement de curseur réussi.
  - Valeur non nulle indique une erreur lors du déplacement.

### 12. `rewind` - Retour au Début du Fichier

- **Valeurs Attendues :**
  - Aucune.

- **Interprétation :**
  - Aucune valeur renvoyée.

### 13. `feof` - Fin de Fichier Atteinte

- **Valeurs Attendues :**
  - Valeur non nulle si la fin de fichier a été atteinte.
  - `0` sinon.

- **Interprétation :**
  - Valeur non nulle indique que la fin de fichier a été atteinte.
  - `0` indique que la fin de fichier n'a pas été atteinte.

### 14. `remove` - Suppression de Fichier

- **Valeurs Attendues :**
  - `0` en cas de succès.
  - Valeur non nulle en cas d'erreur.

- **Interprétation :**
  - `0` indique la suppression réussie du fichier.
  - Valeur non nulle indique une erreur lors de la suppression du fichier.

### Gestion des Erreurs

#### Fonction de Gestion d'Erreur pour la Vérification de Fichier

- **Valeurs Attendues :**
  - Aucune.

- **Interprétation :**
  - Aucune valeur renvoyée.
  - Affiche un message d'erreur et termine le programme en cas d'échec d'ouverture du fichier.

Ces explications devraient aider à comprendre le fonctionnement de chaque fonction de manipulation de fichiers et les valeurs qu'elles peuvent renvoyer.


Les fonctions `read` et `write` ne sont pas spécifiques au langage C standard. Elles font partie des appels système UNIX/Linux utilisés pour la manipulation des fichiers. Ces appels système sont généralement utilisés dans le contexte de la programmation système en langage C sous des systèmes d'exploitation de type UNIX.

### Fonction `read` :

La fonction `read` est utilisée pour lire un certain nombre d'octets depuis un descripteur de fichier (file descriptor). Voici comment elle est utilisée :

```c
#include <unistd.h>

ssize_t read(int fd, void *buf, size_t count);
```

- `fd` : Le descripteur de fichier à partir duquel lire.
- `buf` : Le tampon dans lequel stocker les données lues.
- `count` : Le nombre d'octets à lire.

**Valeur Attendue :**
- Le nombre d'octets lus avec succès, renvoyé en tant que valeur de retour.
- `-1` en cas d'erreur, et une description de l'erreur est disponible dans la variable `errno`.

**Exemple :**
```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("exemple.txt", O_RDONLY);
    if (fd == -1) {
        perror("Erreur lors de l'ouverture du fichier");
        return 1;
    }

    char buffer[1024];
    ssize_t bytesRead = read(fd, buffer, sizeof(buffer));
    if (bytesRead == -1) {
        perror("Erreur lors de la lecture du fichier");
        close(fd);
        return 1;
    }

    printf("Lus %zd octets : %.*s\n", bytesRead, (int)bytesRead, buffer);

    close(fd);
    return 0;
}
```

### Fonction `write` :

La fonction `write` est utilisée pour écrire un certain nombre d'octets vers un descripteur de fichier. Voici comment elle est utilisée :

```c
#include <unistd.h>

ssize_t write(int fd, const void *buf, size_t count);
```

- `fd` : Le descripteur de fichier vers lequel écrire.
- `buf` : Le tampon contenant les données à écrire.
- `count` : Le nombre d'octets à écrire.

**Valeur Attendue :**
- Le nombre d'octets écrits avec succès, renvoyé en tant que valeur de retour.
- `-1` en cas d'erreur, et une description de l'erreur est disponible dans la variable `errno`.

**Exemple :**
```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("exemple.txt", O_WRONLY | O_CREAT | O_TRUNC, 0666);
    if (fd == -1) {
        perror("Erreur lors de l'ouverture du fichier");
        return 1;
    }

    const char *message = "Hello, fichier!\n";
    ssize_t bytesWritten = write(fd, message, strlen(message));
    if (bytesWritten == -1) {
        perror("Erreur lors de l'écriture dans le fichier");
        close(fd);
        return 1;
    }

    printf("Écrits %zd octets.\n", bytesWritten);

    close(fd);
    return 0;
}
```

**Remarque :** Ces exemples utilisent les appels système de bas niveau (`open`, `read`, `write`, `close`). Ils sont plus spécifiques aux systèmes d'exploitation de type UNIX/Linux et ne sont pas des fonctions de la bibliothèque standard C.



### Position dans un Fichier : `ftell`, `rewind`, `fseek`

#### `ftell` - Obtenir la Position Courante dans un Fichier

La fonction `ftell` est utilisée pour obtenir la position courante du curseur dans un fichier. Elle prend comme argument un pointeur vers le fichier et renvoie la position actuelle en octets par rapport au début du fichier.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        long position = ftell(fichier);  // Obtient la position courante

        printf("La position courante dans le fichier est : %ld octets\n", position);

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`long position = ftell(fichier);`** : Utilisation de `ftell` pour obtenir la position courante dans le fichier. La position est stockée dans une variable de type `long`.

- **`printf("La position courante dans le fichier est : %ld octets\n", position);`** : Affichage de la position courante sur la console.

#### `rewind` - Revenir au Début du Fichier

La fonction `rewind` permet de réinitialiser le curseur de lecture/écriture d'un fichier à sa position de début.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        rewind(fichier);  // Réinitialise le curseur au début du fichier

        // Lecture ou écriture à partir du début du fichier

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`rewind(fichier);`** : Utilisation de `rewind` pour réinitialiser le curseur au début du fichier.

#### `fseek` - Déplacer le Curseur à une Position Spécifique

La fonction `fseek` est utilisée pour déplacer le curseur de lecture/écriture à une position spécifique dans un fichier. Elle prend comme arguments le pointeur vers le fichier, le déplacement par rapport à la position de référence, et la position de référence elle-même.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        fseek(fichier, 20, SEEK_SET);  // Déplace le curseur à la 20e position depuis le début du fichier

        // Lecture ou écriture à partir de la nouvelle position

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`fseek(fichier, 20, SEEK_SET);`** : Utilisation de `fseek` pour déplacer le curseur à la 20e position depuis le début du fichier. Les arguments sont respectivement le fichier, le déplacement et le point de référence (`SEEK_SET` signifie le début du fichier).

### Gestion des Erreurs : `ferror`, `feof`

#### `ferror` - Vérifier les Erreurs lors d'Opérations de Fichier

La fonction `ferror` est utilisée pour vérifier si une erreur s'est produite lors d'opérations de fichiers. Elle renvoie une valeur non nulle si une erreur est détectée, sinon elle renvoie zéro.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        // Effectuer des opérations de lecture ou d'écriture

        if (ferror(fichier)) {
            perror("Erreur lors d'une opération de fichier");
        }

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`if (ferror(fichier)) { perror("Erreur lors d'une opération de fichier"); }`** : Utilisation de `ferror` pour vérifier si une erreur s'est produite lors d'opérations de fichier. Si c'est le cas, la fonction `perror` est utilisée pour afficher un message d'erreur.

#### `feof` - Vérifier la Fin d'un Fichier

La fonction `feof` est utilisée pour vérifier si la fin d'un fichier a été atteinte après une opération de lecture. Elle renvoie une valeur non nulle si la fin du fichier est atteinte, sinon elle renvoie zéro.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        char caractere;

        // Lire caractères jusqu'à la fin du fichier
        while ((caractere = fgetc(fichier)) != EOF) {
            // Traiter le caractère lu
        }

        if (feof(fichier)) {
            printf("Fin du fichier atteinte.\n");
        } else {
            perror("Erreur lors d'une opération de fichier");
        }

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`while ((caractere = fgetc(fichier)) != EOF)`** : Utilisation d'une boucle pour lire les caractères du fichier jusqu'à ce que la fin du fichier (`EOF`) soit atteinte.

- **`if (feof(fichier)) { printf("Fin du fichier atteinte.\n"); }`** : Utilisation de `feof` pour vérifier si la fin du fichier a été atteinte après la boucle de lecture. Un message est affiché si la fin du fichier est atteinte.

### Opérations de Caractères : `fgetc`, `fputc`

#### `fgetc` - Lire un Caractère depuis un Fichier

La fonction `fgetc` est utilisée pour lire un caractère à la fois depuis

 un fichier.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        char caractere;

        // Lire un caractère à la fois jusqu'à la fin du fichier
        while ((caractere = fgetc(fichier)) != EOF) {
            // Traiter le caractère lu
            printf("%c", caractere);
        }

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`while ((caractere = fgetc(fichier)) != EOF)`** : Utilisation d'une boucle pour lire un caractère à la fois jusqu'à la fin du fichier.

#### `fputc` - Écrire un Caractère dans un Fichier

La fonction `fputc` est utilisée pour écrire un caractère dans un fichier.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "w");

    if (fichier != NULL) {
        char caractere = 'A';

        // Écrire le caractère dans le fichier
        fputc(caractere, fichier);

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`fputc(caractere, fichier);`** : Utilisation de `fputc` pour écrire le caractère dans le fichier.

### Opérations de Chaînes de Caractères : `fgets`, `fputs`

#### `fgets` - Lire une Ligne depuis un Fichier

La fonction `fgets` est utilisée pour lire une ligne de texte depuis un fichier.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        char ligne[100];

        // Lire une ligne de texte depuis le fichier
        while (fgets(ligne, sizeof(ligne), fichier) != NULL) {
            // Traiter la ligne lue
            printf("%s", ligne);
        }

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`while (fgets(ligne, sizeof(ligne), fichier) != NULL)`** : Utilisation d'une boucle pour lire une ligne de texte à la fois depuis le fichier.

#### `fputs` - Écrire une Ligne dans un Fichier

La fonction `fputs` est utilisée pour écrire une ligne de texte dans un fichier.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "w");

    if (fichier != NULL) {
        char ligne[] = "Ceci est une ligne de texte.";

        // Écrire la ligne dans le fichier
        fputs(ligne, fichier);

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`fputs(ligne, fichier);`** : Utilisation de `fputs` pour écrire la ligne dans le fichier.

### Opérations de Format : `fprintf`, `fscanf`

#### `fprintf` - Écrire dans un Fichier avec un Format

La fonction `fprintf` est utilisée pour écrire dans un fichier en utilisant un format similaire à `printf`.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "w");

    if (fichier != NULL) {
        int entier = 42;
        float reel = 3.14;

        // Écrire dans le fichier avec un format
        fprintf(fichier, "Entier : %d, Réel : %.2f\n", entier, reel);

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`fprintf(fichier, "Entier : %d, Réel : %.2f\n", entier, reel);`** : Utilisation de `fprintf` pour écrire dans le fichier avec un format.

#### `fscanf` - Lire depuis un Fichier avec un Format

La fonction `fscanf` est utilisée pour lire depuis un fichier en utilisant un format similaire à `scanf`.

```c
#include <stdio.h>

int main() {
    FILE *fichier = fopen("exemple.txt", "r");

    if (fichier != NULL) {
        int entier;
        float reel;

        // Lire depuis le fichier avec un format
        fscanf(fichier, "Entier : %d, Réel : %f", &entier, &reel);

        // Traiter les valeurs lues
        printf("Entier : %d, Réel : %.2f\n", entier, reel);

        fclose(fichier);
    } else {
        printf("Erreur lors de l'ouverture du fichier.\n");
    }

    return 0;
}
```

- **`fscanf(fichier, "Entier : %d, Réel : %f", &entier, &reel);`** : Utilisation de `fscanf` pour lire depuis le fichier avec un format. Les valeurs lues sont stockées dans les variables `entier` et `reel`.

### Exemple Complet : Copie de Fichier

Voici un exemple complet de copie de fichier en utilisant `fgetc` et `fputc` :

```c
#include <stdio.h>

int main() {
    FILE *source = fopen("source.txt", "r");
    FILE *destination = fopen("destination.txt", "w");

    if (source != NULL && destination != NULL) {
        int caractere;

        // Copier caractère par caractère
        while ((caractere = fgetc(source)) != EOF) {
            fputc(caractere, destination);
        }

        fclose(source);
        fclose(destination);
    } else {
        printf("Erreur lors de l'ouverture des fichiers.\n");
    }

    return 0;
}
```

Cet exemple ouvre un fichier source en mode lecture (`"r"`) et un fichier destination en mode écriture (`"w"`). Ensuite, il copie le contenu du fichier source dans le fichier destination caractère par caractère à l'aide de `fgetc` et `fputc`. Enfin, les fichiers sont fermés avec `fclose`.