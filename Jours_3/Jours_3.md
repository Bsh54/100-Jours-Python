
## Variables dans le langage Python

Pour les débutants qui souhaitent apprendre la programmation, deux questions les intéressent probablement beaucoup : premièrement, « Qu'est-ce qu'un programme (informatique) ? », et deuxièmement, « À quoi sert l'écriture de programmes (informatiques) ? ». Commençons par exprimer ma compréhension de ces deux questions : **Un programme est un ensemble ordonné de données et d'instructions** ; **Écrire un programme consiste à contrôler l'ordinateur avec des données et des instructions pour qu'il fasse ce que nous voulons**. Aujourd'hui, pourquoi tant de personnes choisissent-elles d'écrire des programmes en Python ? Parce que le langage Python est suffisamment simple et puissant. Comparé à des langages de programmation comme C, C++ ou Java, Python est plus convivial pour les débutants et les non-professionnels ; de nombreux problèmes trouvent des solutions simples et élégantes en Python. Ensuite, commençons par les éléments de langage les plus basiques pour vous présenter et vous faire utiliser le langage Python.

### Quelques connaissances de base

Avant de commencer à apprendre systématiquement la programmation Python, apportons quelques connaissances de base sur l'ordinateur. Le système matériel d'un ordinateur est généralement constitué de cinq grands composants : **l'unité arithmétique et logique**, **l'unité de contrôle**, **la mémoire**, **les périphériques d'entrée** et **les périphériques de sortie**. L'unité arithmétique et logique et l'unité de contrôle ensemble forment ce que nous appelons couramment le **processeur central (CPU)**, dont la fonction est d'exécuter diverses opérations et instructions de contrôle. Nous avons mentionné précédemment qu'un programme est un ensemble d'instructions ; écrire un programme consiste à organiser une série d'instructions d'une certaine manière, puis à utiliser ces instructions pour contrôler l'ordinateur afin qu'il fasse ce que nous voulons. La mémoire peut être divisée en **mémoire interne** et **mémoire externe**. La première est ce que nous appelons couramment la mémoire vive (RAM) ; c'est l'espace de stockage que le processeur central peut adresser directement. Pendant l'exécution du programme, les données et instructions correspondantes doivent être chargées en mémoire. Les périphériques d'entrée et de sortie sont souvent regroupés sous le nom de périphériques d'E/S. Le clavier, la souris, le microphone, la caméra sont des périphériques d'entrée typiques, tandis que l'écran, l'imprimante, les haut-parleurs, etc., sont des périphériques de sortie typiques. Actuellement, la plupart des ordinateurs que nous utilisons suivent essentiellement l'« architecture de von Neumann ». Cette architecture informatique présente deux points clés : premièrement, **séparer la mémoire et le processeur central** ; deuxièmement, **coder les données en binaire**.

Le binaire est un système de numération « par deux », similaire dans son essence au système décimal « par dix » utilisé par les humains. Les humains, ayant dix doigts, utilisent le système décimal ; lorsque les dix doigts sont épuisés pour compter, ils ne peuvent que recourir à une retenue pour représenter des valeurs plus grandes. Bien sûr, il y a des exceptions à tout : les Mayas, probablement parce qu'ils marchaient pieds nus toute l'année, utilisaient également leurs orteils, d'où leur système vicésimal. Sur la base de ce système de comptage, le calendrier utilisé par les Mayas diffère de celui que nous utilisons couramment.  Pour un ordinateur, le binaire est le plus facile à réaliser sur les composants physiques, car on peut utiliser une haute tension pour représenter 1 et une basse tension pour représenter 0. Tous les programmeurs n'ont pas besoin de maîtriser le binaire, ni les conversions entre les systèmes décimal, binaire, octal et hexadécimal ; la plupart du temps, même sans ces connaissances, on peut écrire des programmes. Cependant, nous devons savoir que l'ordinateur utilise le système binaire ; quelles que soient les données, elles existent sous forme binaire dans la mémoire de l'ordinateur.




### Variables et types

Pour sauvegarder des données dans la mémoire de l'ordinateur, il faut d'abord parler du concept de variable. Dans les langages de programmation, **une variable est un support de données**. En termes simples, c'est un espace mémoire utilisé pour sauvegarder des données. **La valeur d'une variable peut être lue et modifiée**, c'est la base de tous les calculs et contrôles. Les données qu'un ordinateur peut traiter sont de nombreux types, le plus courant étant les valeurs numériques. Outre les valeurs numériques, il existe également du texte, des images, de l'audio, de la vidéo, etc. Bien que les données existent toutes sous forme binaire dans l'ordinateur, nous pouvons utiliser différents types de variables pour représenter les différences de types de données. Le langage Python prévoit plusieurs types de données et nous permet également de définir de nouveaux types de données personnalisés, ce qui sera abordé plus tard. Commençons par comprendre plusieurs types de données couramment utilisés en Python.

1. **Entier (`int`)** : Python peut traiter des entiers de toute taille et prend en charge les représentations binaire (par exemple `0b100`, qui équivaut à 4 en décimal), octale (par exemple `0o100`, qui équivaut à 64 en décimal), décimale (`100`) et hexadécimale (`0x100`, qui équivaut à 256 en décimal). Exécutez le code ci-dessous et voyez ce qu'il affiche.

    ```python
    print(0b100)  # Entier binaire
    print(0o100)  # Entier octal
    print(100)    # Entier décimal
    print(0x100)  # Entier hexadécimal
    ```

2. **Nombre à virgule flottante (`float`)** : Les nombres à virgule flottante sont les nombres décimaux. Ils sont appelés ainsi parce que, selon la notation scientifique, la position de la virgule d'un nombre flottant est variable. Outre la notation mathématique (par exemple `123.456`), les nombres flottants prennent également en charge la notation scientifique (par exemple `1.23456e2`, représentant $\small{1.23456 \times 10^{2}}$). Exécutez le code ci-dessous et voyez ce qu'il affiche.

    ```python
    print(123.456)    # Notation mathématique
    print(1.23456e2)  # Notation scientifique
    ```

3. **Chaîne de caractères (`str`)** : Une chaîne de caractères est un texte quelconque entouré de guillemets simples ou doubles, par exemple `'hello'` et `"hello"`.

4. **Booléen (`bool`)** : Le type booléen n'a que deux valeurs : `True` et `False`, soit `True`, soit `False`. Il peut être utilisé pour représenter le « oui » et le « non » dans le monde réel, la « vérité » et la « fausseté » d'une proposition, l'état « bon » ou « mauvais », le niveau « élevé » ou « bas », etc. Si une variable n'a que deux états possibles, nous pouvons utiliser le type booléen.

### Nommage des variables

Pour chaque variable, nous devons lui donner un nom, tout comme chaque personne a son propre nom. En Python, le nommage des variables doit suivre les règles et conventions suivantes.

- **Partie règles** :
  - Règle 1 : Un nom de variable est constitué de **lettres**, de **chiffres** et de **tirets bas**, et ne peut pas commencer par un chiffre. Il est important de noter que les lettres mentionnées ici font référence aux caractères Unicode. Unicode, appelé code universel, inclut la plupart des systèmes d'écriture du monde, ce qui signifie que les caractères chinois, japonais, grecs, etc., peuvent tous être utilisés comme caractères dans un nom de variable. Cependant, certains caractères spéciaux (comme `!`, `@`, `#`, etc.) ne peuvent pas apparaître dans un nom de variable. Nous vous recommandons fortement de comprendre les lettres mentionnées ici comme **n'utilisant que des lettres anglaises dans la mesure du possible**.
  - Règle 2 : Python est un langage de programmation **sensible à la casse**. En termes simples, un `A` majuscule et un `a` minuscule sont deux variables différentes. Ce point n'est pas vraiment une règle, mais plutôt quelque chose à noter.
  - Règle 3 : Les noms de variables **ne doivent pas être identiques aux mots-clés de Python**, et il faut **éviter autant que possible les mots réservés de Python**. Les mots-clés ici font référence aux mots ayant une signification particulière dans un programme Python (comme `is`, `if`, `else`, `for`, `while`, `True`, `False`, etc.). Les mots réservés font principalement référence aux noms des fonctions intégrées, des modules intégrés, etc., de Python (comme `int`, `print`, `input`, `str`, `math`, `os`, etc.).

- **Partie conventions** :
  - Convention 1 : Les noms de variables utilisent généralement **des lettres anglaises minuscules**, et **plusieurs mots sont reliés par des tirets bas**.
  - Convention 2 : Les variables protégées commencent par un seul tiret bas.
  - Convention 3 : Les variables privées commencent par deux tirets bas.

Les conventions 2 et 3 peuvent être ignorées pour le moment ; elles deviendront claires plus tard. Bien sûr, en tant que programmeur professionnel, il est également très important de donner aux variables des noms **significatifs et évocateurs**, ce qui reflète le professionnalisme d'un programmeur, et de nombreux entretiens pour des postes de développement accordent une grande importance à ce point.

### Utilisation des variables

L'exemple suivant illustre les types de variables et leur utilisation.

```python
"""
Utiliser des variables pour sauvegarder des données et effectuer des opérations d'addition, soustraction, multiplication et division

Version : 1.0
Auteur : Shadrak BESSANH
"""
a = 45        # Définir la variable a, lui attribuer 45
b = 12        # Définir la variable b, lui attribuer 12
print(a, b)   # 45 12
print(a + b)  # 57
print(a - b)  # 33
print(a * b)  # 540
print(a / b)  # 3.75
```

En Python, on peut utiliser la fonction `type` pour vérifier le type d'une variable. Le concept de fonction en programmation est très similaire à celui de fonction en mathématiques. Les fonctions mathématiques ne vous sont probablement pas étrangères ; elles incluent le nom de la fonction, la variable indépendante et la variable dépendante. Si vous ne comprenez pas encore ce concept de fonction, ce n'est pas grave ; nous expliquerons en détail la définition et l'utilisation des fonctions dans les sections suivantes.

```python
"""
Utiliser la fonction type pour vérifier le type des variables

Version : 1.0
Auteur : Shadrak BESSANH
"""
a = 100
b = 123.45
c = 'hello, world'
d = True
print(type(a))  # <class 'int'>
print(type(b))  # <class 'float'>
print(type(c))  # <class 'str'>
print(type(d))  # <class 'bool'>
```

On peut utiliser les fonctions intégrées de Python pour changer le type d'une variable. Voici quelques fonctions couramment utilisées liées aux types de variables.

- `int()` : Convertit une valeur numérique ou une chaîne en entier ; on peut spécifier la base.
- `float()` : Convertit une chaîne (si possible) en nombre à virgule flottante.
- `str()` : Convertit l'objet spécifié en forme de chaîne de caractères ; on peut spécifier l'encodage.
- `chr()` : Convertit un entier (code de caractère) en la chaîne de caractères correspondante (un seul caractère).
- `ord()` : Convertit une chaîne de caractères (d'un seul caractère) en l'entier correspondant (code de caractère).

L'exemple ci-dessous montre les opérations de conversion de type en Python.

```python
"""
Opérations de conversion de type de variables

Version : 1.0
Auteur : Shadrak BESSANH
"""
a = 100
b = 123.45
c = '123'
d = '100'
e = '123.45'
f = 'hello, world'
g = True
print(float(a))         # Conversion de l'int 100 en float, affiche 100.0
print(int(b))           # Conversion du float 123.45 en int, affiche 123
print(int(c))           # Conversion de la str '123' en int, affiche 123
print(int(c, base=16))  # Conversion de la str '123' en int en base 16, affiche 291
print(int(d, base=2))   # Conversion de la str '100' en int en base 2, affiche 4
print(float(e))         # Conversion de la str '123.45' en float, affiche 123.45
print(bool(f))          # Conversion de la str 'hello, world' en bool, affiche True
print(int(g))           # Conversion du bool True en int, affiche 1
print(chr(a))           # Conversion de l'int 100 en str, affiche 'd'
print(ord('d'))         # Conversion de la str 'd' en int, affiche 100
```

> **Remarque** : Lors de la conversion de `str` en `int`, on peut spécifier la base avec le paramètre `base`, considérant la chaîne comme un entier dans la base correspondante. Lors de la conversion de `str` en `bool`, tant que la chaîne a un contenu (pas `''` ou `""`), la valeur booléenne correspondante est `True`. Lors de la conversion de `bool` en `int`, `True` devient `1` et `False` devient `0`. Dans les jeux de caractères ASCII et Unicode, le caractère `'d'` correspond au code `100`.

### Résumé

Dans un programme Python, nous pouvons **utiliser des variables pour sauvegarder des données**. **Les variables ont différents types**, les types couramment utilisés étant `int`, `float`, `str` et `bool`. Si nécessaire, on peut convertir le type d'une variable à l'aide des fonctions intégrées de Python. Les variables peuvent être utilisées dans des opérations ; c'est une condition préalable pour résoudre de nombreux problèmes. Nous expliquerons en détail les opérations sur les variables dans la prochaine leçon.
