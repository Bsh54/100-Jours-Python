## Structures de données courantes : Les dictionnaires (dict)

Jusqu'à présent, nous avons présenté trois types de données conteneurs en Python (listes, tuples, ensembles). Cependant, ces types ne suffisent pas toujours pour résoudre tous les problèmes. Par exemple, imaginons que nous devions stocker plusieurs informations concernant une personne : nom, âge, taille, poids, adresse, numéro de téléphone personnel, numéro de contact d'urgence. Dans ce cas, vous constaterez que les listes, tuples et ensembles ne sont pas idéaux.

```python
person1 = ['Pierre Martin', 55, 168, 60, '123 Rue Exemple, 75001 Paris', '06 12 34 56 78', '06 98 76 54 32']
person2 = ('Pierre Martin', 55, 168, 60, '123 Rue Exemple, 75001 Paris', '06 12 34 56 78', '06 98 76 54 32')
person3 = {'Pierre Martin', 55, 168, 60, '123 Rue Exemple, 75001 Paris', '06 12 34 56 78', '06 98 76 54 32'}
```

Les ensembles sont le choix le moins adapté, car ils ne peuvent pas contenir de doublons. Si l'âge et le poids d'une personne sont identiques, l'ensemble perdra une information. De même, si le numéro personnel et le numéro d'urgence sont les mêmes, une autre information disparaîtra. Les listes et tuples peuvent stocker toutes les informations, mais pour récupérer, par exemple, le numéro de téléphone, vous devez connaître sa position exacte dans la séquence (son index). En résumé, dans ce type de scénario, les listes, tuples et ensembles ne sont pas optimaux. C'est là que le **dictionnaire (dictionary)** entre en jeu. Ce type de données est parfaitement conçu pour associer des informations liées et nous aide à modéliser des entités du monde réel dans nos programmes Python.

Le terme "dictionnaire" ne vous est probablement pas inconnu. Dans notre enfance, beaucoup d'entre nous possédaient un dictionnaire de langue.

Les dictionnaires en Python ressemblent à leurs homologues réels. Ils organisent les données sous forme de **paires clé-valeur**. On peut retrouver une valeur en utilisant sa clé associée. De la même manière qu'un dictionnaire de langue associe un mot (la clé) à sa définition (la valeur), chaque paire clé-valeur constitue une entrée, et un dictionnaire contient généralement de nombreuses entrées.

### Création et utilisation d'un dictionnaire

En Python, on peut créer un dictionnaire avec la syntaxe littérale utilisant les accolades `{}`, comme pour les ensembles. Cependant, les éléments entre accolades sont des paires clé-valeur, séparées par deux-points `:`. La partie avant `:` est la **clé**, la partie après `:` est la **valeur**.

```python
dictionnaire = {
    'ordinateur': 'Machine électronique de traitement de l’information',
    'programme': 'Suite d’instructions exécutables par un ordinateur',
    'algorithme': 'Suite finie d’opérations pour résoudre un problème'
}
print(dictionnaire)

personne = {
    'nom': 'Pierre Martin',
    'age': 55,
    'taille': 168,
    'poids': 60,
    'adresse': '123 Rue Exemple, 75001 Paris',
    'tel': '06 12 34 56 78',
    'contact_urgence': '06 98 76 54 32'
}
print(personne)
```

Comme le montre le code ci-dessus, un dictionnaire est bien plus adapté qu'une liste ou un tuple pour stocker les informations d'une personne. Les clés (avant `:`) donnent du sens à chaque information, tandis que les valeurs (après `:`) contiennent l'information elle-même.

On peut également créer un dictionnaire avec la fonction intégrée `dict()` ou en utilisant une compréhension de dictionnaire.

```python
# Le constructeur dict() peut prendre des arguments nommés (clé=valeur)
personne = dict(nom='Pierre Martin', age=55, taille=168, poids=60, adresse='123 Rue Exemple, 75001 Paris')
print(personne)  # {'nom': 'Pierre Martin', 'age': 55, 'taille': 168, 'poids': 60, 'adresse': '123 Rue Exemple, 75001 Paris'}

# On peut utiliser zip() pour "zipper" deux séquences en paires clé-valeur
items1 = dict(zip('ABCDE', '12345'))
print(items1)  # {'A': '1', 'B': '2', 'C': '3', 'D': '4', 'E': '5'}
items2 = dict(zip('ABCDE', range(1, 10)))
print(items2)  # {'A': 1, 'B': 2, 'C': 3, 'D': 4, 'E': 5}

# Compréhension de dictionnaire
items3 = {x: x ** 3 for x in range(1, 6)}
print(items3)  # {1: 1, 2: 8, 3: 27, 4: 64, 5: 125}
```

On utilise `len()` pour obtenir le nombre de paires clé-valeur. Pour parcourir un dictionnaire avec une boucle `for`, on itère par défaut sur ses clés. Nous verrons ensuite comment accéder aux valeurs via ces clés.

```python
personne = {
    'nom': 'Pierre Martin',
    'age': 55,
    'taille': 168,
    'poids': 60,
    'adresse': '123 Rue Exemple, 75001 Paris'
}
print(len(personne))  # 5
for cle in personne:
    print(cle)  # Affiche les clés : nom, age, taille, poids, adresse
```

### Opérations sur les dictionnaires

Pour les dictionnaires, les **tests d'appartenance** et l'**indexation** sont essentiels. Les premiers vérifient si une clé existe. La seconde permet d'accéder à la valeur associée à une clé ou d'ajouter une nouvelle paire clé-valeur. Il est crucial de noter que **les clés d'un dictionnaire doivent être de type immuable (hashable)** : entiers (`int`), flottants (`float`), chaînes de caractères (`str`), tuples (`tuple`). C'est la même exigence que pour les éléments d'un ensemble. Par conséquent, **les listes (`list`), ensembles (`set`) et autres dictionnaires (`dict`) ne peuvent pas être utilisés comme clés**, car ils sont mutables. En revanche, ces types peuvent être utilisés **comme valeurs** dans un dictionnaire.

```python
personne = {
    'nom': 'Pierre Martin',
    'age': 55,
    'taille': 168,
    'poids': 60,
    'adresses': ['123 Rue Exemple, 75001 Paris', '456 Avenue Test, 69002 Lyon'],  # Liste comme valeur
    'voiture': {  # Dictionnaire comme valeur
        'marque': 'BMW X7',
        'vitesse_max': 250,
        'longueur': 5170,
        'largeur': 2000,
        'hauteur': 1835,
        'cylindree': 3.0
    }
}
print(personne)
```

Examinons maintenant les tests d'appartenance et l'indexation :

```python
personne = {'nom': 'Pierre Martin', 'age': 55, 'taille': 168, 'poids': 60, 'adresse': '123 Rue Exemple, 75001 Paris'}

# Tests d'appartenance (vérifient la présence d'une CLÉ)
print('nom' in personne)  # True
print('tel' in personne)  # False

# Indexation : Accès et modification via la clé
print(personne['nom'])     # Accès à la valeur
print(personne['adresse']) # Accès à la valeur
personne['age'] = 25       # Modification d'une valeur existante
personne['taille'] = 178   # Modification
personne['tel'] = '06 12 34 56 78'  # Ajout d'une nouvelle paire clé-valeur
personne['signature'] = 'La vie est belle'
print(personne)

# Parcours avec affichage clé:valeur
for cle in personne:
    print(f'{cle}:\t{personne[cle]}')
```

**Attention** : Si vous tentez d'accéder à une valeur avec une clé qui n'existe pas (par exemple `personne['inexistant']`), Python lèvera une exception `KeyError`.

### Méthodes des dictionnaires

Les méthodes des dictionnaires sont principalement liées à la manipulation des paires clé-valeur.

**Méthode `get()`** : Permet de récupérer la valeur associée à une clé. Contrairement à l'indexation `[]`, `get()` ne lève pas d'erreur si la clé est absente. Elle retourne `None` (ou une valeur par défaut que vous pouvez spécifier).

```python
personne = {'nom': 'Pierre Martin', 'age': 25, 'taille': 178, 'adresse': '123 Rue Exemple, 75001 Paris'}
print(personne.get('nom'))      # Pierre Martin
print(personne.get('sexe'))     # None (pas d'erreur)
print(personne.get('sexe', 'Non spécifié'))  # 'Non spécifié' (valeur par défaut)
```

**Méthodes `keys()`, `values()`, `items()`** :
- `keys()` : Retourne une vue sur toutes les clés du dictionnaire.
- `values()` : Retourne une vue sur toutes les valeurs.
- `items()` : Retourne une vue sur toutes les paires (clé, valeur) sous forme de tuples. C'est très pratique pour itérer.

```python
personne = {'nom': 'Pierre Martin', 'age': 25, 'taille': 178}
print(personne.keys())    # dict_keys(['nom', 'age', 'taille'])
print(personne.values())  # dict_values(['Pierre Martin', 25, 178])
print(personne.items())   # dict_items([('nom', 'Pierre Martin'), ('age', 25), ('taille', 178)])

# Parcours élégant avec .items()
for cle, valeur in personne.items():
    print(f'{cle}:\t{valeur}')
```

**Méthode `update()`** : Fusionne un dictionnaire avec un autre. Si une clé existe dans les deux dictionnaires, la valeur du dictionnaire passé en argument (`other_dict`) écrase celle du dictionnaire original. Les nouvelles clés de `other_dict` sont ajoutées.

```python
personne1 = {'nom': 'Pierre Martin', 'age': 55, 'taille': 178}
personne2 = {'age': 25, 'adresse': '123 Rue Exemple, 75001 Paris'}  # 'age' existe déjà
personne1.update(personne2)
print(personne1)  # {'nom': 'Pierre Martin', 'age': 25, 'taille': 178, 'adresse': '123 Rue Exemple, 75001 Paris'}
```

**Opérateur `|` (Python 3.9+)** : Permet également de fusionner des dictionnaires.

```python
personne1 = {'nom': 'Pierre Martin', 'age': 55, 'taille': 178}
personne2 = {'age': 25, 'adresse': '123 Rue Exemple, 75001 Paris'}
personne1 |= personne2  # Même effet que update()
print(personne1)  # {'nom': 'Pierre Martin', 'age': 25, 'taille': 178, 'adresse': '123 Rue Exemple, 75001 Paris'}
```

**Suppression d'éléments** :
- `pop(clé)` : Supprime la paire avec la clé spécifiée et **retourne sa valeur**. Lève `KeyError` si la clé n'existe pas.
- `popitem()` : Supprime et **retourne une paire (clé, valeur) arbitraire** (souvent la dernière insérée en Python 3.7+ où l'ordre d'insertion est préservé). Pratique pour vider un dictionnaire progressivement.
- `clear()` : Vide complètement le dictionnaire.

```python
personne = {'nom': 'Pierre Martin', 'age': 25, 'taille': 178, 'adresse': '123 Rue Exemple, 75001 Paris'}
print(personne.pop('age'))  # 25 (retourne la valeur supprimée)
print(personne)             # {'nom': 'Pierre Martin', 'taille': 178, 'adresse': '123 Rue Exemple, 75001 Paris'}
print(personne.popitem())   # ('adresse', '123 Rue Exemple, 75001 Paris') (retourne un tuple)
print(personne)             # {'nom': 'Pierre Martin', 'taille': 178}
personne.clear()
print(personne)             # {}
```

On peut aussi utiliser le mot-clé `del` pour supprimer une paire clé-valeur.

```python
personne = {'nom': 'Pierre Martin', 'age': 25, 'taille': 178, 'adresse': '123 Rue Exemple, 75001 Paris'}
del personne['age']
del personne['adresse']
print(personne)  # {'nom': 'Pierre Martin', 'taille': 178}
```

### Applications des dictionnaires

Voyons quelques exemples simples illustrant l'utilité des dictionnaires.

**Exemple 1** : Compter la fréquence des lettres dans une phrase.

```python
phrase = input('Entrez une phrase : ')
compteur = {}
for caractere in phrase:
    if 'A' <= caractere <= 'Z' or 'a' <= caractere <= 'z':
        # Incrémente le compteur pour ce caractère, initialise à 0 si absent
        compteur[caractere] = compteur.get(caractere, 0) + 1

# Trie les clés (lettres) par leur valeur (fréquence) décroissante
cles_triees = sorted(compteur, key=compteur.get, reverse=True)

for lettre in cles_triees:
    print(f"'{lettre}' apparaît {compteur[lettre]} fois.")
```

Entrée :
```
Le Python est un langage de programmation puissant et facile à apprendre.
```

Sortie (approximative, l'ordre peut varier selon les versions) :
```
'e' apparaît 9 fois.
'n' apparaît 6 fois.
'a' apparaît 6 fois.
't' apparaît 5 fois.
'r' apparaît 5 fois.
'g' apparaît 4 fois.
'p' apparaît 4 fois.
...

```

**Exemple 2** : Filtrer un dictionnaire d'actions pour ne garder que celles dont le prix dépasse 100€.

```python
actions = {
    'AAPL': 191.88,
    'GOOG': 1186.96,
    'IBM': 149.24,
    'ORCL': 48.44,
    'ACN': 166.89,
    'FB': 208.09,
    'SYMC': 21.29
}
actions_cher = {cle: valeur for cle, valeur in actions.items() if valeur > 100}
print(actions_cher)
```

Sortie :
```
{'AAPL': 191.88, 'GOOG': 1186.96, 'IBM': 149.24, 'ACN': 166.89, 'FB': 208.09}
```

### Résumé

Les dictionnaires Python sont des structures extrêmement puissantes qui **associent des clés à des valeurs**, permettant une **recherche très efficace** des données par clé. Ils sont idéaux pour modéliser des objets complexes. Rappelez-vous toujours que **les clés doivent être de type immuable** (hashable). Les listes, ensembles et autres dictionnaires ne peuvent donc pas servir de clés, mais peuvent parfaitement être des valeurs.