## Structures de données courantes : Les ensembles (sets)

Après avoir étudié les listes et les tuples, nous allons maintenant découvrir un autre type de données conteneur : l'ensemble (set). Le terme "ensemble" ne devrait pas vous être étranger, car il provient directement des mathématiques. En mathématiques, un ensemble est **une collection d'objets distincts et définis, considérée comme un tout**. Chaque objet est un **élément** de l'ensemble. Un ensemble doit généralement satisfaire aux propriétés suivantes :

1. **Non-ordonnancement (unordered)** : Dans un ensemble, chaque élément a le même statut, il n'y a pas d'ordre défini entre les éléments.
2. **Unicité (no duplicates)** : Dans un ensemble, deux éléments ne peuvent pas être identiques. Un élément ne peut apparaître qu'une seule fois.
3. **Déterminisme (deterministic)** : Étant donné un ensemble et un élément quelconque, cet élément appartient soit à l'ensemble, soit n'y appartient pas. Il n'y a pas d'ambiguïté.

Les ensembles en Python ne diffèrent pas fondamentalement de leurs homologues mathématiques. Il est important de souligner les propriétés de non-ordonnancement et d'unicité. Le non-ordonnancement signifie que les éléments d'un ensemble n'ont pas de position indexée comme dans une liste ; **les ensembles ne supportent pas l'indexation** (opération `[]`). L'unicité implique qu'**un ensemble ne peut pas contenir de doublons**, ce qui le distingue des listes. On ne peut pas ajouter plusieurs fois le même élément à un ensemble.

Le type ensemble supporte naturellement les opérations d'appartenance `in` et `not in`, ce qui permet de vérifier la propriété de déterminisme. **Les tests d'appartenance (`in`/`not in`) sont plus performants sur les ensembles que sur les listes**, en raison de leur implémentation interne (stockage par hachage). Nous n'aborderons pas les détails ici, mais retenez cette conclusion.

> **Note** : Les ensembles utilisent en interne un stockage par hachage (table de hachage). Si vous n'êtes pas familier avec ce concept, vous pouvez consulter des ressources comme ["Hello Algorithm" - Hash Table](https://www.hello-algo.com/chapter_hashing/).

### Création d'un ensemble

En Python, on peut créer un ensemble en utilisant la syntaxe littérale avec des accolades `{}`. Les accolades doivent contenir au moins un élément, car `{}` vide représente un dictionnaire vide (nous verrons les dictionnaires plus tard). On peut aussi utiliser la fonction intégrée `set()` comme constructeur. `set()` sans argument crée un ensemble vide. On peut aussi convertir d'autres séquences (comme une chaîne ou une liste) en ensemble avec `set()`. Enfin, on peut utiliser une compréhension d'ensemble (set comprehension), similaire à la compréhension de liste.

```python
set1 = {1, 2, 3, 3, 3, 2}
print(set1)  # {1, 2, 3} (les doublons sont automatiquement éliminés)

set2 = {'banana', 'pitaya', 'apple', 'apple', 'banana', 'grape'}
print(set2)  # {'banana', 'pitaya', 'apple', 'grape'} (ordre peut varier)

set3 = set('hello')
print(set3)  # {'h', 'e', 'l', 'o'} (un seul 'l')

set4 = set([1, 2, 2, 3, 3, 3, 2, 1])
print(set4)  # {1, 2, 3}

# Compréhension d'ensemble : nombres entre 1 et 19 divisibles par 3 ou 7
set5 = {num for num in range(1, 20) if num % 3 == 0 or num % 7 == 0}
print(set5)  # {3, 6, 7, 9, 12, 14, 15, 18}
```

**Point crucial** : Les éléments d'un ensemble doivent être de type **hashable**. Un type hashable est un type pour lequel on peut calculer une valeur de hachage (hash code) stable. En général, **les types immuables sont hashables** : entiers (`int`), flottants (`float`), booléens (`bool`), chaînes de caractères (`str`), tuples (`tuple`). **Les types mutables ne sont pas hashables** car leur valeur (et donc leur hash) peut changer. Par conséquent, on ne peut pas mettre une liste ou un dictionnaire dans un ensemble. De même, comme les ensembles sont mutables, un ensemble ne peut pas contenir un autre ensemble. On peut créer des listes de listes, mais pas des ensembles d'ensembles.

> **Conseil** : Si les concepts de hash code et de stockage par hachage ne vous sont pas familiers, vous pouvez continuer à apprendre Python sans inquiétude. Cependant, pour les étudiants en informatique, il est fortement recommandé d'approfondir ce sujet.

### Parcours des éléments

On peut obtenir le nombre d'éléments avec `len()`. Comme les ensembles ne sont pas ordonnés, on ne peut pas les parcourir avec un index. On utilise une boucle `for-in` pour itérer sur les éléments.

```python
set1 = {'Python', 'C++', 'Java', 'Kotlin', 'Swift'}
for elem in set1:
    print(elem)
```

> **Note** : Observez l'ordre de sortie des éléments dans la console. Il est imprévisible et illustre la propriété de non-ordonnancement.

### Opérations sur les ensembles

Python offre un riche éventail d'opérations pour les ensembles : tests d'appartenance, intersection, union, différence, différence symétrique, ainsi que des comparaisons (égalité, sous-ensemble, sur-ensemble).

#### Tests d'appartenance

On utilise `in` et `not in` pour vérifier si un élément est présent dans un ensemble.

```python
set1 = {11, 12, 13, 14, 15}
print(10 in set1)      # False
print(15 in set1)      # True
set2 = {'Python', 'Java', 'C++', 'Swift'}
print('Ruby' in set2)  # False
print('Java' in set2)  # True
```

#### Opérations binaires

Les opérations binaires principales sur les ensembles sont l'intersection, l'union, la différence et la différence symétrique. Elles peuvent être réalisées à l'aide d'opérateurs ou de méthodes.

```python
set1 = {1, 2, 3, 4, 5, 6, 7}
set2 = {2, 4, 6, 8, 10}

# Intersection (éléments communs aux deux ensembles)
print(set1 & set2)                      # {2, 4, 6}
print(set1.intersection(set2))          # {2, 4, 6}

# Union (tous les éléments des deux ensembles, sans doublon)
print(set1 | set2)                      # {1, 2, 3, 4, 5, 6, 7, 8, 10}
print(set1.union(set2))                 # {1, 2, 3, 4, 5, 6, 7, 8, 10}

# Différence (éléments de set1 qui ne sont pas dans set2)
print(set1 - set2)                      # {1, 3, 5, 7}
print(set1.difference(set2))            # {1, 3, 5, 7}

# Différence symétrique (éléments présents dans un seul des deux ensembles)
print(set1 ^ set2)                      # {1, 3, 5, 7, 8, 10}
print(set1.symmetric_difference(set2))  # {1, 3, 5, 7, 8, 10}
```

Comme on peut le voir, l'opérateur `&` et la méthode `intersection()` sont équivalents. Les opérateurs sont souvent plus concis et lisibles.

Ces opérations peuvent être combinées avec des affectations pour former des opérations d'affectation composée (compound assignment). Par exemple :
- `set1 |= set2` équivaut à `set1 = set1 | set2`. La méthode correspondante est `update()`.
- `set1 &= set2` équivaut à `set1 = set1 & set2`. La méthode correspondante est `intersection_update()`.
- `set1 -= set2` équivaut à `set1 = set1 - set2`. La méthode correspondante est `difference_update()`.

```python
set1 = {1, 3, 5, 7}
set2 = {2, 4, 6}
set1 |= set2          # Union avec affectation
# set1.update(set2)   # Méthode équivalente
print(set1)  # {1, 2, 3, 4, 5, 6, 7}

set3 = {3, 6, 9}
set1 &= set3          # Intersection avec affectation
# set1.intersection_update(set3) # Méthode équivalente
print(set1)  # {3, 6}

set2 -= set1          # Différence avec affectation
# set2.difference_update(set1) # Méthode équivalente
print(set2)  # {2, 4}
```

#### Comparaisons

On peut utiliser `==` et `!=` pour vérifier l'égalité de deux ensembles. Ils sont égaux s'ils contiennent exactement les mêmes éléments.

Si tout élément de l'ensemble A est aussi un élément de l'ensemble B, alors A est un **sous-ensemble** (subset) de B, noté A ⊆ B. Dans ce cas, B est un **sur-ensemble** (superset) de A. Si A ⊆ B et A ≠ B, alors A est un **sous-ensemble propre** (proper subset) de B.

Python utilise les opérateurs de comparaison `<`, `<=`, `>`, `>=` pour exprimer ces relations. On peut aussi utiliser les méthodes `issubset()` et `issuperset()`.

```python
set1 = {1, 3, 5}
set2 = {1, 2, 3, 4, 5}
set3 = {5, 4, 3, 2, 1}  # Mêmes éléments que set2 mais ordre différent

print(set1 < set2)    # True (set1 est un sous-ensemble propre de set2)
print(set1 <= set2)   # True (set1 est un sous-ensemble de set2)
print(set2 < set3)    # False (pas un sous-ensemble propre car égaux)
print(set2 <= set3)   # True (set2 est un sous-ensemble de set3)
print(set2 > set1)    # True (set2 est un sur-ensemble de set1)
print(set2 == set3)   # True (mêmes éléments)

print(set1.issubset(set2))    # True
print(set2.issuperset(set1))  # True
```

> **Explication** : `set1 < set2` vérifie si `set1` est un sous-ensemble **propre** de `set2`. `set1 <= set2` vérifie si `set1` est un sous-ensemble (propre ou égal). Les méthodes `issubset()` et `issuperset()` correspondent à `<=` et `>=`.

### Méthodes des ensembles

Les ensembles en Python sont mutables. On peut ajouter ou supprimer des éléments à l'aide de méthodes.

```python
set1 = {1, 10, 100}

# Ajout d'éléments
set1.add(1000)
set1.add(10000)
print(set1)  # {1, 100, 1000, 10, 10000} (ordre peut varier)

# Suppression d'éléments
set1.discard(10)        # Supprime 10 s'il est présent, sinon ne fait rien (pas d'erreur)
if 100 in set1:
    set1.remove(100)    # Supprime 100, lève une KeyError si l'élément n'est pas présent
print(set1)  # {1, 1000, 10000}

# Vidage de l'ensemble
set1.clear()
print(set1)  # set() (ensemble vide)
```

> **Note** : La méthode `remove()` lève une exception `KeyError` si l'élément n'existe pas. C'est pourquoi on vérifie souvent avec `in` avant de l'utiliser. La méthode `discard()` est plus sûre car elle ne lève pas d'erreur. La méthode `pop()` supprime et **retourne** un élément **arbitraire** (aléatoire) de l'ensemble. `remove()` et `discard()` ne retournent pas l'élément supprimé.

La méthode `isdisjoint()` vérifie si deux ensembles sont **disjoints**, c'est-à-dire s'ils n'ont aucun élément en commun. Elle retourne `True` s'ils sont disjoints, `False` sinon.

```python
set1 = {'Java', 'Python', 'C++', 'Kotlin'}
set2 = {'Kotlin', 'Swift', 'Java', 'Dart'}
set3 = {'HTML', 'CSS', 'JavaScript'}
print(set1.isdisjoint(set2))  # False (ils ont 'Java' et 'Kotlin' en commun)
print(set1.isdisjoint(set3))  # True (aucun élément commun)
```

### Ensembles immuables (frozenset)

Python propose également un type d'ensemble immuable : `frozenset`. La différence entre `set` et `frozenset` est analogue à celle entre `list` et `tuple`. Comme `frozenset` est immuable (et donc hashable), il peut être utilisé comme élément d'un autre ensemble (ou comme clé de dictionnaire). À part l'impossibilité d'ajouter ou de supprimer des éléments, `frozenset` supporte les mêmes opérations que `set`.

```python
fset1 = frozenset({1, 3, 5, 7})
fset2 = frozenset(range(1, 6))
print(fset1)          # frozenset({1, 3, 5, 7})
print(fset2)          # frozenset({1, 2, 3, 4, 5})
print(fset1 & fset2)  # frozenset({1, 3, 5})
print(fset1 | fset2)  # frozenset({1, 2, 3, 4, 5, 7})
print(fset1 - fset2)  # frozenset({7})
print(fset1 < fset2)  # False (fset1 n'est pas un sous-ensemble propre de fset2)
```

### Résumé

Le type **ensemble** en Python est un **conteneur non ordonné qui ne permet pas les doublons**. En raison de son implémentation par hachage, ses éléments doivent être de type **hashable** (généralement immuables). La principale différence avec une liste est l'**absence d'ordre** et l'**impossibilité d'accéder aux éléments par index**. En revanche, les ensembles supportent des opérations algébriques efficaces comme l'intersection, l'union, la différence et permettent de vérifier facilement les relations de sous-ensemble/sur-ensemble.