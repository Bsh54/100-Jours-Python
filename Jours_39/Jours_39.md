## SQL en détail : DQL (Data Query Language)

Nous allons maintenant utiliser la base de données du système de sélection de cours créée précédemment pour illustrer l'opération de requête du DML. La requête est essentielle, que l'on soit développeur ou analyste de données, car elle permet d'extraire les informations nécessaires d'une base de données relationnelle. Assurez-vous d'avoir exécuté le DDL de création de la base et des tables (avant-dernière leçon) ainsi que le DML d'insertion des données (dernière leçon) pour que les tables et les données soient correctes avant de procéder.

```SQL
USE school;

-- Sélectionner toutes les informations de tous les étudiants
SELECT stu_id,
       stu_name,
       stu_sex,
       stu_birth,
       stu_addr,
       col_id
  FROM tb_student;

-- Sélectionner le numéro, le nom et le lieu d'origine des étudiants (projection et alias)
SELECT stu_id AS numéro_étudiant,
       stu_name AS nom,
       stu_addr AS origine
  FROM tb_student;

-- Sélectionner le nom et les crédits de tous les cours (projection et alias)
SELECT cou_name AS nom_cours,
       cou_credit AS crédits
  FROM tb_course;

-- Sélectionner le nom et la date de naissance de toutes les étudiantes (filtrage)
SELECT stu_name,
       stu_birth
  FROM tb_student
 WHERE stu_sex = 0;

-- Sélectionner le nom et la date de naissance des étudiantes originaires de "四川成都" (filtrage)
SELECT stu_name,
       stu_birth
  FROM tb_student
 WHERE stu_sex = 0
       AND stu_addr = '四川成都';

-- Sélectionner les étudiants originaires de "四川成都" OU de sexe féminin (filtrage)
SELECT stu_name,
       stu_birth
  FROM tb_student
 WHERE stu_sex = 0
       OR stu_addr = '四川成都';

-- Sélectionner le nom, le sexe et la date de naissance de tous les étudiants nés dans les années 80 (filtrage)
SELECT stu_name,
       stu_sex,
       stu_birth
  FROM tb_student
 WHERE '1980-01-01' <= stu_birth 
       AND stu_birth <= '1989-12-31';
       
SELECT stu_name,
       stu_sex,
       stu_birth
  FROM tb_student
 WHERE stu_birth BETWEEN '1980-01-01' AND '1989-12-31';

-- Sélectionner le nom et les crédits des cours ayant plus de 2 crédits (filtrage)
SELECT cou_name,
	   cou_credit
  FROM tb_course
 WHERE cou_credit > 2;

-- Sélectionner le nom et les crédits des cours dont le nombre de crédits est impair (filtrage)
SELECT cou_name,
	   cou_credit
  FROM tb_course
 WHERE cou_credit MOD 2 <> 0;

-- Sélectionner les numéros d'étudiants ayant une note supérieure à 90 au cours 1111 (filtrage)
SELECT stu_id
  FROM tb_record
 WHERE cou_id = 1111
       AND score > 90;

-- Sélectionner le nom et le sexe de l'étudiant nommé "杨过" (filtrage)
SELECT stu_name AS nom, 
       CASE stu_sex WHEN 1 THEN '男' ELSE '女' END AS sexe
  FROM tb_student
 WHERE stu_name = '杨过';
 
SELECT stu_name AS nom, 
       IF(stu_sex, '男', '女') AS sexe
  FROM tb_student
 WHERE stu_name = '杨过';
    
-- Sélectionner le nom et le sexe des étudiants dont le nom de famille est "杨" (correspondance approximative)
-- Le caractère générique % correspond à zéro ou plusieurs caractères.
SELECT stu_name AS nom, 
       CASE stu_sex WHEN 1 THEN '男' ELSE '女' END AS sexe
  FROM tb_student
 WHERE stu_name LIKE '杨%';

-- Sélectionner le nom et le sexe des étudiants dont le nom de famille est "杨" et le prénom comporte deux caractères (correspondance approximative)
-- Le caractère générique _ correspond à un seul caractère.
SELECT stu_name AS nom, 
       CASE stu_sex WHEN 1 THEN '男' ELSE '女' END AS sexe
  FROM tb_student
 WHERE stu_name LIKE '杨_';

-- Sélectionner le nom et le sexe des étudiants dont le nom de famille est "杨" et le prénom comporte trois caractères (correspondance approximative)
SELECT stu_name AS nom, 
       CASE stu_sex WHEN 1 THEN '男' ELSE '女' END AS sexe
  FROM tb_student
 WHERE stu_name LIKE '杨__';
 
-- Sélectionner le numéro et le nom des étudiants dont le numéro se termine par 3 (correspondance approximative)
SELECT stu_id,
       stu_name
  FROM tb_student
 WHERE stu_id LIKE '%3';

-- Sélectionner le numéro et le nom des étudiants dont le nom contient "不" ou "嫣" (correspondance approximative et union)
SELECT stu_id,
       stu_name
  FROM tb_student
 WHERE stu_name LIKE '%不%'
       OR stu_name LIKE '%嫣%';
       
SELECT stu_id,
       stu_name
  FROM tb_student
 WHERE stu_name LIKE '%不%'
 UNION
SELECT stu_id,
       stu_name
  FROM tb_student
 WHERE stu_name LIKE '%嫣%';

-- Sélectionner le numéro et le nom des étudiants dont le nom de famille est "杨" ou "林" et le prénom comporte trois caractères (correspondance par expression régulière)
SELECT stu_id,
       stu_name
  FROM tb_student
 WHERE stu_name REGEXP '[林杨][\\u4e00-\\u9fa5]{2}';

-- Sélectionner les noms des étudiants dont le lieu d'origine n'est pas renseigné (traitement des valeurs NULL)
SELECT stu_name
  FROM tb_student
 WHERE TRIM(stu_addr) = ''
       OR stu_addr IS NULL;
 
-- Sélectionner les noms des étudiants dont le lieu d'origine est renseigné (traitement des valeurs NULL)
SELECT stu_name
  FROM tb_student
 WHERE TRIM(stu_addr) <> ''
       AND stu_addr IS NOT NULL;

-- Sélectionner toutes les dates de sélection de cours (élimination des doublons)
SELECT DISTINCT sel_date
  FROM tb_record;

-- Sélectionner les lieux d'origine des étudiants (élimination des doublons)
SELECT DISTINCT stu_addr
  FROM tb_student
 WHERE TRIM(stu_addr) <> ''
       AND stu_addr IS NOT NULL;

-- Sélectionner le nom et la date de naissance des étudiants masculins, triés par âge décroissant (tri)
SELECT stu_name,
       stu_birth
  FROM tb_student
 WHERE stu_sex = 1
 ORDER BY stu_birth ASC;
 
-- Supplément : convertir la date de naissance en âge (fonctions de date, fonctions numériques)
SELECT stu_name AS nom,
       FLOOR(DATEDIFF(CURDATE(), stu_birth) / 365) AS âge
  FROM tb_student
 WHERE stu_sex = 1
 ORDER BY âge DESC;

-- Sélectionner la date de naissance de l'étudiant le plus âgé (fonctions d'agrégation)
SELECT MIN(stu_birth)
  FROM tb_student;

-- Sélectionner la date de naissance de l'étudiant le plus jeune (fonctions d'agrégation)
SELECT MAX(stu_birth)
  FROM tb_student;

-- Sélectionner la note maximale obtenue au cours 1111 (fonctions d'agrégation)
SELECT MAX(score)
  FROM tb_record
 WHERE cou_id = 1111;

-- Sélectionner la note minimale, maximale, moyenne, écart-type et variance des notes de l'étudiant 1001 (fonctions d'agrégation)
SELECT MIN(score) AS note_min,
       MAX(score) AS note_max,
	   ROUND(AVG(score), 1) AS moyenne,
       STDDEV(score) AS écart_type,
       VARIANCE(score) AS variance
  FROM tb_record
 WHERE stu_id = 1001;

-- Sélectionner la note moyenne de l'étudiant 1001, en considérant les NULL comme 0 (fonctions d'agrégation)
SELECT ROUND(SUM(score) / COUNT(*), 1) AS moyenne
  FROM tb_record
 WHERE stu_id = 1001;

-- Compter le nombre d'étudiants par sexe (regroupement et fonctions d'agrégation)
SELECT CASE stu_sex WHEN 1 THEN '男' ELSE '女' END AS sexe,
       COUNT(*) AS effectif
  FROM tb_student
 GROUP BY stu_sex;

-- Compter le nombre d'étudiants par faculté (regroupement et fonctions d'agrégation)
SELECT col_id AS numéro_faculté,
       COUNT(*) AS effectif
  FROM tb_student
 GROUP BY col_id
  WITH ROLLUP;

-- Compter le nombre d'étudiants par faculté et par sexe (regroupement et fonctions d'agrégation)
SELECT col_id AS numéro_faculté,
       CASE stu_sex WHEN 1 THEN '男' ELSE '女' END AS sexe,
       COUNT(*) AS effectif
  FROM tb_student
 GROUP BY col_id, stu_sex;

-- Sélectionner le numéro et la moyenne des notes de chaque étudiant (regroupement et fonctions d'agrégation)
SELECT stu_id AS numéro_étudiant,
	   ROUND(AVG(score), 1) AS moyenne
  FROM tb_record
 GROUP BY stu_id;

-- Sélectionner le numéro et la moyenne des étudiants dont la moyenne est supérieure ou égale à 90 (filtrage après regroupement)
SELECT stu_id AS numéro_étudiant,
	   ROUND(AVG(score), 1) AS moyenne
  FROM tb_record
 GROUP BY stu_id
HAVING moyenne >= 90;

-- Sélectionner le numéro et la moyenne des étudiants dont la moyenne aux cours 1111, 2222 et 3333 est supérieure ou égale à 90 (filtrage avant et après regroupement)
SELECT stu_id AS numéro_étudiant,
	   ROUND(AVG(score), 1) AS moyenne
  FROM tb_record
 WHERE cou_id IN (1111, 2222, 3333)
 GROUP BY stu_id
HAVING moyenne >= 90
 ORDER BY moyenne ASC;

-- Sélectionner le nom de l'étudiant le plus âgé (sous-requête)
SELECT stu_name
  FROM tb_student
 WHERE stu_birth = (SELECT MIN(stu_birth)
                      FROM tb_student);

-- Sélectionner le nom des étudiants qui ont suivi plus de deux cours (sous-requête et opération ensembliste)
SELECT stu_name
  FROM tb_student
 WHERE stu_id IN (SELECT stu_id
				    FROM tb_record
				   GROUP BY stu_id
				  HAVING COUNT(*) > 2);

-- Sélectionner le nom, la date de naissance et le nom de la faculté de chaque étudiant (jointure de tables)
SELECT stu_name,
       stu_birth,
       col_name
  FROM tb_student AS t1, tb_college AS t2
 WHERE t1.col_id = t2.col_id;
 
SELECT stu_name,
       stu_birth,
	   col_name
  FROM tb_student INNER JOIN tb_college
       ON tb_student.col_id = tb_college.col_id;

SELECT stu_name,
       stu_birth,
	   col_name
  FROM tb_student NATURAL JOIN tb_college;
  
SELECT stu_name,
       stu_birth,
	   col_name
  FROM tb_student CROSS JOIN tb_college;

-- Sélectionner le nom de l'étudiant, le nom du cours et la note (jointure de tables)
SELECT stu_name,
       cou_name,
	   score
  FROM tb_student, tb_course, tb_record
 WHERE tb_student.stu_id = tb_record.stu_id
       AND tb_course.cou_id = tb_record.cou_id
       AND score IS NOT NULL;

SELECT stu_name,
       cou_name,
	   score
  FROM tb_student 
       INNER JOIN tb_record
	       ON tb_student.stu_id = tb_record.stu_id
	   INNER JOIN tb_course
	       ON tb_course.cou_id = tb_record.cou_id
 WHERE score IS NOT NULL;
 
SELECT stu_name,
       cou_name,
       score
  FROM tb_student 
	   NATURAL JOIN tb_record
       NATURAL JOIN tb_course
 WHERE score IS NOT NULL;

-- Supplément : prendre les 5 premiers résultats de la requête ci-dessus (pagination)
SELECT stu_name,
       cou_name,
       score
  FROM tb_student 
	   NATURAL JOIN tb_record
       NATURAL JOIN tb_course
 WHERE score IS NOT NULL
 ORDER BY cou_id ASC, score DESC
 LIMIT 5;

-- Supplément : prendre les résultats 6 à 10 de la requête ci-dessus (pagination)
SELECT stu_name,
       cou_name,
       score
  FROM tb_student 
	   NATURAL JOIN tb_record
       NATURAL JOIN tb_course
 WHERE score IS NOT NULL
 ORDER BY cou_id ASC, score DESC
 LIMIT 5
OFFSET 5;

-- Supplément : prendre les résultats 11 à 15 de la requête ci-dessus (pagination)
SELECT stu_name,
       cou_name,
       score
  FROM tb_student 
	   NATURAL JOIN tb_record
       NATURAL JOIN tb_course
 WHERE score IS NOT NULL
 ORDER BY cou_id ASC, score DESC
 LIMIT 10, 5;

-- Sélectionner le nom et la moyenne des notes de chaque étudiant (sous-requête et jointure)
-- Erreur : chaque table dérivée doit avoir son propre alias
SELECT stu_name,
	   avg_score
  FROM tb_student
       NATURAL JOIN (SELECT stu_id,
                            ROUND(AVG(score), 1) AS avg_score
                       FROM tb_record
                      GROUP BY stu_id) AS tmp;

-- Sélectionner le nom et le nombre de cours suivis par chaque étudiant (sous-requête et jointure)
SELECT stu_name,
	   total
  FROM tb_student
       NATURAL JOIN (SELECT stu_id,
                            COUNT(*) AS total
                       FROM tb_record
                      GROUP BY stu_id) AS tmp;

-- Sélectionner le nom et le nombre de cours suivis de chaque étudiant (sous-requête et jointure externe gauche)
SELECT stu_name AS nom,
	   COALESCE(total, 0) AS nb_cours_suivis
  FROM tb_student AS t1
	   LEFT JOIN (SELECT stu_id,
			             COUNT(*) AS total
		            FROM tb_record
				   GROUP BY stu_id) AS t2
	       ON t1.stu_id = t2.stu_id;
```

Quelques points à noter :

1. Les versions actuelles de MySQL **ne prennent pas en charge la jointure externe complète (FULL OUTER JOIN)**. On peut simuler son effet en combinant les résultats d'une jointure externe gauche (LEFT JOIN) et d'une jointure externe droite (RIGHT JOIN) avec l'opérateur `UNION`. Le diagramme suivant peut aider à visualiser les différents types de jointures :

   <img src="http://localhost/mypic/20211121135117.png" style="zoom:50%">

2. MySQL prend en charge de nombreux types d'opérateurs : arithmétiques (`+`, `-`, `*`, `/`, `%`), de comparaison (`=`, `<>`, `<=>`, `<`, `<=`, `>`, `>=`, `BETWEEN...AND...`, `IN`, `IS NULL`, `IS NOT NULL`, `LIKE`, `RLIKE`, `REGEXP`), logiques (`NOT`, `AND`, `OR`, `XOR`) et bit à bit (`&`, `|`, `^`, `~`, `>>`, `<<`). Ces opérateurs peuvent être utilisés dans les instructions DML pour manipuler les données.

3. Lors des requêtes, on peut utiliser des fonctions dans les clauses `SELECT`, `WHERE`, `ORDER BY`, `HAVING`, etc. Ces fonctions incluent des fonctions de chaîne, numériques, de date/heure, de contrôle de flux, etc. Voici un aperçu :

   **Fonctions de chaîne courantes :**
   - `CONCAT` : Concatène plusieurs chaînes.
   - `FORMAT` : Formate un nombre en chaîne avec un nombre spécifié de décimales.
   - `LOWER` / `UPPER` : Convertit en minuscules / majuscules.
   - `LEFT` / `RIGHT` : Extrait un nombre donné de caractères depuis la gauche/droite.
   - `LENGTH` / `CHAR_LENGTH` : Retourne la longueur en octets / caractères.
   - `TRIM` / `LTRIM` / `RTRIM` : Supprime les espaces.
   - `SUBSTRING` : Extrait une sous-chaîne.

   **Fonctions numériques courantes :**
   - `ABS` : Valeur absolue.
   - `CEILING` / `FLOOR` : Arrondi à l'entier supérieur / inférieur.
   - `ROUND` : Arrondi.
   - `RAND` : Nombre aléatoire entre 0 et 1.
   - `SQRT` : Racine carrée.
   - `POW` : Puissance.
   - `SIN`, `COS`, `TAN`, etc. : Fonctions trigonométriques.

   **Fonctions de date et heure courantes :**
   - `CURDATE` / `CURTIME` / `NOW` : Date/heure actuelle.
   - `YEAR` / `MONTH` / `DAY` : Extrait l'année, le mois, le jour.
   - `HOUR` / `MINUTE` / `SECOND` : Extrait l'heure, la minute, la seconde.
   - `DATEDIFF` : Différence en jours entre deux dates.
   - `ADDDATE` / `SUBDATE` : Ajoute/soustrait un intervalle à une date.

   **Fonctions de contrôle de flux courantes :**
   - `IF` : Retourne une valeur selon une condition.
   - `IFNULL` : Retourne une valeur spécifiée si l'expression est NULL.
   - `NULLIF` : Retourne NULL si deux expressions sont égales.
   - `CASE` : Structure conditionnelle (utilisée dans les exemples).

   **Autres fonctions utiles :**
   - `MD5`, `SHA1`, `SHA2` : Hash.
   - `USER`, `DATABASE` : Utilisateur et base de données courants.
   - `VERSION` : Version de MySQL.
   - `LAST_INSERT_ID` : Dernier ID auto-incrémenté inséré.
   - `UUID` : Génère un identifiant unique universel.