## Structures de données courantes : les listes - Partie 2

### Méthodes des listes

Les variables de type liste possèdent de nombreuses méthodes qui nous aident à manipuler une liste. Supposons que nous ayons une liste nommée `foos` et que cette liste ait une méthode nommée `bar`. La syntaxe pour utiliser une méthode de liste est : `foos.bar()`. C'est une syntaxe qui appelle une méthode d'un objet via une référence à cet objet. Nous expliquerons en détail cette syntaxe lorsque nous aborderons la programmation orientée objet. Cette syntaxe est également appelée **envoi de message à un objet**.

#### Ajout et suppression d'éléments

Une liste est un conteneur **mutable**, ce qui signifie que nous pouvons ajouter des éléments au conteneur, en supprimer ou modifier les éléments existants. Nous pouvons utiliser la méthode `append` d'une liste pour ajouter un élément à la fin de la liste, et la méthode `insert` pour insérer un élément à une position spécifique. L'ajout place l'élément à la fin de la liste, tandis que l'insertion ajoute un nouvel élément à un index donné. Observez le code ci-dessous.

```python
languages = ['Python', 'Java', 'C++']
languages.append('JavaScript')
print(languages)  # ['Python', 'Java', 'C++', 'JavaScript']
languages.insert(1, 'SQL')
print(languages)  # ['Python', 'SQL', 'Java', 'C++', 'JavaScript']
```

Nous pouvons utiliser la méthode `remove` d'une liste pour supprimer un élément spécifique. Il est important de noter que si l'élément à supprimer n'est pas dans la liste, une erreur `ValueError` se produit, provoquant un plantage du programme. Il est donc recommandé de vérifier l'appartenance avant de supprimer. Nous pouvons également utiliser la méthode `pop` pour supprimer un élément. Par défaut, `pop` supprime le dernier élément de la liste, mais nous pouvons également spécifier une position pour supprimer l'élément à cet index. Si l'index fourni à `pop` est hors limites, une erreur `IndexError` se produit. De plus, les listes ont une méthode `clear` qui vide la liste de tous ses éléments, comme illustré ci-dessous.

```python
languages = ['Python', 'SQL', 'Java', 'C++', 'JavaScript']
if 'Java' in languages:
    languages.remove('Java')
if 'Swift' in languages:
    languages.remove('Swift')
print(languages)  # ['Python', 'SQL', C++', 'JavaScript']
languages.pop()
temp = languages.pop(1)
print(temp)       # SQL
languages.append(temp)
print(languages)  # ['Python', C++', 'SQL']
languages.clear()
print(languages)  # []
```

> **Remarque** : La méthode `pop` retourne l'élément supprimé. Dans le code ci-dessus, nous attribuons l'élément supprimé par `pop` à la variable `temp`. Si vous le souhaitez, vous pouvez réajouter cet élément à la liste, comme le fait `languages.append(temp)`.

Une petite question : si la liste `languages` contient plusieurs occurrences de `'Python'`, alors `languages.remove('Python')` supprimera-t-elle tous les `'Python'` ou seulement le premier ? Essayez de le deviner, puis testez par vous-même.

Il existe une autre manière de supprimer un élément d'une liste : utiliser le mot-clé `del` de Python suivi de l'élément à supprimer. Cette approche ne diffère pas fondamentalement de l'utilisation de `pop` avec un index, mais `pop` retourne l'élément supprimé, tandis que `del` est légèrement plus performant. En effet, l'instruction de bas niveau pour `del` est `DELETE_SUBSCR`, tandis que pour `pop` ce sont `CALL_METHOD` et `POP_TOP`. Si vous ne comprenez pas, ne vous en souciez pas.

```python
items = ['Python', 'Java', 'C++']
del items[1]
print(items)  # ['Python', 'C++']
```

#### Position et fréquence des éléments

La méthode `index` d'une liste permet de trouver l'index d'un élément dans la liste. Si l'élément spécifié n'est pas trouvé, `index` lève une erreur `ValueError`. La méthode `count` permet de compter le nombre d'occurrences d'un élément dans la liste, comme illustré ci-dessous.

```python
items = ['Python', 'Java', 'Java', 'C++', 'Kotlin', 'Python']
print(items.index('Python'))     # 0
# Rechercher 'Python' à partir de l'index 1
print(items.index('Python', 1))  # 5
print(items.count('Python'))     # 2
print(items.count('Kotlin'))     # 1
print(items.count('Swfit'))      # 0
# Rechercher 'Java' à partir de l'index 3
print(items.index('Java', 3))    # ValueError: 'Java' is not in list
```

#### Tri et inversion des éléments

La méthode `sort` permet de trier les éléments d'une liste, tandis que `reverse` inverse l'ordre des éléments, comme illustré ci-dessous.

```python
items = ['Python', 'Java', 'C++', 'Kotlin', 'Swift']
items.sort()
print(items)  # ['C++', 'Java', 'Kotlin', 'Python', 'Swift']
items.reverse()
print(items)  # ['Swift', 'Python', 'Kotlin', 'Java', 'C++']
```

### Compréhension de liste (List Comprehensions)

En Python, les listes peuvent également être créées à l'aide d'une syntaxe littérale spéciale appelée **compréhension de liste**. Voyons, à travers des exemples, quels sont les avantages de cette syntaxe.

**Scénario 1** : Créer une liste de nombres compris entre `1` et `99` qui sont divisibles par `3` ou `5`.

```python
items = []
for i in range(1, 100):
    if i % 3 == 0 or i % 5 == 0:
        items.append(i)
print(items)
```

Avec une compréhension de liste, le code devient :

```python
items = [i for i in range(1, 100) if i % 3 == 0 or i % 5 == 0]
print(items)
```

**Scénario 2** : À partir d'une liste d'entiers `nums1`, créer une nouvelle liste `nums2` où chaque élément est le carré de l'élément correspondant dans `nums1`.

```python
nums1 = [35, 12, 97, 64, 55]
nums2 = []
for num in nums1:
    nums2.append(num ** 2)
print(nums2)
```

Avec une compréhension de liste :

```python
nums1 = [35, 12, 97, 64, 55]
nums2 = [num ** 2 for num in nums1]
print(nums2)
```

**Scénario 3** : À partir d'une liste d'entiers `nums1`, créer une nouvelle liste `nums2` contenant uniquement les éléments de `nums1` supérieurs à `50`.

```python
nums1 = [35, 12, 97, 64, 55]
nums2 = []
for num in nums1:
    if num > 50:
        nums2.append(num)
print(nums2)
```

Avec une compréhension de liste :

```python
nums1 = [35, 12, 97, 64, 55]
nums2 = [num for num in nums1 if num > 50]
print(nums2)
```

L'utilisation de la compréhension de liste pour créer des listes est non seulement plus élégante et concise, mais aussi plus performante que l'approche avec une boucle `for-in` et `append`. Pourquoi ? Parce que l'interpréteur Python dispose d'instructions de bas niveau spécialisées pour les compréhensions de liste (instruction `LIST_APPEND`), tandis que la boucle `for` passe par des appels de méthode (instructions `LOAD_METHOD` et `CALL_METHOD`), qui sont relativement plus coûteux. Si vous ne comprenez pas ce point, retenez simplement la conclusion : **il est fortement recommandé d'utiliser la syntaxe de compréhension de liste pour créer des listes**.

### Listes imbriquées

Le langage Python n'impose pas que les éléments d'une liste soient du même type de données. Ainsi, une liste peut contenir des éléments de n'importe quel type, y compris d'autres listes. Lorsque les éléments d'une liste sont eux-mêmes des listes, on parle de **listes imbriquées**. Les listes imbriquées peuvent représenter des tableaux ou des matrices mathématiques. Par exemple, pour stocker les notes de 5 étudiants dans 3 matières, nous pouvons utiliser la liste suivante.

```python
scores = [[95, 83, 92], [80, 75, 82], [92, 97, 90], [80, 78, 69], [65, 66, 89]]
print(scores[0])
print(scores[0][1])
```

Dans la liste imbriquée ci-dessus, chaque élément correspond aux notes d'un étudiant dans 3 matières, par exemple `[95, 83, 92]`. La valeur `83` dans cette liste représente la note d'un étudiant dans une matière spécifique. Pour accéder à cette valeur, nous utilisons deux opérations d'indexation : `scores[0][1]`. Ici, `scores[0]` donne la liste `[95, 83, 92]`, et l'indexation `[1]` sur cette liste donne le deuxième élément.

Si nous souhaitons saisir au clavier les notes de 5 étudiants dans 3 matières et les stocker dans une liste, nous pouvons utiliser le code suivant.

```python
scores = []
for _ in range(5):
    temp = []
    for _ in range(3):
        score = int(input('Entrez une note : '))
        temp.append(score)
    scores.append(temp)
print(scores)
```

Si nous voulons générer aléatoirement les notes de 5 étudiants dans 3 matières et les stocker dans une liste, nous pouvons utiliser une compréhension de liste, comme illustré ci-dessous.

```python
import random

scores = [[random.randrange(60, 101) for _ in range(3)] for _ in range(5)]
print(scores)
```

> **Remarque** : Le code `[random.randrange(60, 101) for _ in range(3)]` génère une liste de 3 entiers aléatoires. Nous plaçons ce code dans une autre compréhension de liste en tant qu'élément, et nous générons 5 de ces éléments, ce qui donne finalement une liste imbriquée.

### Applications des listes

Examinons un exemple d'application des listes : un programme de sélection aléatoire de numéros pour le jeu "Double Chromatic Ball" (loterie chinoise). Ce jeu consiste à choisir 6 boules rouges (numérotées de 1 à 33) et 1 boule bleue (numérotée de 1 à 16) pour former un ticket.



> **Indication** : Il existe une excellente analyse sur la nature des loteries, que je partage avec vous : **"Inventer une personne qui gagne sans effort, pour tromper un groupe de personnes qui veulent gagner sans effort, et finalement entretenir un groupe de personnes qui gagnent réellement sans effort."** Beaucoup de personnes qui ne comprennent pas les probabilités pensent même que la chance de gagner à la loterie est de 50 %, ou que si la probabilité de gagner est de 1 %, acheter 100 billets garantit de gagner. Ce sont des idées absurdes. **Prenez soin de vous, éloignez-vous des jeux de hasard, surtout si vous ne comprenez rien aux probabilités !**

Voici un programme Python pour générer une combinaison aléatoire.

```python
"""
Programme de sélection aléatoire pour le Double Chromatic Ball

Auteur : Shadrak BESSANH
Version : 1.0
"""
import random

red_balls = list(range(1, 34))
selected_balls = []
# Ajouter 6 boules rouges à la liste sélectionnée
for _ in range(6):
    # Générer un entier aléatoire représentant l'index de la boule rouge sélectionnée
    index = random.randrange(len(red_balls))
    # Retirer la boule sélectionnée de la liste des boules rouges et l'ajouter à la liste sélectionnée
    selected_balls.append(red_balls.pop(index))
# Trier les boules rouges sélectionnées
selected_balls.sort()
# Afficher les boules rouges sélectionnées
for ball in selected_balls:
    print(f'\033[031m{ball:0>2d}\033[0m', end=' ')
# Sélectionner aléatoirement 1 boule bleue
blue_ball = random.randrange(1, 17)
# Afficher la boule bleue sélectionnée
print(f'\033[034m{blue_ball:0>2d}\033[0m')
```

> **Remarque** : Dans le code ci-dessus, `print(f'\033[0m...\033[0m')` contrôle la couleur de sortie : rouge pour les boules rouges, bleu pour la boule bleue. Les points de suspension représentent le contenu à afficher. `\033[0m` est un code de contrôle qui désactive tous les attributs, annulant ainsi les codes de contrôle précédents. Vous pouvez le considérer comme un délimiteur. Le `0` avant `m` indique le mode d'affichage par défaut de la console (peut être omis). `1` signifie brillant, `5` clignotant, `7` inversion, etc. Entre `0` et `m`, nous pouvons spécifier un nombre représentant une couleur : `30` pour noir, `31` pour rouge, `32` pour vert, `33` pour jaune, `34` pour bleu, etc.

Nous pouvons simplifier le code ci-dessus en utilisant les fonctions `sample` et `choice` du module `random`. La première permet un **échantillonnage aléatoire sans remise**, la seconde permet de choisir un élément aléatoire. Voici le code modifié.

```python
"""
Programme de sélection aléatoire pour le Double Chromatic Ball

Auteur : Shadrak BESSANH
Version : 1.1
"""
import random

red_balls = [i for i in range(1, 34)]
blue_balls = [i for i in range(1, 17)]
# Tirer 6 boules rouges au hasard sans remise
selected_balls = random.sample(red_balls, 6)
# Trier les boules rouges sélectionnées
selected_balls.sort()
# Afficher les boules rouges sélectionnées
for ball in selected_balls:
    print(f'\033[031m{ball:0>2d}\033[0m', end=' ')
# Tirer 1 boule bleue au hasard
blue_ball = random.choice(blue_balls)
# Afficher la boule bleue sélectionnée
print(f'\033[034m{blue_ball:0>2d}\033[0m')
```

Pour générer aléatoirement `N` combinaisons, il suffit de placer le code ci-dessus dans une boucle qui s'exécute `N` fois.

```python
"""
Programme de sélection aléatoire pour le Double Chromatic Ball

Auteur : Shadrak BESSANH
Version : 1.2
"""
import random

n = int(input('Combien de combinaisons générer ? '))
red_balls = [i for i in range(1, 34)]
blue_balls = [i for i in range(1, 17)]
for _ in range(n):
    # Tirer 6 boules rouges au hasard sans remise
    selected_balls = random.sample(red_balls, 6)
    # Trier les boules rouges sélectionnées
    selected_balls.sort()
    # Afficher les boules rouges sélectionnées
    for ball in selected_balls:
        print(f'\033[031m{ball:0>2d}\033[0m', end=' ')
    # Tirer 1 boule bleue au hasard
    blue_ball = random.choice(blue_balls)
    # Afficher la boule bleue sélectionnée
    print(f'\033[034m{blue_ball:0>2d}\033[0m')
```

Exécutons le code ci-dessus dans PyCharm, entrons `5`, le résultat est illustré ci-dessous.



Profitons-en pour vous présenter une bibliothèque tierce Python appelée **rich**. Elle nous permet de produire des sorties magnifiques de manière très simple. Vous pouvez l'installer avec pip dans le terminal. Pour les utilisateurs de PyCharm, exécutez la commande pip dans le terminal de PyCharm pour installer rich dans l'environnement virtuel du projet, comme indiqué ci-dessous.

```bash
pip install rich
```


Comme illustré ci-dessus, une fois rich installé, nous pouvons contrôler la sortie avec le code suivant.

```python
"""
Programme de sélection aléatoire pour le Double Chromatic Ball

Auteur : Shadrak BESSANH
Version : 1.3
"""
import random

from rich.console import Console
from rich.table import Table

# Créer la console
console = Console()

n = int(input('Combien de combinaisons générer ? '))
red_balls = [i for i in range(1, 34)]
blue_balls = [i for i in range(1, 17)]

# Créer un tableau et ajouter les en-têtes
table = Table(show_header=True)
for col_name in ('N°', 'Boules rouges', 'Boule bleue'):
    table.add_column(col_name, justify='center')

for i in range(n):
    selected_balls = random.sample(red_balls, 6)
    selected_balls.sort()
    blue_ball = random.choice(blue_balls)
    # Ajouter une ligne au tableau (numéro, boules rouges, boule bleue)
    table.add_row(
        str(i + 1),
        f'[red]{" ".join([f"{ball:0>2d}" for ball in selected_balls])}[/red]',
        f'[blue]{blue_ball:0>2d}[/blue]'
    )

# Afficher le tableau via la console
console.print(table)
```

> **Remarque** : La ligne 31 du code ci-dessus utilise une compréhension de liste pour transformer les numéros des boules rouges en chaînes de caractères et les stocker dans une liste. `" ".join([...])` concatène les chaînes de la liste en une seule chaîne, séparées par des espaces. Si ce n'est pas clair, laissez cela de côté pour l'instant. `[red]...[/red]` dans la chaîne définit la couleur de sortie en rouge, et `[blue]...[/blue]` à la ligne 32 définit la couleur en bleu. Pour en savoir plus sur la bibliothèque rich, consultez la [documentation officielle](https://github.com/textualize/rich/blob/master/README.cn.md).

La sortie finale est illustrée ci-dessous. Une telle sortie ne rend-elle pas l'expérience plus agréable ?



### Résumé

En Python, une liste est implémentée sous forme de tableau dynamique qui peut s'agrandir. Les éléments d'une liste sont stockés de manière contiguë en mémoire, ce qui permet un **accès aléatoire** (obtenir un élément via un index valide en temps constant, indépendant du nombre d'éléments). Vous n'avez pas besoin de vous préoccuper des détails de stockage sous-jacents pour l'instant, ni de comprendre la complexité temporelle asymptotique de chaque méthode. L'important est d'apprendre à utiliser les listes pour résoudre des problèmes concrets.