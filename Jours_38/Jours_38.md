## SQL en détail : DML

Poursuivons avec la base de données du système de sélection de cours que nous avons créée dans la leçon précédente, et explorons l'utilisation du DML (Data Manipulation Language). Le DML permet d'insérer des données dans une table (`INSERT`), de supprimer des données (`DELETE`) et de mettre à jour des données (`UPDATE`). Avant d'exécuter des commandes DML, utilisons la commande `USE` pour nous placer dans la base de données `school`.

```SQL
USE `school`;
```

### Opération INSERT

Comme son nom l'indique, `INSERT` permet d'insérer des lignes dans une table. Les méthodes d'insertion incluent : insérer une ligne complète, insérer une partie d'une ligne, insérer plusieurs lignes, ou insérer le résultat d'une requête.

Insérons une faculté dans la table `tb_college`.

```SQL
INSERT INTO `tb_college` 
VALUES
    (DEFAULT, 'Faculté d''Informatique', 'Un endroit pour apprendre l''informatique et la technologie');
```

Puisque la clé primaire de la table `tb_college` est un champ auto-incrémenté, nous utilisons `DEFAULT` pour indiquer que la colonne utilise sa valeur par défaut. Nous pouvons également utiliser la syntaxe suivante, qui est équivalente :

```SQL
INSERT INTO `tb_college` (`col_name`, `col_intro`) 
VALUES 
    ('Faculté d''Informatique', 'Un endroit pour apprendre l''informatique et la technologie');
```

**Il est recommandé d'utiliser cette deuxième approche**, car elle spécifie explicitement les colonnes à remplir. Cela permet de ne pas suivre l'ordre des colonnes défini lors de la création de la table et d'assigner les valeurs dans l'ordre des colonnes listées avant `VALUES`. Cependant, toutes les colonnes qui ne sont pas `NULL`able ou n'ont pas de valeur par défaut doivent être listées et recevoir une valeur dans le tuple après `VALUES`.

Pour insérer plusieurs enregistrements en une seule fois, nous pouvons ajouter plusieurs tuples après `VALUES` :

```SQL
INSERT INTO `tb_college` 
    (`col_name`, `col_intro`) 
VALUES 
    ('Faculté des Langues Étrangères', 'Apprendre les langues étrangères'),
    ('Faculté de Gestion Économique', 'Gérer l''économie, gouverner le pays ; science de la gestion, voie de prospérité'),
    ('Faculté des Sports', 'Développer les sports, améliorer la santé du peuple');
```

Lors de l'insertion de données, il faut veiller à ce que les **clés primaires ne soient pas dupliquées**. Si une insertion tente d'utiliser une clé primaire déjà existante, une erreur "Duplicated Entry" se produira.

Rappel : si une commande `INSERT` omet certaines colonnes, ces colonnes doivent soit avoir une valeur par défaut, soit autoriser `NULL`, sinon une erreur se produira.

Dans les systèmes de production, pour éviter que les opérations `INSERT` n'affectent les performances d'autres opérations (notamment les `SELECT`), on peut ajouter `LOW_PRIORITY` entre `INSERT` et `INTO` pour réduire la priorité de l'insertion. Cette astuce s'applique également aux opérations `DELETE` et `UPDATE`.

Supposons qu'il existe une table nommée `tb_temp` avec deux colonnes `a` et `b` contenant respectivement les noms et descriptions de facultés. Nous pouvons insérer ces données dans la table `tb_college` en utilisant une sous-requête `SELECT` (DQL) :

```SQL
INSERT INTO `tb_college`
    (`col_name`, `col_intro`)
SELECT `a`, `b` 
  FROM `tb_temp`;
```

### Opération DELETE

Pour supprimer des données d'une table, utilisez `DELETE`. Cela permet de supprimer des lignes spécifiques ou toutes les lignes. Par exemple, pour supprimer la faculté dont l'ID est `1` :

```SQL
DELETE
  FROM `tb_college`
 WHERE col_id = 1;
```

**Attention :** la clause `WHERE` est utilisée pour spécifier une condition. Seules les lignes satisfaisant cette condition seront supprimées. La commande suivante supprimerait **tous** les enregistrements de la table, ce qui est très dangereux et rarement souhaitable en production :

```SQL
DELETE
  FROM `tb_college`;
```

Même si toutes les données sont supprimées, `DELETE` ne supprime pas la table elle-même et ne réinitialise pas la valeur auto-incrémentée (AUTO_INCREMENT). Pour supprimer toutes les données **et** réinitialiser le compteur auto-incrémenté, utilisez `TRUNCATE TABLE` :

```SQL
TRUNCATE TABLE `tb_college`;
```

`TRUNCATE` supprime la table et la recrée, ce qui est généralement plus rapide car il ne supprime pas les lignes une par une. Cependant, **`TRUNCATE` est extrêmement dangereux** car il supprime toutes les données sans possibilité de restauration facile (la table originale est supprimée).

### Opération UPDATE

Pour modifier des données dans une table, utilisez `UPDATE`. Cela permet de mettre à jour des lignes spécifiques ou toutes les lignes. Par exemple, changeons le nom de l'étudiant "杨过" en "杨逍". Supposons que son numéro étudiant (`stu_id`) soit `1001` :

```SQL
UPDATE `tb_student`
   SET `stu_name` = '杨逍'
 WHERE `stu_id` = 1001;
```

**Remarques :**
- La clause `WHERE` utilise le numéro étudiant pour identifier l'enregistrement. Nous n'utilisons pas le nom comme condition de filtrage, car plusieurs étudiants pourraient s'appeler "杨过", ce qui entraînerait la mise à jour de plusieurs lignes.
- Le mot-clé `SET` est utilisé pour l'assignation. En SQL, `=` est normalement un opérateur de comparaison. Ce n'est que dans le contexte de `SET` qu'il prend la signification d'assignation.

Pour modifier à la fois le nom et la date de naissance d'un étudiant :

```SQL
UPDATE `tb_student`
   SET `stu_name` = '杨逍',
       `stu_birth` = '1975-12-29'
 WHERE `stu_id` = 1001;
```

Il est également possible d'utiliser une sous-requête dans une instruction `UPDATE` pour obtenir les données de mise à jour. Cependant, en pratique, les commandes `UPDATE` incluent presque toujours une clause `WHERE` pour éviter des mises à jour involontaires sur toute la table.



> **Note :** Les instructions `INSERT` ci-dessus utilisent l'insertion par lots, ce qui est plus efficace que d'insérer ligne par ligne.