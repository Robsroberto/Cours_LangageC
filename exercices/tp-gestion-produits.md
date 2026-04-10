### **Travail Pratique (TP) : Gestion d'Inventaire en Langage C**

#### **Contexte :**
Vous devez développer une application en ligne de commande pour gérer l'inventaire d'une petite entreprise ou d'un magasin. Cette application doit permettre de stocker, manipuler et afficher des informations sur des produits disponibles dans l'inventaire.

### **Travail à réaliser :**

#### **1. Définition de la structure Produit**
- Créez une structure nommée `Produit` contenant les informations suivantes :
  - `code` : identifiant unique du produit (entier).
  - `nom` : nom du produit (chaîne de caractères).
  - `prix` : prix unitaire (réel).
  - `quantite` : quantité en stock (entier).

#### **3. Organisation modulaire**
- Divisez votre programme en plusieurs fichiers pour une meilleure organisation :
  1. **`main.c`** : Gère le menu principal et appelle les fonctions appropriées.
  2. **`inventaire.h`** : Contient la définition de la structure `Produit` et les prototypes des fonctions.
  3. **`inventaire.c`** : Contient l'implémentation des fonctionnalités.

### **Exigences techniques :**
1. Le programme doit gérer jusqu’à **100 produits**.
2. Les entrées utilisateur doivent être validées pour éviter les erreurs (par exemple, vérifier que le code d’un produit est unique lors de l’ajout).
3. L’organisation modulaire doit être respectée (séparation en fichiers).

### **Évaluation :**
- **20 points total** :
  - Définition correcte de la structure : **2 points**.
  - Fonctionnalités implémentées (ajout, recherche, affichage, mise à jour, suppression, rapport) : **12 points**.
  - Organisation modulaire : **3 points**.