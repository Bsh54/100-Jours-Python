# 10 Exercices MySQL pour la Maîtrise

## Exercice 1 - Modélisation Conceptuelle
Un site de vente en ligne a besoin d'une base de données pour :
- Gérer les clients (nom, email, adresse)
- Suivre les commandes (date, statut, montant)
- Gérer les produits (nom, prix, stock)
- Enregistrer les articles de commande (quantité, prix au moment de l'achat)

1. Dessine le diagramme entité-relation (ER) avec les relations appropriées
2. Identifie les cardinalités (1:1, 1:N, M:N)
3. Propose les clés primaires et étrangères
4. Quelle table intermédiaire serait nécessaire ?

## Exercice 2 - Installation et Configuration Critique
Après avoir installé MySQL 8.0 sur un serveur Linux :

1. Quelles commandes pour vérifier que le service est bien démarré ?
2. Comment sécuriser l'installation initiale ?
3. Quel fichier de configuration modifier pour :
   - Changer le port par défaut
   - Activer les logs des requêtes lentes
   - Limiter les connexions simultanées
4. Comment créer un utilisateur sans accès root ?

## Exercice 3 - DDL : Création de Tables
À partir du modèle ER de l'exercice 1 :

1. Écris le SQL pour créer les tables avec :
   - Types de données appropriés (INT, VARCHAR, DECIMAL, DATE, etc.)
   - Contraintes NOT NULL, UNIQUE, CHECK
   - Clés primaires et étrangères
   - Index sur les colonnes fréquemment recherchées
2. Quelle différence entre CHAR et VARCHAR ?
3. Quand utiliser DATETIME vs TIMESTAMP ?

## Exercice 4 - DML : Opérations CRUD de Base
Avec ces tables :
```sql
CREATE TABLE produits (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(100) NOT NULL,
    prix DECIMAL(10,2) CHECK (prix > 0),
    stock INT DEFAULT 0,
    categorie VARCHAR(50)
);

CREATE TABLE commandes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    client_id INT,
    date_commande DATE DEFAULT (CURRENT_DATE),
    total DECIMAL(10,2)
);
```

1. Insère 5 produits différents
2. Augmente le prix de tous les produits de 10%
3. Baisse le stock de 2 unités pour le produit avec id=3
4. Supprime les produits dont le stock est à 0
5. Trouve tous les produits entre 10€ et 50€

## Exercice 5 - Jointures Complexes
Données : `clients`, `commandes`, `articles_commande`, `produits`

1. Liste tous les clients avec leur nombre total de commandes
2. Trouve les produits jamais commandés
3. Calcule le chiffre d'affaires par client
4. Identifie les 3 produits les plus vendus
5. Trouve les clients qui ont commandé au moins 3 fois

Quels types de JOIN utiliser dans chaque cas ?

## Exercice 6 - Agrégations et Groupements
Analyse des ventes mensuelles :

1. Calcule le chiffre d'affaires mensuel
2. Trouve le mois avec le plus grand nombre de commandes
3. Calcule la moyenne du panier par client
4. Identifie les produits vendus en moins de 10 unités par mois
5. Trouve la catégorie de produits la plus rentable

Quand utiliser HAVING vs WHERE avec GROUP BY ?

## Exercice 7 - Sous-requêtes et Vues
1. Crée une vue `chiffre_affaires_client` qui montre le CA total par client
2. Utilise une sous-requête pour trouver les clients ayant dépensé plus que la moyenne
3. Crée une vue `stock_critique` pour les produits avec moins de 5 unités
4. Avec une CTE (Common Table Expression), calcule le classement des vendeurs
5. Quelle est la différence entre une vue et une table temporaire ?

## Exercice 8 - Transactions et Intégrité
Scénario : Un client passe une commande :
1. Crée la commande
2. Ajoute les articles
3. Met à jour le stock
4. Calcule et met à jour le total

1. Comment encapsuler ces opérations dans une transaction ?
2. Quels niveaux d'isolation choisir et pourquoi ?
3. Comment gérer les erreurs (ROLLBACK) ?
4. Quels verrous utiliser pour éviter les problèmes de concurrence ?

## Exercice 9 - Indexation et Performance
Une table `logs` avec 10 millions de lignes :
```sql
CREATE TABLE logs (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    action VARCHAR(50),
    timestamp DATETIME,
    details JSON
);
```

Les requêtes principales sont :
- Chercher par `user_id`
- Chercher par `action` et `timestamp`
- Agrégations par jour

1. Quels index créer et pourquoi ?
2. Comment mesurer l'efficacité d'un index ?
3. Quels sont les inconvénients d'ajouter trop d'index ?
4. Quand utiliser un index composite vs multiple index simples ?

## Exercice 10 - Sauvegarde et Récupération
Un serveur MySQL en production :

1. Quelle stratégie de backup mettre en place ?
2. Comment faire un backup à chaud sans interrompre le service ?
3. Procédure de restauration après une suppression accidentelle
4. Comment tester régulièrement les backups ?
5. Quels outils utiliser pour la réplication (master-slave) ?

---

**Méthode d'apprentissage recommandée :**

1. **Pratique immédiate** : Exécute chaque requête pour voir le résultat
2. **Comprendre l'exécution** : Utilise `EXPLAIN` pour voir les plans d'exécution
3. **Test de charge** : Crée des grandes tables pour tester les performances
4. **Journal d'apprentissage** : Note les erreurs et leurs solutions
5. **Projet réel** : Crée une petite base de données pour un besoin personnel

**Points clés à retenir :**
- ACID : Atomicité, Cohérence, Isolation, Durabilité
- Normalisation : Évite la redondance, préserve l'intégrité
- Index : Améliore la lecture, ralentit l'écriture
- Transactions : Garantit la cohérence en cas d'erreur
- Sécurité : Moins de privilèges possible, toujours des backups