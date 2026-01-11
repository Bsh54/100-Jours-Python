## Structures de données courantes : les listes - Partie 1

Avant de commencer le contenu de cette leçon, donnons-nous une tâche de programmation : lancer un dé 6000 fois et compter le nombre d'apparitions de chaque face. Cette tâche devrait être très simple pour vous. Nous pouvons simuler le lancer d'un dé en utilisant des nombres aléatoires uniformément distribués entre 1 et 6, puis utiliser six variables pour enregistrer le nombre d'apparitions de chaque face. Grâce aux apprentissages précédents, je pense que vous pouvez écrire le code suivant sans trop de difficultés.

```python
"""
Lancer un dé 6000 fois et compter le nombre d'apparitions de chaque face

Auteur : Shadrak BESSANH
Version : 1.0
"""
import random

f1 = 0
f2 = 0
f3 = 0
f4 = 0
f5 = 0
f6 = 0
for _ in range(6000):
    face = random.randrange(1, 7)
    if face == 1:
        f1 += 1
    elif face == 2:
        f2 += 1
    elif face == 3:
        f3 += 1
    elif face == 4:
        f4 += 1
    elif face == 5:
        f5 += 1
    else:
        f6 += 1
print(f'Face 1 apparue {f1} fois')
print(f'Face 2 apparue {f2} fois')
print(f'Face 3 apparue {f3} fois')
print(f'Face 4 apparue {f4} fois')
print(f'Face 5 apparue {f5} fois')
print(f'Face 6 apparue {f6} fois')
```

Je n'ai pas besoin de souligner à quel point le code ci-dessus est "laid". Bien sûr, ce qui est encore plus effrayant, c'est que si nous voulons lancer deux dés ou plus, puis compter le nombre d'apparitions de chaque somme de points, nous devrons définir encore plus de variables et écrire plus de structures conditionnelles. Rien que d'y penser, cela peut sembler repoussant. À ce stade, je suis sûr qu'une question vous vient à l'esprit : existe-t-il un moyen de sauvegarder plusieurs données dans une seule variable, et un moyen d'opérer sur plusieurs données avec un code unifié ? La réponse est oui. En Python, nous pouvons utiliser des variables de type conteneur pour sauvegarder et manipuler plusieurs données. Nous commencerons par vous présenter un nouveau type de données : la liste (`list`).

### Créer une liste

En Python, **une liste est une séquence de données constituée d'une série d'éléments dans un ordre spécifique**. Cela signifie que si nous définissons une variable de type liste, **nous pouvons l'utiliser pour sauvegarder plusieurs données**. En Python, nous pouvons utiliser la syntaxe littérale `[]` pour définir une liste. Les éléments d'une liste sont séparés par des virgules, comme illustré ci-dessous.

```python
items1 = [35, 12, 99, 68, 55, 35, 87]
items2 = ['Python', 'Java', 'Go', 'Kotlin']
items3 = [100, 12.3, 'Python', True]
print(items1)  # [35, 12, 99, 68, 55, 35, 87]
print(items2)  # ['Python', 'Java', 'Go', 'Kotlin']
print(items3)  # [100, 12.3, 'Python', True]
```

> **Remarque** : Une liste peut contenir des éléments en double, comme `35` dans `items1`. Une liste peut contenir des éléments de types différents, comme dans `items3` où l'on trouve des éléments de type `int`, `float`, `str` et `bool`. Cependant, il n'est généralement pas recommandé de placer des éléments de types différents dans la même liste, car cela complique grandement les opérations.

Nous pouvons utiliser la fonction `type` pour vérifier le type d'une variable. Si vous êtes curieux, vous pouvez vérifier quel type est `items1`. Comme une liste peut contenir plusieurs éléments, c'est un type de données conteneur. Par conséquent, lorsque nous nommons une variable de type liste, le nom de variable est généralement un mot au pluriel.

De plus, nous pouvons utiliser la fonction intégrée `list` de Python pour transformer d'autres séquences en liste. Plus précisément, `list` n'est pas une fonction ordinaire ; c'est un constructeur qui crée des objets de type liste. Nous aborderons les concepts d'objets et de constructeurs dans les leçons suivantes.

```python
items4 = list(range(1, 10))
items5 = list('hello')
print(items4)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(items5)  # ['h', 'e', 'l', 'l', 'o']
```

> **Remarque** : `range(1, 10)` produit une séquence d'entiers de 1 à 9. Passée au constructeur `list`, elle crée une liste d'entiers de 1 à 9. Une chaîne de caractères est une séquence de caractères. `list('hello')` utilise les caractères de la chaîne `'hello'` comme éléments de la liste pour créer un objet liste.

### Opérations sur les listes

Nous pouvons utiliser l'opérateur `+` pour concaténer deux listes. L'opération de concaténation combine les éléments des deux listes en une seule liste, comme illustré ci-dessous.

```python
items5 = [35, 12, 99, 45, 66]
items6 = [45, 58, 29]
items7 = ['Python', 'Java', 'JavaScript']
print(items5 + items6)  # [35, 12, 99, 45, 66, 45, 58, 29]
print(items6 + items7)  # [45, 58, 29, 'Python', 'Java', 'JavaScript']
items5 += items6
print(items5)  # [35, 12, 99, 45, 66, 45, 58, 29]
```

Nous pouvons utiliser l'opérateur `*` pour répéter une liste. L'opérateur `*` répète les éléments de la liste un nombre spécifié de fois. Ajoutons deux lignes au code ci-dessus.

```python
print(items6 * 3)  # [45, 58, 29, 45, 58, 29, 45, 58, 29]
print(items7 * 2)  # ['Python', 'Java', 'JavaScript', 'Python', 'Java', 'JavaScript']
```

Nous pouvons utiliser les opérateurs `in` ou `not in` pour déterminer si un élément est présent dans une liste. Ajoutons encore deux lignes au code ci-dessus.

```python
print(29 in items6)  # True
print(99 in items6)  # False
print('C++' not in items7)     # True
print('Python' not in items7)  # False
```

Comme une liste contient plusieurs éléments placés dans un ordre spécifique, lorsque nous voulons manipuler un élément particulier de la liste, nous pouvons utiliser l'opérateur `[]`. En spécifiant la position de l'élément entre `[]`, nous accédons à cet élément. Cette opération est appelée **indexation**. Il est important de noter que la position dans `[]` peut être un entier de `0` à `N - 1` (indexation positive) ou un entier de `-1` à `-N` (indexation négative), où `N` représente le nombre d'éléments dans la liste. Pour l'indexation positive, `[0]` accède au premier élément de la liste, `[N - 1]` au dernier élément. Pour l'indexation négative, `[-1]` accède au dernier élément de la liste, `[-N]` au premier élément. Exemple :

```python
items8 = ['apple', 'waxberry', 'pitaya', 'peach', 'watermelon']
print(items8[0])   # apple
print(items8[2])   # pitaya
print(items8[4])   # watermelon
items8[2] = 'durian'
print(items8)      # ['apple', 'waxberry', 'durian', 'peach', 'watermelon']
print(items8[-5])  # 'apple'
print(items8[-4])  # 'waxberry'
print(items8[-1])  # watermelon
items8[-4] = 'strawberry'
print(items8)      # ['apple', 'strawberry', 'durian', 'peach', 'watermelon']
```

Lors de l'utilisation de l'indexation, il faut éviter les **dépassements d'indice**. Pour `items8` ci-dessus, si nous essayons d'accéder à `items8[5]` ou `items8[-6]`, cela provoquera une erreur `IndexError`, entraînant un plantage du programme. Le message d'erreur serait : *list index out of range*, ce qui signifie "indice de liste hors limites". En effet, pour une liste de cinq éléments comme `items8`, les indices positifs valides sont de `0` à `4`, et les indices négatifs valides sont de `-1` à `-5`.

Si nous souhaitons accéder à plusieurs éléments d'une liste en une seule fois, nous pouvons utiliser le **découpage en tranches (slicing)**. L'opération de découpage utilise la syntaxe `[start:end:stride]`, où `start` représente la position de départ, `end` la position de fin (l'élément à la position `end` n'est pas inclus), et `stride` le pas (l'incrément). Par exemple, si le premier élément accédé est à la position `start`, le second sera à `start + stride`, à condition que `start + stride` soit inférieur à `end`. Ajoutons les instructions suivantes au code ci-dessus pour utiliser le découpage.

```python
print(items8[1:3:1])     # ['strawberry', 'durian']
print(items8[0:3:1])     # ['apple', 'strawberry', 'durian']
print(items8[0:5:2])     # ['apple', 'durian', 'watermelon']
print(items8[-4:-2:1])   # ['strawberry', 'durian']
print(items8[-2:-6:-1])  # ['peach', 'durian', 'strawberry', 'apple']
```

> **Remarque** : Observez la dernière ligne du code ci-dessus et réfléchissez à la façon dont le découpage fonctionne lorsque le pas est négatif.

Si `start` vaut `0`, il peut être omis dans l'opération de découpage. Si `end` vaut `N` (le nombre d'éléments de la liste), il peut également être omis. Si `stride` vaut `1`, il peut également être omis. Ainsi, le code ci-dessous est équivalent au code précédent.

```python
print(items8[1:3])     # ['strawberry', 'durian']
print(items8[:3:1])    # ['apple', 'strawberry', 'durian']
print(items8[::2])     # ['apple', 'durian', 'watermelon']
print(items8[-4:-2])   # ['strawberry', 'durian']
print(items8[-2::-1])  # ['peach', 'durian', 'strawberry', 'apple']
```

En réalité, nous pouvons également modifier les éléments d'une liste via le découpage. Par exemple, ajoutons une ligne au code ci-dessus et observons la sortie.

```python
items8[1:3] = ['x', 'o']
print(items8)  # ['apple', 'x', 'o', 'peach', 'watermelon']
```

Deux listes peuvent également être comparées à l'aide d'opérateurs relationnels. Nous pouvons vérifier si deux listes sont égales, ou comparer leur ordre, comme illustré ci-dessous.

```python
nums1 = [1, 2, 3, 4]
nums2 = list(range(1, 5))
nums3 = [3, 2, 1]
print(nums1 == nums2)  # True
print(nums1 != nums2)  # False
print(nums1 <= nums3)  # True
print(nums2 >= nums3)  # False
```

> **Remarque** : Les éléments de `nums1` et `nums2` sont identiques, donc le résultat de `==` est `True`. Pour la comparaison entre `nums2` et `nums3`, comme le premier élément de `nums2` (`1`) est inférieur au premier élément de `nums3` (`3`), le résultat de `nums2 >= nums3` est `False`. Les opérations relationnelles entre listes ne sont pas très utilisées en pratique. Si vous ne comprenez pas, vous pouvez passer sans vous inquiéter.

### Parcours des éléments

Si vous souhaitez extraire chaque élément d'une liste un par un, vous pouvez utiliser une boucle `for-in` de deux manières.

**Méthode 1** : Utiliser l'indexation dans la structure de boucle pour parcourir les éléments de la liste.

```python
languages = ['Python', 'Java', 'C++', 'Kotlin']
for index in range(len(languages)):
    print(languages[index])
```

Sortie :

```
Python
Java
C++
Kotlin
```

> **Remarque** : La fonction `len` ci-dessus permet d'obtenir le nombre d'éléments `N` de la liste, et `range(N)` produit une plage de `0` à `N-1`, qui correspond exactement aux indices des éléments de la liste.

**Méthode 2** : Parcourir directement la liste ; la variable de boucle représente alors chaque élément.

```python
languages = ['Python', 'Java', 'C++', 'Kotlin']
for language in languages:
    print(language)
```

Sortie :

```
Python
Java
C++
Kotlin
```

### Résumé

À ce stade, nous pouvons utiliser nos connaissances sur les listes pour restructurer le code "lancer un dé et compter les occurrences de chaque face".

```python
"""
Lancer un dé 6000 fois et compter le nombre d'apparitions de chaque face

Auteur : Shadrak BESSANH
Version : 1.1
"""
import random

counters = [0] * 6
# Simuler le lancer de dé et enregistrer le nombre d'occurrences de chaque face
for _ in range(6000):
    face = random.randrange(1, 7)
    counters[face - 1] += 1
# Afficher le nombre d'occurrences de chaque face
for face in range(1, 7):
    print(f'Face {face} apparue {counters[face - 1]} fois')
```

Dans le code ci-dessus, nous utilisons les six éléments de la liste `counters` pour représenter le nombre d'occurrences des faces 1 à 6. Initialement, les six éléments valent 0. Ensuite, nous simulons le lancer de dé avec des nombres aléatoires uniformément distribués entre 1 et 6. Si la face 1 sort, `counters[0]` est incrémenté de 1 ; si la face 2 sort, `counters[1]` est incrémenté de 1, et ainsi de suite. Remarquez qu'en utilisant le type liste combiné à une structure de boucle, nous traitons les données par lots, ce qui rend le code modifié bien plus simple et élégant que le précédent.