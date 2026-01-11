## Structures de données courantes : Les chaînes de caractères

La Seconde Guerre mondiale a conduit à la naissance de l'ordinateur moderne. Le premier ordinateur électronique polyvalent s'appelait ENIAC (Electronic Numerical Integrator and Computer). Né à l'Université de Pennsylvanie aux États-Unis, il occupait 167 mètres carrés, pesait environ 27 tonnes et pouvait effectuer environ 5000 opérations en virgule flottante par seconde. Après sa création, ENIAC a été utilisé pour le calcul de trajectoires de missiles, et le calcul numérique reste l'une des fonctions les plus importantes des ordinateurs électroniques modernes.

Au fil du temps, bien que les calculs numériques constituent toujours une part essentielle du travail quotidien des ordinateurs, ceux-ci doivent aujourd'hui traiter d'énormes quantités d'informations sous forme textuelle. Si nous souhaitons manipuler ces informations textuelles avec un programme Python, il est indispensable de comprendre le type de données "chaîne de caractères" ainsi que les opérations et méthodes qui lui sont associées.

### Définition d'une chaîne de caractères

Une **chaîne de caractères** est une **séquence finie de zéro ou plusieurs caractères**, généralement notée :

$$
s = a_1a_2 \cdots a_n \,\,\,\,\, (0 \le n \le \infty)
$$

Dans un programme Python, nous pouvons représenter une chaîne de caractères en entourant un ou plusieurs caractères par des apostrophes simples (`'`) ou doubles (`"`). Les caractères d'une chaîne peuvent être des symboles spéciaux, des lettres de l'alphabet latin, des caractères issus d'autres systèmes d'écriture (comme le grec), ou même des emojis (comme 💩, 🐷, 🀄️).

```python
s1 = 'hello, world!'
s2 = "Bonjour le monde ! ❤️"
s3 = '''hello,
wonderful
world!'''
print(s1)
print(s2)
print(s3)
```

#### Caractères d'échappement

Nous pouvons utiliser la barre oblique inversée `\` (antislash) dans une chaîne pour indiquer un caractère d'échappement. Cela signifie que le caractère suivant le `\` ne représente pas son sens littéral. Par exemple, `\n` ne représente pas les caractères `\` et `n`, mais un saut de ligne. De même, `\t` représente une tabulation. Donc, si la chaîne elle-même contient des caractères spéciaux comme `'`, `"` ou `\`, nous devons les échapper en utilisant `\`. Par exemple, pour afficher une chaîne contenant une apostrophe ou un antislash :

```python
s1 = '\'hello, world!\''
s2 = '\\hello, world!\\'
print(s1)
print(s2)
```

#### Chaînes brutes (raw strings)

Python permet de créer des chaînes brutes en les faisant précéder de `r` ou `R`. Dans une telle chaîne, chaque caractère est interprété littéralement, y compris les antislashs. Il n'y a pas de caractères d'échappement. Par exemple, dans la chaîne `'hello\n'`, `\n` représente un saut de ligne. Dans `r'hello\n'`, `\n` représente simplement les caractères `\` et `n`. Exécutez le code suivant pour observer la différence.

```python
s1 = '\it \is \time \to \read \now'
s2 = r'\it \is \time \to \read \now'
print(s1)
print(s2)
```

> **Note** : Dans la variable `s1` ci-dessus, `\t`, `\r` et `\n` sont des caractères d'échappement. `\t` est une tabulation, `\n` un saut de ligne, et `\r` un retour chariot (qui ramène le curseur au début de la ligne). Comparez les sorties des deux appels `print` pour voir la différence.

#### Représentation spéciale des caractères

Python permet également de représenter un caractère en suivant `\` par un nombre octal ou hexadécimal. Par exemple, `\141` et `\x61` représentent tous deux la lettre minuscule `a` (le premier en octal, le second en hexadécimal). Une autre méthode consiste à utiliser `\u` suivi d'un point de code Unicode. Par exemple, `\u0041` représente la lettre majuscule `A`. Exécutez le code suivant :

```python
s1 = '\141\142\143\x61\x62\x63'
s2 = '\u0041\u0042'
print(s1)  # Affiche : abcabc
print(s2)  # Affiche : AB
```

### Opérations sur les chaînes

Le langage Python offre un riche ensemble d'opérateurs pour le type chaîne de caractères, dont beaucoup sont similaires à ceux des listes. Par exemple, nous pouvons utiliser l'opérateur `+` pour concaténer des chaînes, l'opérateur `*` pour répéter une chaîne, les opérateurs `in` et `not in` pour vérifier l'inclusion, et les opérateurs `[]` et `[:]` pour extraire un ou plusieurs caractères.

#### Concaténation et répétition

L'exemple suivant montre l'utilisation des opérateurs `+` et `*`.

```python
s1 = 'hello' + ', ' + 'world'
print(s1)    # hello, world
s2 = '!' * 3
print(s2)    # !!!
s1 += s2
print(s1)    # hello, world!!!
s1 *= 2
print(s1)    # hello, world!!!hello, world!!!
```

L'opérateur `*` pour répéter une chaîne est très pratique. Dans de nombreux langages, pour représenter une chaîne de 10 `a`, il faut écrire `'aaaaaaaaaa'`. En Python, on peut écrire `'a' * 10`. Imaginez devoir répéter un caractère 100 ou 1000 fois !

#### Comparaisons

Pour deux variables de type chaîne, on peut utiliser directement les opérateurs de comparaison pour vérifier l'égalité ou comparer leur ordre. La comparaison se fait caractère par caractère en fonction de leur valeur numérique (code point Unicode). Par exemple, le code de `A` est `65` et celui de `a` est `97`, donc `'A' < 'a'` donne `True`. Pour `'boy' < 'bad'`, la première lettre (`'b'`) est identique, on compare donc la seconde : `'o'` (111) < `'a'` (97) est `False`, donc l'expression globale est `False`. La fonction `ord()` permet d'obtenir le code d'un caractère.

```python
s1 = 'a whole new world'
s2 = 'hello world'
print(s1 == s2)             # False
print(s1 < s2)              # True
print(s1 == 'hello world')  # False
print(s2 == 'hello world')  # True
print(s2 != 'Hello world')  # True
print(ord('A'))             # 65
print(ord('a'))             # 97
print('A' < 'a')            # True
print('boy' < 'bad')        # False
```

#### Vérification d'appartenance

On peut utiliser `in` et `not in` pour vérifier si une chaîne ou un caractère est présent dans une autre chaîne, comme pour les listes.

```python
s1 = 'hello, world'
s2 = 'goodbye, world'
print('wo' in s1)      # True
print('wo' not in s2)  # False
print(s2 in s1)        # False
```

#### Longueur d'une chaîne

Comme pour les listes, on utilise la fonction intégrée `len()`.

```python
s = 'hello, world'
print(len(s))                 # 12
print(len('goodbye, world'))  # 14
```

#### Indexation et découpage (slicing)

L'indexation et le découpage des chaînes fonctionnent presque de la même manière que pour les listes et les tuples, car une chaîne est aussi une séquence ordonnée. Cependant, il est crucial de se rappeler que **les chaînes sont immuables**. On **ne peut pas modifier un caractère via son index**.

```python
s = 'abc123456'
n = len(s)
print(s[0], s[-n])    # a a
print(s[n-1], s[-1])  # 6 6
print(s[2], s[-7])    # c c
print(s[5], s[-4])    # 3 3
print(s[2:5])         # c12
print(s[-7:-4])       # c12
print(s[2:])          # c123456
print(s[:2])          # ab
print(s[::2])         # ac246
print(s[::-1])        # 654321cba
```

> **Attention** : Un accès avec un index hors limites provoquera une exception `IndexError` avec le message `string index out of range`.

### Parcours des caractères

Pour parcourir chaque caractère d'une chaîne, on peut utiliser une boucle `for-in` de deux manières.

Méthode 1 :
```python
s = 'hello'
for i in range(len(s)):
    print(s[i])
```

Méthode 2 (plus pythonique) :
```python
s = 'hello'
for elem in s:
    print(elem)
```

### Méthodes des chaînes

En Python, nous pouvons manipuler les chaînes en utilisant leurs méthodes. Si nous avons une chaîne nommée `foo` et une méthode nommée `bar`, la syntaxe est `foo.bar()`. C'est la syntaxe standard pour appeler une méthode sur un objet.

#### Méthodes liées à la casse

```python
s1 = 'hello, world!'
# Capitalise la première lettre
print(s1.capitalize())  # Hello, world!
# Met en majuscule la première lettre de chaque mot
print(s1.title())       # Hello, World!
# Met toute la chaîne en majuscules
print(s1.upper())       # HELLO, WORLD!
s2 = 'GOODBYE'
# Met toute la chaîne en minuscules
print(s2.lower())       # goodbye
# Vérifie les valeurs originales (les chaînes sont immuables)
print(s1)               # hello, world!
print(s2)               # GOODBYE
```

> **Note** : Les chaînes étant immuables, les méthodes renvoient une nouvelle chaîne sans modifier l'originale. C'est pourquoi `s1` et `s2` conservent leurs valeurs initiales.

#### Recherche

Pour rechercher une sous-chaîne, on utilise `find()` ou `index()`. On peut également spécifier une plage de recherche (début, fin). `find()` renvoie `-1` si la sous-chaîne n'est pas trouvée, tandis que `index()` lève une exception `ValueError`.

```python
s = 'hello, world!'
print(s.find('or'))      # 8
print(s.find('or', 9))   # -1
print(s.find('of'))      # -1
print(s.index('or'))     # 8
# print(s.index('or', 9))  # ValueError: substring not found
```

Il existe aussi des versions de recherche inversée (de droite à gauche) : `rfind()` et `rindex()`.

```python
s = 'hello world!'
print(s.find('o'))       # 4
print(s.rfind('o'))      # 7
print(s.rindex('o'))     # 7
# print(s.rindex('o', 8))  # ValueError: substring not found
```

#### Vérification de propriétés

Les méthodes `startswith()` et `endswith()` vérifient le début et la fin d'une chaîne. D'autres méthodes commençant par `is` vérifient des caractéristiques. Elles renvoient un booléen.

```python
s1 = 'hello, world!'
print(s1.startswith('He'))   # False
print(s1.startswith('hel'))  # True
print(s1.endswith('!'))      # True
s2 = 'abc123456'
print(s2.isdigit())  # False (pas uniquement des chiffres)
print(s2.isalpha())  # False (pas uniquement des lettres)
print(s2.isalnum())  # True (lettres et chiffres uniquement)
```

> **Note** : `isdigit()` vérifie si la chaîne est composée uniquement de chiffres. `isalpha()` vérifie si elle est composée uniquement de lettres (caractères Unicode alphabétiques, hors emojis). `isalnum()` vérifie si elle est composée de lettres et/ou de chiffres.

#### Formatage

Les méthodes `center()`, `ljust()`, `rjust()` permettent d'aligner une chaîne dans un champ de largeur donnée, en la complétant avec un caractère spécifique (espace par défaut). `zfill()` remplit avec des zéros à gauche.

```python
s = 'hello, world'
print(s.center(20, '*'))  # ****hello, world****
print(s.rjust(20))        # '        hello, world' (8 espaces)
print(s.ljust(20, '~'))   # hello, world~~~~~~~~
print('33'.zfill(5))      # 00033
print('-33'.zfill(5))     # -0033
```

Nous avons vu précédemment qu'on pouvait formater une chaîne avec l'opérateur `%` dans `print()` :

```python
a = 321
b = 123
print('%d * %d = %d' % (a, b, a * b))
```

La méthode `format()` offre une alternative :

```python
a = 321
b = 123
print('{0} * {1} = {2}'.format(a, b, a * b))
```

Depuis Python 3.6, les f-strings (chaînes formatées) offrent une syntaxe plus concise et lisible :

```python
a = 321
b = 123
print(f'{a} * {b} = {a * b}')
```

Pour un contrôle précis du format, on peut utiliser des spécificateurs de format à l'intérieur des accolades :

| Valeur      | Spécificateur | Résultat       | Description |
| ----------- | ------------- | -------------- | ----------- |
| `3.1415926` | `{:.2f}`      | `'3.14'`       | Deux décimales |
| `3.1415926` | `{:+.2f}`     | `'+3.14'`      | Deux décimales avec signe |
| `-1`        | `{:+.2f}`     | `'-1.00'`      | Deux décimales avec signe |
| `3.1415926` | `{:.0f}`      | `'3'`          | Pas de décimale |
| `123`       | `{:0>10d}`    | `'0000000123'` | Remplissage à gauche par des `0` (largeur 10) |
| `123`       | `{:x<10d}`    | `'123xxxxxxx'` | Remplissage à droite par des `x` (largeur 10) |
| `123`       | `{:>10d}`     | `'       123'` | Alignement à droite (largeur 10) |
| `123`       | `{:<10d}`     | `'123       '` | Alignement à gauche (largeur 10) |
| `123456789` | `{:,}`        | `'123,456,789'`| Séparateur de milliers |
| `0.123`     | `{:.2%}`      | `'12.30%'`     | Format pourcentage |
| `123456789` | `{:.2e}`      | `'1.23e+08'`   | Notation scientifique |

#### Élagage (trim)

La méthode `strip()` supprime les caractères spécifiés (espaces par défaut) aux deux extrémités de la chaîne. `lstrip()` et `rstrip()` ne le font qu'à gauche ou à droite. Très utile pour nettoyer les entrées utilisateur.

```python
s1 = '   jackfrued@126.com  '
print(s1.strip())      # 'jackfrued@126.com'
s2 = '~Bonjour le monde~'
print(s2.lstrip('~'))  # 'Bonjour le monde~'
print(s2.rstrip('~'))  # '~Bonjour le monde'
```

#### Remplacement

La méthode `replace()` remplace toutes les occurrences d'une sous-chaîne par une autre. Un troisième argument optionnel limite le nombre de remplacements.

```python
s = 'hello, good world'
print(s.replace('o', '@'))     # hell@, g@@d w@rld
print(s.replace('o', '@', 1))  # hell@, good world
```

#### Découpage et jointure

`split()` divise une chaîne en une liste de sous-chaînes selon un séparateur (espace par défaut). `join()` fait l'inverse : elle assemble une liste de chaînes en une seule, en les joignant par la chaîne sur laquelle elle est appelée.

```python
s = 'I love you'
words = s.split()
print(words)            # ['I', 'love', 'you']
print('~'.join(words))  # I~love~you
```

`split()` accepte un séparateur personnalisé et un argument `maxsplit` pour limiter le nombre de découpes.

```python
s = 'I#love#you#so#much'
words = s.split('#')
print(words)  # ['I', 'love', 'you', 'so', 'much']
words = s.split('#', 2)
print(words)  # ['I', 'love', 'you#so#much']
```

#### Encodage et décodage

En plus du type `str`, Python a un type `bytes` pour représenter des données binaires (séquence d'octets). La méthode `encode()` d'une chaîne la code en une séquence d'octets selon un encodage spécifique (comme UTF-8). La méthode `decode()` d'un objet `bytes` fait l'opération inverse.

```python
a = 'Élodie'
b = a.encode('utf-8')
c = a.encode('latin-1')
print(b)                  # b'\xc3\x89lodie' (repr. hexa des octets UTF-8)
print(c)                  # b'\xc9lodie' (repr. hexa des octets latin-1)
print(b.decode('utf-8'))  # Élodie
print(c.decode('latin-1'))# Élodie
```

> **Attention** : Utiliser un encodage pour le codage et un autre pour le décodage entraînera une erreur `UnicodeDecodeError` ou un affichage incorrect (mojibake).

#### Autres méthodes

Une opération courante consiste à vérifier si une chaîne correspond à un modèle spécifique (expression régulière). Le module standard `re` de Python fournit des outils puissants pour cela, sujet qui sera abordé ultérieurement.

### Résumé

Savoir représenter et manipuler les chaînes de caractères est fondamental pour tout programmeur, car le traitement de texte est omniprésent. Python offre pour cela des opérateurs pratiques (concaténation, indexation, découpage) et une gamme très complète de méthodes intégrées au type `str`.