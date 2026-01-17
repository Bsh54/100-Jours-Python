# 10 Exercices DCL MySQL - Gestion des Permissions

## Exercice 1 - Analyse des Rôles d'une Application Web
Une application web a trois types d'utilisateurs :
1. **AppUser** : L'application elle-même, doit pouvoir lire/écrire dans toutes les tables sauf `users`
2. **ReportUser** : Génération de rapports, seulement SELECT sur toutes les tables
3. **AdminUser** : Administration, tous les droits sur toutes les tables

La base `ecommerce` contient : `products`, `orders`, `customers`, `users`

1. Crée les 3 utilisateurs avec des mots de passe sécurisés
2. Donne les permissions appropriées à chaque rôle
3. Teste que chaque utilisateur a exactement les droits nécessaires
4. Quel est le risque de donner `ALL PRIVILEGES` à AppUser ?

## Exercice 2 - Contrôle Granulaire des Permissions
Dans une base `hospital` avec ces tables :
- `patients` (données sensibles)
- `doctors` 
- `appointments`
- `medical_records`

Besoin :
- Les médecins peuvent lire/écrire leurs rendez-vous
- Les médecins peuvent lire/mettre à jour les dossiers médicaux de leurs patients
- Les administrateurs peuvent tout faire sauf supprimer des patients
- Les analystes peuvent seulement lire (SELECT) toutes les tables

1. Crée les utilisateurs correspondants
2. Accorde les permissions les plus précises possibles
3. Comment gérer le "leurs" (doctors ne voit que ses propres données) ?

## Exercice 3 - Permissions au Niveau des Colonnes
Table `employees` avec colonnes sensibles :
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    salary DECIMAL(10,2),
    ssn VARCHAR(20),  -- Numéro de sécurité sociale
    performance_rating INT
);
```

Besoin :
- HR peut voir toutes les colonnes
- Managers peuvent voir tout sauf `salary` et `ssn`
- Team Leads peuvent voir tout sauf `ssn`

1. Accorde ces permissions au niveau des colonnes
2. Quelles sont les limitations des permissions par colonnes ?
3. Comment vérifier qu'un utilisateur ne peut pas voir une colonne spécifique ?

## Exercice 4 - Procédures Stockées et Sécurité
Au lieu de donner un accès direct aux tables, on utilise des procédures stockées :

1. Crée une procédure `get_customer_orders(customer_id)` qui retourne les commandes d'un client
2. Crée un utilisateur `api_user` qui peut EXECUTE cette procédure mais pas SELECT sur `orders`
3. Quel est l'avantage de cette approche ?
4. Comment gérer les permissions pour les procédures qui modifient des données ?

## Exercice 5 - Vues comme Mécanisme de Sécurité
Crée des vues sécurisées :
```sql
-- Vue pour les données publiques des produits
CREATE VIEW public_products AS
SELECT id, name, price, category FROM products WHERE is_active = 1;

-- Vue pour les statistiques internes
CREATE VIEW sales_stats AS
SELECT product_id, SUM(quantity) as total_sold, AVG(price) as avg_price
FROM orders GROUP BY product_id;
```

1. Crée un utilisateur `public_user` qui peut seulement SELECT sur `public_products`
2. Crée un utilisateur `analyst` qui peut SELECT sur `sales_stats`
3. Les utilisateurs ont-ils besoin de permissions sur les tables sous-jacentes ?
4. Quelle est la différence entre GRANT sur une vue vs sur une table ?

## Exercice 6 - Audit des Permissions
Dans un environnement de production :

1. Comment lister tous les utilisateurs et leurs permissions ?
2. Quelles requêtes pour voir :
   - Les utilisateurs qui peuvent DROP des tables
   - Les utilisateurs avec accès à des données sensibles
   - Les permissions globales (sur *.*)
3. Comment détecter les permissions excessives ?
4. Crée un rapport automatique des permissions

## Exercice 7 - Rotation des Identifiants
Politique de sécurité : rotation des mots de passe tous les 90 jours

1. Comment forcer un utilisateur à changer son mot de passe ?
2. Comment expirer un mot de passe après une durée définie ?
3. Que se passe-t-il si un mot de passe expire ?
4. Comment gérer l'historique des mots de passes (empêcher la réutilisation) ?

## Exercice 8 - Contrôle d'Accès par Hôte
Sécurité réseau : restreindre l'accès par IP

1. Crée un utilisateur qui ne peut se connecter que depuis `192.168.1.%`
2. Crée un utilisateur qui peut se connecter depuis n'importe où sauf `10.0.0.%`
3. Comment bloquer complètement un hôte malveillant ?
4. Quelle est la différence entre `'user'@'192.168.1.100'` et `'user'@'192.168.1.%'` ?

## Exercice 9 - Rôles MySQL 8.0+
MySQL 8.0 introduit les rôles :

1. Crée des rôles : `read_only`, `data_entry`, `manager`
2. Accorde des permissions à chaque rôle
3. Assigne les rôles aux utilisateurs appropriés
4. Comment activer/désactiver des rôles pour une session ?
5. Quels sont les avantages des rôles vs permissions directes ?

## Exercice 10 - Scénario de Sécurité Complet
Une startup a ces besoins :
- Développeurs : accès en lecture à la production (pour debug)
- Application mobile : accès limité à l'API
- Backup système : besoin de SELECT et LOCK TABLES
- Monitoring : besoin de PROCESS et REPLICATION CLIENT
- Pentest : utilisateur temporaire avec limites de temps

1. Conçois la stratégie de permissions
2. Crée tous les utilisateurs avec leurs permissions
3. Ajoute des limites (max queries per hour, max connections)
4. Planifie la révision trimestrielle des permissions
5. Quel outil utiliser pour auditer régulièrement ?

---

**Bonnes pratiques à retenir :**

1. **Principe du moindre privilège** : Donner seulement les permissions nécessaires
2. **Séparation des rôles** : Un utilisateur = un rôle bien défini
3. **Revue régulière** : Auditer les permissions périodiquement
4. **Journalisation** : Activer le log des accès
5. **Défense en profondeur** : Combiner permissions SQL + vues + procédures

**Commandes utiles :**
```sql
-- Voir ses propres permissions
SHOW GRANTS;

-- Voir les permissions d'un autre utilisateur
SHOW GRANTS FOR 'user'@'host';

-- Voir tous les utilisateurs
SELECT user, host FROM mysql.user;

-- Voir les permissions détaillées
SELECT * FROM mysql.db WHERE user = 'username';
```

**Questions de réflexion :**
1. Pourquoi ne pas utiliser le compte root pour l'application ?
2. Comment gérer les permissions dans un environnement CI/CD ?
3. Quelle est la procédure en cas de compromission d'un compte ?
4. Comment versionner les changements de permissions ?