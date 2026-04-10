# Les Chaînes de Caractères en C

## 1. Principe

En C, une chaîne de caractères est un **tableau de `char`** terminé par le caractère nul `'\0'`.

```c
char prenom[10] = "Alice";
// En mémoire : ['A','l','i','c','e','\0', ?, ?, ?, ?]
```

---

## 2. Déclaration et initialisation

```c
// Avec taille explicite
char nom[20] = "Empire du Web";

// Taille automatique
char ville[] = "Dakar";

// Pointeur (chaîne constante, non modifiable)
char *msg = "Bonjour";

// Caractère par caractère
char s[4];
s[0] = 'O'; s[1] = 'k'; s[2] = '!'; s[3] = '\0';
```

---

## 3. Lire et afficher

```c
#include <stdio.h>

int main() {
    char nom[50];

    printf("Entrez votre nom : ");
    scanf("%49s", nom);          // Lit jusqu'à l'espace
    printf("Bonjour %s !\n", nom);

    // Lire une ligne complète (avec espaces)
    char phrase[100];
    printf("Entrez une phrase : ");
    fgets(phrase, 100, stdin);
    printf("Phrase : %s", phrase);

    return 0;
}
```

---

## 4. Fonctions essentielles de `<string.h>`

```c
#include <stdio.h>
#include <string.h>

int main() {
    char s1[50] = "Bonjour";
    char s2[]   = " le monde";
    char s3[50];

    // Longueur (ne compte pas le '\0')
    printf("strlen  : %lu\n", strlen(s1));     // 7

    // Copie
    strcpy(s3, s1);
    printf("strcpy  : %s\n", s3);              // Bonjour

    // Copie sécurisée (N caractères max)
    strncpy(s3, s1, 3);
    s3[3] = '\0';
    printf("strncpy : %s\n", s3);              // Bon

    // Concaténation
    strcat(s1, s2);
    printf("strcat  : %s\n", s1);              // Bonjour le monde

    // Comparaison (0 si égales)
    printf("strcmp  : %d\n", strcmp("abc", "abc"));  // 0
    printf("strcmp  : %d\n", strcmp("abc", "abd"));  // négatif

    // Recherche d'un caractère
    char *p = strchr(s1, 'l');
    if (p) printf("strchr  : %s\n", p);        // le monde

    // Recherche d'une sous-chaîne
    char *q = strstr(s1, "monde");
    if (q) printf("strstr  : %s\n", q);        // monde

    return 0;
}
```

---

## 5. Manipulation caractère par caractère

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char s[] = "Bonjour le Monde";
    int n = strlen(s);

    // Compter les voyelles
    int voyelles = 0;
    for (int i = 0; i < n; i++) {
        char c = tolower(s[i]);
        if (c=='a'||c=='e'||c=='i'||c=='o'||c=='u') voyelles++;
    }
    printf("Voyelles : %d\n", voyelles);

    // Mettre en majuscules
    for (int i = 0; i < n; i++)
        s[i] = toupper(s[i]);
    printf("Majuscules : %s\n", s);

    // Inverser
    for (int i = 0; i < n / 2; i++) {
        char tmp = s[i];
        s[i]     = s[n - 1 - i];
        s[n-1-i] = tmp;
    }
    printf("Inversé : %s\n", s);

    return 0;
}
```

---

## 6. Tableau de chaînes

```c
#include <stdio.h>

int main() {
    char jours[7][10] = {
        "Lundi", "Mardi", "Mercredi",
        "Jeudi", "Vendredi", "Samedi", "Dimanche"
    };

    for (int i = 0; i < 7; i++)
        printf("Jour %d : %s\n", i + 1, jours[i]);

    return 0;
}
```

---

## 7. Conversion chaîne <-> nombre

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char s1[] = "42";
    int  n    = atoi(s1);         // Chaîne → entier
    printf("atoi   : %d\n", n);

    char s2[] = "3.14";
    double f  = atof(s2);         // Chaîne → flottant
    printf("atof   : %.2f\n", f);

    char buf[20];
    sprintf(buf, "%d", 1234);     // Entier → chaîne
    printf("sprintf: %s\n", buf);

    return 0;
}
```

---

## Résumé des fonctions essentielles

| Fonction | Rôle |
|----------|------|
| `strlen(s)` | Longueur (sans `\0`) |
| `strcpy(dst, src)` | Copier src dans dst |
| `strncpy(dst, src, n)` | Copier au plus n caractères |
| `strcat(s1, s2)` | Concaténer s2 à la fin de s1 |
| `strcmp(s1, s2)` | Comparer (0 = égales) |
| `strchr(s, c)` | Chercher un caractère |
| `strstr(s1, s2)` | Chercher une sous-chaîne |
| `fgets(s, n, stdin)` | Lire une ligne complète |
| `atoi(s)` | Chaîne → entier |
| `sprintf(buf, fmt, ...)` | Écrire une valeur dans une chaîne |
