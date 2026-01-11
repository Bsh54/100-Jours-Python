# Exercices sur les Listes en Python - Partie 2

## **Exercices sur les méthodes des listes**

### Exercice 1 : Comportement de `remove()`
1. Que se passe-t-il si vous appelez `remove()` avec un élément qui n'existe pas dans la liste ?
2. Si un élément apparaît plusieurs fois, quelle occurrence est supprimée par `remove()` ?
3. Comment supprimer toutes les occurrences d'un élément ?

### Exercice 2 : Différence entre `pop()`, `remove()` et `del`
Pour chaque situation, quelle méthode utiliseriez-vous et pourquoi :
1. Supprimer un élément à un index connu
2. Supprimer un élément par sa valeur (sans connaître son index)
3. Supprimer le dernier élément et l'utiliser ensuite
4. Vider complètement une liste

### Exercice 3 : Méthodes qui modifient vs méthodes qui retournent
Classez ces méthodes :
- Modifient la liste : `append()`, `insert()`, `remove()`, `pop()`, `sort()`, `reverse()`, `clear()`
- Retournent une valeur sans modifier : `index()`, `count()`
- Que fait `copy()` ?

## **Exercices sur les compréhensions de liste**

### Exercice 4 : Transformation de base
Transformez ces boucles en compréhensions de liste :
```python
# 1. Carrés des nombres de 1 à 10
result = []
for i in range(1, 11):
    result.append(i ** 2)

# 2. Nombres pairs entre 0 et 50
pairs = []
for i in range(51):
    if i % 2 == 0:
        pairs.append(i)

# 3. Longueurs des mots d'une liste
words = ['hello', 'world', 'python', 'list']
lengths = []
for word in words:
    lengths.append(len(word))
```

### Exercice 5 : Compréhensions conditionnelles
Créez des listes avec compréhension qui :
1. Contiennent les nombres de 1 à 100 divisibles par 3 et 5
2. Contiennent les voyelles d'une chaîne donnée
3. Transforment une liste de températures en Celsius en Fahrenheit (si > 0°C)

### Exercice 6 : Compréhensions imbriquées
1. Créez une matrice 5x5 avec des nombres aléatoires entre 1 et 10
2. Aplatissez une matrice (liste de listes) en une liste simple
3. Générez toutes les paires (x,y) où x∈[1,3] et y∈[1,3]

## **Exercices sur les listes imbriquées**

### Exercice 7 : Accès aux éléments imbriqués
Pour `matrix = [[1,2,3], [4,5,6], [7,8,9]]` :
1. Comment accéder à l'élément 5 ?
2. Comment obtenir la deuxième ligne ?
3. Comment obtenir la première colonne ?
4. Comment modifier le 8 en 88 ?

### Exercice 8 : Opérations sur les matrices
Écrivez des fonctions qui :
1. Additionnent deux matrices de même taille
2. Multiplient une matrice par un scalaire
3. Vérifient si une matrice est carrée
4. Calculez la trace d'une matrice carrée (somme de la diagonale)

### Exercice 9 : Conversion de structures
1. Convertissez une liste plate en matrice 3x3
2. Convertissez une matrice en liste plate
3. Créez une matrice identité n×n (1 sur la diagonale, 0 ailleurs)

## **Exercices d'application pratique**

### Exercice 10 : Statistiques des étudiants améliorées
Reprenez l'exemple des notes d'étudiants :
1. Calculez la moyenne de chaque étudiant
2. Calculez la moyenne de chaque matière
3. Trouvez l'étudiant avec la meilleure moyenne
4. Ajoutez une fonction pour saisir les notes interactivement

### Exercice 11 : Système de vote
Créez un programme qui :
1. Permet de voter pour 3 candidats (A, B, C)
2. Stocke les votes dans une liste
3. Calcule les pourcentages
4. Détecte les votes invalides
5. Affiche le gagnant

### Exercice 12 : Tri personnalisé
1. Triez une liste de chaînes par longueur
2. Triez une liste de tuples (nom, âge) par âge
3. Triez une liste de nombres par leur distance à 50

## **Exercices sur l'efficacité et performance**

### Exercice 13 : Comparaison de vitesse
Comparez ces deux façons de créer une liste de 1 000 000 d'éléments :
```python
# Version 1 : Boucle + append
result = []
for i in range(1000000):
    result.append(i ** 2)

# Version 2 : Compréhension de liste
result = [i ** 2 for i in range(1000000)]
```
Utilisez `time.time()` pour mesurer la différence.

### Exercice 14 : Opérations coûteuses
Pour une liste de 1000 éléments :
1. Combien de temps prend `item in list` en moyenne ?
2. Que se passe-t-il si vous insérez un élément au début vs à la fin ?
3. Pourquoi `list.pop(0)` est-il plus lent que `list.pop()` ?

### Exercice 15 : Alternatives aux listes
Dans quels cas utiliseriez-vous plutôt :
1. Un `tuple` (immuable) ?
2. Un `deque` (collections.deque) ?
3. Un `array` (array.array) ?

## **Exercices créatifs avec la loterie**

### Exercice 16 : Analyse de la loterie
1. Modifiez le programme pour qu'il évite les combinaisons improbables (ex: 1,2,3,4,5,6)
2. Ajoutez la possibilité de choisir des numéros "chance" fixes
3. Calculez la probabilité de gagner le gros lot

### Exercice 17 : Simulateur de tirages
1. Simulez 1000 tirages et comptez combien de fois chaque numéro sort
2. Vérifiez si certains numéros sortent plus souvent (biais éventuel)
3. Implémentez une stratégie de sélection basée sur les fréquences passées

### Exercice 18 : Vérificateur de tickets
1. Créez un programme qui vérifie si un ticket gagne
2. Calculez les gains selon le nombre de numéros correspondants
3. Gardez un historique des tickets achetés

## **Exercices de réflexion critique**

### Exercice 19 : Mutabilité et effets de bord
Observez ce code :
```python
def ajouter_element(liste, element):
    liste.append(element)
    
ma_liste = [1, 2, 3]
ajouter_element(ma_liste, 4)
print(ma_liste)  # [1, 2, 3, 4]
```
1. Pourquoi `ma_liste` a-t-elle changé à l'extérieur de la fonction ?
2. Comment éviter cet effet de bord si on ne veut pas modifier l'original ?
3. Quand cet effet de bord est-il utile ?

### Exercice 20 : Copies profondes vs superficielles
```python
a = [[1, 2], [3, 4]]
b = a.copy()
b[0][0] = 100
print(a)  # [[100, 2], [3, 4]]
```
1. Pourquoi `a` a-t-il changé ?
2. Comment faire une copie complète (deep copy) ?
3. Dans quels cas une copie superficielle (shallow copy) suffit-elle ?

### Exercice 21 : Éviter les compréhensions trop complexes
Quand une compréhension de liste devient-elle trop complexe ?
Transformez cette compréhension en boucle normale :
```python
result = [(x, y) for x in range(10) if x % 2 == 0 
          for y in range(10) if x + y > 10]
```

## **Exercices avancés**

### Exercice 22 : Implémentation d'une pile (stack)
Utilisez une liste pour implémenter une pile avec :
- `push(element)` : ajoute en haut
- `pop()` : retire et retourne le haut
- `peek()` : regarde le haut sans retirer
- `is_empty()` : vérifie si vide

### Exercice 23 : Implémentation d'une file (queue)
Implémentez une file avec une liste (attention à l'efficacité) :
- `enqueue(element)` : ajoute à la fin
- `dequeue()` : retire du début
- Pourquoi est-ce moins efficace qu'avec `collections.deque` ?

### Exercice 24 : Algorithme de tri
Implémentez le tri à bulles (bubble sort) :
1. Comparez les éléments adjacents et échangez-les si nécessaire
2. Répétez jusqu'à ce que la liste soit triée
3. Mesurez le temps pour trier 1000, 10000 éléments

## **Exercice bonus : Jeu du Sudoku**

### Exercice 25 : Générateur et vérificateur de Sudoku
Créez un programme qui :
1. Génère une grille de Sudoku 9x9 partiellement remplie
2. Vérifie si une grille est valide (pas de doublons en ligne/colonne/région)
3. Résout une grille simple en utilisant un algorithme de backtracking
4. Utilise des listes imbriquées pour représenter la grille

---

## **Consignes pédagogiques avancées**

### Pour les méthodes de liste :
1. **Apprenez par catégories** :
   - Ajout/suppression : `append`, `insert`, `remove`, `pop`, `clear`
   - Recherche : `index`, `count`
   - Réorganisation : `sort`, `reverse`, `copy`
   
2. **Mémo technique** :
   - `append` ajoute à la fin, `insert` à une position
   - `remove` prend une valeur, `pop` prend un index
   - `sort` modifie sur place, `sorted()` retourne une nouvelle liste

### Pour les compréhensions de liste :
**Structure** : `[expression for élément in itérable if condition]`

**Exemples progressifs** :
- Simple : `[x*2 for x in range(5)]`
- Avec condition : `[x for x in range(10) if x%2==0]`
- Imbriquée : `[(x,y) for x in range(3) for y in range(3)]`

**À éviter** : Les compréhensions trop complexes qui nuisent à la lisibilité.

### Pour les listes imbriquées :
**Visualisez** comme des tables :
```python
matrice = [
    [1, 2, 3],  # Ligne 0
    [4, 5, 6],  # Ligne 1
    [7, 8, 9]   # Ligne 2
]
# matrice[ligne][colonne]
```

**Opérations courantes** :
- Nombre de lignes : `len(matrice)`
- Nombre de colonnes : `len(matrice[0])` (si régulière)
- Parcours complet : deux boucles imbriquées

### Bonnes pratiques :
1. **Nommage** : `students_grades` plutôt que `sg` ou `list1`
2. **Documentation** : Commentez le but des listes complexes
3. **Validation** : Vérifiez que les listes imbriquées sont régulières
4. **Performance** : Utilisez des compréhensions pour les gros calculs

### Techniques de debug pour les listes :
1. **Affichez les étapes** :
```python
print(f"Liste initiale: {liste}")
# Opération complexe
print(f"Après opération: {liste}")
```

2. **Utilisez des assertions** :
```python
assert len(liste) > 0, "La liste ne doit pas être vide"
assert all(isinstance(x, int) for x in liste), "Tous les éléments doivent être des entiers"
```

3. **Testez avec des petits exemples** :
Commencez avec 3-5 éléments que vous pouvez vérifier manuellement.

**Objectif final** : Être capable de choisir la bonne structure (liste simple, liste imbriquée, compréhension) pour chaque problème, et d'utiliser les méthodes appropriées de manière efficace.