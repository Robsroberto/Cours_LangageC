# COURS 3 — Les Structures Répétitives (boucles) en C

# 1. Introduction aux boucles

Une boucle permet de **répéter** une ou plusieurs instructions **tant qu’une condition est vraie**, ou **pendant un nombre de fois déterminé**.

Les boucles évitent de répéter manuellement des instructions.

Exemples de situations adaptées aux boucles :

* Afficher les nombres de 1 à 10
* Lire plusieurs valeurs
* Parcourir un tableau
* Compter, calculer, répéter une action tant qu’une condition n’est pas atteinte

## 2.1 Exemple : afficher les nombres de 1 à 5

```c
for (int i = 1; i <= 5; i++) {
    printf("%d ", i);
}
```

Explication :

* `int i = 1` → début à 1
* `i <= 5` → répéter tant que i ≤ 5
* `i++` → augmente i de 1 à chaque tour

Affichage :

```
1 2 3 4 5
```

## 2.3 Exemple : descendre de 10 à 1

```c
for (int i = 10; i >= 1; i--) {
    printf("%d ", i);
}
```

## Exercices – boucle `for`

1. Afficher les entiers de 1 à 20.
2. Afficher les multiples de 5 entre 5 et 50.
3. Lire un entier `n` et afficher les `n` premiers entiers.
4. Lire un entier `n` et afficher la table de multiplication de `n`.
5. Calculer la somme des entiers de 1 à `n`.

## 3.1 Exemple : afficher les nombres de 1 à 5

```c
int i = 1;

while (i <= 5) {
    printf("%d ", i);
    i++;
}
```

Ici, il faut **manuellement** :

* déclarer l’indice (`int i = 1`)
* mettre à jour l’indice (`i++`)

## 3.3 Exemple : afficher uniquement les pairs jusqu'à 20

```c
int i = 2;

while (i <= 20) {
    printf("%d ", i);
    i += 2;
}
```

# 4. La boucle `do … while`

Contrairement à `while`, une boucle `do … while` :

→ **exécute le bloc une première fois**,
→ vérifie la condition ensuite.

Format général :

```c
do {
    instructions;
} while (condition);
```

Elle garantit **au moins une exécution**.

## 4.2 Exemple : menu simple

```c
int choix;

do {
    printf("1: Bonjour\n");
    printf("2: Au revoir\n");
    printf("3: Quitter\n");
    printf("Votre choix : ");
    scanf("%d", &choix);
} while (choix != 3);
```

## Exercices – boucle `do...while`

3. Lire un caractère puis recommencer tant qu’il n’est pas une voyelle.
4. Lire 5 notes avec un `do...while` en utilisant un compteur.
5. Lire un nombre et compter ses chiffres.

# 6. Exercices finaux (synthèse des trois boucles)

## Exercice A

Lire un entier `n` et afficher les entiers de 1 à `n` avec un `for`.

## Exercice B

Lire un entier positif, recommencer jusqu’à ce qu’il soit valide (`while`).

## Exercice C

Créer un menu :

```
1 - Afficher bonjour
2 - Afficher un nombre aléatoire
3 - Quitter
```

Utiliser `do...while`.

## Exercice D

Calculer la somme des entiers de 1 à `n` en utilisant :

* une version `for`
* une version `while`

## Exercice E

Afficher tous les multiples de 3 entre 0 et 50.