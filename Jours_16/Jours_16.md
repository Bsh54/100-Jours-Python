## Utilisation avancée des fonctions

Nous poursuivons notre exploration des fonctions. Nous avons vu que les fonctions ont des **arguments** (variables indépendantes) et une **valeur de retour** (variable dépendante). Les arguments et la valeur de retour peuvent être de n'importe quel type de données. Une question se pose alors : pouvons-nous utiliser une fonction **comme argument** d'une autre fonction, ou **comme valeur de retour** ?

La réponse est **oui**. En Python, les fonctions sont des **citoyens de première classe** (*first-class citizens*). Cela signifie que :

1. Une fonction peut être assignée à une variable.
2. Une fonction peut être passée en argument à une autre fonction.
3. Une fonction peut être retournée par une autre fonction.

Lorsqu'on passe une fonction en argument ou qu'on la retourne, on parle de **fonction d'ordre supérieur** (*higher-order function*).

### Fonctions d'ordre supérieur

Reprenons un exemple précédent : une fonction qui accepte un nombre variable d'arguments et fait la somme de ceux qui sont des entiers (`int`) ou des flottants (`float`). Raffinons le code pour le rendre plus compact.

```python
def calc(*args, **kwargs):
    items = list(args) + list(kwargs.values())
    result = 0
    for item in items:
        if type(item) in (int, float):
            result += item
    return result
```

Supposons que nous souhaitions que `calc` ne fasse pas seulement des additions, mais puisse effectuer d'autres opérations binaires, voire des opérations personnalisées. Actuellement, le code est **couplé** à l'addition à cause de l'opérateur `+=`. Pour le rendre plus générique, nous pouvons **remplacer l'opérateur par un appel de fonction** et passer cette fonction en paramètre.

```python
def calc(valeur_initiale, fonction_op, *args, **kwargs):
    """
    Applique une opération binaire cumulative sur les éléments numériques.
    
    :param valeur_initiale: Valeur de départ pour l'opération cumulative.
    :param fonction_op: Fonction binaire (ex: add, mul) à appliquer.
    :param *args, **kwargs: Éléments sur lesquels opérer.
    :return: Résultat de l'opération cumulative.
    """
    items = list(args) + list(kwargs.values())
    resultat = valeur_initiale
    for item in items:
        if type(item) in (int, float):
            resultat = fonction_op(resultat, item)
    return resultat
```

La fonction a maintenant deux paramètres supplémentaires :
- `valeur_initiale` : la valeur de départ pour l'opération cumulative.
- `fonction_op` : la fonction qui représente l'opération binaire à effectuer.

Définissons deux fonctions simples pour l'addition et la multiplication :

```python
def add(x, y):
    return x + y

def mul(x, y):
    return x * y
```

Appelons `calc` pour une somme :

```python
print(calc(0, add, 1, 2, 3, 4, 5))  # 15
```

Appelons `calc` pour un produit :

```python
print(calc(1, mul, 1, 2, 3, 4, 5))  # 120
```

En déplaçant l'opération dans un paramètre fonction, nous avons **découplé** la logique de `calc` d'une opération spécifique. C'est une technique puissante qui améliore la flexibilité. Notez la différence de syntaxe :

- **Passer une fonction en argument** : on utilise juste le nom de la fonction (`add`, `mul`).
- **Appeler une fonction** : on utilise le nom suivi de parenthèses (`add(1,2)`).

Le module `operator` de la bibliothèque standard fournit déjà des fonctions pour les opérateurs courants. Nous pouvons l'utiliser :

```python
import operator

print(calc(0, operator.add, 1, 2, 3, 4, 5))  # 15
print(calc(1, operator.mul, 1, 2, 3, 4, 5))  # 120
```

Python possède plusieurs fonctions d'ordre supérieur intégrées. Nous avons déjà rencontré `filter` et `map`. 

- `filter(fonction, sequence)` : filtre les éléments de `sequence` en ne gardant que ceux pour lesquels `fonction(element)` retourne `True`.
- `map(fonction, sequence)` : applique `fonction` à chaque élément de `sequence` et retourne un itérateur avec les résultats.

Exemple : prenons une liste d'entiers, gardons les nombres pairs et élevons-les au carré.

```python
def est_pair(num):
    return num % 2 == 0

def carre(num):
    return num ** 2

anciens_nombres = [35, 12, 8, 99, 60, 52]
nouveaux_nombres = list(map(carre, filter(est_pair, anciens_nombres)))
print(nouveaux_nombres)  # [144, 64, 3600, 2704]
```

La même opération peut être réalisée de manière plus concise avec une **compréhension de liste** :

```python
anciens_nombres = [35, 12, 8, 99, 60, 52]
nouveaux_nombres = [num ** 2 for num in anciens_nombres if num % 2 == 0]
print(nouveaux_nombres)  # [144, 64, 3600, 2704]
```

Parlons maintenant de la fonction intégrée `sorted`. Elle permet de trier n'importe quel itérable (liste, tuple, etc.) et retourne une **nouvelle liste** triée, sans modifier l'originale. C'est un exemple de **fonction sans effet de bord** (*side-effect free*) : elle ne modifie pas l'état du programme en dehors de sa valeur de retour. 

```python
mots = ['in', 'apple', 'zoo', 'waxberry', 'pear']
mots_tries = sorted(mots)
print(mots_tries)  # ['apple', 'in', 'pear', 'waxberry', 'zoo'] (ordre alphabétique)
```

Mais `sorted` accepte un argument `key` qui est une **fonction** permettant de spécifier le critère de tri. Par exemple, pour trier par longueur de chaîne :

```python
mots = ['in', 'apple', 'zoo', 'waxberry', 'pear']
mots_tries = sorted(mots, key=len)
print(mots_tries)  # ['in', 'zoo', 'pear', 'apple', 'waxberry'] (ordre croissant de longueur)
```

> **Note** : La méthode `sort` des listes possède également un paramètre `key` similaire.

### Fonctions Lambda (anonymes)

Lorsque la fonction passée en argument est très simple (une seule expression) et n'a pas besoin d'être réutilisée ailleurs, on peut utiliser une **fonction lambda** (ou **fonction anonyme**). Une fonction lambda est définie sur une seule ligne, sans nom. Le résultat de l'expression est automatiquement retourné.

Reprenons l'exemple avec `map` et `filter` et remplaçons `est_pair` et `carre` par des lambdas :

```python
anciens_nombres = [35, 12, 8, 99, 60, 52]
nouveaux_nombres = list(map(lambda x: x ** 2, filter(lambda x: x % 2 == 0, anciens_nombres)))
print(nouveaux_nombres)  # [144, 64, 3600, 2704]
```

La syntaxe d'une fonction lambda est :
```
lambda arguments: expression
```
- `lambda` : mot-clé.
- `arguments` : liste des paramètres, séparés par des virgules.
- `:` : séparateur.
- `expression` : une seule expression Python. Son résultat est la valeur de retour. Pas besoin de `return`.

Comme les fonctions sont des citoyens de première classe, on peut assigner une lambda à une variable. Voici des exemples de fonctions définies en une ligne :

```python
import functools
import operator

# Factorielle (n!) avec lambda et reduce
factorielle = lambda n: functools.reduce(operator.mul, range(2, n + 1), 1)

# Vérification de nombre premier (version compacte)
est_premier = lambda x: x > 1 and all(x % i != 0 for i in range(2, int(x ** 0.5) + 1))

# Appel
print(factorielle(6))    # 720
print(est_premier(37))   # True
```

> **Note 1** : `reduce(fonction, sequence, initial)` du module `functools` applique cumulativement `fonction` aux éléments de `sequence`, en partant de `initial`. C'est une fonction d'ordre supérieur. Avec `map` et `filter`, elles forment trois opérations fondamentales en traitement de données : **map** (transformation), **filter** (filtrage) et **reduce** (réduction/agrégation).
>
> **Note 2** : `all(iterable)` retourne `True` si tous les éléments de l'itérable sont évalués à `True`. Dans la lambda `est_premier`, on vérifie qu'aucun nombre entre 2 et √x ne divise x.

### Fonctions partielles (partial functions)

Une fonction partielle (*partial function*) est une fonction dont certains arguments ont été **fixés** à l'avance, créant ainsi une nouvelle fonction avec moins de paramètres. Cela évite de répéter les mêmes arguments à chaque appel. Le module `functools` fournit la fonction `partial` pour cela.

Exemple : la fonction `int()` convertit une chaîne en entier. Par défaut, elle suppose que la chaîne est en base 10. On peut spécifier une base différente avec l'argument `base`. Utilisons `partial` pour créer des convertisseurs spécialisés :

```python
import functools

int2 = functools.partial(int, base=2)   # Convertit une chaîne binaire en entier
int8 = functools.partial(int, base=8)   # Convertit une chaîne octale en entier
int16 = functools.partial(int, base=16) # Convertit une chaîne hexadécimale en entier

print(int('1001'))    # 1001 (base 10 par défaut)

print(int2('1001'))   # 9 (car 1*8 + 0*4 + 0*2 + 1*1)
print(int8('1001'))   # 513 (car 1*512 + 0*64 + 0*8 + 1*1)
print(int16('1001'))  # 4097 (car 1*4096 + 0*256 + 0*16 + 1*1)
```

`partial` prend une fonction et des arguments à fixer, et retourne une nouvelle fonction. C'est une façon élégante de créer des fonctions spécialisées à partir de fonctions plus générales.

### Résumé

- En Python, les fonctions sont des **citoyens de première classe** : elles peuvent être assignées, passées en argument et retournées.
- Une **fonction d'ordre supérieur** prend une fonction en argument ou en retourne une. Cela permet des designs flexibles et puissants (ex: `map`, `filter`, `sorted` avec `key`).
- Les **fonctions lambda** sont des fonctions anonymes à une seule expression. Utiles pour des opérations simples et ponctuelles.
- Les **fonctions partielles** (`functools.partial`) permettent de fixer des arguments d'une fonction pour en créer une nouvelle plus spécialisée.

Ces concepts, bien qu'un peu abstraits au début, sont fondamentaux pour écrire du code Python expressif, réutilisable et élégant.