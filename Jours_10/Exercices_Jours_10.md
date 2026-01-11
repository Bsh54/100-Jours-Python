# Exercices sur les Tuples en Python

## **Exercices de compréhension fondamentale**

### Exercice 1 : Immutabilité des tuples
1. Pourquoi Python a-t-il à la fois des listes (mutables) et des tuples (immuables) ?
2. Donnez trois exemples concrets où vous utiliseriez un tuple plutôt qu'une liste.
3. Que se passe-t-il si vous essayez de modifier un élément d'un tuple ?

### Exercice 2 : Syntaxe des tuples
Identifiez lesquels sont des tuples et lesquels ne le sont pas :
```python
a = (1)
b = (1,)
c = 1,
d = ()
e = (1, 2, 3)
f = 1, 2, 3
```
Justifiez vos réponses et testez avec `type()`.

### Exercice 3 : Performances tuples vs listes
1. Pourquoi les tuples sont-ils généralement plus rapides à créer que les listes ?
2. Pourquoi `x in tuple` est-il parfois plus rapide que `x in list` ?
3. Quels sont les coûts de mémoire comparés entre tuples et listes ?

## **Exercices sur les opérations de base**

### Exercice 4 : Indexation et slicing
Pour `t = (10, 20, 30, 40, 50, 60, 70, 80, 90, 100)` :
1. Accédez au troisième élément (positif et négatif)
2. Obtenez les trois premiers éléments
3. Obtenez les trois derniers éléments
4. Obtenez un élément sur deux
5. Inversez le tuple

### Exercice 5 : Concaténation et répétition
1. Que donne `(1, 2) + (3, 4)` ?
2. Que donne `(1, 2) * 3` ?
3. Pourquoi `(1, 2) + [3, 4]` ne fonctionne-t-il pas ?
4. Comment concaténer un tuple et une liste ?

### Exercice 6 : Tests et comparaisons
Pour `t1 = (1, 2, 3)`, `t2 = (1, 2, 4)`, `t3 = (1, 2, 3, 0)` :
1. Que valent `t1 == (1, 2, 3)`, `t1 < t2`, `t1 < t3` ?
2. Comment Python compare-t-il des tuples de longueurs différentes ?
3. Créez une fonction qui compare deux tuples élément par élément

## **Exercices sur packing/unpacking**

### Exercice 7 : Dépaquetage de base
1. Dépaquetez `(x, y) = (10, 20)` puis échangez `x` et `y` sans variable temporaire
2. Dépaquetez `(a, b, c) = "XYZ"` - que se passe-t-il ?
3. Dépaquetez `(first, *middle, last) = range(10)` - que contient `middle` ?

### Exercice 8 : Star expression avancée
Pour `t = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)` :
1. Utilisez star expression pour obtenir le premier et le dernier élément
2. Utilisez star expression pour obtenir les 3 premiers et les 3 derniers
3. Pourquoi ne peut-on utiliser qu'une seule star expression par dépaquetage ?

### Exercice 9 : Applications pratiques du dépaquetage
1. Une fonction retourne `(valeur, erreur)` - dépaquetez proprement
2. Lisez un fichier CSV simple et dépaquetez chaque ligne en variables
3. Transformez un dictionnaire en liste de tuples `(clé, valeur)`

## **Exercices sur les conversions**

### Exercice 10 : Conversions tuple ↔ liste
1. Convertissez `[1, 2, 3]` en tuple, puis rajoutez 4 au tuple (indice : reconvertissez en liste)
2. Pourquoi `tuple(liste)` et `list(tuple)` fonctionnent-ils ?
3. Quand est-il utile de convertir une liste en tuple ?

### Exercice 11 : Conversions avec d'autres types
1. Convertissez la chaîne "hello" en tuple de caractères
2. Convertissez le tuple `('h', 'e', 'l', 'l', 'o')` en chaîne sans boucle
3. Convertissez un range en tuple

### Exercice 12 : Préservation de l'ordre
1. Les tuples préservent-ils l'ordre des éléments comme les listes ?
2. Que se passe-t-il si on convertit un ensemble (set) en tuple ?
3. Les éléments du tuple résultant sont-ils dans un ordre prévisible ?

## **Exercices d'application pratique**

### Exercice 13 : Coordonnées géométriques
Utilisez des tuples pour représenter :
1. Un point 2D `(x, y)` et calculez la distance entre deux points
2. Un vecteur 3D `(x, y, z)` et calculez le produit scalaire
3. Un rectangle `(x, y, largeur, hauteur)` et vérifiez si un point est à l'intérieur

### Exercice 14 : Retour de fonctions multiples
Écrivez des fonctions qui retournent des tuples :
1. `divmod` personnalisé qui retourne quotient et reste
2. Une fonction qui retourne min, max, moyenne d'une liste
3. Une fonction qui résout ax²+bx+c=0 et retourne les racines (0, 1 ou 2)

### Exercice 15 : Données structurées
1. Représentez une date `(année, mois, jour)`
2. Représentez une personne `(nom, âge, ville)`
3. Comparez deux dates pour voir laquelle est antérieure

## **Exercices sur les tuples nommés (introduction)**

### Exercice 16 : Utilisation basique de `namedtuple`
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
```
1. Quels sont les avantages par rapport à un tuple normal ?
2. Comment accéder aux attributs `x` et `y` ?
3. Pouvez-vous modifier `p.x` après création ?

### Exercice 17 : Conversion depuis/depuis les tuples normaux
1. Convertissez un `namedtuple` en tuple normal
2. Créez un `namedtuple` à partir d'un tuple normal
3. Comparez la mémoire utilisée par les deux représentations

### Exercice 18 : Méthodes des namedtuples
Explorez les méthodes disponibles :
1. `_asdict()` pour convertir en dictionnaire
2. `_replace()` pour créer une nouvelle instance modifiée
3. `_fields` pour voir les noms des champs

## **Exercices de réflexion critique**

### Exercice 19 : Quand utiliser tuple vs liste vs dict
Pour chaque scénario, choisissez la structure appropriée :
1. Les jours de la semaine
2. Les notes d'un étudiant sur 10 examens
3. Les propriétés d'un rectangle (couleur, position, taille)
4. Un jeu d'échecs (position des pièces)

### Exercice 20 : Immuabilité et hashabilité
1. Pourquoi les tuples sont-ils hashables alors que les listes ne le sont pas ?
2. Testez : `hash((1, 2, 3))` vs `hash([1, 2, 3])`
3. Quelles sont les implications pour les clés de dictionnaires ?

### Exercice 21 : Performance dans les boucles
Comparez ces deux codes :
```python
# Version tuple
points = [(x, y) for x in range(100) for y in range(100)]
for x, y in points:
    pass

# Version liste
points = [[x, y] for x in range(100) for y in range(100)]
for point in points:
    x, y = point[0], point[1]
```
Quelle version est plus rapide ? Pourquoi ?

## **Exercices créatifs**

### Exercice 22 : Système de coordonnées polaires
Créez des fonctions pour :
1. Convertir des coordonnées cartésiennes `(x, y)` en polaires `(r, θ)`
2. Convertir des coordonnées polaires en cartésiennes
3. Additionner deux vecteurs en coordonnées polaires

### Exercice 23 : Jeu de morpion (Tic-Tac-Toe)
Représentez un plateau 3x3 comme tuple de tuples :
```python
board = (
    ('X', 'O', ' '),
    (' ', 'X', 'O'),
    ('O', ' ', 'X')
)
```
Écrivez des fonctions pour :
1. Afficher le plateau
2. Vérifier s'il y a un gagnant
3. Faire un mouvement (créer un nouveau plateau)

### Exercice 24 : Compression de données
Utilisez des tuples pour la compression RLE (Run-Length Encoding) :
1. Codez "aaabbbcc" en `[('a',3), ('b',3), ('c',2)]`
2. Décodez `[('a',3), ('b',3), ('c',2)]` en "aaabbbcc"
3. Comparez l'efficacité pour différentes données

## **Exercice bonus : Algèbre linéaire simple**

### Exercice 25 : Opérations sur les matrices avec tuples
Représentez des matrices comme tuples de tuples :
```python
A = (
    (1, 2, 3),
    (4, 5, 6),
    (7, 8, 9)
)
```
Implémentez :
1. Addition et multiplication de matrices
2. Multiplication par un scalaire
3. Transposition
4. Vérification si une matrice est symétrique

---

## **Consignes pédagogiques avancées**

### Pour maîtriser les tuples :
1. **Comprenez l'immuabilité** : C'est le concept le plus important
   - Avantages : sécurité thread, hashabilité, performances
   - Inconvénients : ne peut être modifié après création

2. **Utilisez le packing/unpacking** :
   - Pour échanger des variables : `a, b = b, a`
   - Pour retourner plusieurs valeurs d'une fonction
   - Pour ignorer des valeurs : `x, _, z = (1, 2, 3)`

3. **Choisissez la bonne structure** :
   - Tuple : données hétérogènes, immuables, petites collections
   - Liste : données homogènes, mutables, opérations fréquentes
   - Namedtuple : besoin de champs nommés mais immuabilité

### Bonnes pratiques :
1. **Nommez vos tuples** : Utilisez `namedtuple` pour la clarté
2. **Utilisez les parenthèses** : Même si optionnelles, elles améliorent la lisibilité
3. **Documentez la structure** : Commentez ce que représente chaque position

### Erreurs courantes à éviter :
- Oublier la virgule pour les singletons : `(1)` n'est pas un tuple !
- Essayer de modifier un tuple après création
- Utiliser des tuples pour de grandes collections modifiées fréquemment
- Confondre `(x, y) = a, b` avec `(x, y) = (a, b)` (elles sont équivalentes)

### Techniques de debug :
1. **Vérifiez les types** :
```python
print(type(variable))  # Surtout pour les singletons
```

2. **Testez l'immuabilité** :
```python
try:
    t[0] = 100
except TypeError as e:
    print(f"Attendu : {e}")
```

3. **Visualisez le packing/unpacking** :
```python
a = 1, 2, 3, 4, 5
print(f"a = {a}")  # (1, 2, 3, 4, 5)
x, *y, z = a
print(f"x={x}, y={y}, z={z}")  # x=1, y=[2, 3, 4], z=5
```

**Objectif** : Les tuples semblent simples mais ont des utilisations sophistiquées. Maîtrisez-les pour écrire du code plus sûr, plus rapide et plus pythonique.