# Chapitre : Les Fichiers en C
       

### **Introduction aux Fichiers en C**

Les fichiers sont utilisés pour **stocker des données de manière persistante**. En langage C, la bibliothèque `<stdio.h>` fournit des fonctions pour manipuler des fichiers.

Deux types de fichiers principaux :

### **2. Lecture de Fichiers**

#### **a) Lire caractère par caractère : `fgetc`**
Lit un caractère à la fois.

```c
FILE *fichier = fopen("exemple.txt", "r");
int caractere;
while ((caractere = fgetc(fichier)) != EOF) {
    putchar(caractere); // Affiche le caractère
}
```

#### **b) Lire une ligne entière : `fgets`**
Lit une ligne jusqu'à un certain nombre de caractères.

```c
FILE *fichier = fopen("exemple.txt", "r");
char ligne[100];
while (fgets(ligne, sizeof(ligne), fichier) != NULL) {
    printf("%s", ligne); // Affiche la ligne
}
```

#### **c) Lire des données formatées : `fscanf`**
Lit des données avec un format spécifique.

```c
FILE *fichier = fopen("donnees.txt", "r");
int entier;
float reel;
char texte[50];
fscanf(fichier, "%d %f %s", &entier, &reel, texte);
printf("Entier : %d, Réel : %.2f, Texte : %s\n", entier, reel, texte);
```

#### **d) Lire des blocs de données : `fread`**
Utile pour les fichiers binaires.

```c
FILE *fichier = fopen("donnees.bin", "rb");
char buffer[1024];
size_t tailleLue = fread(buffer, 1, sizeof(buffer), fichier);
```

### **4. Fonctions Utiles pour la Gestion des Fichiers**

#### **a) Vérifier la fin d’un fichier : `feof`**
```c
if (feof(fichier)) {
    printf("Fin du fichier atteinte.\n");
}
```

#### **b) Vider un tampon : `fflush`**
Force l’écriture immédiate des données.

```c
fflush(fichier);
```

#### **c) Obtenir la position actuelle : `ftell`**
Renvoie la position actuelle du curseur en octets.

```c
long position = ftell(fichier);
printf("Position : %ld\n", position);
```

#### **d) Revenir au début : `rewind`**
Réinitialise le curseur au début du fichier.

```c
rewind(fichier);
```

#### **e) Déplacer le curseur : `fseek`**
Déplace le curseur à une position spécifique.

```c
fseek(fichier, 20, SEEK_SET); // 20 octets depuis le début
```

### **Conclusion**

Ce cours  vous donne toutes les bases nécessaires pour :
1. Lire, écrire et modifier des fichiers texte et binaires.
2. Manipuler les fichiers en utilisant les fonctions standards.
3. Traiter des données formatées ou brutes efficacement.

Entraînez-vous avec les exemples pratiques pour maîtriser les bases de la gestion des fichiers en C !