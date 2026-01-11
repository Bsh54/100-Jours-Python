
## Premier programme Python

Dans la leçon précédente, nous avons pris connaissance du passé et du présent du langage Python et avons préparé l'environnement de l'interpréteur nécessaire pour exécuter des programmes Python. Je suis sûr que vous êtes impatients de commencer votre voyage en programmation Python. Mais une nouvelle question se pose : où devrions-nous écrire notre programme Python, et comment l'exécuter ensuite ?

### Outils pour écrire du code

Nous allons maintenant vous présenter plusieurs outils pour écrire et exécuter du code Python. Vous pouvez choisir l'outil qui vous convient en fonction de vos besoins. Bien sûr, pour les débutants, je recommande personnellement d'utiliser PyCharm, car il ne nécessite pas beaucoup de configuration, il est très puissant et assez convivial pour les novices. Si vous en avez également entendu parler ou si vous aimez PyCharm, vous pouvez passer directement à la section sur PyCharm, en sautant les descriptions des autres outils ci-dessous.

#### Environnement interactif par défaut

Ouvrez l'outil « Invite de commandes » ou « PowerShell » sous Windows, saisissez `python`, puis appuyez sur la touche `Entrée`. Cette commande nous amènera dans un environnement interactif. Par environnement interactif, nous entendons que lorsque nous saisissons une ligne de code et appuyons sur `Entrée`, le code est immédiatement exécuté. Si le code produit un résultat, celui-ci s'affiche dans la fenêtre, comme ci-dessous.

```Bash
Python 3.10.10
Type "help", "copyright", "credits" or "license" for more information.
>>> 2 * 3
6
>>> 2 + 3
5
>>>
```

> **Remarque** : Les utilisateurs sous macOS doivent ouvrir l'outil « Terminal » et saisir `python3` pour entrer dans l'environnement interactif.

Pour quitter l'environnement interactif, vous pouvez saisir `quit()` dans celui-ci, comme ci-dessous.

```Bash
>>> quit()
```

#### Un meilleur environnement interactif - IPython

L'environnement interactif mentionné ci-dessus n'offre pas une expérience utilisateur très agréable, vous pourrez le constater en l'utilisant. Nous pouvons le remplacer par IPython, car IPython offre des fonctionnalités d'édition et d'interaction bien plus puissantes. Nous pouvons utiliser l'outil de gestion de paquets `pip` de Python dans l'invite de commandes ou le terminal pour installer IPython, comme ci-dessous.

```bash
pip install ipython
```



Ensuite, vous pouvez utiliser la commande suivante pour lancer IPython et entrer dans l'environnement interactif.

```bash
ipython
```

> **Remarque** : Il existe également une version web d'IPython appelée Jupyter. Nous la présenterons lorsque nous en aurons besoin.

#### L'éditeur de texte génial - Visual Studio Code

Visual Studio Code est un éditeur de code génial développé par Microsoft, capable de fonctionner sur des systèmes d'exploitation tels que Windows, Linux et macOS. Il prend en charge la coloration syntaxique, la complétion automatique, l'édition multiple, l'exécution et le débogage, ainsi qu'une série de fonctionnalités pratiques, et prend en charge de nombreux langages de programmation. Si vous devez choisir un outil d'édition de texte avancé, Visual Studio Code est vivement recommandé. Les lecteurs intéressés peuvent étudier par eux-mêmes son téléchargement, son installation et son utilisation.

#### Environnement de développement intégré (IDE) - PyCharm

Pour développer des projets commerciaux en Python, nous vous recommandons d'utiliser un outil plus professionnel : PyCharm. PyCharm est un environnement de développement intégré (IDE) fourni par une entreprise tchèque appelée JetBrains pour le langage Python. Un environnement de développement intégré désigne généralement un outil de développement qui offre une série de fonctionnalités puissantes et d'opérations pratiques, telles que l'écriture de code, l'exécution de code, le débogage, l'analyse de code, le contrôle de version, etc. Il est donc particulièrement adapté au développement de projets commerciaux. Vous pouvez trouver le lien de téléchargement de PyCharm sur le site officiel de JetBrains.

Le site officiel propose deux versions de PyCharm : une version communautaire gratuite (Community Edition), relativement limitée en fonctionnalités, mais tout à fait suffisante pour les débutants ; et une version professionnelle payante (Professional Edition), très puissante, mais nécessitant un paiement annuel ou mensuel. Les nouveaux utilisateurs peuvent l'essayer gratuitement pendant 30 jours. L'installation de PyCharm ne présente aucune difficulté : exécutez le programme d'installation téléchargé et utilisez presque tous les paramètres par défaut.

Lorsque vous exécutez PyCharm pour la première fois, sur l'écran vous invitant à importer les paramètres de PyCharm, choisissez directement « Do not import settings ». Ensuite, nous verrons l'écran d'accueil. Ici, nous pouvons d'abord cliquer sur l'option « Customize » pour effectuer quelques réglages personnalisés de PyCharm.

Ensuite, dans l'option « Projects », nous pouvons cliquer sur « New Project » pour créer un nouveau projet. Vous pouvez également « Ouvrir un projet existant » ou « Obtenir un projet depuis un serveur de contrôle de version (VCS) ».

Lors de la création d'un projet, vous devez spécifier le chemin du projet et créer un « environnement virtuel ». Nous recommandons que chaque projet Python s'exécute dans son propre environnement virtuel dédié. Si votre système ne dispose pas encore d'environnement Python, PyCharm fournira un lien de téléchargement vers le site officiel. Lorsque vous cliquez sur le bouton « Create » pour créer le projet, il téléchargera l'interpréteur Python via Internet.

Bien sûr, nous ne recommandons pas de faire cela, car nous avons déjà installé l'environnement Python dans la leçon précédente. Si le système dispose d'un environnement Python, PyCharm détectera généralement automatiquement l'emplacement de l'interpréteur Python et créera un environnement virtuel basé sur celui-ci.

> **Remarque** : Le comportement peut varier légèrement entre Windows et macOS (chemin du projet, chemin de l'interpréteur).

Après avoir créé le projet, l'écran principal de PyCharm apparaîtra. Nous pouvons cliquer avec le bouton droit sur le dossier du projet, choisir « New » dans le menu, puis « Python File » pour créer un fichier Python. Lors du nommage du fichier, il est recommandé d'utiliser une combinaison de lettres anglaises et de tirets bas. Le fichier Python créé s'ouvrira automatiquement et sera en mode éditable.

Ensuite, nous pouvons écrire notre code Python dans la fenêtre de code. Après avoir écrit le code, vous pouvez cliquer avec le bouton droit dans la fenêtre et choisir l'élément de menu « Run » pour exécuter le code. La fenêtre « Run » ci-dessous affichera le résultat de l'exécution du code.

À ce stade, notre premier programme Python est opérationnel, c'est cool ! Au fait, PyCharm a une fenêtre contextuelle appelée « Tip of the Day » qui vous apprendra quelques astuces pour utiliser PyCharm. Si vous n'en avez pas besoin, fermez-la simplement. Si vous ne voulez plus la voir apparaître, cochez « Don't show tips on startup » avant de la fermer.

### Bonjour le monde

Selon la tradition du secteur, le premier programme que nous écrivons lorsque nous apprenons n'importe quel langage de programmation est d'afficher `hello, world`. En effet, ce code est le premier code écrit par les grands Dennis Ritchie (père du langage C, ayant développé le système d'exploitation Unix avec Ken Thompson) et Brian Kernighan (inventeur du langage awk) dans leur ouvrage immortel *The C Programming Language*. Voici la version correspondante en langage Python.

```python
print('hello, world')
```

> **Attention** : Les parenthèses et les guillemets simples dans le code ci-dessus sont saisis en mode de saisie anglais. Si vous les écrivez par inadvertance en parenthèses ou guillemets simples chinois, l'exécution du code affichera une erreur comme `SyntaxError: invalid character '（' (U+FF08)` ou `SyntaxError: invalid character '‘' (U+2018)`.

Le code ci-dessus ne comporte qu'une seule instruction. Dans cette instruction, nous utilisons une fonction nommée `print`, qui nous aide à afficher le contenu spécifié. `'hello, world'` entre les parenthèses de la fonction `print` est une chaîne de caractères, représentant un contenu textuel. En langage Python, nous pouvons utiliser des guillemets simples ou doubles pour représenter une chaîne de caractères. Contrairement à des langages de programmation comme C, C++ ou Java, les instructions en code Python n'ont pas besoin d'un point-virgule pour indiquer la fin. Autrement dit, si nous voulons écrire une autre instruction, il suffit simplement de passer à la ligne, comme dans le code ci-dessous. De plus, le code Python n'a pas besoin non plus d'une fonction d'entrée nommée `main` pour pouvoir s'exécuter. Fournir une fonction d'entrée est nécessaire pour écrire du code exécutable en C, C++ ou Java, ce que beaucoup de programmeurs connaissent bien, mais ce n'est pas obligatoire en langage Python.

```python
print('hello, world')
print('goodbye, world')
```

Si nous n'utilisons pas d'environnement de développement intégré comme PyCharm, nous pouvons également appeler directement l'interpréteur Python pour exécuter un programme Python. Nous pouvons sauvegarder le code ci-dessus dans un fichier nommé `example01.py`. Pour un système Windows, supposons que ce fichier se trouve dans le répertoire `C:\code`, nous ouvrons l'« Invite de commandes » ou « PowerShell » et saisissons la commande suivante pour l'exécuter.

```powershell
python C:\code\example01.py
```

Pour un système macOS, supposons que notre fichier se trouve dans le répertoire `/Users/Hao`, nous pouvons saisir la commande suivante dans le terminal pour exécuter le programme.

```Bash
python3 /Users/Hao/example01.py
```

> **Astuce** : Si le chemin est long et que vous ne voulez pas le saisir manuellement, vous pouvez faire glisser le fichier directement dans l'« Invite de commandes » ou le « Terminal ». Cela saisira automatiquement le chemin complet du fichier.

Vous pouvez essayer de modifier le code ci-dessus, par exemple en remplaçant `hello, world` entre guillemets simples par autre chose, ou en écrivant plusieurs instructions de ce type, et voir quels résultats vous obtenez. Il est important de rappeler que lors de l'écriture de code Python, il est préférable de n'écrire qu'une seule instruction par ligne. Bien que nous puissions utiliser `;` comme séparateur pour écrire plusieurs instructions sur une ligne, cela rend le code très moche et lui fait perdre sa lisibilité.

### Commenter votre code

Les commentaires sont une partie importante des langages de programmation. Ils servent à expliquer le rôle du code, augmentant ainsi la lisibilité. Bien sûr, nous pouvons également désactiver temporairement des portions de code en les mettant en commentaire. Ainsi, lorsque vous avez besoin de réutiliser ces codes, il suffit de supprimer les symboles de commentaire. En termes simples, **les commentaires facilitent la compréhension du code mais n'affectent pas le résultat de son exécution**.

Il existe deux formes de commentaires en Python :

1. Commentaire sur une ligne : commence par `#` et un espace, peut commenter toute la ligne à partir du `#`.
2. Commentaire multiligne : commence par trois guillemets (généralement doubles), se termine par trois guillemets, généralement utilisé pour ajouter un contenu explicatif sur plusieurs lignes.

```python
"""
Premier programme Python - hello, world

Version : 1.0
Auteur : Shadrak BESSANH
"""
# print('hello, world')
print("Bonjour le monde !")
```

### Résumé

À présent, nous avons fait fonctionner notre premier programme Python. N'est-ce pas gratifiant ?! Si vous persistez dans votre apprentissage, dans quelque temps, nous pourrons faire des choses bien plus cool avec le langage Python. Aujourd'hui, la programmation, comme l'anglais, est une compétence que beaucoup doivent maîtriser.
