## Structures de boucle

Lorsque nous écrivons des programmes, il est très probable que nous rencontrions des scénarios où nous devons répéter certaines instructions. Par exemple, nous pourrions avoir besoin d'afficher "hello, world" toutes les secondes pendant une heure. Le code ci-dessous effectue une telle opération. Pour le faire durer une heure, nous devrions écrire ce code 3600 fois. Accepteriez-vous de le faire ?

```python
import time

print('hello, world')
time.sleep(1)
```

> **Remarque** : La fonction `sleep` du module intégré `time` de Python permet de mettre le programme en pause. Le paramètre `1` indique le nombre de secondes de pause. Il peut être de type `int` ou `float`. Par exemple, `0.05` représente 50 millisecondes. Nous aborderons les fonctions et les modules dans les leçons suivantes.

Pour résoudre le problème décrit ci-dessus, nous pouvons utiliser des **structures de boucle** dans nos programmes Python. Une structure de boucle est une structure qui contrôle la répétition d'une ou plusieurs instructions. Avec une telle structure, le code précédent n'a pas besoin d'être écrit 3600 fois ; il suffit de l'écrire une fois et de le placer dans une boucle qui se répète 3600 fois. En Python, il existe deux façons de construire une structure de boucle : la boucle `for-in` et la boucle `while`.

### Boucle `for-in`

Si le nombre de répétitions de la boucle est connu à l'avance, nous recommandons d'utiliser la boucle `for-in`. Par exemple, pour le scénario de répétition 3600 fois mentionné précédemment, nous pouvons utiliser le code ci-dessous. Notez que le bloc de code contrôlé par la boucle `for-in` est également construit par indentation, de la même manière que pour les structures conditionnelles. Le bloc de code contrôlé par la boucle `for-in` est appelé **corps de la boucle**. Généralement, les instructions dans le corps de la boucle sont exécutées en fonction des paramètres de la boucle.

```python
"""
Affiche "hello, world" toutes les secondes pendant une heure

Auteur : Shadrak BESSANH
Version : 1.0
"""
import time

for i in range(3600):
    print('hello, world')
    time.sleep(1)
```

Il est important de noter que `range(3600)` dans le code ci-dessus génère une séquence d'entiers de `0` à `3599`. Lorsque nous plaçons cette séquence dans une boucle `for-in`, la variable de boucle `i` prend successivement les valeurs de `0` à `3599`, ce qui fait que les instructions dans le bloc `for-in` sont répétées 3600 fois. Bien sûr, `range` est très flexible. Voici quelques exemples d'utilisation de la fonction `range` :

- `range(101)` : génère les entiers de `0` à `100`. Notez que `101` n'est pas inclus.
- `range(1, 101)` : génère les entiers de `1` à `100`. C'est un intervalle semi-ouvert à droite : `[1, 101)`.
- `range(1, 101, 2)` : génère les nombres impairs de `1` à `100`. Ici, `2` est le pas (l'incrément), et `101` n'est pas inclus.
- `range(100, 0, -2)` : génère les nombres pairs de `100` à `1`. Ici, `-2` est le pas (le décrément), et `0` n'est pas inclus.

Vous avez peut-être remarqué que dans le code ci-dessus, la variable de boucle `i` n'est pas utilisée pour l'affichage ni pour la pause. Pour les boucles `for-in` où la variable de boucle n'est pas nécessaire, selon les conventions de programmation Python, nous nommons généralement la variable de boucle `_`. Le code modifié est présenté ci-dessous. Bien que le résultat ne change pas, cette pratique montre un niveau professionnel plus élevé.

```python
"""
Affiche "hello, world" toutes les secondes pendant une heure

Auteur : Shadrak BESSANH
Version : 1.1
"""
import time

for _ in range(3600):
    print('hello, world')
    time.sleep(1)
```

Le code ci-dessus s'exécute pendant une heure. Si vous souhaitez l'arrêter plus tôt, dans PyCharm, vous pouvez cliquer sur le bouton d'arrêt dans la fenêtre d'exécution, comme illustré ci-dessous. Si vous exécutez le code dans l'invite de commandes ou le terminal, vous pouvez utiliser la combinaison de touches `Ctrl+C` pour terminer le programme.

<img src="res/day06/terminate_program.png" style="zoom:40%;">

Maintenant, utilisons une boucle `for-in` pour calculer la somme des entiers de 1 à 100, c'est-à-dire $\small{\sum_{n=1}^{100}{n}}$.

```python
"""
Somme des entiers de 1 à 100

Version : 1.0
Auteur : Shadrak BESSANH
"""
total = 0
for i in range(1, 101):
    total += i
print(total)
```

Dans le code ci-dessus, la variable `total` sert à stocker le résultat de l'accumulation. Pendant la boucle, la variable de boucle `i` prend successivement les valeurs de 1 à 100. Pour chaque valeur de `i`, nous exécutons `total += i`, ce qui équivaut à `total = total + i`. Cette instruction réalise l'accumulation. Ainsi, à la fin de la boucle, nous affichons la valeur de `total`, qui est le résultat de la somme de 1 à 100, soit 5050. Notez que l'instruction `print(total)` n'est pas indentée ; elle n'est pas contrôlée par la boucle `for-in` et ne sera pas répétée.

Écrivons maintenant un code pour calculer la somme des nombres pairs de 1 à 100, comme indiqué ci-dessous.

```python
"""
Somme des nombres pairs de 1 à 100

Version : 1.0
Auteur : Shadrak BESSANH
"""
total = 0
for i in range(1, 101):
    if i % 2 == 0:
        total += i
print(total)
```

> **Remarque** : Dans la boucle `for-in` ci-dessus, nous utilisons une structure conditionnelle pour vérifier si la variable de boucle `i` est paire.

Nous pouvons également modifier les paramètres de la fonction `range` pour définir la valeur de départ et le pas à `2`, ce qui permet d'implémenter la somme des nombres pairs de 1 à 100 de manière plus simple.

```python
"""
Somme des nombres pairs de 1 à 100

Version : 1.1
Auteur : Shadrak BESSANH
"""
total = 0
for i in range(2, 101, 2):
    total += i
print(total)
```

Bien sûr, une méthode encore plus simple consiste à utiliser la fonction intégrée `sum` de Python pour effectuer la somme, ce qui nous évite même d'utiliser une structure de boucle.

```python
"""
Somme des nombres pairs de 1 à 100

Version : 1.2
Auteur : Shadrak BESSANH
"""
print(sum(range(2, 101, 2)))
```

### Boucle `while`

Si nous voulons construire une structure de boucle mais que nous ne connaissons pas à l'avance le nombre de répétitions, nous recommandons d'utiliser la boucle `while`. La boucle `while` est contrôlée par une valeur booléenne ou une expression produisant une valeur booléenne. Lorsque la valeur booléenne ou l'expression est `True`, les instructions dans le corps de la boucle (le bloc de code avec la même indentation sous l'instruction `while`) sont répétées. Lorsque l'expression devient `False`, la boucle se termine.

Utilisons maintenant une boucle `while` pour calculer la somme des entiers de 1 à 100, comme indiqué ci-dessous.

```python
"""
Somme des entiers de 1 à 100

Version : 1.1
Auteur : Shadrak BESSANH
"""
total = 0
i = 1
while i <= 100:
    total += i
    i += 1
print(total)
```

Comparé à la boucle `for-in`, le code ci-dessus ajoute une variable `i` avant le début de la boucle. Nous utilisons cette variable pour contrôler la boucle, donc la condition après `while` est `i <= 100`. Dans le corps de la boucle `while`, en plus de l'accumulation, nous devons incrémenter la variable `i`. Nous ajoutons donc l'instruction `i += 1`, de sorte que `i` prenne successivement les valeurs 1, 2, 3, …, jusqu'à 101. Lorsque `i` devient 101, la condition de la boucle `while` n'est plus remplie, et le code quitte la boucle `while`. À ce moment, nous affichons la valeur de `total`, qui est le résultat de la somme de 1 à 100, soit 5050.

Pour calculer la somme des nombres pairs de 1 à 100, nous pouvons modifier légèrement le code ci-dessus.

```python
"""
Somme des nombres pairs de 1 à 100

Version : 1.3
Auteur : Shadrak BESSANH
"""
total = 0
i = 2
while i <= 100:
    total += i
    i += 2
print(total)
```

### `break` et `continue`

Que se passe-t-il si nous définissons la condition de la boucle `while` sur `True`, c'est-à-dire une condition toujours vraie ? Examinons le code ci-dessous, qui utilise `while` pour construire une structure de boucle et calculer la somme des nombres pairs de 1 à 100.

```python
"""
Somme des nombres pairs de 1 à 100

Version : 1.4
Auteur : Shadrak BESSANH
"""
total = 0
i = 2
while True:
    total += i
    i += 2
    if i > 100:
        break
print(total) 
```

Le code ci-dessus utilise `while True` pour créer une boucle dont la condition est toujours vraie, ce qui signifie que sans traitement particulier, la boucle ne se terminera jamais. C'est ce qu'on appelle une **boucle infinie**. Pour arrêter la boucle lorsque la valeur de `i` dépasse 100, nous utilisons le mot-clé `break`, qui permet de terminer l'exécution de la structure de boucle. Il est important de noter que `break` ne termine que la boucle dans laquelle il se trouve. Ce point est crucial lorsqu'on utilise des structures de boucle imbriquées, dont nous parlerons plus tard. Outre `break`, il existe un autre mot-clé utilisable dans les structures de boucle : `continue`. Il permet d'ignorer le reste du code de l'itération courante et de passer directement à l'itération suivante, comme illustré ci-dessous.

```python
"""
Somme des nombres pairs de 1 à 100

Version : 1.5
Auteur : Shadrak BESSANH
"""
total = 0
for i in range(1, 101):
    if i % 2 != 0:
        continue
    total += i
print(total)
```

> **Remarque** : Le code ci-dessus utilise le mot-clé `continue` pour ignorer les cas où `i` est impair. L'instruction `total += i` n'est exécutée que lorsque `i` est pair.

### Structures de boucle imbriquées

Comme les structures conditionnelles, les structures de boucle peuvent être **imbriquées**, c'est-à-dire qu'une structure de boucle peut contenir une autre structure de boucle. L'exemple ci-dessous montre comment utiliser des boucles imbriquées pour afficher une table de multiplication (table de 9).

```python
"""
Affiche la table de multiplication

Version : 1.0
Auteur : Shadrak BESSANH
"""
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f'{i}×{j}={i * j}', end='\t')
    print()
```

Dans le code ci-dessus, le corps de la boucle `for-in` externe contient une autre boucle `for-in`. La boucle externe contrôle la production des lignes (valeur de `i`), tandis que la boucle interne contrôle les colonnes (valeur de `j`) dans chaque ligne. Évidemment, la sortie de la boucle interne correspond à une ligne complète de la table de multiplication. Ainsi, après la fin de la boucle interne, nous utilisons `print()` pour effectuer un saut de ligne, de sorte que la sortie suivante commence sur une nouvelle ligne. Le résultat final est affiché ci-dessous.

```
1×1=1	
2×1=2	2×2=4	
3×1=3	3×2=6	3×3=9	
4×1=4	4×2=8	4×3=12	4×4=16	
5×1=5	5×2=10	5×3=15	5×4=20	5×5=25	
6×1=6	6×2=12	6×3=18	6×4=24	6×5=30	6×6=36	
7×1=7	7×2=14	7×3=21	7×4=28	7×5=35	7×6=42	7×7=49	
8×1=8	8×2=16	8×3=24	8×4=32	8×5=40	8×6=48	8×7=56	8×8=64	
9×1=9	9×2=18	9×3=27	9×4=36	9×5=45	9×6=54	9×7=63	9×8=72	9×9=81
```

### Applications des structures de boucle

#### Exemple 1 : Vérifier si un nombre est premier

Objectif : Saisir un entier positif supérieur à 1 et déterminer s'il est premier.

> **Indication** : Un nombre premier est un entier supérieur à 1 qui n'est divisible que par 1 et par lui-même. Par exemple, pour un entier positif $\small{n}$, nous pouvons vérifier s'il possède un facteur entre 2 et $\small{n - 1}$ pour déterminer s'il est premier. Cependant, la boucle n'a pas besoin d'aller de 2 à $\small{n - 1}$, car pour les entiers positifs supérieurs à 1, les facteurs apparaissent généralement par paires. Ainsi, il suffit de vérifier jusqu'à $\small{\sqrt{n}}$.

```python
"""
Saisir un entier positif supérieur à 1 et déterminer s'il est premier

Version : 1.0
Auteur : Shadrak BESSANH
"""
num = int(input('Entrez un entier positif : '))
end = int(num ** 0.5)
is_prime = True
for i in range(2, end + 1):
    if num % i == 0:
        is_prime = False
        break
if is_prime:
    print(f'{num} est premier')
else:
    print(f'{num} n'est pas premier')
```

> **Remarque** : Dans le code ci-dessus, nous utilisons une variable booléenne `is_prime`. Nous l'initialisons à `True`, en supposant que `num` est premier. Ensuite, nous recherchons un facteur de `num` entre 2 et `num ** 0.5`. Si nous trouvons un facteur, alors `num` n'est pas premier ; nous définissons `is_prime` à `False` et utilisons `break` pour terminer la boucle. Enfin, nous affichons un message en fonction de la valeur de `is_prime` (`True` ou `False`).

#### Exemple 2 : Plus grand commun diviseur (PGCD)

Objectif : Saisir deux entiers positifs supérieurs à 0 et calculer leur plus grand commun diviseur.

> **Indication** : Le plus grand commun diviseur de deux nombres est le plus grand entier qui divise les deux nombres.

```python
"""
Saisir deux entiers positifs et calculer leur plus grand commun diviseur

Version : 1.0
Auteur : Shadrak BESSANH
"""
x = int(input('x = '))
y = int(input('y = '))
for i in range(x, 0, -1):
    if x % i == 0 and y % i == 0:
        print(f'PGCD : {i}')
        break
```

> **Remarque** : Dans le code ci-dessus, la boucle `for-in` parcourt les valeurs de `i` de manière décroissante. Ainsi, le premier `i` trouvé qui divise à la fois `x` et `y` est leur plus grand commun diviseur, et nous utilisons `break` pour terminer la boucle. Si `x` et `y` sont premiers entre eux, la boucle continuera jusqu'à ce que `i` devienne 1, car 1 est un diviseur de tous les entiers positifs. Dans ce cas, le PGCD de `x` et `y` est 1.

L'efficacité du code ci-dessus pour trouver le PGCD pose problème. Supposons que `x` vaut `999999999998` et `y` vaut `999999999999`. Il est évident que ces deux nombres sont premiers entre eux, leur PGCD étant 1. Cependant, avec le code ci-dessus, la boucle s'exécuterait `999999999998` fois, ce qui est généralement inacceptable. Nous pouvons utiliser l'**algorithme d'Euclide** pour trouver le PGCD de manière plus efficace, comme illustré ci-dessous.

```python
"""
Saisir deux entiers positifs et calculer leur plus grand commun diviseur

Version : 1.1
Auteur : Shadrak BESSANH
"""
x = int(input('x = '))
y = int(input('y = '))
while y % x != 0:
    x, y = y % x, x
print(f'PGCD : {x}')
```

> **Remarque** : Les méthodes et étapes pour résoudre un problème sont appelées **algorithmes**. Pour un même problème, nous pouvons concevoir différents algorithmes, qui diffèrent en termes d'utilisation de la mémoire et d'efficacité d'exécution. Ces différences déterminent la qualité d'un algorithme. Comparez les deux codes ci-dessus pour comprendre pourquoi l'algorithme d'Euclide est un meilleur choix. L'instruction `x, y = y % x, x` dans le code ci-dessus signifie : attribuer la valeur de `y % x` à `x`, et la valeur originale de `x` à `y`.

#### Exemple 3 : Jeu de devinette

Objectif : L'ordinateur génère un nombre aléatoire entre 1 et 100. Le joueur saisit un nombre deviné, et l'ordinateur donne un indice correspondant : "plus grand", "plus petit" ou "bravo". Si le joueur devine correctement, l'ordinateur indique combien de tentatives ont été nécessaires, puis le jeu se termine. Sinon, le jeu continue.

```python
"""
Jeu de devinette

Version : 1.0
Auteur : Shadrak BESSANH
"""
import random

answer = random.randrange(1, 101)
counter = 0
while True:
    counter += 1
    num = int(input('Entrez un nombre : '))
    if num < answer:
        print('Plus grand.')
    elif num > answer:
        print('Plus petit.')
    else:
        print('Bravo !')
        break
print(f'Vous avez deviné en {counter} tentative(s).')
```

> **Remarque** : Le code ci-dessus utilise `import random` pour importer le module `random` de la bibliothèque standard de Python. La fonction `randrange` de ce module génère un nombre aléatoire entre 1 et 100 (100 exclus). La variable `counter` enregistre le nombre d'exécutions de la boucle, c'est-à-dire le nombre de tentatives du joueur. À chaque itération, `counter` est incrémenté de 1.

### Résumé

En maîtrisant les structures conditionnelles et les structures de boucle en Python, nous pouvons résoudre de nombreux problèmes pratiques. Grâce à cette leçon, vous devriez maintenant savoir comment utiliser les mots-clés `for` et `while` pour construire des structures de boucle. **Si le nombre de répétitions est connu à l'avance, nous utilisons généralement une boucle** `for`** ; si le nombre de répétitions est indéterminé, nous utilisons une boucle** `while`. De plus, nous pouvons **utiliser** `break` **pour interrompre une boucle** et **utiliser** `continue` **pour passer directement à l'itération suivante**.