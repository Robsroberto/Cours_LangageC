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



### **Travail Pratique (TP) : Gestion d'Inventaire en Langage C**

## Par Robert DIASSÉ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="../C.jpeg" alt="ISI" width="50px">

#### **Contexte :**
Vous devez développer une application en ligne de commande pour gérer l'inventaire d'une petite entreprise ou d'un magasin. Cette application doit permettre de stocker, manipuler et afficher des informations sur des produits disponibles dans l'inventaire.

---

### **Objectif :**
Mettre en pratique les concepts appris en C, notamment :
- Les **entrées/sorties**.
- Les **structures de contrôle** (conditions et boucles).
- Les **tableaux** et **tableaux de structures**.
- Les **modules** pour organiser le programme.
- Les **chaînes de caractères**.

---

### **Travail à réaliser :**

#### **1. Définition de la structure Produit**
- Créez une structure nommée `Produit` contenant les informations suivantes :
  - `code` : identifiant unique du produit (entier).
  - `nom` : nom du produit (chaîne de caractères).
  - `prix` : prix unitaire (réel).
  - `quantite` : quantité en stock (entier).

---

#### **2. Fonctionnalités demandées :**

1. **Ajouter un produit**
   - L'utilisateur saisit les informations d'un nouveau produit.
   - Ajoutez ce produit dans un tableau de structures, en vérifiant que l'inventaire n'est pas plein (limite : 100 produits).

2. **Rechercher un produit**
   - Implémentez une fonction qui permet de rechercher un produit par :
     - **Code** : affiche les informations du produit si le code est trouvé.
     - **Nom** : affiche les informations du produit si le nom correspond.

3. **Afficher l'inventaire**
   - Affichez tous les produits actuellement stockés avec leurs informations (code, nom, prix et quantité).

4. **Mettre à jour un produit**
   - Implémentez une fonction permettant de modifier :
     - Le **prix** d’un produit.
     - La **quantité** d’un produit.
   - La recherche du produit à modifier doit se faire via son **code**.

5. **Supprimer un produit**
   - Supprimez un produit de l'inventaire en le recherchant par son **code**.
   - Réorganisez le tableau pour combler l’espace laissé par le produit supprimé.

6. **Générer un rapport**
   - Calculez et affichez la **valeur totale du stock**, définie comme :
     Valeur totale = Σ (prix unitaire × quantité en stock)


---

#### **3. Organisation modulaire**
- Divisez votre programme en plusieurs fichiers pour une meilleure organisation :
  1. **`main.c`** : Gère le menu principal et appelle les fonctions appropriées.
  2. **`inventaire.h`** : Contient la définition de la structure `Produit` et les prototypes des fonctions.
  3. **`inventaire.c`** : Contient l'implémentation des fonctionnalités.

---

#### **4. Menu principal**
- Implémentez un menu interactif qui propose les options suivantes :
  ```
  === Gestion d'Inventaire ===
  1. Ajouter un produit
  2. Rechercher un produit
  3. Afficher l'inventaire
  4. Mettre à jour un produit
  5. Supprimer un produit
  6. Générer un rapport
  7. Quitter
  ```

- L'utilisateur choisit une option en entrant un numéro, et le programme exécute l'action correspondante.

---

### **Exigences techniques :**
1. Le programme doit gérer jusqu’à **100 produits**.
2. Les entrées utilisateur doivent être validées pour éviter les erreurs (par exemple, vérifier que le code d’un produit est unique lors de l’ajout).
3. L’organisation modulaire doit être respectée (séparation en fichiers).

---

### **Travail attendu :**
1. Un programme fonctionnel compilé avec succès.
2. Un code bien commenté et structuré.
3. Une gestion des erreurs utilisateur (saisie invalide, produit introuvable, etc.).
4. Une démonstration de l'application via un exemple concret (inventaire avec plusieurs produits).

---

### **Évaluation :**
- **20 points total** :
  - Définition correcte de la structure : **2 points**.
  - Fonctionnalités implémentées (ajout, recherche, affichage, mise à jour, suppression, rapport) : **12 points**.
  - Organisation modulaire : **3 points**.
  - Qualité du code (lisibilité et pertinance des éléments utilisés) : **3 points**.