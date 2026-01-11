## Fonctions et modules

Avant d'aborder le contenu de cette leçon, examinons un petit problème mathématique : Combien existe-t-il de solutions entières positives à l'équation suivante ?

$$
x_{1} + x_{2} + x_{3} + x_{4} = 8
$$

Vous avez peut-être déjà deviné que ce problème équivaut à déterminer de combien de façons on peut diviser 8 pommes en quatre groupes, chaque groupe contenant au moins une pomme. Cela équivaut aussi à placer trois séparateurs dans les 7 interstices entre les 8 pommes pour former quatre groupes. La réponse est donc $\small{C_{7}^{3} = 35}$, où $\small{C_{7}^{3}}$ représente le nombre de combinaisons de 3 éléments choisis parmi 7, calculé par la formule :

$$
C_m^n = \frac {m!} {n!(m-n)!}
$$

Avec nos connaissances actuelles, nous pourrions calculer $\small{m!}$, $\small{n!}$ et $\small{(m-n)!}$ à l'aide de boucles accumulant des multiplications, puis effectuer la division pour obtenir $\small{C_{m}^{n}}$, comme dans le code suivant.

```python
"""
Entrez m et n, calculez la valeur du coefficient binomial C(m,n)

Version: 1.0
Auteur: 骆昊
"""

m = int(input('m = '))
n = int(input('n = '))
# Calcul de la factorielle de m
fm = 1
for num in range(1, m + 1):
    fm *= num
# Calcul de la factorielle de n
fn = 1
for num in range(1, n + 1):
    fn *= num
# Calcul de la factorielle de m-n
fk = 1
for num in range(1, m - n + 1):
    fk *= num
# Calcul de la valeur de C(m,n)
print(fm // fn // fk)
```

Entrée :
```
m = 7
n = 3
```

Sortie :
```
35
```

Remarquez-vous que dans le code ci-dessus, nous effectuons trois fois l'opération de calcul de factorielle ? Bien que les valeurs de $\small{m}$, $\small{n}$ et $\small{m - n}$ soient différentes, les trois blocs de code sont structurellement identiques. C'est du code dupliqué. Le maître de la programmation *Martin Fowler* a dit : "**Il y a plusieurs mauvaises odeurs dans le code, la duplication est la pire !**" Pour écrire du code de qualité, la première étape est d'éliminer la duplication.

Dans le code précédent, nous pouvons encapsuler la fonctionnalité de calcul de factorielle dans un bloc de code appelé **fonction**. Là où nous avons besoin de calculer une factorielle, il suffira d'**appeler la fonction** pour réutiliser cette fonctionnalité.

### Définition d'une fonction

En mathématiques, une fonction s'écrit généralement sous la forme $\small{y = f(x)}$ ou $\small{z = g(x, y)}$. Dans $\small{y = f(x)}$, $\small{f}$ est le nom de la fonction, $\small{x}$ est la variable indépendante (l'argument) et $\small{y}$ est la variable dépendante (la valeur de retour). En Python, c'est similaire : chaque fonction a un nom, des arguments et une valeur de retour.

En Python, on utilise le mot-clé `def` pour définir une fonction. Comme pour les variables, une fonction doit avoir un nom significatif, suivant les mêmes règles de nommage. Les arguments (variables indépendantes) sont placés entre parenthèses après le nom de la fonction. Le résultat de l'exécution de la fonction (la valeur de retour) est spécifié avec le mot-clé `return`. Si une fonction n'a pas d'instruction `return`, elle retourne `None` (valeur nulle). Une fonction peut aussi n'avoir aucun argument, mais les parenthèses après le nom sont obligatoires. Le code à exécuter par la fonction est indenté après la ligne de définition, de la même manière que pour les blocs de code des structures conditionnelles et de boucle.

Refactorisons maintenant le code précédent en plaçant le calcul de factorielle dans une fonction. **Refactoriser signifie réorganiser la structure du code sans en changer le comportement.**

```python
"""
Entrez m et n, calculez la valeur du coefficient binomial C(m,n)

Version: 1.1
Auteur: 骆昊
"""

# Définition de la fonction factorielle avec le mot-clé def
# L'argument (variable indépendante) num est un entier non négatif
# La valeur de retour (variable dépendante) est la factorielle de num
def factorielle(num):
    resultat = 1
    for n in range(2, num + 1):
        resultat *= n
    return resultat


m = int(input('m = '))
n = int(input('n = '))
# Au lieu de répéter le code, on appelle simplement la fonction
# La syntaxe d'appel est : nom_fonction(paramètres)
print(factorielle(m) // factorielle(n) // factorielle(m - n))
```

Ce code est plus élégant et concis. Plus important encore, notre fonction `factorielle` peut être réutilisée dans d'autres parties du code où un calcul de factorielle est nécessaire. Ainsi, **les fonctions nous aident à encapsuler du code fonctionnellement indépendant et destiné à être réutilisé**. Lorsque nous avons besoin de ce code, au lieu de le réécrire, nous **l'appelons via la fonction**.

En réalité, le module `math` de la bibliothèque standard Python possède déjà une fonction nommée `factorial` qui calcule la factorielle. Nous pouvons l'importer avec `import math` puis l'appeler via `math.factorial`. Ou bien importer directement la fonction avec `from math import factorial`.

```python
"""
Entrez m et n, calculez la valeur du coefficient binomial C(m,n)

Version: 1.2
Auteur: 骆昊
"""
from math import factorial

m = int(input('m = '))
n = int(input('n = '))
print(factorial(m) // factorial(n) // factorial(m - n))
```

À l'avenir, les fonctions que nous utiliserons seront soit des fonctions personnalisées, soit des fonctions provenant de la bibliothèque standard ou de bibliothèques tierces. S'il existe déjà une fonction disponible, il est inutile d'en redéfinir une. "**Réinventer la roue**" est une mauvaise pratique. Si le nom `factorial` vous semble trop long, vous pouvez lui attribuer un alias lors de l'importation en utilisant le mot-clé `as`.

```python
"""
Entrez m et n, calculez la valeur du coefficient binomial C(m,n)

Version: 1.3
Auteur: 骆昊
"""
from math import factorial as f

m = int(input('m = '))
n = int(input('n = '))
print(f(m) // f(n) // f(m - n))
```

### Arguments des fonctions

#### Arguments positionnels et arguments nommés

Écrivons une autre fonction qui détermine si trois longueurs peuvent former un triangle. Elle retourne `True` si c'est possible, `False` sinon.

```python
def peut_former_triangle(a, b, c):
    """Détermine si trois longueurs peuvent former un triangle."""
    return a + b > c and b + c > a and a + c > b
```

La fonction `peut_former_triangle` a trois paramètres. Ce sont des **arguments positionnels**. Lors de l'appel, ils sont généralement fournis dans l'ordre de gauche à droite, et le nombre d'arguments doit correspondre au nombre de paramètres définis.

```python
print(peut_former_triangle(1, 2, 3))  # False
print(peut_former_triangle(4, 5, 6))  # True
```

Si vous ne souhaitez pas fournir les valeurs dans l'ordre `a`, `b`, `c`, vous pouvez utiliser des **arguments nommés** en utilisant la syntaxe `nom_parametre=valeur`.

```python
print(peut_former_triangle(b=2, c=3, a=1))  # False
print(peut_former_triangle(c=6, b=4, a=5))  # True
```

Lors de la définition d'une fonction, vous pouvez utiliser `/` dans la liste des paramètres pour définir des **arguments exclusivement positionnels** (*positional-only arguments*), et `*` pour définir des **arguments nommés obligatoires** (*keyword-only arguments*). Les arguments exclusivement positionnels ne peuvent être fournis que par position lors de l'appel. Les arguments nommés obligatoires ne peuvent être fournis qu'avec la syntaxe `nom=valeur`.

```python
# Les paramètres avant / sont exclusivement positionnels
def peut_former_triangle(a, b, c, /):
    """Détermine si trois longueurs peuvent former un triangle."""
    return a + b > c and b + c > a and a + c > b


# Le code suivant générera une TypeError : les arguments exclusivement positionnels ne peuvent pas être passés comme arguments nommés.
# print(peut_former_triangle(b=2, c=3, a=1))
```

> **Note** : Les arguments exclusivement positionnels sont une fonctionnalité introduite dans Python 3.8.

```python
# Les paramètres après * sont des arguments nommés obligatoires
def peut_former_triangle(*, a, b, c):
    """Détermine si trois longueurs peuvent former un triangle."""
    return a + b > c and b + c > a and a + c > b


# Le code suivant générera une TypeError : la fonction n'attend pas d'arguments positionnels mais 3 ont été fournis.
# print(peut_former_triangle(1, 2, 3))
```

#### Valeurs par défaut des arguments

Python permet de définir des valeurs par défaut pour les arguments. Reprenons un exemple précédent : la fonction qui simule le lancer de dés dans le jeu "CRAPS". Nous pouvons l'encapsuler dans une fonction.

```python
from random import randrange


# Définition de la fonction de lancer de dés
# L'argument n représente le nombre de dés, avec une valeur par défaut de 2.
# La valeur de retour représente la somme des points obtenus en lançant n dés.
def lancer_des(n=2):
    total = 0
    for _ in range(n):
        total += randrange(1, 7)
    return total


# Si aucun argument n'est fourni, n prend la valeur par défaut 2 (lancer deux dés).
print(lancer_des())
# En passant l'argument 3, la variable n reçoit la valeur 3 (lancer trois dés).
print(lancer_des(3))
```

Un autre exemple plus simple :

```python
def addition(a=0, b=0, c=0):
    """Additionne trois nombres."""
    return a + b + c


# Appel sans arguments : a, b, c prennent leur valeur par défaut 0.
print(addition())         # 0
# Un argument fourni : a reçoit 1, b et c valent 0.
print(addition(1))        # 1
# Deux arguments fournis : a=1, b=2, c=0.
print(addition(1, 2))     # 3
# Trois arguments fournis : a=1, b=2, c=3.
print(addition(1, 2, 3))  # 6
```

**Important** : **Les paramètres avec une valeur par défaut doivent être placés après les paramètres sans valeur par défaut**. Sinon, une erreur `SyntaxError` se produira, avec le message `non-default argument follows default argument`.

#### Arguments variables

Python permet à une fonction d'accepter un nombre variable d'arguments grâce à la syntaxe avec un astérisque (`*`). Cela est utile lorsque vous ne savez pas à l'avance combien d'arguments l'appelant va fournir.

Le code suivant montre une fonction `addition` qui accepte un nombre quelconque d'arguments (positionnels) et en fait la somme. Les arguments sont reçus sous forme d'un tuple.

```python
# L'expression *args indique que la fonction peut recevoir 0 ou plusieurs arguments positionnels.
# Les n arguments fournis lors de l'appel sont assemblés en un n-uplet (tuple) assigné à args.
# Si aucun argument n'est passé, args est un tuple vide.
def addition(*args):
    total = 0
    # Parcourt le tuple contenant les arguments variables.
    for val in args:
        # Vérifie le type (seuls les types numériques sont additionnés).
        if type(val) in (int, float):
            total += val
    return total


# Appels avec différents nombres d'arguments.
print(addition())               # 0
print(addition(1))              # 1
print(addition(1, 2, 3))        # 6
print(addition(1, 2, 'hello', 3.45, 6))  # 12.45 (ignore 'hello')
```

Si vous souhaitez accepter un nombre variable d'arguments **nommés**, utilisez `**kwargs`. Les arguments nommés sont reçus sous forme d'un dictionnaire.

```python
# **kwargs peut recevoir 0 ou plusieurs arguments nommés.
# Les arguments nommés sont assemblés en un dictionnaire (clé=nom, valeur=valeur).
# Si aucun argument nommé n'est fourni, kwargs est un dictionnaire vide.
def foo(*args, **kwargs):
    print(args)   # Affiche le tuple des arguments positionnels
    print(kwargs) # Affiche le dictionnaire des arguments nommés


foo(3, 2.1, True, nom='Pierre', age=43, moyenne=4.95)
```

Sortie :
```
(3, 2.1, True)
{'nom': 'Pierre', 'age': 43, 'moyenne': 4.95}
```

### Gestion des fonctions avec les modules

Quel que soit le langage de programmation, nommer les variables et les fonctions peut être problématique en raison des **conflits de noms**. Le cas le plus simple est de définir deux fonctions du même nom dans le même fichier `.py`.

```python
def foo():
    print('Bonjour, le monde !')


def foo():
    print('Au revoir, le monde !')


foo()  # Que va-t-il se passer ?
```

Nous pouvons éviter ce cas simple, mais dans un projet collaboratif, plusieurs développeurs pourraient définir des fonctions nommées `foo`. Comment résoudre ce conflit ? La réponse est simple : en Python, chaque fichier représente un **module**. Différents modules peuvent contenir des fonctions de même nom. Pour les utiliser, nous importons le module avec `import` et utilisons le **nom qualifié complet** (`nom_module.nom_fonction`).

`module1.py`
```python
def foo():
    print('Bonjour, le monde !')
```

`module2.py`
```python
def foo():
    print('Au revoir, le monde !')
```

`test.py`
```python
import module1
import module2

# Utilisation du nom qualifié complet
module1.foo()  # Bonjour, le monde !
module2.foo()  # Au revoir, le monde !
```

Lors de l'importation d'un module, vous pouvez également utiliser `as` pour lui attribuer un alias, ce qui permet d'utiliser un nom qualifié plus court.

`test.py`
```python
import module1 as m1
import module2 as m2

m1.foo()  # Bonjour, le monde !
m2.foo()  # Au revoir, le monde !
```

Au lieu d'importer le module entier, vous pouvez importer spécifiquement une fonction avec `from ... import ...`.

`test.py`
```python
from module1 import foo

foo()  # Bonjour, le monde !

from module2 import foo

foo()  # Au revoir, le monde !
```

Cependant, si vous importez deux fonctions portant le même nom de modules différents, la seconde importation écrasera la première. Dans le code ci-dessous, `foo()` affichera `'Au revoir, le monde !'`.

`test.py`
```python
from module1 import foo
from module2 import foo

foo()  # Au revoir, le monde !
```

Pour utiliser les deux fonctions `foo`, utilisez des alias lors de l'importation.

`test.py`
```python
from module1 import foo as f1
from module2 import foo as f2

f1()  # Bonjour, le monde !
f2()  # Au revoir, le monde !
```

### Modules et fonctions de la bibliothèque standard

La bibliothèque standard Python fournit de nombreux modules et fonctions pour simplifier le développement. Nous avons déjà utilisé le module `random` pour générer des nombres aléatoires et effectuer des tirages. Le module `time` fournit des fonctions liées au temps. Le module `math` contient des fonctions mathématiques comme sinus, cosinus, exponentielle, logarithme, etc. Nous en découvrirons d'autres au fil de l'apprentissage.

Certaines fonctions sont disponibles sans importation : ce sont les **fonctions intégrées** (*built-in functions*). Elles sont très utiles et fréquemment utilisées. En voici quelques-unes :

| Fonction | Description |
|----------|-------------|
| `abs`    | Retourne la valeur absolue d'un nombre. Ex. : `abs(-1.3)` retourne `1.3`. |
| `bin`    | Convertit un entier en une chaîne binaire commençant par `'0b'`. Ex. : `bin(123)` retourne `'0b1111011'`. |
| `chr`    | Convertit un code Unicode en caractère correspondant. Ex. : `chr(8364)` retourne `'€'`. |
| `hex`    | Convertit un entier en une chaîne hexadécimale commençant par `'0x'`. Ex. : `hex(123)` retourne `'0x7b'`. |
| `input`  | Lit une ligne depuis l'entrée standard et la retourne sous forme de chaîne. |
| `len`    | Retourne la longueur d'une chaîne, liste, etc. |
| `max`    | Retourne la plus grande valeur parmi plusieurs arguments ou dans un itérable. Ex. : `max(12, 95, 37)` retourne `95`. |
| `min`    | Retourne la plus petite valeur parmi plusieurs arguments ou dans un itérable. Ex. : `min(12, 95, 37)` retourne `12`. |
| `oct`    | Convertit un entier en une chaîne octale commençant par `'0o'`. Ex. : `oct(123)` retourne `'0o173'`. |
| `open`   | Ouvre un fichier et retourne un objet fichier. |
| `ord`    | Convertit un caractère en son code Unicode correspondant. Ex. : `ord('€')` retourne `8364`. |
| `pow`    | Calcule la puissance. Ex. : `pow(2, 3)` retourne `8` ; `pow(2, 0.5)` retourne `1.4142135623730951`. |
| `print`  | Affiche du texte ou des valeurs. |
| `range`  | Génère une séquence d'entiers. Ex. : `range(100)` génère les entiers de 0 à 99. |
| `round`  | Arrondit un nombre avec une précision spécifiée. Ex. : `round(1.23456, 4)` retourne `1.2346`. |
| `sum`    | Calcule la somme des éléments d'un itérable. Ex. : `sum(range(1, 101))` retourne `5050`. |
| `type`   | Retourne le type d'un objet. Ex. : `type(10)` retourne `int` ; `type('hello')` retourne `str`. |

### Résumé

**Une fonction est l'encapsulation d'un bloc de code fonctionnellement indépendant et destiné à être réutilisé.** Apprendre à définir et utiliser des fonctions permet d'écrire du code de meilleure qualité. La bibliothèque standard Python fournit déjà de nombreux modules et fonctions courants ; les utiliser permet de faire plus avec moins de code. Si ces fonctions ne suffisent pas, nous pouvons créer nos propres fonctions et les organiser à l'aide de modules.