## Opérateurs dans le langage Python

Le langage Python prend en charge de nombreux types d'opérateurs. Le tableau ci-dessous énumère les opérateurs Python, classés par priorité de la plus élevée à la plus basse. Avec les variables et les opérateurs, nous pouvons construire diverses expressions pour résoudre des problèmes pratiques. En informatique, **une expression est une entité syntaxique dans un programme informatique, composée d'une ou plusieurs constantes, variables, fonctions et opérateurs combinés, que le langage de programmation peut interpréter et calculer pour obtenir une autre valeur**. Il n'est pas grave de ne pas comprendre cette phrase, mais il est important de savoir que, quel que soit le langage de programmation utilisé, la construction d'expressions est très importante.

| Opérateur                                                    | Description                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------- |
| `[]`, `[:]`                                                  | Indexation, tranche (slicing)                                 |
| `**`                                                         | Exponentiation                                                |
| `~`, `+`, `-`                                                | Complément bit à bit, signe plus, signe moins                 |
| `*`, `/`, `%`, `//`                                          | Multiplication, division, modulo, division entière            |
| `+`, `-`                                                     | Addition, soustraction                                        |
| `>>`, `<<`                                                   | Décalage à droite, décalage à gauche                          |
| `&`                                                          | ET bit à bit                                                  |
| `^`, `\|`                                                    | OU exclusif (XOR) bit à bit, OU bit à bit                     |
| `<=`, `<`, `>`, `>=`                                         | Inférieur ou égal, inférieur, supérieur, supérieur ou égal    |
| `==`, `!=`                                                   | Égal à, différent de                                          |
| `is`, `is not`                                               | Opérateurs d'identité                                         |
| `in`, `not in`                                               | Opérateurs d'appartenance                                     |
| `not`, `or`, `and`                                           | Opérateurs logiques                                           |
| `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `//=`, `**=`, `&=`, `\|=`, `^=`, `>>=`, `<<=` | Opérateurs d'affectation (assignation)                        |

> **Remarque** : La priorité détermine, dans une expression comportant plusieurs opérateurs, l'ordre dans lequel les opérations doivent être exécutées. Lors de l'écriture du code, si l'on n'est pas sûr de la priorité des opérateurs dans une expression, on peut utiliser des parenthèses pour garantir l'ordre d'exécution des opérations.

### Opérateurs arithmétiques

Les opérateurs arithmétiques en Python sont très variés. Outre les opérations d'addition, soustraction, multiplication et division bien connues, il existe également l'opérateur de division entière, l'opérateur de modulo (reste de la division) et l'opérateur d'exponentiation. L'exemple ci-dessous illustre l'utilisation des opérateurs arithmétiques.

```python
"""
Opérateurs arithmétiques

Version : 1.0
Auteur : Shadrak BESSANH
"""
print(321 + 12)     # Addition, affiche 333
print(321 - 12)     # Soustraction, affiche 309
print(321 * 12)     # Multiplication, affiche 3852
print(321 / 12)     # Division, affiche 26.75
print(321 // 12)    # Division entière, affiche 26
print(321 % 12)     # Modulo (reste), affiche 9
print(321 ** 12)    # Exponentiation, affiche 1196906950228928915420617322241
```

Les opérations arithmétiques suivent la règle "multiplication et division avant addition et soustraction", ce qui ne diffère pas des connaissances enseignées en mathématiques. Autrement dit, la priorité des opérations de multiplication et division est supérieure à celle de l'addition et de la soustraction. S'il y a également une exponentiation, la priorité de l'exponentiation est supérieure à celle de la multiplication et de la division. Pour changer l'ordre d'exécution des opérations arithmétiques, on peut utiliser des parenthèses (en anglais, petits parenthèses). Les expressions entre parenthèses sont exécutées en priorité, comme le montre l'exemple ci-dessous.

```python
"""
Priorité des opérations arithmétiques

Version : 1.0
Auteur : Shadrak BESSANH
"""
print(2 + 3 * 5)           # 17
print((2 + 3) * 5)         # 25
print((2 + 3) * 5 ** 2)    # 125
print(((2 + 3) * 5) ** 2)  # 625
```

### Opérateurs d'affectation

Les opérateurs d'affectation sont probablement les opérateurs les plus courants. Leur rôle est d'affecter la valeur de droite à la variable de gauche. Les opérateurs d'affectation peuvent également être combinés avec les opérateurs arithmétiques ci-dessus pour former des opérateurs d'affectation composés. Par exemple : `a += b` équivaut à `a = a + b` ; `a *= a + 2` équivaut à `a = a * (a + 2)`. L'exemple ci-dessous illustre l'utilisation des opérateurs d'affectation et des opérateurs d'affectation composés.

```python
"""
Opérateurs d'affectation et opérateurs d'affectation composés

Version : 1.0
Auteur : Shadrak BESSANH
"""
a = 10
b = 3
a += b        # Équivaut à : a = a + b
a *= a + 2    # Équivaut à : a = a * (a + 2)
print(a)      # Calculez ce qui sera affiché ici
```

Une expression d'affectation ne produit aucune valeur en elle-même. Autrement dit, si vous placez une expression d'affectation dans la fonction `print` pour tenter d'afficher la valeur de l'expression, cela provoquera une erreur de syntaxe. Pour résoudre ce problème, Python 3.8 a introduit un nouvel opérateur d'affectation `:=`, appelé opérateur morse (walrus operator). Devinez pourquoi il porte ce nom ? L'opérateur morse affecte également la valeur de droite à la variable de gauche, mais contrairement à l'opérateur d'affectation classique, la valeur de droite est également la valeur de toute l'expression. Regardez le code ci-dessous pour comprendre.

```python
"""
Opérateur morse (walrus operator)

Version : 1.0
Auteur : Shadrak BESSANH
"""
# SyntaxError: invalid syntax
# print((a = 10))
# Opérateur morse
print((a := 10))  # 10
print(a)          # 10
```

> **Astuce** : Si la ligne 8 de code ci-dessus n'est pas commentée, l'exécution du code affichera l'erreur `SyntaxError: invalid syntax`. Notez que dans cette ligne de code, nous avons mis `a = 10` entre parenthèses. Si vous écrivez par erreur `print(a = 10)`, vous verrez l'erreur `TypeError: 'a' is an invalid keyword argument for print()`. Vous comprendrez la signification de ce message d'erreur lorsque nous aborderons les fonctions.

### Opérateurs de comparaison et opérateurs logiques

Les opérateurs de comparaison, également appelés opérateurs relationnels, incluent `==`, `!=`, `<`, `>`, `<=`, `>=`. Je pense que vous les comprenez tous. Il est important de noter que l'égalité se compare avec `==` (deux signes égal), car `=` est l'opérateur d'affectation que nous venons de voir. L'inégalité se compare avec `!=`, différent du symbole $\small{\neq}$ utilisé en mathématiques. Python 2 utilisait autrefois `<>` pour représenter "différent de", mais en Python 3, utiliser `<>` provoque une `SyntaxError`. Les opérateurs de comparaison produisent des valeurs booléennes, soit `True`, soit `False`.

Il y a trois opérateurs logiques : `and`, `or` et `not`. Littéralement, `and` signifie "et", donc l'opérateur `and` relie deux valeurs booléennes ou expressions produisant des valeurs booléennes. Si les deux valeurs booléennes sont `True`, le résultat est `True` ; si l'une des deux valeurs booléennes est `False`, le résultat final est `False`. Bien sûr, si la valeur booléenne à gauche de l'opérateur `and` est `False`, quelle que soit la valeur booléenne de droite, le résultat final est `False`, et la valeur booléenne de droite est ignorée (on parle d'évaluation paresseuse ou court-circuit ; si à droite de `and` se trouve une expression, cette expression ne sera pas exécutée). Littéralement, `or` signifie "ou", donc l'opérateur `or` relie également deux valeurs booléennes ou expressions produisant des valeurs booléennes. Si l'une des deux valeurs booléennes est `True`, le résultat final est `True`. L'opérateur `or` possède également une évaluation paresseuse : lorsque la valeur booléenne de gauche est `True`, la valeur booléenne de droite est court-circuitée (si à droite de `or` se trouve une expression, elle ne sera pas exécutée). L'opérateur `not` peut être suivi d'une valeur booléenne. Si la valeur booléenne ou l'expression après `not` est `True`, le résultat est `False` ; si elle est `False`, le résultat est `True`.

```python
"""
Utilisation des opérateurs de comparaison et des opérateurs logiques

Version : 1.0
Auteur : Shadrak BESSANH
"""
flag0 = 1 == 1
flag1 = 3 > 2
flag2 = 2 < 1
flag3 = flag1 and flag2
flag4 = flag1 or flag2
flag5 = not flag0
print('flag0 =', flag0)     # flag0 = True
print('flag1 =', flag1)     # flag1 = True
print('flag2 =', flag2)     # flag2 = False
print('flag3 =', flag3)     # flag3 = False
print('flag4 =', flag4)     # flag4 = True
print('flag5 =', flag5)     # flag5 = False
print(flag1 and not flag2)  # True
print(1 > 2 or 2 == 3)      # False
```

> **Remarque** : La priorité des opérateurs de comparaison est supérieure à celle des opérateurs d'affectation. Ainsi, dans `flag0 = 1 == 1`, l'opération `1 == 1` est effectuée d'abord, produisant la valeur booléenne `True`, qui est ensuite assignée à la variable `flag0`. La fonction `print` peut afficher plusieurs valeurs, séparées par des virgules `,`, et les sorties sont séparées par des espaces par défaut.

### Applications des opérateurs et expressions

#### Exemple 1 : Conversion de Fahrenheit en Celsius

> **Objectif** : Saisir une température en degrés Fahrenheit et la convertir en degrés Celsius. La formule de conversion est : $\small{C = (F - 32) / 1.8}$.

```python
"""
Convertir les degrés Fahrenheit en degrés Celsius

Version : 1.0
Auteur : Shadrak BESSANH
"""
f = float(input('Entrez la température en Fahrenheit : '))
c = (f - 32) / 1.8
print('%.1f Fahrenheit = %.1f Celsius' % (f, c))
```

> **Remarque** : Dans le code ci-dessus, la fonction `input` est utilisée pour recevoir une entrée utilisateur au clavier. Comme les entrées sont des chaînes de caractères, si l'on souhaite les traiter comme des nombres décimaux pour les calculs ultérieurs, on peut utiliser la méthode de conversion de type expliquée dans la leçon précédente, avec la fonction `float` pour convertir le type `str` en `float`.

Dans le code ci-dessus, nous avons formaté la sortie de la fonction `print`. La chaîne de caractères affichée par `print` contient deux espaces réservés `%.1f`. Ces espaces réservés seront remplacés par les valeurs des deux variables de type `float` dans `(f, c)` qui suivent le `%`, avec un chiffre après la virgule. Si la chaîne contient un espace réservé `%d`, il sera remplacé par une valeur de type `int` ; si elle contient un espace réservé `%s`, il sera remplacé par une valeur de type `str`.

Outre cette méthode de formatage de sortie, Python permet également d'utiliser l'approche ci-dessous. Nous fournissons une chaîne de caractères avec des espaces réservés. Le `f` devant la chaîne indique que cette chaîne nécessite un formatage. Les sections `{f:.1f}` et `{c:.1f}` peuvent d'abord être considérées comme `{f}` et `{c}`, signifiant qu'à l'affichage, les valeurs des variables `f` et `c` remplaceront ces espaces réservés. La partie `:.1f` qui suit indique qu'il s'agit d'un nombre à virgule flottante avec un chiffre après la virgule.

```python
"""
Convertir les degrés Fahrenheit en degrés Celsius

Version : 1.1
Auteur : Shadrak BESSANH
"""
f = float(input('Entrez la température en Fahrenheit : '))
c = (f - 32) / 1.8
print(f'{f:.1f} Fahrenheit = {c:.1f} Celsius')
```

#### Exemple 2 : Calcul du périmètre et de l'aire d'un cercle

> **Objectif** : Saisir le rayon d'un cercle ($\small{r}$) et calculer son périmètre ($\small{2 \pi r}$) et son aire ($\small{\pi r^{2}}$).

```python
"""
Saisir le rayon et calculer le périmètre et l'aire d'un cercle

Version : 1.0
Auteur : Shadrak BESSANH
"""
radius = float(input('Entrez le rayon du cercle : '))
perimeter = 2 * 3.1416 * radius
area = 3.1416 * radius * radius
print('Périmètre : %.2f' % perimeter)
print('Aire : %.2f' % area)
```

Python possède un module intégré appelé `math`, dans lequel est définie une variable nommée `pi`, dont la valeur est celle de π. Pour utiliser ce `pi` intégré à Python, nous pouvons légèrement modifier le code ci-dessus.

```python
"""
Saisir le rayon et calculer le périmètre et l'aire d'un cercle

Version : 1.1
Auteur : Shadrak BESSANH
"""
import math

radius = float(input('Entrez le rayon du cercle : '))
perimeter = 2 * math.pi * radius
area = math.pi * radius ** 2
print(f'Périmètre : {perimeter:.2f}')
print(f'Aire : {area:.2f}')
```

> **Remarque** : L'instruction `import math` dans le code ci-dessus signifie que l'on importe le module `math`. Après avoir importé ce module, on peut utiliser `math.pi` pour obtenir la valeur de π.

Il existe en fait une autre méthode de formatage de sortie, ajoutée dans Python 3.8. Regardez simplement le code ci-dessous pour comprendre.

```python
"""
Saisir le rayon et calculer le périmètre et l'aire d'un cercle

Version : 1.2
Auteur : Shadrak BESSANH
"""
import math

radius = float(input('Entrez le rayon du cercle : '))  # Entrée : 5.5
perimeter = 2 * math.pi * radius
area = math.pi * radius ** 2
print(f'{perimeter = :.2f}')  # Sortie : perimeter = 34.56
print(f'{area = :.2f}')       # Sortie : area = 95.03
```

> **Remarque** : Supposons que la valeur de la variable `a` soit `9.87`. Alors la chaîne `f'{a = }'` aura pour valeur `a = 9.87` ; et la chaîne `f'{a = :.1f}'` aura pour valeur `a = 9.9`. Cette méthode de formatage de sortie affiche à la fois le nom de la variable et sa valeur.

#### Exemple 3 : Détermination d'une année bissextile

Objectif : Saisir une année postérieure à 1582 et déterminer si c'est une année bissextile.

```python
"""
Saisir une année, afficher True si bissextile, False sinon

Version : 1.0
Auteur : Shadrak BESSANH
"""
year = int(input('Entrez l'année : '))
is_leap = year % 4 == 0 and year % 100 != 0 or year % 400 == 0
print(f'{is_leap = }')
```

> **Remarque** : Pour le calendrier grégorien, c'est-à-dire le calendrier que nous utilisons aujourd'hui, les règles pour déterminer une année bissextile sont : 1. Les années qui ne sont pas multiples de 4 sont des années communes. 2. Les années multiples de 4 mais non multiples de 100 sont bissextiles. 3. Les années multiples de 400 sont bissextiles. Le calendrier grégorien a été introduit par le pape Grégoire XIII en octobre 1582, en remplacement du calendrier julien. Nous devons en tenir compte lors de la saisie de l'année. Le code ci-dessus utilise l'opérateur `%` pour déterminer si `year` est un multiple de `4`, de `100` ou de `400`. Ensuite, il combine les trois conditions avec les opérateurs `and` et `or`. Les deux premières conditions doivent être satisfaites simultanément, tandis que la troisième condition doit être satisfaite en alternative à la combinaison des deux premières.

### Résumé

À travers les explications et exemples ci-dessus, vous avez sans doute ressenti la puissance des opérateurs et expressions. De nombreux problèmes de programmation pratique nécessitent la construction d'expressions pour être résolus. Ainsi, les variables, opérateurs et expressions sont des bases extrêmement importantes pour tout langage de programmation. S'il y a des points dans cette leçon que vous ne comprenez pas, ne vous précipitez pas vers la leçon suivante. Posez vos questions dans la section des commentaires, je répondrai en temps voulu.