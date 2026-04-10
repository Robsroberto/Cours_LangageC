### **Programmation Modulaire en Langage C**

# **COURS C —Introduction**

# 1. Introduction : qu’est-ce que le langage C ?

Le **langage C** est un langage de programmation inventé dans les années 1970.
Il sert à écrire :

* des systèmes (Linux, Windows, macOS → beaucoup de parties écrites en C)
* des logiciels rapides
* des programmes embarqués (robots, cartes électroniques…)
* des applications nécessitant exactitude et performance.

Le C est un **langage compilé** :

* On écrit un fichier texte appelé **fichier source** : `programme.c`.
* Ce fichier est traduit (compilé) en un **programme exécutable** que l’ordinateur peut comprendre.

On peut imaginer :

# 3. Structure minimale d’un programme C

Voici **le plus petit programme valide en C** :

```c
#include <stdio.h>

int main(void) {
    return 0;
}
```

Il ne fait rien, mais il est **correct**.
Voyons chaque ligne :

###   `int main(void) { ... }`

C’est la **fonction principale** du programme.

* `int` = la fonction renvoie un entier (généralement 0 si tout se passe bien).
* `main` = nom obligatoire.
* `(void)` = la fonction ne reçoit aucun paramètre.
* `{ ... }` = bloc d’instructions.

**Conclusion :**
Tout programme C commence par `main`, même les plus grands logiciels.

# 5. Les chaînes de caractères : texte entre guillemets `"..."`

Lorsque vous écrivez :

```c
"Bonjour C !"
```

C’est ce qu’on appelle une **chaîne de caractères** (type `char[]` en interne).
En C, **le texte doit être entouré de guillemets doubles `" "`**.

Exemple incorrect :
`Bonjour` ❌

Exemple correct :
`"Bonjour"` ✔️

# 7. Les commentaires (explications dans le code)

Deux formes possibles :

```c
// Commentaire court

/* Commentaire
   sur plusieurs lignes */
```

Les commentaires ne sont **pas exécutés**, ils servent à expliquer.

###   Les règles pour nommer une variable

* Doit commencer par une lettre ou `_`
* Pas d’espace
* Sensible à la casse (`Nom` ≠ `nom`)
* Doit être claire (`note`, `prix`, `age`…)

# 10. Les constantes : valeurs qui ne changent pas

Deux façons :

### **1) Constante du préprocesseur :**

```c
#define PI 3.14
```

C’est remplacé **avant** la compilation.

### **2) Constante C :**

```c
const int MAX = 100;
```

On ne peut pas modifier `MAX`.

# 12. Exemple complet et très simple

```c
#include <stdio.h>

int main(void) {
    int age;
    float note;
    char prenom[20];

    printf("Votre prenom : ");
    scanf("%19s", prenom);

    printf("Age : ");
    scanf("%d", &age);

    printf("Note : ");
    scanf("%f", &note);

    printf("\n--- Résultat ---\n");
    printf("Prenom : %s\n", prenom);
    printf("Age : %d\n", age);
    printf("Note : %.2f\n", note);

    return 0;
}
```

Tout ici est maîtrisable sans structures de contrôle.

### **Exercice 2 : Lire et afficher une variable**

Lire un entier `x` et afficher :

```

```

### **Exercice 4 : Tester les codes d’échappement**

Afficher un tableau aligné comme :

```
Nom     Age     Ville
Ali     20      Dakar
```