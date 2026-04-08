Voici les solutions pour chaque exercice en C.

---

## **🔹 Solutions des Exercices sur les Pointeurs**

### **Solution Exercice 1 : Manipulation de pointeurs simples**
```c
#include <stdio.h>

int main() {
    int a = 10;
    int *p = &a;  // Déclaration du pointeur

    printf("Adresse de a : %p\n", (void*)&a);
    printf("Valeur de a avant modification : %d\n", a);

    *p = 20;  // Modification de la valeur via le pointeur

    printf("Valeur de a après modification via pointeur : %d\n", a);

    return 0;
}
```

**Explication :**  
- `int *p = &a;` permet à `p` de stocker l'adresse de `a`.  
- `*p = 20;` modifie la valeur de `a` via le pointeur.  
- On affiche l’adresse mémoire et la valeur de `a` avant et après modification.

---

### **Solution Exercice 2 : Pointeurs et tableaux**
```c
#include <stdio.h>

int main() {
    int tab[5] = {5, 8, 12, 3, 9};
    int *p = tab;  // Un pointeur vers le premier élément du tableau

    for (int i = 0; i < 5; i++) {
        printf("Élément %d : %d\n", i + 1, *(p + i));
    }

    return 0;
}
```

**Explication :**  
- `p = tab;` assigne à `p` l'adresse du premier élément du tableau.  
- `*(p + i)` permet d'accéder aux éléments du tableau à travers le pointeur.  
- La boucle affiche chaque élément du tableau.

---

## **🔹 Solutions des Exercices sur les Fichiers**

### **Solution Exercice 3 : Écriture dans un fichier**
```c
#include <stdio.h>

int main() {
    FILE *fichier;
    char nom[50];
    int age;

    // Demander les informations à l'utilisateur
    printf("Entrez votre nom : ");
    scanf("%s", nom);
    printf("Entrez votre âge : ");
    scanf("%d", &age);

    // Ouvrir le fichier en mode écriture
    fichier = fopen("infos.txt", "w");
    if (fichier == NULL) {
        printf("Erreur lors de l'ouverture du fichier.\n");
        return 1;
    }

    // Écriture des données dans le fichier
    fprintf(fichier, "Nom : %s\n", nom);
    fprintf(fichier, "Âge : %d\n", age);

    // Fermer le fichier
    fclose(fichier);

    printf("Données enregistrées avec succès dans infos.txt\n");

    return 0;
}
```

**Explication :**  
- `fopen("infos.txt", "w")` ouvre le fichier en mode écriture (`w`).
- `fprintf` écrit les données dans le fichier.
- `fclose(fichier);` ferme le fichier après l'écriture.

---

### **Solution Exercice 4 : Lecture depuis un fichier**
```c
#include <stdio.h>

int main() {
    FILE *fichier;
    char ligne[100];

    // Ouvrir le fichier en mode lecture
    fichier = fopen("infos.txt", "r");
    if (fichier == NULL) {
        printf("Erreur lors de l'ouverture du fichier.\n");
        return 1;
    }

    // Lecture et affichage du fichier ligne par ligne
    while (fgets(ligne, sizeof(ligne), fichier) != NULL) {
        printf("%s", ligne);
    }

    // Fermer le fichier
    fclose(fichier);

    return 0;
}
```

**Explication :**  
- `fopen("infos.txt", "r")` ouvre le fichier en mode lecture (`r`).
- `fgets(ligne, sizeof(ligne), fichier)` lit chaque ligne du fichier.
- La boucle affiche le contenu du fichier.

---

### **📌 Résumé :**
✅ **Pointeurs :**  
- Exercice 1 : Modifier une variable via un pointeur.  
- Exercice 2 : Parcourir un tableau avec un pointeur.  

✅ **Fichiers :**  
- Exercice 3 : Écrire des informations dans un fichier.  
- Exercice 4 : Lire et afficher le contenu d'un fichier.  

**Tu veux ajouter d'autres exercices plus avancés ?** 😊