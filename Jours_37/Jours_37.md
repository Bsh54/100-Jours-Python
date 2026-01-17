## SQL en détail : DDL

Le SQL est généralement divisé en quatre catégories : **DDL** (Data Definition Language - langage de définition de données), **DML** (Data Manipulation Language - langage de manipulation de données), **DCL** (Data Control Language - langage de contrôle de données) et **TCL** (Transaction Control Language - langage de contrôle des transactions). Le DDL est principalement utilisé pour créer, supprimer et modifier des objets dans la base de données, comme créer, supprimer et modifier des tables. Les mots-clés principaux sont `create`, `drop` et `alter`. Le DML est responsable de l'insertion, suppression, mise à jour et interrogation des données, avec les mots-clés `insert`, `delete`, `update` et `select`. Le DCL sert à accorder et révoquer des autorisations, les mots-clés principaux étant `grant` et `revoke`. Le TCL est utilisé pour le contrôle des transactions.

> **Note :** Le SQL est un langage insensible à la casse. Généralement, il est recommandé d'écrire les mots-clés en majuscules et le reste en minuscules. Si l'entreprise a des conventions de codage spécifiques, suivez-les. Les préférences personnelles ne doivent pas primer sur les normes de l'entreprise, ce qui est une notion de base pour un professionnel.

### Créer une base de données et des tables

Implémentons une base de données simple pour un système de sélection de cours d'une école. Nous nommerons la base de données `school`. Les quatre entités principales sont : la faculté (college), les enseignants (teacher), les étudiants (student) et les cours (course). Un étudiant appartient à une faculté, relation de type plusieurs-à-un (many-to-one), car une faculté peut avoir plusieurs étudiants, et un étudiant n'appartient généralement qu'à une seule faculté. De même, la relation entre enseignant et faculté est aussi plusieurs-à-un. Un enseignant peut donner plusieurs cours, et si un cours n'est enseigné que par un seul professeur, la relation cours-enseignant est également plusieurs-à-un. Pour simplifier, nous concevons la relation cours-enseignant comme plusieurs-à-un. La relation étudiant-cours est typiquement plusieurs-à-plusieurs (many-to-many), car un étudiant peut choisir plusieurs cours et un cours peut être choisi par plusieurs étudiants. Les bases de données relationnelles nécessitent une table de jonction (table d'association) pour gérer une relation plusieurs-à-plusieurs. Finalement, notre système scolaire comportera cinq tables : `tb_college` (faculté), `tb_student` (étudiant), `tb_teacher` (enseignant), `tb_course` (cours) et `tb_record` (enregistrement de sélection de cours), où `tb_record` est la table de jonction gérant la relation plusieurs-à-plusieurs entre étudiants et cours.

```SQL
-- Supprime la base de données 'school' si elle existe déjà.
DROP DATABASE IF EXISTS `school`;

-- Crée la base de données 'school' avec l'encodage par défaut utf8mb4 et la collation utf8mb4_general_ci.
CREATE DATABASE `school` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;

-- Utilise la base de données 'school'.
USE `school`;

-- Crée la table des facultés.
CREATE TABLE `tb_college`
(
`col_id`    int unsigned AUTO_INCREMENT      COMMENT 'ID',
`col_name`  varchar(50)  NOT NULL            COMMENT 'Nom',
`col_intro` varchar(500) NOT NULL DEFAULT '' COMMENT 'Description',
PRIMARY KEY (`col_id`)
);

-- Crée la table des étudiants.
CREATE TABLE `tb_student`
(
`stu_id`    int unsigned NOT NULL           COMMENT 'Numéro étudiant',
`stu_name`  varchar(20)  NOT NULL           COMMENT 'Nom',
`stu_sex`   boolean      NOT NULL DEFAULT 1 COMMENT 'Sexe (1 pour homme, 0 pour femme)',
`stu_birth` date         NOT NULL           COMMENT 'Date de naissance',
`stu_addr`  varchar(255) DEFAULT ''         COMMENT 'Lieu d''origine',
`col_id`    int unsigned NOT NULL           COMMENT 'ID de la faculté',
PRIMARY KEY (`stu_id`),
CONSTRAINT `fk_student_col_id` FOREIGN KEY (`col_id`) REFERENCES `tb_college` (`col_id`)
);

-- Crée la table des enseignants.
CREATE TABLE `tb_teacher`
(
`tea_id`    int unsigned NOT NULL                COMMENT 'Numéro employé',
`tea_name`  varchar(20)  NOT NULL                COMMENT 'Nom',
`tea_title` varchar(10)  NOT NULL DEFAULT '助教' COMMENT 'Titre (Assistant par défaut)',
`col_id`    int unsigned NOT NULL                COMMENT 'ID de la faculté',
PRIMARY KEY (`tea_id`),
CONSTRAINT `fk_teacher_col_id` FOREIGN KEY (`col_id`) REFERENCES `tb_college` (`col_id`)
);

-- Crée la table des cours.
CREATE TABLE `tb_course`
(
`cou_id`     int unsigned NOT NULL COMMENT 'ID',
`cou_name`   varchar(50)  NOT NULL COMMENT 'Nom',
`cou_credit` int          NOT NULL COMMENT 'Crédits',
`tea_id`     int unsigned NOT NULL COMMENT 'ID de l''enseignant',
PRIMARY KEY (`cou_id`),
CONSTRAINT `fk_course_tea_id` FOREIGN KEY (`tea_id`) REFERENCES `tb_teacher` (`tea_id`)
);

-- Crée la table des enregistrements de sélection de cours.
CREATE TABLE `tb_record`
(
`rec_id`   bigint unsigned AUTO_INCREMENT COMMENT 'ID d''enregistrement',
`stu_id`   int unsigned    NOT NULL       COMMENT 'Numéro étudiant',
`cou_id`   int unsigned    NOT NULL       COMMENT 'ID du cours',
`sel_date` date            NOT NULL       COMMENT 'Date de sélection',
`score`    decimal(4,1)                   COMMENT 'Note',
PRIMARY KEY (`rec_id`),
CONSTRAINT `fk_record_stu_id` FOREIGN KEY (`stu_id`) REFERENCES `tb_student` (`stu_id`),
CONSTRAINT `fk_record_cou_id` FOREIGN KEY (`cou_id`) REFERENCES `tb_course` (`cou_id`),
CONSTRAINT `uk_record_stu_cou` UNIQUE (`stu_id`, `cou_id`)
);
```

Quelques points à souligner dans le DDL ci-dessus :

- Les noms de base de données, de tables et de colonnes sont entourés de **backticks** (\`). Ce n'est pas obligatoire, mais cela évite les conflits avec les mots-clés SQL réservés.
- Lors de la création de la base de données, nous spécifions l'encodage par défaut `utf8mb4` (UTF-8 sur 4 octets maximum). C'est l'encodage par défaut de MySQL 8.x, recommandé car il prend en charge l'internationalisation, y compris les caractères Emoji.
- Les mots-clés `database` et `schema` sont interchangeables pour créer ou supprimer une base de données.
- `NOT NULL` est une contrainte de non-nullité. `DEFAULT` définit une valeur par défaut. `PRIMARY KEY` définit la clé primaire (identifiant unique). `FOREIGN KEY` définit une clé étrangère assurant l'intégrité référentielle entre les tables. `CONSTRAINT` permet de nommer une contrainte.
- `COMMENT` ajoute un commentaire à une colonne ou une table, améliorant la lisibilité.
- Le moteur de stockage par défaut dans MySQL 5.5+ est **InnoDB**, recommandé pour sa prise en charge des transactions, du verrouillage au niveau des lignes et des clés étrangères. Il peut être spécifié avec `ENGINE=InnoDB` à la fin de la déclaration `CREATE TABLE`.
- Pour choisir le type de données approprié, utilisez `? data types` (ou `HELP data types` dans MySQL Workbench) pour obtenir des informations sur les types de données disponibles.
  - Pour les chaînes de caractères : `VARCHAR` (taille variable) et `CHAR` (taille fixe). Pour de très grands textes, utilisez `TEXT` (et ses variantes `MEDIUMTEXT`, `LONGTEXT`). Pour des données binaires volumineuses, utilisez `BLOB`.
  - Pour les nombres à virgule flottante : `FLOAT` (déconseillé) ou `DOUBLE`. Pour les nombres à virgule fixe (monnaie, précision exacte) : `DECIMAL`.
  - Pour les dates/heures : `DATETIME` (plage plus large) est préférable à `TIMESTAMP` (limité à 2038).
- `AUTO_INCREMENT` génère automatiquement des identifiants uniques incrémentiels. Attention aux problèmes de récupération d'ID dans MySQL 5.x (résolus en 8.x). Pour les systèmes à haute concurrence, envisagez des algorithmes de génération d'ID distribués (Snowflake, etc.).

### Supprimer et modifier des tables

Prenons la table `tb_student` comme exemple pour illustrer la suppression et la modification.

**Supprimer une table** avec `DROP TABLE` :

```SQL
DROP TABLE `tb_student`;
-- ou
DROP TABLE IF EXISTS `tb_student`;
```

> **Note :** Si la table contient des données référencées par d'autres tables (via des clés étrangères), la suppression échouera.

**Modifier une table** avec `ALTER TABLE` :

1. **Ajouter une colonne** (exemple : ajouter un numéro de téléphone) :

   ```SQL
   ALTER TABLE `tb_student` ADD COLUMN `stu_tel` varchar(20) NOT NULL COMMENT 'Téléphone';
   ```
   > **Attention :** Ajouter une colonne `NOT NULL` à une table qui contient déjà des données provoquera une erreur, car les lignes existantes n'auront pas de valeur pour cette colonne. Utilisez `DEFAULT` pour fournir une valeur par défaut, ou ajoutez la colonne sans `NOT NULL`, puis mettez à jour les données.

2. **Supprimer une colonne** :

   ```SQL
   ALTER TABLE `tb_student` DROP COLUMN `stu_tel`;
   ```

3. **Modifier le type de données d'une colonne** (exemple : changer `stu_sex` en `char`) :

   ```SQL
   ALTER TABLE `tb_student` MODIFY COLUMN `stu_sex` char(1) NOT NULL DEFAULT 'M' COMMENT 'Sexe';
   ```

4. **Renommer une colonne** (exemple : `stu_sex` devient `stu_gender`) :

   ```SQL
   ALTER TABLE `tb_student` CHANGE COLUMN `stu_sex` `stu_gender` boolean DEFAULT 1 COMMENT 'Sexe';
   ```

5. **Supprimer une contrainte de clé étrangère** :

   ```SQL
   ALTER TABLE `tb_student` DROP FOREIGN KEY `fk_student_col_id`;
   ```

6. **Ajouter une contrainte de clé étrangère** :

   ```SQL
   ALTER TABLE `tb_student` ADD FOREIGN KEY (`col_id`) REFERENCES `tb_college` (`col_id`);
   -- ou avec un nom de contrainte personnalisé
   ALTER TABLE `tb_student` ADD CONSTRAINT `fk_student_col_id` FOREIGN KEY (`col_id`) REFERENCES `tb_college` (`col_id`);
   ```

   > **Note :** Lors de l'ajout d'une clé étrangère, vous pouvez spécifier le comportement `ON UPDATE` et `ON DELETE`. Les valeurs possibles sont :
   > - `RESTRICT` (par défaut) : Interdit la mise à jour/suppression de la ligne référencée.
   > - `CASCADE` : Met à jour/supprime automatiquement les lignes correspondantes dans la table enfant.
   > - `SET NULL` : Met à `NULL` la clé étrangère dans la table enfant.
   > - `NO ACTION` : Similaire à `RESTRICT`.

7. **Renommer une table** (exemple : `tb_student` devient `tb_stu_info`) :

   ```SQL
   ALTER TABLE `tb_student` RENAME TO `tb_stu_info`;
   ```

> **Conseil :** En général, évitez de renommer des bases de données ou des tables en production, car cela peut casser des applications ou des scripts qui y font référence.