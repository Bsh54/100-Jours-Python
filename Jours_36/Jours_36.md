## Bases de données relationnelles et présentation de MySQL

### Vue d'ensemble des bases de données relationnelles

1. **Persistance des données** - Sauvegarde des données sur un support de stockage durable, de sorte que les données ne soient pas perdues en cas de coupure de courant.

2. **Historique du développement des bases de données** - Base de données en réseau, base de données hiérarchique, base de données relationnelle, base de données NoSQL, base de données NewSQL.

   > En 1970, le chercheur d'IBM, E.F. Codd, a publié un article intitulé *A Relational Model of Data for Large Shared Data Banks* dans *Communication of the ACM*, introduisant le concept de **modèle relationnel**, jetant ainsi les bases théoriques du modèle relationnel. Plus tard, Codd a publié d'autres articles discutant de la théorie de la normalisation et des 12 critères pour évaluer les systèmes relationnels, établissant les fondements mathématiques des bases de données relationnelles.

3. **Caractéristiques des bases de données relationnelles**.
   - Fondement théorique : **Algèbre relationnelle** (théorie des ensembles, logique du premier ordre, opérations relationnelles).
   - Représentation concrète : Organisation des données en **tables bidimensionnelles** (lignes et colonnes).
   - Langage de programmation : **Structured Query Language (SQL)**.
       - DDL : Langage de définition de données.
       - DML : Langage de manipulation de données.
       - DCL : Langage de contrôle de données.
       - TCL : Langage de contrôle des transactions.

4. **Modèle entité-association (ER) et diagrammes de modèles conceptuels**.

   Le **modèle ER**, ou **modèle entité-association** (Entity-Relationship Model), a été proposé par l'informaticien américano-chinois Chen P.P. (Peter Pin-Shan) et constitue une méthode de description de haut niveau pour les modèles de données conceptuels, comme illustré ci-dessous.

   <img src="res/er_diagram.png" width="75%">

   - Entité : Rectangle.
   - Attribut : Ovale.
   - Relation : Losange.
   - Multiplicité : 1:1 (un à un) / 1:N (un à plusieurs) / M:N (plusieurs à plusieurs).

   Dans le développement de projets réels, nous pouvons utiliser des outils de modélisation de bases de données (comme PowerDesigner) pour dessiner des modèles de données conceptuels, puis configurer le système de base de données cible pour transformer le modèle conceptuel en modèle physique (comme illustré ci-dessous), générant finalement le SQL pour créer les tables bidimensionnelles (de nombreux outils peuvent exporter du SQL ou générer directement les tables de données à partir du modèle physique conçu et de la base de données cible définie).

   <img src="res/conceptual_model.png" style="zoom:50%;">

5. **Produits de bases de données relationnelles**.
   - **[Oracle](https://www.oracle.com/index.html)** - Actuellement le système de gestion de base de données le plus largement utilisé au monde. En tant que système de base de données généraliste, il offre des fonctionnalités complètes de gestion de données ; en tant que base de données relationnelle, c'est un produit relationnel complet ; en tant que base de données distribuée, il met en œuvre des fonctionnalités de traitement distribué. Dans les versions récentes d'Oracle, l'architecture multi-locataire a été introduite, facilitant le déploiement et la gestion de bases de données dans le cloud.
   - **[DB2](https://www.ibm.com/analytics/us/en/db2/)** - Produit de base de données relationnelle développé par IBM, fonctionnant principalement sur Unix (y compris AIX propre à IBM), Linux et Windows Server. DB2 a une longue histoire et est considéré comme l'un des premiers produits de base de données à utiliser SQL, possédant des fonctionnalités commerciales intelligentes assez puissantes.
   - **[SQL Server](https://www.microsoft.com/en-us/sql-server/)** - Produit de base de données relationnelle développé et promu par Microsoft, initialement adapté à la gestion de données des petites et moyennes entreprises, mais son champ d'application s'est étendu ces dernières années, certaines grandes entreprises, voire des multinationales, l'utilisent désormais pour construire leurs systèmes de gestion de données.
   - **[MySQL](https://www.mysql.com/)** - MySQL est open source, et toute personne peut le télécharger sous licence GPL (General Public License) et le modifier selon ses besoins. MySQL est reconnu pour sa vitesse, sa fiabilité et son adaptabilité.
   - **[PostgreSQL]()** - Produit de base de données relationnelle open source distribué sous licence BSD.

### Présentation de MySQL

MySQL a été initialement développé par la société suédoise MySQL AB comme un système de gestion de base de données relationnelle open source. La société a été rachetée par Sun Microsystems en 2008. En 2009, Oracle Corporation a racheté Sun Microsystems, faisant ainsi de MySQL un produit d'Oracle.

MySQL, grâce à ses performances élevées, son faible coût et sa fiabilité, est devenu la base de données open source la plus populaire, largement utilisée dans le développement de sites web de petite et moyenne taille. Avec la maturation de MySQL, il est de plus en plus utilisé dans des sites et applications à grande échelle, tels que Wikipédia, Google, Facebook, Baidu, Taobao, Tencent, Sina, Qunar, etc., qui utilisent MySQL pour fournir des services de persistance des données.

Après le rachat de Sun Microsystems par Oracle, le prix de la version commerciale de MySQL a considérablement augmenté, et Oracle n'a plus pris en charge le développement d'un autre projet de logiciel libre, [OpenSolaris](https://zh.wikipedia.org/wiki/OpenSolaris), ce qui a conduit la communauté du logiciel libre à s'inquiéter de la poursuite du support de la version communautaire de MySQL (la seule version gratuite des différentes distributions de MySQL). Le fondateur de MySQL, Michael Widenius, a créé une branche, [MariaDB](https://zh.wikipedia.org/wiki/MariaDB) (nommée d'après sa fille), basée sur MySQL. De nombreuses entreprises utilisant MySQL (comme Wikipédia) ont déjà migré de MySQL vers MariaDB.

### Installation de MySQL

#### Environnement Windows

1. Téléchargez le programme d'installation du "Serveur MySQL Community Edition" via le [lien de téléchargement](https://dev.mysql.com/downloads/windows/installer/8.0.html) fourni sur le [site officiel](https://www.mysql.com/), comme illustré ci-dessous. Il est recommandé de télécharger le programme d'installation hors ligne (MySQL Installer).

    <img src="res/20211105230905.png" style="zoom:50%">

2. Exécutez l'installateur et suivez les étapes ci-dessous pour l'installation.

    - Sélectionnez l'installation personnalisée.

    <img src="res/20211105231152.jpg" style="zoom:35%">

    - Sélectionnez les composants à installer.

    <img src="res/20211105231255.jpg" style="zoom:35%">

    - Si des dépendances sont manquantes, installez-les d'abord.

    <img src="res/20211105231620.png" style="zoom:35%">

    - Prêt pour l'installation.

    <img src="res/20211105231719.jpg" style="zoom:35%">

    - Installation terminée.

    <img src="res/20211105232024.jpg" style="zoom:35%">

    - Préparation de l'exécution de l'assistant de configuration.

    <img src="res/20211105231815.jpg" style="zoom:35%">

3. Exécutez l'assistant de configuration post-installation.

    - Configurez le type de serveur et le réseau.

    <img src="res/20211105232109.jpg" style="zoom:35%">

    - Configurez la méthode d'authentification (méthode de protection du mot de passe).

        <img src="res/20211105232408.jpg" style="zoom:35%">

    - Configurez les utilisateurs et les rôles.

        <img src="res/20211105232521.jpg" style="zoom:35%">

    - Configurez le nom du service Windows et le démarrage automatique.

        <img src="res/20211105232608.jpg" style="zoom:35%">

    - Configurez les journaux.

        <img src="res/20211105232641.jpg" style="zoom:35%">

    - Configurez les options avancées.

        <img src="res/20211105232724.jpg" alt="ACAC15B8633133B65476286A49BFBD7E" style="zoom:35%">

    - Appliquez la configuration.

        <img src="res/20211105232800.jpg" style="zoom:35%">

4. Vous pouvez démarrer ou arrêter MySQL dans la fenêtre "Services" du système Windows.

    <img src="res/20211105232926.jpg" style="zoom:50%">

5. Configurez la variable d'environnement PATH pour utiliser les outils clients MySQL dans l'invite de commandes.

    - Ouvrez la fenêtre "Système" de Windows et cliquez sur "Paramètres système avancés".

        <img src="res/20211105233054.jpg" style="zoom:50%">

    - Dans la fenêtre "Avancé" des "Propriétés système", cliquez sur le bouton "Variables d'environnement".

        <img src="res/20211105233312.jpg" style="zoom:50%">

    - Modifiez la variable d'environnement PATH, ajoutez le chemin du dossier `bin` de l'installation de MySQL à la variable d'environnement PATH.

        <img src="res/20211105233359.jpg" style="zoom:50%">

    - Une fois la configuration terminée, vous pouvez essayer d'utiliser les outils en ligne de commande MySQL dans l'invite de commandes.

        <img src="res/20211105233643.jpg" style="zoom:50%">

#### Environnement Linux

L'exemple ci-dessous utilise CentOS 7.x pour démontrer l'installation de MySQL 5.7.x. Si vous devez installer d'autres versions de MySQL sur d'autres systèmes Linux, veuillez rechercher les tutoriels d'installation correspondants sur Internet.

1. **Installer MySQL**.

   Vous pouvez télécharger les fichiers d'installation sur le [site officiel de MySQL](<https://www.mysql.com/>). Sélectionnez d'abord la plateforme et la version sur la page de téléchargement, puis trouvez le lien de téléchargement correspondant, téléchargez directement l'archive contenant tous les fichiers d'installation, extrayez l'archive et installez via le gestionnaire de paquets.

   ```Shell
   wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.26-1.el7.x86_64.rpm-bundle.tar
   tar -xvf mysql-5.7.26-1.el7.x86_64.rpm-bundle.tar
   ```

   Si le système contient des fichiers liés à MariaDB, supprimez-les d'abord.

   ```Shell
   yum list installed | grep mariadb | awk '{print $1}' | xargs yum erase -y
   ```

   Mettez à jour et installez les bibliothèques système potentielles nécessaires.

   ```Bash
   yum update
   yum install -y libaio libaio-devel
   ```

   Ensuite, vous pouvez installer MySQL dans l'ordre indiqué ci-dessous en utilisant l'outil RPM (Redhat Package Manager).

   ```Shell
   rpm -ivh mysql-community-common-5.7.26-1.el7.x86_64.rpm
   rpm -ivh mysql-community-libs-5.7.26-1.el7.x86_64.rpm
   rpm -ivh mysql-community-libs-compat-5.7.26-1.el7.x86_64.rpm
   rpm -ivh mysql-community-devel-5.7.26-1.el7.x86_64.rpm
   rpm -ivh mysql-community-client-5.7.26-1.el7.x86_64.rpm
   rpm -ivh mysql-community-server-5.7.26-1.el7.x86_64.rpm
   ```

   Vous pouvez utiliser la commande suivante pour voir les paquets MySQL installés.

   ```Shell
   rpm -qa | grep mysql
   ```

2. **Configurer MySQL**.

   Le fichier de configuration de MySQL se trouve dans le répertoire `/etc`, nommé `my.cnf`. Le contenu du fichier de configuration par défaut est le suivant.

   ```Shell
   cat /etc/my.cnf
   ```

   ```INI
   # For advice on how to change settings please see
   # http://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html
   
   [mysqld]
   #
   # Remove leading # and set to the amount of RAM for the most important data
   # cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
   # innodb_buffer_pool_size = 128M
   #
   # Remove leading # to turn on a very important data integrity option: logging
   # changes to the binary log between backups.
   # log_bin
   #
   # Remove leading # to set options mainly useful for reporting servers.
   # The server defaults are faster for transactions and fast SELECTs.
   # Adjust sizes as needed, experiment to find the optimal values.
   # join_buffer_size = 128M
   # sort_buffer_size = 2M
   # read_rnd_buffer_size = 2M
   datadir=/var/lib/mysql
   socket=/var/lib/mysql/mysql.sock
   
   # Disabling symbolic-links is recommended to prevent assorted security risks
   symbolic-links=0
   
   log-error=/var/log/mysqld.log
   pid-file=/var/run/mysqld/mysqld.pid
   ```

   Via le fichier de configuration, nous pouvons modifier le port utilisé par le service MySQL, le jeu de caractères, le nombre maximal de connexions, la taille de la file d'attente des sockets, la taille maximale des paquets de données, l'emplacement des fichiers journaux, la durée de conservation des journaux, etc. Nous pouvons également ajuster les performances et renforcer la sécurité du serveur MySQL en modifiant le fichier de configuration.

3. **Démarrer le service MySQL**.

   Vous pouvez utiliser la commande suivante pour démarrer MySQL.

   ```Shell
   service mysqld start
   ```

   Sur CentOS 7, il est recommandé d'utiliser la commande suivante pour démarrer MySQL.

   ```Shell
   systemctl start mysqld
   ```

   Après avoir démarré MySQL avec succès, vous pouvez vérifier l'utilisation des ports réseau avec la commande suivante. MySQL utilise par défaut le port `3306`.

   ```Shell
   netstat -ntlp | grep mysql
   ```

   Vous pouvez également utiliser la commande suivante pour vérifier s'il existe un processus nommé `mysqld`.

   ```Shell
   pgrep mysqld
   ```

4. **Utiliser l'outil client MySQL pour se connecter au serveur**.

   Outil en ligne de commande :

   ```Shell
   mysql -u root -p
   ```

   > **Note :** Lors du lancement du client, l'option `-u` spécifie le nom d'utilisateur, le compte administrateur par défaut de MySQL est `root` ; `-p` indique qu'il faut saisir le mot de passe ; si vous vous connectez à une autre machine que la machine locale, vous pouvez utiliser `-h` pour spécifier le nom d'hôte ou l'adresse IP de l'hôte distant.

   S'il s'agit de la première installation de MySQL, vous pouvez utiliser la commande suivante pour trouver le mot de passe initial par défaut.

   ```Shell
   cat /var/log/mysqld.log | grep password
   ```

   La commande ci-dessus examine le journal MySQL pour les lignes contenant `password`. Dans le résultat affiché, la partie après `root@localhost:` est le mot de passe initial défini par défaut.

   Une fois dans l'outil client, vous pouvez modifier le mot de passe d'accès du super-administrateur (root) en `123456` avec les instructions suivantes.

   ```SQL
   set global validate_password_policy=0;
   set global validate_password_length=6;
   alter user 'root'@'localhost' identified by '123456';
   ```

   > **Note :** Les versions récentes de MySQL interdisent par défaut l'utilisation de mots de passe faibles. Le code ci-dessus modifie donc la politique de validation des mots de passe et la longueur minimale. En réalité, nous ne devrions pas utiliser de mots de passe faibles en raison du risque de piratage par force brute. Ces dernières années, les **attaques de bases de données pour voler des données et les rançons en bitcoins via des bases de données piratées** sont fréquentes. Pour éviter ces risques potentiels, le point le plus important est de **ne pas exposer le serveur de base de données sur l'Internet public** (la meilleure pratique est de placer la base de données dans un réseau interne, au minimum de ne pas ouvrir le port d'accès du serveur de base de données sur l'Internet public). Il faut également protéger le mot de passe du compte `root`. Lorsqu'un système d'application a besoin d'accéder à la base de données, il n'utilise généralement pas le compte `root` mais **crée d'autres comptes avec les autorisations appropriées**.

   Lors de la prochaine connexion au serveur MySQL avec l'outil client, vous pouvez utiliser le nouveau mot de passe. Dans le développement réel, pour faciliter les opérations des utilisateurs, vous pouvez choisir des outils clients graphiques pour vous connecter au serveur MySQL, notamment :

   - MySQL Workbench (outil officiel)

       <img src="res/20211106063939.png" style="zoom:50%">

   - Navicat for MySQL (interface simple et conviviale)

       <img src="res/20210521152457.png" style="zoom:50%;">

#### Environnement macOS

L'installation de MySQL sur macOS est relativement simple. Il suffit de télécharger le fichier d'installation DMG depuis le site officiel mentionné précédemment et de l'exécuter. Lors du téléchargement, choisissez le lien de téléchargement en fonction du type de processeur (Intel ou Apple M1), comme illustré ci-dessous.

<img src="res/20211121215901.png" style="zoom:50%;">

Une fois l'installation réussie, vous pouvez trouver "MySQL" dans les "Préférences Système". Sur l'écran ci-dessous, vous pouvez démarrer et arrêter le serveur MySQL, ainsi que configurer le chemin des fichiers principaux de MySQL.

<img src="res/20211121215153.png" style="zoom:40%;">

### Commandes de base MySQL

#### Commandes d'affichage

1. Afficher toutes les bases de données

```SQL
show databases;
```

2. Afficher tous les jeux de caractères

```SQL
show character set;
```

3. Afficher toutes les règles de classement (collations)

```SQL
show collation;
```

4. Afficher tous les moteurs de stockage

```SQL
show engines;
```

5. Afficher tous les fichiers journaux binaires

```SQL
show binary logs;
```

6. Afficher toutes les tables d'une base de données

```SQL
show tables;
```

#### Obtenir de l'aide

Dans l'outil en ligne de commande MySQL, vous pouvez utiliser la commande `help` ou `?` pour obtenir de l'aide, comme indiqué ci-dessous.

1. Obtenir de l'aide sur la commande `show`.

    ```MySQL
    ? show
    ```

2. Voir les sujets d'aide disponibles.

    ```MySQL
    ? contents
    ```

3. Obtenir de l'aide sur les fonctions.

    ```MySQL
    ? functions
    ```

4. Obtenir de l'aide sur les types de données.

    ```MySQL
    ? data types
    ```

#### Autres commandes

1. Établir/réinitialiser une connexion au serveur - `connect` / `resetconnection`.

2. Effacer la saisie en cours - `\c`. En cas d'erreur de saisie, utilisez `\c` pour effacer la saisie en cours et recommencer.

3. Modifier le délimiteur - `delimiter`. Le délimiteur par défaut est `;`. Vous pouvez le modifier en un autre caractère, par exemple `$`, avec la commande `delimiter $`.

4. Ouvrir l'éditeur système par défaut - `edit`. Après avoir enregistré et fermé l'éditeur, la ligne de commande exécutera automatiquement le contenu édité.

5. Vérifier l'état du serveur - `status`.

6. Modifier l'invite par défaut - `prompt`.

7. Exécuter une commande système - `system`. Vous pouvez exécuter une commande système après la commande `system`. La commande `system` peut également être abrégée en `\!`.

8. Exécuter un fichier SQL - `source`. La commande `source` est suivie du chemin du fichier SQL.

9. Rediriger la sortie - `tee` / `notee`. Vous pouvez rediriger la sortie des commandes vers un fichier spécifié.

10. Changer de base de données - `use`.

11. Afficher les avertissements - `warnings`.

12. Quitter la ligne de commande - `quit` ou `exit`.