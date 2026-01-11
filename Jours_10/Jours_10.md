## Structures de données courantes : les tuples

Dans les deux leçons précédentes, nous avons expliqué les listes en Python, un type de données conteneur. Grâce aux variables de type liste, nous pouvons sauvegarder plusieurs données et effectuer des opérations par lots via des boucles. Bien sûr, Python possède d'autres types de données conteneurs. Nous allons maintenant aborder un autre type de données conteneur : le **tuple**.

### Définition et opérations sur les tuples

En Python, un tuple est également une séquence d'éléments ordonnés. La différence entre un tuple et une liste réside dans le fait que **le tuple est un type immuable**. Cela signifie qu'une fois qu'un tuple est défini, ses éléments ne peuvent être ajoutés, supprimés ou modifiés. Toute tentative de modification d'un élément d'un tuple lèvera une erreur `TypeError`, provoquant l'arrêt du programme. Les tuples sont généralement définis à l'aide de la syntaxe littérale `(x, y, z)`. Les opérateurs supportés par les tuples sont les mêmes que ceux des listes. Observons le code ci-dessous.

```python
# Définir un tuple à trois éléments
t1 = (35, 12, 98)
# Définir un tuple à quatre éléments
t2 = ('Shadrak BESSANH', 45, True, 'Sichuan Chengdu')

# Vérifier le type des variables
print(type(t1))  # <class 'tuple'>
print(type(t2))  # <class 'tuple'>

# Vérifier le nombre d'éléments dans les tuples
print(len(t1))  # 3
print(len(t2))  # 4

# Indexation
print(t1[0])    # 35
print(t1[2])    # 98
print(t2[-1])   # Sichuan Chengdu

# Découpage (slicing)
print(t2[:2])   # ('Shadrak BESSANH', 43)
print(t2[::3])  # ('Shadrak BESSANH', 'Sichuan Chengdu')

# Parcourir les éléments du tuple avec une boucle
for elem in t1:
    print(elem)

# Appartenance (membership)
print(12 in t1)         # True
print(99 in t1)         # False
print('Hao' not in t2)  # True

# Concaténation
t3 = t1 + t2
print(t3)  # (35, 12, 98, 'Shadrak BESSANH', 43, True, 'Sichuan Chengdu')

# Comparaison
print(t1 == t3)            # False
print(t1 >= t3)            # False
print(t1 <= (35, 11, 99))  # False
```

Un tuple avec deux éléments est appelé **doublet** ; un tuple avec cinq éléments est un **quintuplet**. Il est important de noter que `()` représente un tuple vide. Cependant, si un tuple ne contient qu'un seul élément, il faut ajouter une virgule, sinon `()` n'est pas interprété comme la syntaxe littérale d'un tuple, mais comme des parenthèses modifiant la priorité des opérations. Ainsi, `('hello', )` et `(100, )` sont des **singletons** (tuples à un élément), tandis que `('hello')` et `(100)` sont respectivement une chaîne de caractères et un entier. Nous pouvons le vérifier avec le code suivant.

```python
a = ()
print(type(a))  # <class 'tuple'>
b = ('hello')
print(type(b))  # <class 'str'>
c = (100)
print(type(c))  # <class 'int'>
d = ('hello', )
print(type(d))  # <class 'tuple'>
e = (100, )
print(type(e))  # <class 'tuple'>
```

### Empaquetage (packing) et dépaquetage (unpacking)

Lorsque nous attribuons plusieurs valeurs séparées par des virgules à une variable, ces valeurs sont **empaquetées** en un tuple. Inversement, lorsque nous attribuons un tuple à plusieurs variables, le tuple est **dépaqueté** en plusieurs valeurs affectées aux variables correspondantes, comme illustré ci-dessous.

```python
# Empaquetage
a = 1, 10, 100
print(type(a))  # <class 'tuple'>
print(a)        # (1, 10, 100)
# Dépaquetage
i, j, k = a
print(i, j, k)  # 1 10 100
```

Lors du dépaquetage, si le nombre d'éléments dépaquetés ne correspond pas au nombre de variables, une exception `ValueError` est levée, avec le message `too many values to unpack` (trop de valeurs à dépaqueter) ou `not enough values to unpack` (pas assez de valeurs à dépaqueter).

```python
a = 1, 10, 100, 1000
# i, j, k = a             # ValueError: too many values to unpack (expected 3)
# i, j, k, l, m, n = a    # ValueError: not enough values to unpack (expected 6, got 4)
```

Une solution pour gérer un nombre de variables inférieur au nombre d'éléments consiste à utiliser une **expression étoilée (star expression)**. Grâce à celle-ci, une variable peut recevoir plusieurs valeurs, comme illustré ci-dessous. Deux points importants : premièrement, la variable modifiée par une expression étoilée devient une liste contenant zéro ou plusieurs éléments ; deuxièmement, dans la syntaxe de dépaquetage, l'expression étoilée ne peut apparaître qu'une seule fois.

```python
a = 1, 10, 100, 1000
i, j, *k = a
print(i, j, k)        # 1 10 [100, 1000]
i, *j, k = a
print(i, j, k)        # 1 [10, 100] 1000
*i, j, k = a
print(i, j, k)        # [1, 10] 100 1000
*i, j = a
print(i, j)           # [1, 10, 100] 1000
i, *j = a
print(i, j)           # 1 [10, 100, 1000]
i, j, k, *l = a
print(i, j, k, l)     # 1 10 100 [1000]
i, j, k, l, *m = a
print(i, j, k, l, m)  # 1 10 100 1000 []
```

Il est important de noter que la syntaxe de dépaquetage s'applique à **toutes les séquences**, ce qui signifie que les listes, les séquences générées par `range`, et même les chaînes de caractères peuvent être dépaquetées. Essayez d'exécuter le code suivant pour observer le résultat.

```python
a, b, *c = range(1, 10)
print(a, b, c)
a, b, c = [1, 10, 100]
print(a, b, c)
a, *b, c = 'hello'
print(a, b, c)
```

### Échange de valeurs entre variables

L'échange de valeurs entre variables est une opération courante en programmation. Dans de nombreux langages, échanger deux valeurs nécessite une variable temporaire ou des opérations bit à bit obscures. En Python, échanger les valeurs de deux variables `a` et `b` se fait simplement ainsi :

```python
a, b = b, a
```

De même, pour permuter circulairement trois variables `a`, `b`, `c` (affecter `b` à `a`, `c` à `b`, et `a` à `c`), on peut procéder ainsi :

```python
a, b, c = b, c, a
```

Il est important de noter que les opérations ci-dessus n'utilisent pas la syntaxe d'empaquetage/dépaquetage. Les instructions de bytecode Python incluent `ROT_TWO` et `ROT_THREE` pour effectuer ces opérations directement, ce qui est très efficace. Cependant, s'il y a plus de trois variables à permuter, il n'existe pas d'instruction de bytecode directe ; il faut alors recourir à l'empaquetage/dépaquetage.

### Comparaison entre tuples et listes

Une question intéressante se pose : Python possédant déjà le type liste, pourquoi a-t-il besoin du type tuple ? Cette question peut sembler difficile pour les débutants, mais ne vous inquiétez pas. Voici quelques points de réflexion que vous pourrez approfondir au fur et à mesure de votre apprentissage.

1.  Les tuples sont immuables. **Les types immuables sont plus adaptés aux environnements multithreadés**, car ils réduisent les coûts de synchronisation lors d'accès concurrents aux variables. Nous aborderons ce point lorsque nous parlerons de programmation concurrente.

2.  Les tuples sont immuables. Généralement, **les types immuables sont plus rapides à créer que leurs équivalents mutables**. Nous pouvons utiliser la fonction `timeit` du module `timeit` pour comparer le temps nécessaire à la création d'un tuple et d'une liste contenant les mêmes éléments. Le paramètre `number` de `timeit` indique le nombre d'exécutions. Dans le code ci-dessous, nous créons une liste et un tuple contenant les entiers de 1 à 9, en répétant chaque opération 10 000 000 de fois, puis nous mesurons le temps d'exécution.

    ```python
    import timeit
    
    print('%.3f secondes' % timeit.timeit('[1, 2, 3, 4, 5, 6, 7, 8, 9]', number=10000000))
    print('%.3f secondes' % timeit.timeit('(1, 2, 3, 4, 5, 6, 7, 8, 9)', number=10000000))
    ```

    Sortie :

    ```
    0.635 secondes
    0.078 secondes
    ```

    > **Remarque** : Les résultats peuvent varier selon le matériel et le logiciel. Sur mon ordinateur actuel, créer une liste 10 000 000 de fois prend 0,635 secondes, tandis que créer un tuple 10 000 000 de fois prend 0,078 secondes. La création de tuples est clairement plus rapide, avec une différence d'ordre de grandeur. Exécutez ce code sur votre propre machine et partagez vos résultats dans les commentaires !

Bien sûr, les tuples et les listes en Python sont interconvertibles. Nous pouvons réaliser cette conversion avec le code suivant.

```python
infos = ('Shadrak BESSANH', 43, True, 'Sichuan Chengdu')
# Convertir un tuple en liste
print(list(infos))  # ['Shadrak BESSANH', 43, True, 'Sichuan Chengdu']

frts = ['apple', 'banana', 'orange']
# Convertir une liste en tuple
print(tuple(frts))  # ('apple', 'banana', 'orange')
```

### Résumé

**Les listes et les tuples sont des types de données conteneurs**, c'est-à-dire qu'une variable peut contenir plusieurs données, organisées de manière ordonnée. **Les listes sont mutables**, **les tuples sont immuables**. Ainsi, les listes permettent d'ajouter, supprimer, vider, trier et inverser des éléments, ce qui n'est pas possible avec les tuples. Les listes et les tuples supportent tous deux les opérations de **concaténation**, **d'appartenance**, **d'indexation** et de **découpage**. Le type chaîne de caractères, que nous aborderons plus tard, supporte également ces opérations, car une chaîne est une séquence de caractères ordonnée ; à cet égard, les trois types sont similaires. **Nous vous recommandons d'utiliser la syntaxe de compréhension de liste pour créer des listes** : elle est non seulement pratique mais aussi très performante, et constitue l'une des syntaxes les plus caractéristiques de Python.