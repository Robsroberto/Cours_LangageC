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
<img src="../isi.png" alt="ISI" width="100px">

### **Programmation Modulaire en Langage C**

## Par Robert DIASSÉ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
<img src="../C.jpeg" alt="ISI" width="50px">

---

### **Introduction**

La **programmation modulaire** est une approche de développement qui consiste à diviser un programme en plusieurs parties appelées **modules**. Chaque module est autonome, responsable d’une tâche précise, et peut être réutilisé dans d’autres programmes.

En C, cela se traduit par la création de **fichiers séparés** contenant du code spécifique, souvent en lien avec une fonction ou une fonctionnalité précise.

---

### **1. Pourquoi utiliser la programmation modulaire ?**

#### **Avantages :**
1. **Lisibilité améliorée** :
   - Le code est organisé et divisé en sections logiques, ce qui le rend plus facile à lire et à comprendre.

2. **Réutilisabilité** :
   - Les modules peuvent être utilisés dans plusieurs projets sans modification.

3. **Maintenance facilitée** :
   - Modifier un module n’affecte pas directement les autres parties du programme.

4. **Collaboration** :
   - Plusieurs développeurs peuvent travailler simultanément sur différents modules d’un projet.

5. **Débogage simplifié** :
   - Les bugs peuvent être isolés et corrigés plus rapidement, car chaque module est indépendant.

---

### **2. Comment structurer un programme modulaire en C ?**

Un programme modulaire typique en C utilise trois types de fichiers :
1. **Fichier d’en-tête (`.h`)** :
   - Contient les déclarations des fonctions, des constantes et des structures.
   - Sert d'interface entre les modules.

2. **Fichier source (`.c`)** :
   - Contient l’implémentation des fonctions déclarées dans le fichier `.h`.

3. **Fichier principal (`main.c`)** :
   - Point d’entrée du programme, utilise les modules via les fichiers d’en-tête.

---

### **3. Procédures et Fonctions en Programmation Modulaire**

#### **a) Qu’est-ce qu’une fonction ?**
Une **fonction** est un bloc de code qui effectue une tâche spécifique. Elle peut :
- Recevoir des **paramètres** en entrée.
- Retourner un **résultat**.

---

#### **b) Différence entre une procédure et une fonction**
En C, une **procédure** est simplement une **fonction qui ne retourne aucune valeur** (type `void`).

- **Fonction** : Retourne une valeur.  
  Exemple :
  ```c
  int addition(int a, int b) {
      return a + b;
  }
  ```

- **Procédure** : N’effectue qu’une action, sans retourner de valeur.  
  Exemple :
  ```c
  void afficherMessage() {
      printf("Bonjour, monde !\n");
  }
  ```

---

### **4. Les Types de Fonctions**

#### **a) Fonctions sans paramètres ni retour**
Utilisées pour exécuter une tâche fixe.

```c
void afficherBonjour() {
    printf("Bonjour !\n");
}
```

#### **b) Fonctions avec paramètres mais sans retour**
Utilisées pour effectuer une action en utilisant des données d’entrée.

```c
void afficherSomme(int a, int b) {
    printf("La somme de %d et %d est %d\n", a, b, a + b);
}
```

#### **c) Fonctions sans paramètres mais avec retour**
Utilisées pour renvoyer un résultat calculé, sans avoir besoin de données d’entrée.

```c
int obtenirValeurFixe() {
    return 42;
}
```

#### **d) Fonctions avec paramètres et retour**
Les plus courantes. Utilisées pour effectuer des calculs sur des données d’entrée et retourner un résultat.

```c
float calculerMoyenne(int total, int nombre) {
    return (float)total / nombre;
}
```

---

### **5. Organisation d’un Programme Modulaire**

#### **Étape 1 : Créer un fichier d’en-tête (`module.h`)**
- Déclarez les fonctions et définitions nécessaires.

Exemple (`module.h`) :
```c
#ifndef MODULE_H
#define MODULE_H

// Déclarations des fonctions
void afficherMessage();
int addition(int a, int b);

#endif
```

---

#### **Étape 2 : Créer un fichier source (`module.c`)**
- Implémentez les fonctions déclarées dans le fichier d’en-tête.

Exemple (`module.c`) :
```c
#include <stdio.h>
#include "module.h"

// Implémentation des fonctions
void afficherMessage() {
    printf("Bienvenue dans la programmation modulaire !\n");
}

int addition(int a, int b) {
    return a + b;
}
```

---

#### **Étape 3 : Créer un fichier principal (`main.c`)**
- Incluez le fichier d’en-tête et utilisez les fonctions.

Exemple (`main.c`) :
```c
#include <stdio.h>
#include "module.h"

int main() {
    afficherMessage();

    int resultat = addition(5, 7);
    printf("Résultat de l'addition : %d\n", resultat);

    return 0;
}
```

---

#### **Étape 4 : Compiler le programme**
Utilisez une commande pour compiler tous les fichiers :
```bash
gcc main.c module.c -o programme
```
Exécutez ensuite :
```bash
./programme
```

---

### **6. Bonne Pratiques en Programmation Modulaire**

1. **Utiliser des noms significatifs** :
   - Les noms des fichiers, des fonctions et des variables doivent refléter leur rôle.

2. **Un fichier pour chaque module** :
   - Ne mettez pas toutes les fonctions dans un seul fichier. Par exemple :
     - Fichier `calculs.c` : Contient des fonctions mathématiques.
     - Fichier `affichage.c` : Contient des fonctions d'affichage.

3. **Commentaires clairs** :
   - Documentez chaque fonction avec son rôle, ses paramètres et son retour.

4. **Limiter l’accès aux données** :
   - Utilisez des variables globales uniquement si nécessaire. Privilégiez les paramètres et les retours.

---

### **7. Exemple Complet : Programme Modulaire**

#### **Objectif** :
Créer un programme pour gérer des calculs mathématiques simples.

---

#### **Fichier d’en-tête : `calculs.h`**
```c
#ifndef CALCULS_H
#define CALCULS_H

int addition(int a, int b);
int soustraction(int a, int b);
int multiplication(int a, int b);
float division(int a, int b);

#endif
```

---

#### **Fichier source : `calculs.c`**
```c
#include "calculs.h"

int addition(int a, int b) {
    return a + b;
}

int soustraction(int a, int b) {
    return a - b;
}

int multiplication(int a, int b) {
    return a * b;
}

float division(int a, int b) {
    if (b != 0) {
        return (float)a / b;
    } else {
        return 0.0; // Division par zéro
    }
}
```

---

#### **Fichier principal : `main.c`**
```c
#include <stdio.h>
#include "calculs.h"

int main() {
    int a = 20, b = 10;

    printf("Addition : %d\n", addition(a, b));
    printf("Soustraction : %d\n", soustraction(a, b));
    printf("Multiplication : %d\n", multiplication(a, b));
    printf("Division : %.2f\n", division(a, b));

    return 0;
}
```

---

### **8. Avantages et Limites de la Programmation Modulaire**

#### **Avantages :**
1. **Facilité de maintenance** : Le code est mieux organisé et plus facile à modifier.
2. **Réutilisation** : Les modules peuvent être réutilisés dans d'autres programmes.
3. **Travail en équipe** : Les développeurs peuvent travailler sur des modules différents sans se gêner.

#### **Limites :**
1. **Complexité initiale** : Demande un effort pour organiser le projet dès le départ.
2. **Dépendances entre modules** : Mauvaise gestion des dépendances peut compliquer le débogage.

---

### **Conclusion**

La programmation modulaire en C est une méthode puissante pour écrire des programmes bien organisés, maintenables et réutilisables. En utilisant des **fichiers d’en-tête**, des **modules bien définis** et des **fonctions claires**, vous pouvez structurer efficacement vos projets, même les plus complexes.