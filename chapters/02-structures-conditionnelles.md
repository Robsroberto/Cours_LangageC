# COURS 2 — Entrées / Sorties, Opérateurs, et Structures Conditionnelles en C

# 1. Rappel essentiel : Entrées et sorties en C

Le langage C utilise principalement deux fonctions pour communiquer avec l’utilisateur :

* `printf` : affichage
* `scanf`  : lecture de valeurs

## 1.2 Lecture avec `scanf`

`scanf` lit une valeur tapée au clavier et la stocke dans une variable.

Format :

```c
scanf("format", &variable);
```

L’opérateur `&` donne l’adresse de la variable, nécessaire pour que `scanf` puisse y stocker la valeur.

Exemples :

```c
int age;
scanf("%d", &age);

double note;
scanf("%lf", &note);

char nom[20];
scanf("%19s", nom);     // lit un mot, max 19 caractères
```

## 2.1 Opérateurs arithmétiques

| Opérateur | Signification                      |
| --------- | ---------------------------------- |
| `+`       | addition                           |
| `-`       | soustraction                       |
| `*`       | multiplication                     |

Exemple :

```c
int a = 7, b = 3;
int s  = a + b;   // 10
int d  = a - b;   // 4
int p  = a * b;   // 21
int q  = a / b;   // 2
int r  = a % b;   // 1
```

Diviser deux entiers donne un résultat entier.

```c
double x = 7.0 / 3.0;
```

## 2.3 Opérateurs de comparaison

Utilisés pour tester une relation entre deux valeurs.

| Opérateur | Signification     |
| --------- | ----------------- |
| `==`      | égal à            |
| `!=`      | différent de      |
| `<`       | inférieur         |
| `>`       | supérieur         |
| `<=`      | inférieur ou égal |
| `>=`      | supérieur ou égal |

Exemples :

```c
5 < 8   // vrai
5 == 8  // faux
```

Le résultat est 1 (vrai) ou 0 (faux).

> ⚠ Ne pas confondre :
> `=` affecte une valeur
> `==` compare deux valeurs

## 2.5 Priorité des opérateurs

Pour éviter les ambiguïtés, utiliser des parenthèses :

```c
if ((a + b * c > 10) && (d == 0)) { ... }
```

## 3.1 Condition simple : `if`

```c
if (condition) {
    instructions;
}
```

Exemple :

```c
if (note >= 10) {
    printf("Admis\n");
}
```

## 3.3 Conditions multiples : `if ... else if ... else`

```c
if (note >= 16) {
    printf("Très bien\n");
}
else if (note >= 14) {
    printf("Bien\n");
}
else if (note >= 10) {
    printf("Passable\n");
}
else {
    printf("Échec\n");
}
```

# 4. Exercices d’application

## Exercice 1

Lire deux entiers et afficher leur :

* somme
* différence
* produit
* quotient entier
* reste

## Exercice 3

Lire une note (0 à 20) et afficher :

* A si note ≥ 16
* B si [14 ; 16[
* C si [10 ; 14[
* D si < 10

## Exercice 5 (switch)

Lire un entier entre 1 et 7 et afficher le jour correspondant.