# 10 Exercices DDL MySQL - Création et Modification de Schéma

## Exercice 1 - Analyser un Modèle et Créer les Tables
Voici un modèle simplifié pour une bibliothèque :
- **Livre** (isbn, titre, auteur, année, éditeur, catégorie)
- **Membre** (id, nom, email, date_inscription, statut)
- **Emprunt** (id, membre_id, livre_isbn, date_emprunt, date_retour, statut)

Relations :
- Un membre peut emprunter plusieurs livres
- Un livre peut être emprunté par plusieurs membres (mais un à la fois)

1. Dessine le diagramme ER
2. Écris le DDL pour créer ces 3 tables avec :
   - Types de données appropriés
   - Clés primaires et étrangères
   - Contraintes NOT NULL où nécessaire
   - Valeurs par défaut (ex: statut='disponible')

## Exercice 2 - Choix des Types de Données
Pour chaque scénario, choisis le type MySQL le plus approprié :

1. Numéro de téléphone français
2. Prix d'un produit (avec 2 décimales)
3. Date de naissance
4. Contenu d'un article de blog (jusqu'à 10 000 caractères)
5. Image de profil (binaire, max 1MB)
6. Statut booléen (actif/inactif)
7. Code postal (5 chiffres)
8. Pourcentage (0-100 avec 1 décimale)
9. Horodatage de dernière connexion
10. JSON stockant des métadonnées flexibles

Justifie chaque choix.

## Exercice 3 - Clés et Contraintes d'Intégrité
Dans une table `commandes` :
```sql
CREATE TABLE commandes (
    id INT,
    client_id INT,
    produit_id INT,
    quantite INT,
    date_commande DATETIME
);
```

1. Ajoute une clé primaire auto-incrémentée
2. Ajoute des clés étrangères vers `clients(id)` et `produits(id)`
3. Assure que `quantite` est > 0
4. Ajoute une contrainte UNIQUE sur `(client_id, produit_id, date_commande)`
5. Quelle erreur se produit si on supprime un client ayant des commandes ?

## Exercice 4 - Modifier une Table Existant
Table `employes` existante :
```sql
CREATE TABLE employes (
    id INT PRIMARY KEY,
    nom VARCHAR(50),
    salaire DECIMAL(10,2)
);
```

Modifications demandées :
1. Renommer la table en `salaries`
2. Ajouter colonnes `email` (UNIQUE) et `date_embauche` (DATE)
3. Changer `nom` en `nom_complet` (VARCHAR(100))
4. Ajouter une colonne `departement_id` avec clé étrangère
5. Supprimer la colonne `salaire` (déplacée vers autre table)
6. Ajouter un index sur `date_embauche`

Écris les requêtes ALTER TABLE nécessaires.

## Exercice 5 - Gestion des Clés Étrangères
Deux tables :
```sql
CREATE TABLE categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) UNIQUE
);

CREATE TABLE produits (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(100),
    categorie_id INT,
    FOREIGN KEY (categorie_id) REFERENCES categories(id)
);
```

1. Que se passe-t-on si on essaie d'insérer un produit avec `categorie_id=999` ?
2. Comment modifier la contrainte pour que la suppression d'une catégorie :
   a) Supprime automatiquement les produits associés ?
   b) Mette `categorie_id` à NULL ?
3. Quelle est la différence entre `RESTRICT` et `NO ACTION` ?
4. Comment temporairement désactiver les vérifications de clés étrangères ?

## Exercice 6 - Index et Performance
Table `logs_acces` prévue pour 100 millions de lignes :
```sql
CREATE TABLE logs_acces (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    ip_address VARCHAR(45),
    url VARCHAR(500),
    methode VARCHAR(10),
    status_code INT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

Requêtes principales :
1. `SELECT * FROM logs_acces WHERE user_id = ? ORDER BY created_at DESC`
2. `SELECT COUNT(*) FROM logs_acces WHERE created_at BETWEEN ? AND ?`
3. `SELECT user_id, COUNT(*) FROM logs_acces GROUP BY user_id`

1. Quels index créer pour optimiser ces requêtes ?
2. Écris le DDL avec les index appropriés
3. Quel impact sur l'insertion de nouvelles lignes ?
4. Comment vérifier l'utilisation des index ?

## Exercice 7 - Schéma de Base de Données Temporelle
Pour un système de réservation de salles :
- **Salle** (id, nom, capacité, équipements)
- **Réservation** (id, salle_id, utilisateur_id, date_debut, date_fin, statut)
- **Événement périodique** (id, salle_id, jour_semaine, heure_debut, heure_fin)

1. Conçois les tables avec contraintes d'intégrité temporelle
2. Comment empêcher les réservations qui se chevauchent ?
3. Quel type utiliser pour `date_debut`/`date_fin` ?
4. Comment gérer les événements récurrents ?

## Exercice 8 - Normalisation
Table non normalisée `commandes_details` :
```sql
CREATE TABLE commandes_details (
    commande_id INT,
    client_nom VARCHAR(100),
    client_email VARCHAR(100),
    produit_nom VARCHAR(100),
    categorie_nom VARCHAR(50),
    quantite INT,
    prix_unitaire DECIMAL(10,2),
    total DECIMAL(10,2)
);
```

Problèmes : redondance, anomalies d'insertion/suppression/mise à jour.

1. Normalise en 3NF (Forme Normale Troisième)
2. Identifie les dépendances fonctionnelles
3. Crée les nouvelles tables avec DDL
4. Quelle est la forme normale maximale atteinte ?

## Exercice 9 - Partitionnement
Table `mesures_capteurs` avec 1 milliard de lignes :
- Données de capteurs IoT
- Chaque capteur envoie des données toutes les 5 minutes
- Requêtes toujours filtrées par `date_mesure`

1. Quels types de partitionnement sont possibles ?
2. Écris le DDL pour partitionner par mois
3. Quels avantages/inconvénients du partitionnement ?
4. Comment gérer l'archivage des anciennes données ?

## Exercice 10 - Audit et Métadonnées
Besoin : suivre toutes les modifications de structure

1. Crée une table `audit_ddl` qui enregistre :
   - Date/heure de modification
   - Utilisateur
   - Type d'opération (CREATE, ALTER, DROP)
   - Objet modifié
   - Requête SQL exécutée
2. Comment déclencher automatiquement l'insertion dans `audit_ddl` ?
3. Quelle vue système contient les métadonnées des tables ?
4. Comment générer un script de toutes les contraintes ?

---

**Méthode de travail :**

1. **Planifier** : Toujours faire un diagramme ER d'abord
2. **Prototyper** : Tester le DDL dans un environnement de développement
3. **Vérifier** : Utiliser `SHOW CREATE TABLE` et `DESCRIBE`
4. **Documenter** : Ajouter des COMMENT à chaque table/colonne
5. **Versionner** : Garder les scripts DDL dans Git

**Pièges courants à éviter :**
- Oublier les indexes sur les clés étrangères
- Utiliser VARCHAR(255) par défaut sans réfléchir
- Négliger le collation (utf8mb4_unicode_ci recommandé)
- Créer des tables sans penser aux performances futures
- Ignorer la sécurité (mots de passe en clair, permissions)