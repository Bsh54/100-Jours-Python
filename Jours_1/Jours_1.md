# Découverte de Python
## Présentation de Python
Python (prononciation anglaise : /ˈpaɪθən/ ; prononciation américaine : /ˈpaɪθɑːn/) est un langage de programmation inventé par le Néerlandais Guido van Rossum. C’est actuellement le langage de programmation le plus populaire et le plus utilisé dans le monde. Python met l’accent sur la lisibilité du code et la simplicité de la syntaxe. Comparé à des langages de programmation tout aussi influents comme C, C++ ou Java, Python permet aux utilisateurs d’exprimer leurs intentions avec moins de lignes de code. Voici quelques classements de langages de programmation par des autorités, montrant la position de Python. La première image est fournie par le TIOBE Index, la troisième par IEEE Spectrum. Il convient de noter la deuxième image, qui montre la popularité des langages de programmation sur GitHub, la plus grande plateforme d’hébergement de code au monde. Python a occupé la première place ces quatre dernières années.


## Chronologie de Python
Voici quelques dates clés du développement du langage Python :

*   **Décembre 1989 :** Guido van Rossum décide de développer un nouveau langage de script et son interpréteur pour occuper les vacances de Noël. Le nouveau langage sera le successeur du langage ABC, principalement destiné à remplacer les scripts Unix shell et le C pour l’administration système. Guido étant un fan de la série télévisée BBC Monty Python's Flying Circus, il choisit le mot « Python » comme nom du nouveau langage.
*   **Février 1991 :** Guido van Rossum publie le code initial de l’interpréteur Python sur le groupe de discussion alt.sources, marqué version 0.9.0.
*   **Janvier 1994 :** Python 1.0 est publié, le début du rêve.
*   **Octobre 2000 :** Python 2.0 est publié, le processus de développement devient plus transparent et l’écosystème commence à se former.
*   **Décembre 2008 :** Python 3.0 est publié, introduisant de nombreuses caractéristiques des langages de programmation modernes, mais sans être entièrement rétrocompatible.
*   **Avril 2011 :** pip est publié pour la première fois, Python a désormais son propre gestionnaire de paquets.
*   **Juillet 2018 :** Guido van Rossum annonce qu’il se « retire définitivement » de son rôle de « Benevolent Dictator For Life » (BDFL, la personne ayant le dernier mot en cas de litige dans la communauté du projet open source).
*   **Janvier 2020 :** Après 11 ans de coexistence de Python 2 et Python 3, les mises à jour et la maintenance de Python 2 sont officiellement arrêtées, les utilisateurs étant encouragés à passer à Python 3.
*   **Actuellement :** Python est largement utilisé dans de nombreux domaines comme les grands modèles (GPT-3, GPT-4, BERT, etc.), la vision par ordinateur (reconnaissance d’images, détection d’objets, génération d’images, etc.), les recommandations intelligentes (YouTube, Netflix, ByteDance, etc.), la conduite autonome (Waymo, Apollo, etc.), la reconnaissance vocale, la science des données, le trading quantitatif, les tests automatisés, l’administration système automatisée, etc. L’écosystème du langage Python est également très riche.

<<<<<<< HEAD:Jour_1/Jour_1.md
 
=======


>>>>>>> 2347c232da8df7353255f7a672a8c931e4d8238d:Jour_1.md
## Avantages et inconvénients de Python
Python possède de nombreux avantages, en voici quelques-uns.

*   Simple et élégant, comparé à beaucoup d’autres langages de programmation, Python est plus facile à prendre en main.
*   Permet de faire plus avec moins de code, améliore l’efficacité du développement.
*   Open source, dispose d’une communauté et d’un écosystème puissants.
*   Capable de faire énormément de choses, a une capacité d’adaptation extrêmement forte.
*   Langage « glue » (colle), peut relier des composants développés dans d’autres langages.
*   Langage interprété, plus facilement cross-plateforme, peut fonctionner sur plusieurs systèmes d’exploitation.

Le principal inconvénient de Python est sa faible efficacité d’exécution (problème courant des langages interprétés). Si l’efficacité d’exécution du code est primordiale, C, C++ ou Go peuvent être de meilleurs choix.

## Installer l’environnement Python
Pour bien travailler, il faut d’abord aiguiser ses outils. Pour commencer votre voyage en programmation Python, vous devez d’abord installer l’environnement Python sur votre ordinateur. En termes simples, il s’agit d’installer l’interpréteur Python nécessaire pour exécuter les programmes Python. Nous vous recommandons d’installer l’interpréteur Python 3 officiel, écrit en C, souvent appelé CPython. C’est probablement votre meilleur choix actuel. Tout d’abord, vous devez trouver le lien de téléchargement sur la page de téléchargement du site officiel. Après avoir cliqué sur le bouton « Download » pour accéder à la page de téléchargement, choisissez le programme d’installation de Python 3 adapté à votre système d’exploitation.


Sur la page de téléchargement, certaines versions de Python ne fournissent pas de programme d’installation pour Windows et macOS, seulement des archives de code source. Pour les personnes familières avec Linux, nous pouvons procéder à une installation à partir des sources. Pour ceux qui utilisent Windows ou macOS, nous recommandons vivement d’utiliser le programme d’installation. Par exemple, pour installer Python 3.10, en choisissant Python 3.10.10 ou Python 3.10.11, vous trouverez les paquets d’installation pour Windows ou macOS, tandis que d’autres versions peuvent n’avoir que le code source.


### Environnement Windows
Nous prenons Windows 11 comme exemple pour expliquer comment installer l’environnement Python sur un système d’exploitation Windows. Double-cliquez sur le programme d’installation téléchargé depuis le site officiel, cela ouvrira un assistant d’installation.


Tout d’abord, n’oubliez pas de cocher l’option « Add python.exe to PATH ». Elle nous aidera à ajouter l’interpréteur Python à la variable d’environnement PATH du système Windows (ne vous inquiétez pas si vous ne comprenez pas, cochez-la simplement). Ensuite, « Use admin privileges when installing py.exe » permet d’obtenir des privilèges d’administrateur pendant l’installation, il est recommandé de la cocher. Puis, nous choisissons « Customize Installation », le mode d’installation personnalisé. C’est le choix des professionnels, et vous (faites semblant d’) êtes ce professionnel. Il n’est pas recommandé d’utiliser « Install Now » (installation par défaut).

Ensuite, l’assistant vous demandera de cocher les « Optional Features » (fonctionnalités optionnelles) nécessaires. Ici, vous pouvez tout sélectionner directement. Il est notamment important de cocher la deuxième option, pip, le gestionnaire de paquets de Python, qui nous aide à installer des bibliothèques et outils tiers. N’oubliez pas de la cocher, puis cliquez sur « Next » pour passer à l’étape suivante.


Ensuite, il s’agit de choisir les « Advanced Options » (options avancées). Nous vous recommandons de ne cocher que les deux options « Add Python to environment variables » et « Precompile standard library ». La première nous aidera à configurer automatiquement les variables d’environnement, la seconde précompilera la bibliothèque standard (générant des fichiers .pyc), évitant ainsi une compilation temporaire lors de l’utilisation. Encore une fois, ne vous inquiétez pas si vous ne comprenez pas, cochez simplement. En dessous, « Customize install location » (personnaliser le chemin d’installation) est fortement recommandé de le modifier en un chemin personnalisé. Ce chemin ne doit pas contenir de caractères chinois, d’espaces ou d’autres caractères spéciaux. Respecter ce point vous évitera bien des problèmes inutiles à l’avenir. Une fois configuré, cliquez sur « Install » pour commencer l’installation.


Une installation réussie affichera l’écran ci-dessous. Le mot-clé du succès est « successful ». Si l’installation échoue, le mot ici deviendra « failed ».


Après l’installation, vous pouvez ouvrir l’« Invite de commandes » Windows ou PowerShell, puis saisir `python --version` ou `python -V` pour vérifier si l’installation a réussi. Cette commande permet de voir le numéro de version de l’interpréteur Python. Si vous voyez l’écran ci-dessous, félicitations, l’environnement Python est installé avec succès. Nous vous recommandons également de vérifier si l’outil de gestion de paquets pip de Python est disponible, avec la commande `pip --version` ou `pip -V`.





Les « Outils de génération Visual Studio 2022 » téléchargés ci-dessus nécessitent une connexion Internet pour fonctionner. Après exécution, l’écran suivant apparaîtra. Vous pouvez vous référer à l’image ci-dessous pour cocher les options correspondantes et effectuer la réparation. Le processus de réparation nécessite de télécharger les paquets logiciels correspondants via Internet, ce qui peut prendre du temps. Après une réparation réussie, un redémarrage de votre système d’exploitation peut être demandé.


### Environnement macOS
L’installation de l’environnement Python sous macOS est plus simple que sous Windows. Le paquet d’installation téléchargé depuis le site officiel est un fichier .pkg. Double-cliquez dessus, puis cliquez continuellement sur « Continuer » pour installer. Aucun réglage ou sélection n’est nécessaire.


Après l’installation, vous pouvez ouvrir l’outil « Terminal » sous macOS et saisir la commande `python3 --version` pour vérifier si l’installation a réussi. Notez que la commande est `python3`, et non `python` !!! Ensuite, vérifions l’outil de gestion de paquets en saisissant la commande `pip3 --version`.



### Autres méthodes d’installation
*   **Anaconda/Miniconda :** Certains peuvent recommander aux débutants d’installer directement Anaconda, car Anaconda nous aide à installer l’interpréteur Python ainsi que certaines bibliothèques tierces courantes. De plus, il fournit quelques outils pratiques, particulièrement adaptés aux novices. Personnellement, je ne recommande pas cette méthode, car lors de l’installation d’Anaconda, vous installerez sans raison une multitude de bibliothèques tierces utiles ou inutiles (occupant beaucoup d’espace disque), et votre terminal ou invite de commandes sera modifié par Anaconda (activation automatique de l’environnement virtuel à chaque démarrage). Cela ne respecte pas le principe de moindre surprise en conception logicielle. D’autres petits défauts d’Anaconda ne seront pas détaillés ici. Si vous insistez pour utiliser Anaconda, nous recommandons d’installer Miniconda, disponible sur la même page de téléchargement qu’Anaconda.
*   **PyCharm :** Les débutants entendent ou disent souvent : « Je veux écrire un programme Python, il suffit d’installer PyCharm, non ? ». Voici une brève explication : PyCharm n’est qu’un outil d’aide à l’écriture de code Python, il ne possède pas en lui-même la capacité d’exécuter du code Python. L’exécution du code Python dépend de l’interpréteur Python que nous avons installé ci-dessus. Bien sûr, certaines versions de PyCharm, lors de la création d’un projet Python, si elles ne détectent pas l’environnement Python sur votre ordinateur, vous proposeront de télécharger l’interpréteur Python via Internet. L’installation et l’utilisation de PyCharm sont abordées dans la leçon suivante.

## Résumé
Résumons ce que nous avons appris :

*   Le langage Python est puissant, il peut faire beaucoup de choses, il vaut donc la peine d’être appris.
*   Pour utiliser le langage Python, il faut d’abord installer l’environnement Python, c’est-à-dire l’interpréteur Python nécessaire pour exécuter les programmes Python.
*   Sous Windows, vous pouvez saisir `python --version` dans l’invite de commandes ou PowerShell pour vérifier si l’environnement Python est installé avec succès ; sous macOS, vous pouvez saisir `python3 --version` dans le terminal pour le vérifier.
