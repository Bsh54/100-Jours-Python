## Maîtrisez le système d'exploitation Linux

> **Note :** Les explications des commandes Linux dans cet article sont basées sur la distribution Linux CentOS. L'auteur utilise personnellement un serveur cloud Alibaba avec la version système CentOS Linux release 7.6.1810. Différentes distributions Linux peuvent présenter de légères variations dans les commandes Shell et les utilitaires, mais ces différences sont généralement minimes.

### Histoire des systèmes d'exploitation

Un système informatique uniquement matériel, sans logiciel, est appelé "bare metal". Il est difficile d'utiliser une machine "bare metal" pour effectuer des tâches informatiques quotidiennes (comme le stockage et les calculs). Ainsi, des logiciels spécifiques sont nécessaires pour contrôler le fonctionnement du matériel. Le logiciel le plus proche du matériel est le logiciel système, dont le plus important est le "système d'exploitation". Un "système d'exploitation" est un ensemble de programmes qui contrôle et gère l'ensemble des ressources matérielles et logicielles d'un ordinateur, réalise l'allocation des ressources et la répartition des tâches, et fournit une interface et un environnement aux utilisateurs du système ainsi qu'aux autres logiciels.

#### Pas de système d'exploitation (opération manuelle)

Aux débuts de l'informatique, sans système d'exploitation, les utilisateurs chargeaient d'abord le programme sur une bande ou des cartes perforées dans l'ordinateur, démarraient le périphérique d'entrée pour charger le programme, puis lançaient le programme via les interrupteurs de la console. Une fois le programme exécuté, l'imprimante produisait les résultats des calculs, et l'utilisateur retirait et emportait la bande ou les cartes. Un deuxième utilisateur répétait ensuite la même procédure. Durant tout ce processus, l'utilisateur avait un accès exclusif à la machine, le CPU restait en attente des opérations manuelles, et le taux d'utilisation des ressources était extrêmement faible.

#### Systèmes par lots (Batch Processing)

Un programme superviseur est d'abord lancé sur l'ordinateur. Sous son contrôle, l'ordinateur peut traiter automatiquement et par lots les tâches d'un ou plusieurs utilisateurs. Après avoir terminé un lot de tâches, le programme superviseur lit les nouvelles tâches depuis le périphérique d'entrée et les stocke sur bande magnétique. Il répète ensuite ces étapes. Le programme superviseur traite continuellement les différentes tâches, permettant leur transfert automatique, réduisant ainsi le temps d'établissement des tâches et les opérations manuelles, et améliorant le taux d'utilisation des ressources informatiques. Les systèmes par lots peuvent être divisés en systèmes par lots à canal unique, systèmes par lots à canaux multiples, systèmes par lots en ligne et systèmes par lots hors ligne.

#### Systèmes de temps partagé (Time-sharing) et systèmes temps réel

Un système de temps partagé divise le temps d'exécution du processeur en très courts intervalles (time slices) et attribue le processeur à tour de rôle aux différentes tâches connectées. Si une tâche ne peut pas terminer ses calculs dans l'intervalle de temps qui lui est attribué, elle est temporairement interrompue, le processeur est cédé à une autre tâche, et elle reprendra lors du prochain cycle de planification. Comme les ordinateurs sont très rapides, les tâches tournent rapidement, donnant à chaque utilisateur l'impression d'avoir un accès exclusif à l'ordinateur. Chaque utilisateur peut envoyer diverses commandes de contrôle opérationnel via son terminal, permettant ainsi une interaction homme-machine complète pour exécuter les tâches. Pour résoudre le problème des systèmes de temps partagé incapables de répondre rapidement aux instructions des utilisateurs, les systèmes temps réel sont apparus, capables de traiter les événements dans un délai strict et de répondre rapidement aux événements externes aléatoires.

#### Systèmes d'exploitation généralistes

1. **Années 1960** : La série System/360 d'IBM introduit un système d'exploitation unifié, OS/360.
2. **1965** : Les laboratoires Bell d'AT&T rejoignent le projet conjoint de GE et MIT pour développer MULTICS.
3. **1969** : Le projet MULTICS échoue. Ken Thompson, en congé, développe Unics en langage assembleur sur un PDP-7 obsolète pour jouer au jeu "Space Travel".
   > **Note :** Il est fascinant de penser qu'Unix, un système d'exploitation aussi majeur, a été développé par un programmeur en congé (dont la femme et les enfants étaient partis) sur du matériel obsolète, pour jouer à un jeu.
4. **1970–1971** : Ken Thompson et Dennis Ritchie réécrivent Unics en langage B sur un PDP-11 et, sur les conseils de Brian Kernighan, le renomment Unix.
5. **1972–1973** : Dennis Ritchie invente le langage C pour remplacer le langage B, moins portable, et entame la réécriture d'Unix en C.
6. **1974** : Unix atteint la version 5, un jalon, presque entièrement implémenté en C.
7. **1979** : À partir de la version 7 d'Unix, AT&T impose de nouvelles conditions d'utilisation, rendant Unix propriétaire.
8. **1987** : Le professeur Andrew S. Tanenbaum, souhaitant expliquer en détail le fonctionnement des systèmes d'exploitation à ses étudiants sans utiliser de code source d'AT&T pour éviter les problèmes de droits d'auteur, développe Minix.
9. **1991** : Linus Torvalds, étudiant à l'Université d'Helsinki, tente de faire quelques développements sur Minix. Mais comme Minix est uniquement destiné à l'enseignement et n'est pas très puissant, pour faciliter la lecture, l'écriture et le téléchargement de fichiers dans les groupes de discussion et le système de courrier de l'université, Linus écrit des pilotes de disque et un système de fichiers, qui forment l'embryon du noyau Linux.

Le diagramme suivant montre l'arbre généalogique des systèmes d'exploitation de la famille Unix.

![](./res/history-of-unix.png)

### Vue d'ensemble de Linux

Linux est un système d'exploitation généraliste. Un système d'exploitation est responsable de la planification des tâches, de l'allocation de la mémoire, de la gestion des entrées/sorties des périphériques, etc. Un système d'exploitation est généralement constitué de deux parties : le noyau (kernel), le programme central qui exécute d'autres programmes et gère des périphériques matériels comme les disques et les imprimantes, et les programmes système (pilotes de périphériques, bibliothèques de bas niveau, shell, programmes de service, etc.).

Le noyau Linux a été développé par le Finlandais Linus Torvalds et publié en septembre 1991. En tant que produit de l'ère Internet, le système d'exploitation Linux est développé en collaboration par de nombreux développeurs à travers le monde, c'est un système d'exploitation libre (notez que libre et gratuit ne sont pas synonymes ; pour comprendre la différence, vous pouvez [cliquer ici](https://www.debian.org/intro/free)).

### Avantages de Linux

1. Système d'exploitation généraliste, non lié à un matériel spécifique.
2. Écrit en C, très portable, avec une interface de programmation du noyau.
3. Prend en charge les utilisateurs multiples et le multitâche, avec un système de fichiers hiérarchique sécurisé.
4. Nombreux utilitaires, fonctions réseau complètes et documentation solide.
5. Sécurité fiable et stabilité solide, plus convivial pour les développeurs.

### Distributions Linux courantes

1. [Red Hat Enterprise Linux (RHEL)](https://www.redhat.com/en)
2. [Ubuntu](https://ubuntu.com/)
3. [CentOS](https://www.centos.org/)
4. [Fedora](https://getfedora.org/)
5. [Debian](https://www.debian.org/)
6. [openSUSE](https://www.opensuse.org/)

### Commandes de base

Les commandes Linux suivent généralement le format suivant :

```Shell
commande [options] [cible]
```

1. Obtenir les informations de connexion - **w** / **who** / **last** / **lastb**.

   ```Shell
   [root ~]# w
    23:31:16 up 12:16,  2 users,  load average: 0.00, 0.01, 0.05
   USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
   root     pts/0    182.139.66.250   23:03    4.00s  0.02s  0.00s w
   jackfrue pts/1    182.139.66.250   23:26    3:56   0.00s  0.00s -bash
   [root ~]# who
   root     pts/0        2018-04-12 23:03 (182.139.66.250)
   jackfrued pts/1        2018-04-12 23:26 (182.139.66.250)
   [root ~]# who am i
   root     pts/0        2018-04-12 23:03 (182.139.66.250)
   [root ~]# who mom likes
   root     pts/0        2018-04-12 23:03 (182.139.66.250)
   [root ~]# last
   root     pts/0        117.136.63.184   Sun May 26 18:57   still logged in   
   reboot   system boot  3.10.0-957.10.1. Mon May 27 02:52 - 19:10  (-7:-42)   
   root     pts/4        117.136.63.184   Sun May 26 18:51 - crash  (08:01)    
   root     pts/4        117.136.63.184   Sun May 26 18:49 - 18:49  (00:00)    
   root     pts/3        117.136.63.183   Sun May 26 18:35 - crash  (08:17)    
   root     pts/2        117.136.63.183   Sun May 26 18:34 - crash  (08:17)    
   root     pts/0        117.136.63.183   Sun May 26 18:10 - crash  (08:42)    
   ```

2. Vérifier le Shell utilisé - **ps**.

   Le Shell, également appelé "coquille" ou "interpréteur de commandes", est l'interprète entre l'utilisateur et le noyau du système d'exploitation. En termes simples, c'est l'interface d'interaction entre l'homme et l'ordinateur. Actuellement, le Shell par défaut de nombreux systèmes Linux est Bash (Bourne Again Shell), car il permet la complétion par tabulation des commandes et des chemins, la sauvegarde de l'historique des commandes, la configuration facile des variables d'environnement et l'exécution de traitements par lots.

   ```Shell
   [root ~]# ps
     PID TTY          TIME CMD
    3531 pts/0    00:00:00 bash
    3553 pts/0    00:00:00 ps
   ```

3. Obtenir la description et l'emplacement d'une commande - **whatis** / **which** / **whereis**.

   ```Shell
   [root ~]# whatis ps
   ps (1)        - report a snapshot of the current processes.
   [root ~]# whatis python
   python (1)    - an interpreted, interactive, object-oriented programming language
   [root ~]# whereis ps
   ps: /usr/bin/ps /usr/share/man/man1/ps.1.gz
   [root ~]# whereis python
   python: /usr/bin/python /usr/bin/python2.7 /usr/lib/python2.7 /usr/lib64/python2.7 /etc/python /usr/include/python2.7 /usr/share/man/man1/python.1.gz
   [root ~]# which ps
   /usr/bin/ps
   [root ~]# which python
   /usr/bin/python
   ```

4. Effacer l'écran - **clear**.

5. Consulter la documentation - **man** / **info** / **--help** / **apropos**.

   ```Shell
   [root@izwz97tbgo9lkabnat2lo8z ~]# ps --help
   Usage:
    ps [options]
    Try 'ps --help <simple|list|output|threads|misc|all>'
     or 'ps --help <s|l|o|t|m|a>'
    for additional help text.
   For more details see ps(1).
   [root@izwz97tbgo9lkabnat2lo8z ~]# man ps
   PS(1)                                User Commands                                PS(1)
   NAME
          ps - report a snapshot of the current processes.
   SYNOPSIS
          ps [options]
   DESCRIPTION
   ...
   ```

6. Informations système et nom d'hôte - **uname** / **hostname**.

   ```Shell
   [root@izwz97tbgo9lkabnat2lo8z ~]# uname
   Linux
   [root@izwz97tbgo9lkabnat2lo8z ~]# hostname
   izwz97tbgo9lkabnat2lo8z
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat /etc/centos-release
   CentOS Linux release 7.6.1810 (Core)
   ```

   > **Note :** `cat` est une commande qui concatène et affiche le contenu des fichiers sur la sortie standard (nous en parlerons plus tard). `/etc` est un répertoire très important dans les systèmes Linux, contenant de nombreux fichiers de configuration. `centos-release` est l'un de ces fichiers ; comme l'auteur utilise CentOS 7.6, ce fichier est présent.

7. Date et heure - **date** / **cal**.

   ```Shell
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# date
   Wed Jun 20 12:53:19 CST 2018
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cal
         June 2018
   Su Mo Tu We Th Fr Sa
                   1  2
    3  4  5  6  7  8  9
   10 11 12 13 14 15 16
   17 18 19 20 21 22 23
   24 25 26 27 28 29 30
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cal 5 2017
         May 2017
   Su Mo Tu We Th Fr Sa
       1  2  3  4  5  6
    7  8  9 10 11 12 13
   14 15 16 17 18 19 20
   21 22 23 24 25 26 27
   28 29 30 31
   ```

8. Redémarrer et éteindre - **reboot** / **shutdown**.

   ```Shell
   [root ~]# shutdown -h +5
   Shutdown scheduled for Sun 2019-05-26 19:34:27 CST, use 'shutdown -c' to cancel.
   [root ~]# 
   Broadcast message from root (Sun 2019-05-26 19:29:27 CST):
   
   The system is going down for power-off at Sun 2019-05-26 19:34:27 CST!
   [root ~]# shutdown -c
   
   Broadcast message from root (Sun 2019-05-26 19:30:22 CST):
   
   The system shutdown has been cancelled at Sun 2019-05-26 19:31:22 CST!
   [root ~]# shutdown -r 23:58
   Shutdown scheduled for Sun 2019-05-26 23:58:00 CST, use 'shutdown -c' to cancel.
   [root ~]# shutdown -c
   
   Broadcast message from root (Sun 2019-05-26 19:31:06 CST):
   
   The system shutdown has been cancelled at Sun 2019-05-26 19:32:06 CST!
   ```

   > **Note :** Lors de l'exécution de `shutdown`, un avertissement est envoyé aux utilisateurs connectés. Vous pouvez personnaliser ce message après la commande ou utiliser `now` après `-h` pour un arrêt immédiat.

9. Se déconnecter - **exit** / **logout**.

10. Historique des commandes - **history**.

  ```Shell
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# history
  ...
  452  ls
  453  cd Python-3.6.5/
  454  clear
  455  history
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# !454
  ```

  > **Note :** Après avoir consulté l'historique, vous pouvez réexécuter une commande avec `!numéro_de_la_commande`. Utilisez `history -c` pour effacer l'historique.

### Utilitaires

#### Opérations sur les fichiers et répertoires

1. Créer/supprimer un répertoire vide - **mkdir** / **rmdir**.

   ```Shell
   [root ~]# mkdir abc
   [root ~]# mkdir -p xyz/abc
   [root ~]# rmdir abc
   ```

2. Créer/supprimer un fichier - **touch** / **rm**.

   ```Shell
   [root ~]# touch readme.txt
   [root ~]# touch error.txt
   [root ~]# rm error.txt
   rm: remove regular empty file ‘error.txt’? y
   [root ~]# rm -rf xyz
   ```

   - `touch` crée un fichier vide ou modifie son horodatage. Dans Linux, un fichier a trois horodatages :
     - Date de modification du contenu (mtime).
     - Date de modification des permissions (ctime).
     - Date du dernier accès (atime).
   - Options importantes de `rm` :
     - `-i` : Suppression interactive, demande confirmation pour chaque suppression.
     - `-r` : Supprime récursivement les répertoires et leur contenu.
     - `-f` : Force la suppression, ignore les fichiers inexistants, pas de confirmation.

3. Changer et afficher le répertoire de travail courant - **cd** / **pwd**.

   > **Note :** `cd` peut être suivi d'un chemin relatif (par rapport au répertoire courant) ou absolu (commençant par `/`). `cd ..` remonte d'un niveau. Comment remonter de deux niveaux ?

4. Lister le contenu d'un répertoire - **ls**.

   - `-l` : Format long (liste détaillée).
   - `-a` : Affiche les fichiers/dossiers cachés (commençant par un point).
   - `-R` : Récursif (affiche aussi le contenu des sous-répertoires).
   - `-d` : Liste uniquement les répertoires, pas leur contenu.
   - `-S` / `-t` : Trie par taille / date.

5. Afficher le contenu d'un fichier - **cat** / **tac** / **head** / **tail** / **more** / **less** / **rev** / **od**.

   ```Shell
   [root ~]# wget http://www.sohu.com/ -O sohu.html
   --2018-06-20 18:42:34--  http://www.sohu.com/
   Resolving www.sohu.com (www.sohu.com)... 14.18.240.6
   Connecting to www.sohu.com (www.sohu.com)|14.18.240.6|:80... connected.
   HTTP request sent, awaiting response... 200 OK
   Length: 212527 (208K) [text/html]
   Saving to: ‘sohu.html’
   100%[==================================================>] 212,527     --.-K/s   in 0.03s
   2018-06-20 18:42:34 (7.48 MB/s) - ‘sohu.html’ saved [212527/212527]
   [root ~]# cat sohu.html
   ...
   [root ~]# head -10 sohu.html
   <!DOCTYPE html>
   <html>
   <head>
   <title>搜狐</title>
   <meta name="Keywords" content="搜狐,门户网站,新媒体,网络媒体,新闻,财经,体育,娱乐,时尚,汽车,房产,科技,图片,论坛,微博,博客,视频,电影,电视剧"/>
   <meta name="Description" content="搜狐网为用户提供24小时不间断的最新资讯，及搜索、邮件等网络服务。内容包括全球热点事件、突发新闻、时事评论、热播影视剧、体育赛事、行业动态、生活服务信息，以及论坛、博客、微博、我的搜狐等互动空间。" />
   <meta name="shenma-site-verification" content="1237e4d02a3d8d73e96cbd97b699e9c3_1504254750">
   <meta charset="utf-8"/>
   <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"/>
   [root ~]# tail -2 sohu.html
   </body>
   </html>
   [root ~]# less sohu.html
   ...
   [root ~]# cat -n sohu.html | more
   ...
   ```

   > **Note :** L'exemple ci-dessus utilise `wget`, un outil de téléchargement depuis Internet.

6. Copier/déplacer des fichiers - **cp** / **mv**.

   ```Shell
   [root ~]# mkdir backup
   [root ~]# cp sohu.html backup/
   [root ~]# cd backup
   [root backup]# ls
   sohu.html
   [root backup]# mv sohu.html sohu_index.html
   [root backup]# ls
   sohu_index.html
   ```

7. Renommer des fichiers - **rename**.

  ```Shell
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# rename .htm .html *.htm
  ```

8. Rechercher des fichiers et du contenu - **find** / **grep**.

   ```Shell
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# find / -name "*.html"
   /root/sohu.html
   /root/backup/sohu_index.html
   [root@izwz97tbgo9lkabnat2lo8z ~]# find . -atime 7 -type f -print
   [root@izwz97tbgo9lkabnat2lo8z ~]# find . -type f -size +2k
   [root@izwz97tbgo9lkabnat2lo8z ~]# find . -type f -name "*.swp" -delete
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# grep "<script>" sohu.html -n
   20:<script>
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# grep -E \<\/?script.*\> sohu.html -n
   20:<script>
   22:</script>
   24:<script src="//statics.itc.cn/web/v3/static/js/es5-shim-08e41cfc3e.min.js"></script>
   25:<script src="//statics.itc.cn/web/v3/static/js/es5-sham-1d5fa1124b.min.js"></script>
   26:<script src="//statics.itc.cn/web/v3/static/js/html5shiv-21fc8c2ba6.js"></script>
   29:<script type="text/javascript">
   52:</script>
   ...
   ```
   > **Note :** `grep` peut utiliser des expressions régulières. Utilisez `grep -E` ou `egrep` pour les expressions régulières étendues.

9. Créer et afficher des liens - **ln** / **readlink**.

   ```Shell
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
   -rw-r--r-- 1 root root 212131 Jun 20 19:15 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln /root/sohu.html /root/backup/sohu_backup
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
   -rw-r--r-- 2 root root 212131 Jun 20 19:15 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln /root/sohu.html /root/backup/sohu_backup2
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
   -rw-r--r-- 3 root root 212131 Jun 20 19:15 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln -s /etc/centos-release sysinfo
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sysinfo
   lrwxrwxrwx 1 root root 19 Jun 20 19:21 sysinfo -> /etc/centos-release
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat sysinfo
   CentOS Linux release 7.4.1708 (Core)
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat /etc/centos-release
   CentOS Linux release 7.4.1708 (Core)
   ```

   > **Note :** Il existe deux types de liens : les liens physiques (hard links) et les liens symboliques (soft links). Un lien physique peut être considéré comme un pointeur vers les données du fichier, similaire à un compteur de références en Python. Chaque lien physique ajouté incrémente le compteur de liens du fichier. Ce n'est que lorsque ce compteur atteint 0 que l'espace de stockage correspondant peut être réutilisé. Lorsque nous supprimons normalement un fichier, nous ne supprimons pas réellement les données du disque, nous supprimons un pointeur. Un lien symbolique est similaire à un raccourci sous Windows. Si le fichier cible d'un lien symbolique est supprimé, le lien devient invalide.

10. Compresser/décompresser et archiver/désarchiver - **gzip** / **gunzip** / **xz**.

  ```Shell
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# wget http://download.redis.io/releases/redis-4.0.10.tar.gz
  --2018-06-20 19:29:59--  http://download.redis.io/releases/redis-4.0.10.tar.gz
  Resolving download.redis.io (download.redis.io)... 109.74.203.151
  Connecting to download.redis.io (download.redis.io)|109.74.203.151|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 1738465 (1.7M) [application/x-gzip]
  Saving to: ‘redis-4.0.10.tar.gz’
  100%[==================================================>] 1,738,465   70.1KB/s   in 74s
  2018-06-20 19:31:14 (22.9 KB/s) - ‘redis-4.0.10.tar.gz’ saved [1738465/1738465]
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
  redis-4.0.10.tar.gz
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip redis-4.0.10.tar.gz
  [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
  redis-4.0.10.tar
  ```

11. Archiver et désarchiver - **tar**.

   ```Shell
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# tar -xvf redis-4.0.10.tar
   redis-4.0.10/
   redis-4.0.10/.gitignore
   redis-4.0.10/00  -RELEASENOTES
   redis-4.0.10/BUGS
   redis-4.0.10/CONTRIBUTING
   redis-4.0.10/COPYING
   redis-4.0.10/INSTALL
   redis-4.0.10/MANIFESTO
   redis-4.0.10/Makefile
   redis-4.0.10/README.md
   redis-4.0.10/deps/
   redis-4.0.10/deps/Makefile
   redis-4.0.10/deps/README.md
   ...
   ```

   > **Note :** La création d'archives (archivage) et l'extraction utilisent toutes deux la commande `tar`. Généralement, la création d'archive nécessite les options `-cvf`, où `c` signifie créer (create), `v` signifie verbeux (afficher les détails), et `f` spécifie le fichier d'archive. L'extraction utilise `-xvf`, où `x` signifie extraire (extract).

12. Convertir l'entrée standard en arguments de ligne de commande - **xargs**.

   La commande suivante recherche les fichiers HTML dans le répertoire courant, puis utilise `xargs` pour les passer comme arguments à `rm`, réalisant ainsi une recherche et suppression combinée.

   ```Shell
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# find . -type f -name "*.html" | xargs rm -f
   ```

   La commande suivante combine les lignes multiples du fichier a.txt en une seule ligne et écrit le résultat dans b.txt. `<` lit depuis a.txt, `>` écrit dans b.txt.

   ```Shell
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# xargs < a.txt > b.txt
   ```

   > **Note :** Cette commande est souvent utilisée avec les redirections et les pipes (tuyaux), que nous aborderons plus loin.

13. Afficher le nom de fichier ou de répertoire - **basename** / **dirname**.

14. Autres utilitaires.

   - **sort** - Trier du contenu.
   - **uniq** - Supprimer les doublons adjacents.
   - **tr** - Remplacer du texte.
   - **cut** / **paste** - Couper/coller du contenu.
   - **split** - Diviser un fichier.
   - **file** - Déterminer le type de fichier.
   - **wc** - Compter les lignes, mots, octets.
   - **iconv** - Convertir l'encodage.

   ```Shell
   [root ~]# cat foo.txt
   grape
   apple
   pitaya
   [root ~]# cat bar.txt
   100
   200
   300
   400
   [root ~]# paste foo.txt bar.txt
   grape   100
   apple   200
   pitaya  300
           400
   [root ~]# paste foo.txt bar.txt > hello.txt
   [root ~]# cut -b 4-8 hello.txt
   pe      10
   le      20
   aya     3
   0
   [root ~]# cat hello.txt | tr '\t' ','
   grape,100
   apple,200
   pitaya,300
   ,400
   [root ~]# split -l 100 sohu.html hello
   [root ~]# wget https://www.baidu.com/img/bd_logo1.png
   [root ~]# file bd_logo1.png
   bd_logo1.png: PNG image data, 540 x 258, 8-bit colormap, non-interlaced
   [root ~]# wc sohu.html
     2979   6355 212527 sohu.html
   [root ~]# wc -l sohu.html
   2979 sohu.html
   [root ~]# wget http://www.qq.com -O qq.html
   [root ~]# iconv -f gb2312 -t utf-8 qq.html
   ```

#### Pipes et redirections

1. Utilisation des pipes - **|**.

   Exemple : Compter le nombre de fichiers dans le répertoire courant.

   ```Shell
   [root ~]# find ./ | wc -l
   6152
   ```

   Exemple : Lister les fichiers et dossiers du répertoire courant avec une numérotation.

   ```Shell
   [root ~]# ls | cat -n
        1  dump.rdb
        2  mongodb-3.6.5
        3  Python-3.6.5
        4  redis-3.2.11
        5  redis.conf
   ```

   Exemple : Trouver le nombre total d'enregistrements dans record.log contenant AAA mais pas BBB.

   ```Shell
   [root ~]# cat record.log | grep AAA | grep -v BBB | wc -l
   ```

2. Redirection de sortie et redirection d'erreur - **>** / **>>** / **2>**.

   ```Shell
   [root ~]# cat readme.txt
   banana
   apple
   grape
   apple
   grape
   watermelon
   pear
   pitaya
   [root ~]# cat readme.txt | sort | uniq > result.txt
   [root ~]# cat result.txt
   apple
   banana
   grape
   pear
   pitaya
   watermelon
   ```

3. Redirection d'entrée - **<**.

   ```Shell
   [root ~]# echo 'hello, world!' > hello.txt
   [root ~]# wall < hello.txt
   [root ~]#
   Broadcast message from root (Wed Jun 20 19:43:05 2018):
   hello, world!
   [root ~]# echo 'I will show you some code.' >> hello.txt
   [root ~]# wall < hello.txt
   [root ~]#
   Broadcast message from root (Wed Jun 20 19:43:55 2018):
   hello, world!
   I will show you some code.
   ```

4. Redirection multiple - **tee**.

   La commande suivante affiche le résultat de `ls` sur le terminal et l'ajoute également au fichier ls.txt.

   ```Shell
   [root ~]# ls | tee -a ls.txt
   ```

#### Alias

1. **alias**

   ```Shell
   [root ~]# alias ll='ls -l'
   [root ~]# alias frm='rm -rf'
   [root ~]# ll
   ...
   drwxr-xr-x  2 root       root   4096 Jun 20 12:52 abc
   ...
   [root ~]# frm abc
   ```

2. **unalias**

   ```Shell
   [root ~]# unalias frm
   [root ~]# frm sohu.html
   -bash: frm: command not found
   ```

#### Traitement de texte

1. Éditeur de flux de caractères - **sed**.

   Sed est un outil pour manipuler, filtrer et transformer le contenu textuel. Supposons un fichier fruit.txt avec le contenu suivant :

   ```Shell
   [root ~]# cat -n fruit.txt 
        1  banana
        2  grape
        3  apple
        4  watermelon
        5  orange
   ```

   Ajouter "pitaya" après la ligne 2.

   ```Shell
   [root ~]# sed '2a pitaya' fruit.txt 
   banana
   grape
   pitaya
   apple
   watermelon
   orange
   ```

   > **Note :** La commande ci-dessus, comme beaucoup d'autres, n'a pas modifié fruit.txt, mais a produit la sortie à l'écran. Pour sauvegarder, utilisez la redirection de sortie.

   Insérer "waxberry" avant la ligne 2.

   ```Shell
   [root ~]# sed '2i waxberry' fruit.txt
   banana
   waxberry
   grape
   apple
   watermelon
   orange
   ```

   Supprimer la ligne 3.

   ```Shell
   [root ~]# sed '3d' fruit.txt
   banana
   grape
   watermelon
   orange
   ```

   Supprimer les lignes 2 à 4.

   ```Shell
   [root ~]# sed '2,4d' fruit.txt
   banana
   orange
   ```

   Remplacer le caractère 'a' par '@'.

   ```Shell
   [root ~]# sed 's#a#@#' fruit.txt 
   b@nana
   gr@pe
   @pple
   w@termelon
   or@nge
   ```

   Remplacer globalement le caractère 'a' par '@'.

   ```Shell
   [root ~]# sed 's#a#@#g' fruit.txt 
   b@n@n@
   gr@pe
   @pple
   w@termelon
   or@nge
   ```

2. Langage de traitement et de correspondance de motifs - **awk**.

   Awk est un langage de programmation et l'un des outils les plus puissants pour traiter le texte sous Linux. L'un de ses auteurs et l'actuel mainteneur est Brian Kernighan (partenaire proche de Ken et dmr). Awk peut extraire des colonnes spécifiques, utiliser des expressions régulières pour extraire du contenu, afficher des lignes spécifiques, et effectuer des statistiques et calculs.

   Supposons un fichier fruit2.txt avec le contenu suivant :

   ```Shell
   [root ~]# cat fruit2.txt 
   1       banana      120
   2       grape       500
   3       apple       1230
   4       watermelon  80
   5       orange      400
   ```

   Afficher la ligne 3.

   ```Shell
   [root ~]# awk 'NR==3' fruit2.txt 
   3       apple       1230
   ```

   Afficher la colonne 2.

   ```Shell
   [root ~]# awk '{print $2}' fruit2.txt 
   banana
   grape
   apple
   watermelon
   orange
   ```

   Afficher la dernière colonne.

   ```Shell
   [root ~]# awk '{print $NF}' fruit2.txt 
   120
   500
   1230
   80
   400
   ```

   Afficher les lignes où le dernier nombre est >= 300.

   ```Shell
   [root ~]# awk '{if($3 >= 300) {print $0}}' fruit2.txt 
   2       grape       500
   3       apple       1230
   5       orange      400
   ```

   Ceci n'est qu'une infime partie des capacités d'awk. Le lecteur est encouragé à explorer davantage.

### Gestion des utilisateurs

1. Créer/supprimer un utilisateur - **useradd** / **userdel**.

   ```Shell
   [root home]# useradd hellokitty
   [root home]# userdel hellokitty
   ```

   - `-d` : Spécifie le répertoire personnel de l'utilisateur.
   - `-g` : Spécifie le groupe principal de l'utilisateur.

2. Créer/supprimer un groupe - **groupadd** / **groupdel**.

   > **Note :** Les groupes facilitent la gestion collective des utilisateurs.

3. Modifier un mot de passe - **passwd**.

   ```Shell
   [root ~]# passwd hellokitty
   New password: 
   Retype new password: 
   passwd: all authentication tokens updated successfully.
   ```

   > **Note :** La saisie du mot de passe et de sa confirmation n'est pas affichée (aucun écho) et doit être effectuée sans interruption (pas de retour arrière). Les deux entrées doivent correspondre. Sans argument, `passwd` modifie le mot de passe de l'utilisateur courant. Pour modifier en masse, utilisez `chpasswd`.

   - `-l` / `-u` : Verrouille/déverrouille un compte utilisateur.
   - `-d` : Efface le mot de passe d'un utilisateur.
   - `-e` : Force l'expiration immédiate du mot de passe, obligeant l'utilisateur à le changer à la prochaine connexion.
   - `-i` : Désactive le compte après un certain nombre de jours suivant l'expiration du mot de passe.

4. Afficher/modifier la politique d'expiration des mots de passe - **chage**.

   Définir que l'utilisateur hellokitty doit changer son mot de passe dans 100 jours, être averti 15 jours avant expiration, et être désactivé 7 jours après expiration.

   ```Shell
   chage -M 100 -W 15 -I 7 hellokitty
   ```

5. Changer d'utilisateur - **su**.

   ```Shell
   [root ~]# su hellokitty
   [hellokitty root]$
   ```

6. Exécuter une commande en tant qu'administrateur - **sudo**.

   ```Shell
   [hellokitty ~]$ ls /root
   ls: cannot open directory /root: Permission denied
   [hellokitty ~]$ sudo ls /root
   [sudo] password for hellokitty:
   ```

   > **Note :** Pour qu'un utilisateur puisse exécuter des commandes avec sudo, il doit figurer dans la liste sudoers, définie dans le fichier `/etc/sudoers`. Pour éditer ce fichier de manière sécurisée, utilisez `visudo`.

7. Éditer le fichier sudoers - **visudo**.

   L'éditeur par défaut est vi (voir plus bas). Extrait du fichier :

   ```
   ## Allow root to run any commands anywhere 
   root    ALL=(ALL)   ALL
   
   ## Allows members of the 'sys' group to run networking, software, 
   ## service management apps and more.
   # %sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING, PROCESSES, LOCATE, DRIVERS
   ## Allows people in group wheel to run all commands
   %wheel  ALL=(ALL)   ALL
   
   ## Same thing without a password
   # %wheel    ALL=(ALL)   NOPASSWD: ALL
   
   ## Allows members of the users group to mount and unmount the
   ## cdrom as root
   # %users  ALL=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom
   
   ## Allows members of the users group to shutdown this system
   # %users  localhost=/sbin/shutdown -h now
   ```

8. Afficher les informations d'utilisateur et de groupe - **id**.

9. Envoyer un message à un autre utilisateur - **write** / **wall**.

   Expéditeur :

   ```Shell
   [root ~]# write hellokitty
   Dinner is on me.
   Call me at 6pm.
   ```

   Destinataire :

   ```Shell
   [hellokitty ~]$ 
   Message from root on pts/0 at 17:41 ...
   Dinner is on me.
   Call me at 6pm.
   EOF
   ```

10. Vérifier/définir la réception des messages - **mesg**.

   ```Shell
   [hellokitty ~]$ mesg
   is y
   [hellokitty ~]$ mesg n
   [hellokitty ~]$ mesg
   is n
   ```

### Système de fichiers

#### Fichiers et chemins

1. **Règles de nommage** : La longueur maximale d'un nom de fichier dépend du type de système de fichiers. Généralement, elle ne devrait pas dépasser 255 caractères. Bien que la plupart des caractères puissent être utilisés, il est préférable d'utiliser des lettres majuscules/minuscules, des chiffres, des underscores et des points. Les espaces sont possibles, mais à éviter (nécessitent des guillemets ou une échappement avec `\`).
2. **Extensions** : Sous Linux, les extensions sont facultatives mais utiles pour identifier le type de contenu. Certaines applications s'y fient, mais beaucoup d'autres non (comme la commande `file`).
3. **Fichiers cachés** : Les fichiers dont le nom commence par un point (`.`) sont cachés (invisibles par défaut).

#### Structure des répertoires

1. **/bin** - Exécutables des commandes essentielles.
2. **/boot** - Fichiers statiques du chargeur d'amorçage.
3. **/dev** - Fichiers de périphériques.
4. **/etc** - Fichiers de configuration.
5. **/home** - Répertoire parent des répertoires personnels des utilisateurs ordinaires.
6. **/lib** - Bibliothèques partagées.
7. **/lib64** - Bibliothèques partagées 64 bits.
8. **/lost+found** - Fichiers orphelins (après un fsck).
9. **/media** - Point de montage automatique pour médias amovibles.
10. **/mnt** - Point de montage temporaire.
11. **/opt** - Logiciels optionnels/add-ons.
12. **/proc** - Informations sur le noyau et les processus (système de fichiers virtuel).
13. **/root** - Répertoire personnel du superutilisateur (root).
14. **/run** - Données d'exécution du système (runtime).
15. **/sbin** - Exécutables système (administration).
16. **/sys** - Système de fichiers virtuel pour les informations sur les périphériques.
17. **/tmp** - Fichiers temporaires.
18. **/usr** - Hiérarchie secondaire des programmes utilisateur.
19. **/var** - Données variables (logs, caches, files d'attente, etc.).

#### Permissions d'accès

1. **chmod** - Modifie les permissions (mode bits).

   ```Shell
   [root ~]# ls -l
   ...
   -rw-r--r--  1 root       root 211878 Jun 19 16:06 sohu.html
   ...
   [root ~]# chmod g+w,o+w sohu.html
   [root ~]# ls -l
   ...
   -rw-rw-rw-  1 root       root 211878 Jun 19 16:06 sohu.html
   ...
   [root ~]# chmod 644 sohu.html
   [root ~]# ls -l
   ...
   -rw-r--r--  1 root       root 211878 Jun 19 16:06 sohu.html
   ...
   ```
   > **Note :** `chmod` utilise deux syntaxes : symbolique (ex: `g+w`) et numérique (ex: `644`). `umask` définit les permissions à retirer par défaut pour les nouveaux fichiers.

   La correspondance entre l'affichage long (`ls -l`) et la valeur numérique des permissions est résumée dans le tableau suivant :

   ![](./res/file-mode.png)

2. **chown** - Modifie le propriétaire d'un fichier.

    ```Shell
    [root ~]# ls -l
    ...
    -rw-r--r--  1 root root     54 Jun 20 10:06 readme.txt
    ...
    [root ~]# chown hellokitty readme.txt
    [root ~]# ls -l
    ...
    -rw-r--r--  1 hellokitty root     54 Jun 20 10:06 readme.txt
    ...
    ```

3. **chgrp** - Modifie le groupe propriétaire d'un fichier.

#### Gestion des disques

1. Afficher l'utilisation des disques - **df**.

   ```Shell
   [root ~]# df -h
   Filesystem      Size  Used Avail Use% Mounted on
   /dev/vda1        40G  5.0G   33G  14% /
   devtmpfs        486M     0  486M   0% /dev
   tmpfs           497M     0  497M   0% /dev/shm
   tmpfs           497M  356K  496M   1% /run
   tmpfs           497M     0  497M   0% /sys/fs/cgroup
   tmpfs           100M     0  100M   0% /run/user/0
   ```

2. Manipuler la table de partition - **fdisk**.

   ```Shell
   [root ~]# fdisk -l
   Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
   Units = sectors of 1 * 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   Disk label type: dos
   Disk identifier: 0x000a42f4
      Device Boot      Start         End      Blocks   Id  System
   /dev/vda1   *        2048    83884031    41940992   83  Linux
   Disk /dev/vdb: 21.5 GB, 21474836480 bytes, 41943040 sectors
   Units = sectors of 1 * 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   ```

3. Outil de partitionnement - **parted**.

4. Formater un système de fichiers - **mkfs**.

   ```Shell
   [root ~]# mkfs -t ext4 -v /dev/sdb
   ```

   - `-t` : Type de système de fichiers (ex: ext4).
   - `-c` : Vérifie les blocs défectueux.
   - `-v` : Mode verbeux.

5. Vérifier un système de fichiers - **fsck**.

6. Convertir ou copier des fichiers - **dd**.

7. Monter/démonter - **mount** / **umount**.

8. Créer/activer/désactiver une partition d'échange (swap) - **mkswap** / **swapon** / **swapoff**.

> **Note :** Ces commandes peuvent être risquées. Si vous n'êtes pas sûr de leur utilisation, faites preuve de prudence, consultez la documentation et assurez-vous de comprendre les conséquences avant d'agir.

### Éditeur - Vim

1. Lancer vim avec `vi` ou `vim`. On peut spécifier un nom de fichier pour l'ouvrir, ou le nommer lors de la sauvegarde.

   ```Shell
   [root ~]# vim guess.py
   ```

2. **Modes** : Normal (commande), Insertion (édition) et Ligne de commande (ex:).
   - Au démarrage, on est en mode Normal.
   - En mode Normal, appuyer sur `i` passe en mode Insertion (`-- INSERT --` en bas).
   - En mode Insertion, `Esc` revient en mode Normal.
   - En mode Normal, `:` passe en mode Ligne de commande.
   - En mode Normal, `v` passe en mode Visuel (sélection).

3. **Sauvegarder et quitter** :
   - En mode Normal, `:wq` sauvegarde et quitte.
   - `:q!` quitte sans sauvegarder (force).
   - En mode Normal, `ZZ` sauvegarde et quitte.
   - `:w` sauvegarde sans quitter. `:w nom_fichier` sauvegarde sous un autre nom.

4. **Déplacement du curseur** (mode Normal) :
   - `h` (gauche), `j` (bas), `k` (haut), `l` (droite).
   - Préfixer par un nombre (ex: `10h`) pour répéter.
   - `Ctrl+y` / `Ctrl+e` : faire défiler d'une ligne.
   - `Ctrl+f` / `Ctrl+b` : page suivante / précédente.
   - `G` : aller à la fin du fichier.
   - `gg` : aller au début du fichier.
   - `[num]G` : aller à la ligne spécifiée.

5. **Manipulation de texte** (mode Normal) :
   - **Supprimer** : `dd` (ligne), `[num]dd` (plusieurs lignes), `d$` (jusqu'à la fin de la ligne), `d0` (début de ligne), `dw` (mot), `:%d` (supprimer tout le fichier).
   - **Copier/Coller** : `yy` (ligne), `[num]yy`, `p` (coller après le curseur), `P` (coller avant).
   - **Annuler/Rétablir** : `u` (annuler), `Ctrl+r` (rétablir).
   - **Trier** : `%!sort` (trier les lignes).

6. **Rechercher et remplacer** :
   - Recherche : En mode Normal, `/regex` (ex: `/doc.*\.`). `n` pour suivant, `N` pour précédent.
   - Remplacement : En mode Ligne de commande, `:[plage]s/motif/remplacement/[options]`. Ex: `:1,$s/doc.*/hello/gice`
     - `g` : global (toutes les occurrences sur la ligne).
     - `i` : insensible à la casse.
     - `c` : demande confirmation.
     - `e` : ignore les erreurs.

7. **Paramètres** (mode Ligne de commande) :
   - `set ts=4` : définit la taille de la tabulation à 4 espaces.
   - `set nu` / `set nonu` : affiche/masque les numéros de ligne.
   - `syntax on` / `syntax off` : active/désactive la coloration syntaxique.
   - `set ruler` : affiche la position du curseur (ligne, colonne).
   - `set hls` / `set nohls` : met en surbrillance les résultats de recherche.

   > **Note :** Pour rendre ces paramètres permanents, ajoutez-les au fichier `~/.vimrc`.

8. **Techniques avancées**
   - **Comparer des fichiers** : `vim -d fichier1 fichier2`
   - **Ouvrir plusieurs fichiers** : `vim fichier1 fichier2 fichier3`. Ensuite, `:ls` pour les lister, `:b [num]` pour basculer.
   - **Diviser la fenêtre** : `:sp` (horizontal), `:vs` (vertical). `Ctrl+w` deux fois pour naviguer entre les fenêtres.
   - **Mapper des raccourcis** :
     - Exemple en mode Normal : `:map <F4> gg10000dd` (supprime 10000 lignes avec F4).
     - Exemple en mode Insertion : `:inoremap __main if __name__ == '__main__':` (complète __main).
     > **Important :** Utiliser `nore` (`noremap`, `inoremap`) pour éviter la récursion. Ajouter au `~/.vimrc` pour persistance.
   - **Enregistrer une macro** :
     1. En mode Normal, `qa` commence l'enregistrement dans le registre 'a'.
     2. Effectuez les actions (déplacements, modifications).
     3. Appuyez sur `q` pour arrêter.
     4. Rejouez avec `@a`. `100@a` la rejoue 100 fois.

### Installation et configuration des logiciels

#### Utilisation des gestionnaires de paquets

1. **yum** - Gestionnaire de paquets pour RHEL/CentOS/Fedora.
   - `yum search` : Recherche un paquet.
   - `yum list installed` : Liste les paquets installés.
   - `yum install` : Installe un paquet.
   - `yum remove` : Supprime un paquet.
   - `yum update` : Met à jour tous les paquets ou un paquet spécifié.
   - `yum check-update` : Vérifie les mises à jour disponibles.
   - `yum info` : Affiche les informations sur un paquet.

2. **rpm** - Outil de bas niveau pour les paquets RPM.
   - Installation : `rpm -ivh paquet.rpm`
   - Désinstallation : `rpm -e nom_paquet`
   - Requête : `rpm -qa` (liste tous les paquets installés). Ex: `rpm -qa | grep mysql`.

Exemple d'installation de Nginx avec yum :

```Shell
[root ~]# yum -y install nginx
...
Installed:
  nginx.x86_64 1:1.12.2-2.el7
Dependency Installed:
  nginx-all-modules.noarch 1:1.12.2-2.el7
  nginx-mod-http-geoip.x86_64 1:1.12.2-2.el7
  nginx-mod-http-image-filter.x86_64 1:1.12.2-2.el7
  nginx-mod-http-perl.x86_64 1:1.12.2-2.el7
  nginx-mod-http-xslt-filter.x86_64 1:1.12.2-2.el7
  nginx-mod-mail.x86_64 1:1.12.2-2.el7
  nginx-mod-stream.x86_64 1:1.12.2-2.el7
Complete!
[root ~]# yum info nginx
...
[root ~]# nginx -v
nginx version: nginx/1.12.2
```

Désinstaller Nginx :

```Shell
[root ~]# yum -y remove nginx
```

Exemple d'installation de MySQL avec rpm (télécharger les fichiers RPM depuis le site officiel). Note : MySQL est maintenant sous Oracle. MariaDB, un fork de MySQL, est disponible via yum.

```Shell
[root mysql]# ls
mysql-community-client-5.7.22-1.el7.x86_64.rpm
mysql-community-common-5.7.22-1.el7.x86_64.rpm
mysql-community-libs-5.7.22-1.el7.x86_64.rpm
mysql-community-server-5.7.22-1.el7.x86_64.rpm
[root mysql]# yum -y remove mariadb-libs
[root mysql]# yum -y install libaio
[root mysql]# rpm -ivh mysql-community-common-5.7.26-1.el7.x86_64.rpm
...
[root mysql]# rpm -ivh mysql-community-libs-5.7.26-1.el7.x86_64.rpm
...
[root mysql]# rpm -ivh mysql-community-client-5.7.26-1.el7.x86_64.rpm
...
[root mysql]# rpm -ivh mysql-community-server-5.7.26-1.el7.x86_64.rpm
...
```

> **Note :** Il y a des conflits entre les bibliothèques sous-jacentes de MySQL et MariaDB, d'où la suppression de `mariadb-libs` et l'installation de `libaio`.

Désinstaller MySQL :

```Shell
[root ~]# rpm -qa | grep mysql | xargs rpm -e
```

#### Téléchargement, extraction et configuration des variables d'environnement

Exemple avec MongoDB :

```Shell
[root ~]# wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz
--2018-06-21 18:32:53--  https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz
...
[root ~]# gunzip mongodb-linux-x86_64-rhel70-3.6.5.tgz
[root ~]# tar -xvf mongodb-linux-x86_64-rhel70-3.6.5.tar
...
[root ~]# vim .bash_profile
...
PATH=$PATH:$HOME/bin:$HOME/mongodb-linux-x86_64-rhel70-3.6.5/bin
export PATH
...
[root ~]# source .bash_profile
[root ~]# mongod --version
db version v3.6.5
...
[root ~]# mongo --version
MongoDB shell version v3.6.5
...
```

> **Note :** MongoDB peut aussi être installé via yum (voir la documentation officielle).

#### Compilation depuis les sources

1. **Installer Python 3.6**.

   ```Shell
   [root ~]# yum install gcc
   [root ~]# wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz
   [root ~]# gunzip Python-3.6.5.tgz
   [root ~]# tar -xvf Python-3.6.5.tar
   [root ~]# cd Python-3.6.5
   [root ~]# ./configure --prefix=/usr/local/python36 --enable-optimizations
   [root ~]# yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
   [root ~]# make && make install
   ...
   [root ~]# ln -s /usr/local/python36/bin/python3.6 /usr/bin/python3
   [root ~]# python3 --version
   Python 3.6.5
   [root ~]# python3 -m pip install -U pip
   [root ~]# pip3 --version
   ```

   > **Note :** Après l'installation, il faut ajouter le chemin des binaires de Python au PATH. Modifiez soit `~/.bash_profile` (utilisateur) soit `/etc/profile` (système).

2. **Installer Redis-3.2.12**.

   ```Shell
   [root ~]# wget http://download.redis.io/releases/redis-3.2.12.tar.gz
   [root ~]# gunzip redis-3.2.12.tar.gz
   [root ~]# tar -xvf redis-3.2.12.tar
   [root ~]# cd redis-3.2.12
   [root ~]# make && make install
   [root ~]# redis-server --version
   Redis server v=3.2.12 sha=00000000:0 malloc=jemalloc-4.0.3 bits=64 build=5bc5cd3c03d6ceb6
   [root ~]# redis-cli --version
   redis-cli 3.2.12
   ```

### Configurer les services

Linux peut héberger divers services (base de données, serveur web, cache, fichiers, files d'attente, etc.). La plupart des services Linux sont configurés en tant que démons (daemons, processus tournant en arrière-plan, d'où le suffixe 'd' : firewalld, mysqld, httpd, etc.). Après l'installation, utilisez `systemctl` (ou l'ancien `service`) pour gérer un service.

1. Démarrer le service firewall.

   ```Shell
   [root ~]# systemctl start firewalld
   ```

2. Arrêter le service firewall.

   ```Shell
   [root ~]# systemctl stop firewalld
   ```

3. Redémarrer le service firewall.

   ```Shell
   [root ~]# systemctl restart firewalld
   ```

4. Vérifier l'état du service firewall.

    ```Shell
    [root ~]# systemctl status firewalld
    ```

5. Activer/désactiver le démarrage automatique du service firewall.

   ```Shell
   [root ~]# systemctl enable firewalld
   Created symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.
   Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.
   [root ~]# systemctl disable firewalld
   Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
   Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
   ```

### Tâches planifiées

1. **Exécuter une commande à une heure précise** : **at**, **atq**, **atrm**.

   Planifier une tâche pour dans 3 jours à 17h.

   ```Shell
   [root ~]# at 5pm+3days
   at> rm -f /root/*.html
   at> <EOT>
   job 9 at Wed Jun  5 17:00:00 2019
   ```

   Lister les tâches en attente.

   ```Shell
   [root ~]# atq
   9       Wed Jun  5 17:00:00 2019 a root
   ```

   Supprimer une tâche planifiée.

   ```Shell
   [root ~]$ atrm 9
   ```

2. **Table des tâches planifiées (cron)** - **crontab**.

   ```Shell
   [root ~]# crontab -e
   * * * * * echo "hello, world!" >> /root/hello.txt
   59 23 * * * rm -f /root/*.log
   ```
   > **Note :** `crontab -e` ouvre un éditeur (vim) pour définir des expressions Cron et les commandes associées. L'exemple ci-dessus définit deux tâches : une qui ajoute "hello, world!" à un fichier chaque minute, et une autre qui supprime les fichiers .log tous les jours à 23h59. Pour générer des expressions Cron, utilisez un outil en ligne ou consultez `/etc/crontab`.

   Les fichiers liés à cron se trouvent dans `/etc`. Modifier `/etc/crontab` est une autre façon de définir des tâches planifiées (souvent pour le système entier).

   ```Shell
   [root ~]# cd /etc
   [root etc]# ls -l | grep cron
   -rw-------.  1 root root      541 Aug  3  2017 anacrontab
   drwxr-xr-x.  2 root root     4096 Mar 27 11:56 cron.d
   drwxr-xr-x.  2 root root     4096 Mar 27 11:51 cron.daily
   -rw-------.  1 root root        0 Aug  3  2017 cron.deny
   drwxr-xr-x.  2 root root     4096 Mar 27 11:50 cron.hourly
   drwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.monthly
   -rw-r--r--   1 root root      493 Jun 23 15:09 crontab
   drwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.weekly
   [root etc]# vim crontab
     1 SHELL=/bin/bash
     2 PATH=/sbin:/bin:/usr/sbin:/usr/bin
     3 MAILTO=root
     4
     5 # For details see man 4 crontabs
     6
     7 # Example of job definition:
     8 # .---------------- minute (0 - 59)
     9 # |  .------------- hour (0 - 23)
    10 # |  |  .---------- day of month (1 - 31)
    11 # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
    12 # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
    13 # |  |  |  |  |
    14 # *  *  *  *  * user-name  command to be executed
   ```

### Accès et gestion réseau

1. Connexion distante sécurisée - **ssh**.

    ```Shell
    [root ~]$ ssh root@120.77.222.217
    The authenticity of host '120.77.222.217 (120.77.222.217)' can't be established.
    ECDSA key fingerprint is SHA256:BhUhykv+FvnIL03I9cLRpWpaCxI91m9n7zBWrcXRa8w.
    ECDSA key fingerprint is MD5:cc:85:e9:f0:d7:07:1a:26:41:92:77:6b:7f:a0:92:65.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added '120.77.222.217' (ECDSA) to the list of known hosts.
    root@120.77.222.217's password: 
    ```

2. Télécharger des ressources depuis le réseau - **wget**.

   - `-b` : Mode arrière-plan.
   - `-O` : Spécifie le nom du fichier de sortie.
   - `-r` : Téléchargement récursif.

3. Envoyer/recevoir des emails - **mail**.

4. Configuration réseau (ancien) - **ifconfig**.

   ```Shell
   [root ~]# ifconfig eth0
   eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
           inet 172.18.61.250  netmask 255.255.240.0  broadcast 172.18.63.255
           ether 00:16:3e:02:b6:46  txqueuelen 1000  (Ethernet)
           RX packets 1067841  bytes 1296732947 (1.2 GiB)
           RX errors 0  dropped 0  overruns 0  frame 0
           TX packets 409912  bytes 43569163 (41.5 MiB)
           TX errors 0  dropped 0 overruns 0  carrier 0  collisions 
   ```

5. Configuration réseau (nouveau) - **ip**.

   ```Shell
   [root ~]# ip address
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
       link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
       inet 127.0.0.1/8 scope host lo
          valid_lft forever preferred_lft forever
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
       link/ether 00:16:3e:02:b6:46 brd ff:ff:ff:ff:ff:ff
       inet 172.18.61.250/20 brd 172.18.63.255 scope global eth0
          valid_lft forever preferred_lft forever
   ```

6. Vérifier la connectivité réseau - **ping**.

   ```Shell
   [root ~]# ping www.baidu.com -c 3
   PING www.a.shifen.com (220.181.111.188) 56(84) bytes of data.
   64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=1 ttl=51 time=36.3 ms
   64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=2 ttl=51 time=36.4 ms
   64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=3 ttl=51 time=36.4 ms
   --- www.a.shifen.com ping statistics ---
   3 packets transmitted, 3 received, 0% packet loss, time 2002ms
   rtt min/avg/max/mdev = 36.392/36.406/36.427/0.156 ms
   ```

7. Afficher/gérer la table de routage - **route**.

8. Afficher les services réseau et les ports - **netstat** / **ss**.

   ```Shell
   [root ~]# netstat -nap | grep nginx
   ```

9. Analyse du trafic réseau - **tcpdump**.

10. Copie sécurisée de fichiers - **scp**.

  ```Shell
  [root ~]# scp root@1.2.3.4:/root/guido.jpg hellokitty@4.3.2.1:/home/hellokitty/pic.jpg
  ```

11. Synchronisation de fichiers - **rsync**.

    > **Note :** `rsync` est essentiel pour la synchronisation automatique de fichiers, cruciale pour les serveurs de fichiers. Nous verrons son utilisation en détail lors du déploiement de projets.

12. Transfert sécurisé de fichiers - **sftp**.

    ```Shell
    [root ~]# sftp root@1.2.3.4
    root@1.2.3.4's password:
    Connected to 1.2.3.4.
    sftp>
    ```

    - `help` : Aide.
    - `ls` / `lls` : Liste des fichiers distant/local.
    - `cd` / `lcd` : Change de répertoire distant/local.
    - `mkdir` / `lmkdir` : Crée un répertoire distant/local.
    - `pwd` / `lpwd` : Affiche le répertoire courant distant/local.
    - `get` : Télécharge un fichier.
    - `put` : Téléverse un fichier.
    - `rm` : Supprime un fichier distant.
    - `bye` / `exit` / `quit` : Quitte sftp.

### Gestion des processus

1. Afficher les processus - **ps**.

   ```Shell
   [root ~]# ps -ef
   UID        PID  PPID  C STIME TTY          TIME CMD
   root         1     0  0 Jun23 ?        00:00:05 /usr/lib/systemd/systemd --switched-root --system --deserialize 21
   root         2     0  0 Jun23 ?        00:00:00 [kthreadd]
   ...
   [root ~]# ps -ef | grep mysqld
   root      4943  4581  0 22:45 pts/0    00:00:00 grep --color=auto mysqld
   mysql    25257     1  0 Jun25 ?        00:00:39 /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid
   ```

2. Arbre des processus - **pstree**.

    ```Shell
    [root ~]# pstree
    systemd─┬─AliYunDun───18*[{AliYunDun}]
            ├─AliYunDunUpdate───3*[{AliYunDunUpdate}]
            ├─2*[agetty]
            ├─aliyun-service───2*[{aliyun-service}]
            ├─atd
            ├─auditd───{auditd}
            ├─dbus-daemon
            ├─dhclient
            ├─irqbalance
            ├─lvmetad
            ├─mysqld───28*[{mysqld}]
            ├─nginx───2*[nginx]
            ├─ntpd
            ├─polkitd───6*[{polkitd}]
            ├─rsyslogd───2*[{rsyslogd}]
            ├─sshd───sshd───bash───pstree
            ├─systemd-journal
            ├─systemd-logind
            ├─systemd-udevd
            └─tuned───4*[{tuned}]
    ```

3. Rechercher un processus par critères - **pgrep**.

   ```Shell
   [root ~]$ pgrep mysqld
   3584
   ```

4. Tuer un processus par son PID - **kill**.

   ```Shell
   [root ~]$ kill -l
    1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
    6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
   11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
   16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
   21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
   26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
   31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
   38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
   43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
   48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
   53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
   58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
   63) SIGRTMAX-1  64) SIGRTMAX
   [root ~]# kill 1234
   [root ~]# kill -9 1234
   ```

5. Tuer un processus par son nom - **killall** / **pkill**.

    Arrêter le processus mysqld.

    ```Shell
    [root ~]# pkill mysqld
    ```

    Arrêter tous les processus de l'utilisateur hellokitty.

    ```Shell
    [root ~]# pkill -u hellokitty
    ```

    > **Note :** Cela déconnectera l'utilisateur hellokitty.

6. Mettre un processus en arrière-plan.

   - `Ctrl+Z` : Suspend le processus et le place en arrière-plan.
   - `&` : Lance directement le processus en arrière-plan.

   ```Shell
   [root ~]# mongod &
   [root ~]# redis-server
   ...
   ^Z
   [4]+  Stopped                 redis-server
   ```

7. Lister les travaux en arrière-plan - **jobs**.

   ```Shell
   [root ~]# jobs
   [2]   Running                 mongod &
   [3]-  Stopped                 cat
   [4]+  Stopped                 redis-server
   ```

8. Reprendre un travail suspendu en arrière-plan - **bg**.

   ```Shell
   [root ~]# bg %4
   [4]+ redis-server &
   [root ~]# jobs
   [2]   Running                 mongod &
   [3]+  Stopped                 cat
   [4]-  Running                 redis-server &
   ```

9. Ramener un travail en premier plan - **fg**.

    ```Shell
    [root ~]# fg %4
    redis-server
    ```

    > **Note :** Un processus au premier plan peut être arrêté avec `Ctrl+C`.

10. Ajuster la priorité d'un processus - **nice** / **renice**.

11. Exécuter un processus après la déconnexion - **nohup**.

     ```Shell
     [root ~]# nohup ping www.baidu.com > result.txt &
     ```

12. Suivre les appels système d'un processus - **strace**.

     ```Shell
     [root ~]# pgrep mysqld
     8803
     [root ~]# strace -c -p 8803
     strace: Process 8803 attached
     ^Cstrace: Process 8803 detached
     % time     seconds  usecs/call     calls    errors syscall
     ------ ----------- ----------- --------- --------- ----------------
      99.18    0.005719        5719         1           restart_syscall
       0.49    0.000028          28         1           mprotect
       0.24    0.000014          14         1           clone
       0.05    0.000003           3         1           mmap
       0.03    0.000002           2         1           accept
     ------ ----------- ----------- --------- --------- ----------------
     100.00    0.005766                     5           total
     ```

     > **Note :** Cette commande est complexe ; consultez la documentation quand nécessaire.

13. Afficher le niveau d'exécution courant - **runlevel**.

     ```Shell
     [root ~]# runlevel
     N 3
     ```

14. Surveiller l'utilisation des ressources en temps réel - **top**.

     ```Shell
     [root ~]# top
     top - 23:04:23 up 3 days, 14:10,  1 user,  load average: 0.00, 0.01, 0.05
     Tasks:  65 total,   1 running,  64 sleeping,   0 stopped,   0 zombie
     %Cpu(s):  0.3 us,  0.3 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
     KiB Mem :  1016168 total,   191060 free,   324700 used,   500408 buff/cache
     KiB Swap:        0 total,        0 free,        0 used.   530944 avail Mem
     ...
     ```

     - `-c` : Affiche le chemin complet de la commande.
     - `-d` : Intervalle entre les mises à jour (en secondes).
     - `-i` : Ignore les processus inactifs ou zombies.
     - `-p` : Surveille un PID spécifique.

### Diagnostic système

1. Diagnostic du démarrage - **dmesg**.

2. Activité système - **sar**.

   ```Shell
   [root ~]# sar -u -r 5 10
   Linux 3.10.0-957.10.1.el7.x86_64 (izwz97tbgo9lkabnat2lo8z)      06/02/2019      _x86_64_        (2 CPU)
   
   06:48:30 PM     CPU     %user     %nice   %system   %iowait    %steal     %idle
   06:48:35 PM     all      0.10      0.00      0.10      0.00      0.00     99.80
   
   06:48:30 PM kbmemfree kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
   06:48:35 PM   1772012   2108392     54.33    102816   1634528    784940     20.23    793328   1164704         0
   ```

   - `-A` : Tous les périphériques (CPU, mémoire, disque).
   - `-u` : Charge CPU.
   - `-d` : Activité des disques.
   - `-r` : Utilisation de la mémoire.
   - `-n` : État du réseau.

3. Utilisation de la mémoire - **free**.

   ```Shell
   [root ~]# free
                 total        used        free      shared  buff/cache   available
   Mem:        1016168      323924      190452         356      501792      531800
   Swap:             0           0           0
   ```

4. Statistiques de mémoire virtuelle - **vmstat**.

   ```Shell
   [root ~]# vmstat
   procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
    r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
    2  0      0 204020  79036 667532    0    0     5    18  101   58  1  0 99  0  0
   ```

5. Statistiques CPU - **mpstat**.

   ```Shell
   [root ~]# mpstat
   Linux 3.10.0-957.5.1.el7.x86_64 (iZ8vba0s66jjlfmo601w4xZ)       05/30/2019      _x86_64_        (1 CPU)
   
   01:51:54 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
   01:51:54 AM  all    0.71    0.00    0.17    0.04    0.00    0.00    0.00    0.00    0.00   99.07
   ```

6. Utilisation de la mémoire par processus - **pmap**.

   ```Shell
   [root ~]# ps
     PID TTY          TIME CMD
    4581 pts/0    00:00:00 bash
    5664 pts/0    00:00:00 ps
   [root ~]# pmap 4581
   4581:   -bash
   0000000000400000    884K r-x-- bash
   00000000006dc000      4K r---- bash
   00000000006dd000     36K rw--- bash
   00000000006e6000     24K rw---   [ anon ]
   0000000001de0000    400K rw---   [ anon ]
   00007f82fe805000     48K r-x-- libnss_files-2.17.so
   00007f82fe811000   2044K ----- libnss_files-2.17.so
   ...
   ```

7. Statistiques d'E/S et CPU des périphériques - **iostat**.

   ```Shell
   [root ~]# iostat
   Linux 3.10.0-693.11.1.el7.x86_64 (iZwz97tbgo9lkabnat2lo8Z)      06/26/2018      _x86_64_       (1 CPU)
   avg-cpu:  %user   %nice %system %iowait  %steal   %idle
              0.79    0.00    0.20    0.04    0.00   98.97
   Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
   vda               0.85         6.78        21.32    2106565    6623024
   vdb               0.00         0.01         0.00       2088          0
   ```

8. Lister les périphériques PCI - **lspci**.

   ```Shell
   [root ~]# lspci
   00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)
   00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]
   00:01.1 IDE interface: Intel Corporation 82371SB PIIX3 IDE [Natoma/Triton II]
   00:01.2 USB controller: Intel Corporation 82371SB PIIX3 USB [Natoma/Triton II] (rev 01)
   00:01.3 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 03)
   00:02.0 VGA compatible controller: Cirrus Logic GD 5446
   00:03.0 Ethernet controller: Red Hat, Inc. Virtio network device
   00:04.0 Communication controller: Red Hat, Inc. Virtio console
   00:05.0 SCSI storage controller: Red Hat, Inc. Virtio block device
   00:06.0 SCSI storage controller: Red Hat, Inc. Virtio block device
   00:07.0 Unclassified device [00ff]: Red Hat, Inc. Virtio memory balloon
   ```

9. État des mécanismes de communication inter-processus - **ipcs**.

   ```Shell
   [root ~]# ipcs
   
   ------ Message Queues --------
   key        msqid      owner      perms      used-bytes   messages    
   
   ------ Shared Memory Segments --------
   key        shmid      owner      perms      bytes      nattch     status      
   
   ------ Semaphore Arrays --------
   key        semid      owner      perms      nsems
   ```

### Programmation Shell

Le Shell est une interface entre l'utilisateur et le système d'exploitation, offrant un accès aux services du noyau. Un script Shell est un programme écrit pour le Shell, permettant l'administration système et la manipulation de fichiers. Écrire des scripts Shell est une compétence essentielle pour tout utilisateur avancé de Linux.

Plutôt qu'un cours complet, voici quelques exemples pour illustrer.

**Exemple 1** : Somme des entiers de m à n.

```Shell
#!/usr/bin/bash
printf 'm = '
read m
printf 'n = '
read n
a=$m
sum=0
while [ $a -le $n ]
do
    sum=$[ sum + a ]
    a=$[ a + 1 ]
done
echo 'Résultat: '$sum
```

**Exemple 2** : Création automatique de répertoire et de fichiers.

```Shell
#!/usr/bin/bash
printf 'Nom du répertoire: '
read dir
printf 'Nom de base des fichiers: '
read file
printf 'Nombre de fichiers (<1000): '
read num
if [ $num -ge 1000 ]
then
    echo 'Le nombre de fichiers ne peut pas dépasser 1000'
else
    if [ -e $dir -a -d $dir ]
    then
        rm -rf $dir
    else
        if [ -e $dir -a -f $dir ]
        then
            rm -f $dir
        fi
    fi
    mkdir -p $dir
    index=1
    while [ $index -le $num ]
    do
        if [ $index -lt 10 ]
        then
            pre='00'
        elif [ $index -lt 100 ]
        then
            pre='0'
        else
            pre=''
        fi
        touch $dir'/'$file'_'$pre$index
        index=$[ index + 1 ]
    done
fi
```

**Exemple 3** : Installation automatique d'une version spécifique de Redis.

```Shell
#!/usr/bin/bash
install_redis() {
    if ! which redis-server > /dev/null
    then
        cd /root
        wget $1$2'.tar.gz' >> install.log
        gunzip /root/$2'.tar.gz'
        tar -xf /root/$2'.tar'
        cd /root/$2
        make >> install.log
        make install >> install.log
        echo 'Installation terminée'
    else
        echo 'Redis est déjà installé'
    fi
}

install_redis 'http://download.redis.io/releases/' $1
```

### Ressources complémentaires

1. Raccourcis clavier courants en ligne de commande Linux

   | Raccourci | Description |
   |-----------|-------------|
   | Tab | Complétion automatique (commande ou chemin) |
   | Ctrl+a | Déplacer le curseur en début de ligne |
   | Ctrl+e | Déplacer le curseur en fin de ligne |
   | Ctrl+f | Déplacer le curseur d'un caractère vers la droite |
   | Ctrl+b | Déplacer le curseur d'un caractère vers la gauche |
   | Ctrl+k | Couper du curseur à la fin de la ligne |
   | Ctrl+u | Couper du curseur au début de la ligne |
   | Ctrl+w | Couper le mot précédent |
   | Ctrl+y | Coller le texte coupé |
   | Ctrl+c | Interrompre la tâche en cours |
   | Ctrl+h | Effacer le caractère précédent (comme Backspace) |
   | Ctrl+d | Se déconnecter (ou fin de fichier) |
   | Ctrl+r | Recherche dans l'historique des commandes |
   | Ctrl+g | Quitter la recherche dans l'historique |
   | Ctrl+l | Effacer l'écran (clear) |
   | Ctrl+s | Geler l'affichage du terminal |
   | Ctrl+q | Reprendre l'affichage du terminal |
   | Ctrl+z | Suspendre la tâche en cours et la mettre en arrière-plan |
   | !! | Exécuter la dernière commande |
   | !num | Exécuter la commande numéro 'num' de l'historique |
   | !lettre | Exécuter la dernière commande commençant par 'lettre' |
   | !$ / Esc+. | Obtenir le dernier argument de la commande précédente |
   | Esc+b | Aller au début du mot précédent |
   | Esc+f | Aller à la fin du mot suivant |

2. Sections du manuel (man pages)

   | Section | Contenu |
   |---------|---------|
   | NAME | Nom et brève description de la commande |
   | SYNOPSIS | Syntaxe d'utilisation de base |
   | DESCRIPTION | Description détaillée, rôle des options |
   | OPTIONS | Explication des options de la commande |
   | EXAMPLES | Exemples d'utilisation |
   | EXIT STATUS | Codes de retour (0 = succès) |
   | SEE ALSO | Commandes ou informations connexes |
   | BUGS | Problèmes connus |
   | AUTHOR | Auteur de la commande |