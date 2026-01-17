## SQL en détail : DCL (Data Control Language)

Les serveurs de base de données contiennent souvent des données très sensibles. L'accès à ces données peut être contrôlé pour assurer leur sécurité, et c'est précisément le rôle du DCL. Il permet d'accorder des autorisations d'accès à des utilisateurs spécifiques ou de révoquer ces autorisations. Le DCL est crucial pour les administrateurs de base de données, car la gestion des permissions des utilisateurs est liée à la sécurité de la base de données. En résumé, grâce au DCL, nous pouvons autoriser les utilisateurs de confiance à accéder à la base de données, empêcher les utilisateurs non fiables d'y accéder, et minimiser les permissions de chaque utilisateur (principe du moindre privilège : donner juste assez de droits pour accomplir les tâches nécessaires).

### Créer un utilisateur

Nous pouvons utiliser la commande SQL suivante pour créer un utilisateur et lui attribuer un mot de passe d'accès.

```SQL
CREATE USER 'wangdachui'@'%' IDENTIFIED BY 'Wang.618';
```

La commande ci-dessus crée un utilisateur nommé `wangdachui` avec le mot de passe `Wang.618`. Cet utilisateur peut se connecter au serveur de base de données depuis **n'importe quel hôte**, car le symbole `@` est suivi du caractère générique `%` qui représente n'importe quel nombre de caractères. Si nous voulons restreindre l'accès de `wangdachui` uniquement aux hôtes du sous-réseau `192.168.0.x`, nous pouvons modifier la commande SQL comme suit :

```SQL
DROP USER IF EXISTS 'wangdachui'@'%';

CREATE USER 'wangdachui'@'192.168.0.%' IDENTIFIED BY 'Wang.618';
```

À ce stade, si nous utilisons le compte `wangdachui` pour nous connecter au serveur de base de données, nous ne pourrons pratiquement rien faire, car ce compte n'a **aucune permission**.

### Accorder des privilèges (GRANT)

Accordons à `wangdachui` l'autorisation de **lire (SELECT)** la table `tb_college` de la base de données `school` :

```SQL
GRANT SELECT ON `school`.`tb_college` TO 'wangdachui'@'192.168.0.%';
```

Nous pouvons également accorder à `wangdachui` l'autorisation de **lire toutes les tables** de la base de données `school` :

```SQL
GRANT SELECT ON `school`.* TO 'wangdachui'@'192.168.0.%';
```

Si nous souhaitons que `wangdachui` puisse aussi **insérer (INSERT)**, **supprimer (DELETE)** et **mettre à jour (UPDATE)** les données, nous pouvons procéder ainsi :

```SQL
GRANT INSERT, DELETE, UPDATE ON `school`.* TO 'wangdachui'@'192.168.0.%';
```

Pour accorder également les permissions d'exécuter des commandes DDL (créer, supprimer, modifier des tables) :

```SQL
GRANT CREATE, DROP, ALTER ON `school`.* TO 'wangdachui'@'192.168.0.%';
```

Si nous voulons donner à `wangdachui` **tous les privilèges sur toutes les bases de données et tous les objets**, nous pourrions exécuter la commande suivante. **Cependant, en pratique, cela est fortement déconseillé** car cela va à l'encontre du principe du moindre privilège :

```SQL
GRANT ALL PRIVILEGES ON *.* TO 'wangdachui'@'192.168.0.%';
```

### Révoquer des privilèges (REVOKE)

Pour révoquer les permissions `INSERT`, `DELETE` et `UPDATE` de `wangdachui` sur la base de données `school` :

```SQL
REVOKE INSERT, DELETE, UPDATE ON `school`.* FROM 'wangdachui'@'192.168.0.%';
```

Pour révoquer **tous les privilèges** :

```SQL
REVOKE ALL PRIVILEGES ON *.* FROM 'wangdachui'@'192.168.0.%';
```

**Note importante :** Les bases de données mettent souvent en cache les permissions des utilisateurs. Après avoir accordé ou révoqué des permissions, il est recommandé d'exécuter la commande suivante pour que les nouvelles permissions prennent effet immédiatement :

```SQL
FLUSH PRIVILEGES;
```