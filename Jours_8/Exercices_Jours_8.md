# Exercices sur les Listes en Python - Partie 1

## **Exercices de compréhension fondamentale**

### Exercice 1 : Nature des listes
1. En quoi une liste Python est-elle différente d'un tableau (array) dans d'autres langages comme C ou Java ?
2. Pourquoi est-il possible de stocker des types différents dans une même liste Python ?
3. Quels sont les avantages et inconvénients de cette flexibilité ?

### Exercice 2 : Indexation positive vs négative
Pour la liste `items = ['a', 'b', 'c', 'd', 'e']` :
1. Quelle est la relation entre `items[2]` et `items[-3]` ?
2. Quand utiliseriez-vous l'indexation négative plutôt que positive ?
3. Que se passe-t-il si vous essayez d'accéder à `items[10]` ou `items[-10]` ?

### Exercice 3 : Mutabilité des listes
1. Pourquoi dit-on qu'une liste est "mutable" en Python ?
2. Comparez avec une chaîne de caractères (string) qui est "immuable".
3. Donnez un exemple montrant la différence.

## **Exercices sur la création de listes**

### Exercice 4 : Créations variées
Créez les listes suivantes en une seule ligne de code :
1. Les 10 premiers nombres impairs
2. Les carrés des nombres de 1 à 10
3. Les voyelles de l'alphabet français
4. Une liste contenant 100 fois le même mot

### Exercice 5 : Conversion de types
1. Convertissez la chaîne "Bonjour le monde" en une liste de caractères
2. Convertissez la liste `[1, 2, 3, 4, 5]` en une chaîne de caractères (sans utiliser de boucle)
3. Créez une liste des diviseurs d'un nombre n donné

### Exercice 6 : Listes imbriquées
1. Créez une matrice 3x3 (liste de listes) contenant les nombres de 1 à 9
2. Comment accéder à l'élément au centre de cette matrice ?
3. Que donne `len()` sur une liste imbriquée ?

## **Exercices sur les opérations de base**

### Exercice 7 : Concaténation et répétition
Pour `a = [1, 2, 3]` et `b = [4, 5, 6]` :
1. Quelle est la différence entre `a + b` et `a += b` ?
2. Que donne `a * 3` ?
3. Pourquoi `a * 2 + b` fonctionne mais `a + 2` ne fonctionne pas ?

### Exercice 8 : Tests d'appartenance
Écrivez une fonction qui prend une liste et un élément, et retourne :
1. `True` si l'élément apparaît au moins 2 fois
2. Toutes les positions où l'élément apparaît
3. Le nombre d'éléments uniques dans la liste

### Exercice 9 : Comparaisons
Pour `a = [1, 2, 3]`, `b = [1, 2, 4]`, `c = [1, 2, 3, 0]` :
1. Que valent `a == [1, 2, 3]`, `a < b`, `a < c` ?
2. Comment Python compare-t-il deux listes de longueurs différentes ?
3. Quand utiliseriez-vous ces comparaisons en pratique ?

## **Exercices sur le slicing (tranches)**

### Exercice 10 : Compréhension du slicing
Pour `items = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]` :
1. Obtenez les 3 premiers éléments
2. Obtenez les 3 derniers éléments
3. Obtenez tous les éléments sauf le premier et le dernier
4. Obtenez une copie complète de la liste

### Exercice 11 : Slicing avancé
Toujours avec `items = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]` :
1. Obtenez les éléments pairs
2. Obtenez les éléments en ordre inverse
3. Obtenez un élément sur trois
4. Que donne `items[5:1:-1]` ?

### Exercice 12 : Modification par slicing
Pour `items = [0, 1, 2, 3, 4, 5]` :
1. Remplacez les éléments 2, 3, 4 par `['a', 'b', 'c']`
2. Insérez `[10, 11]` entre les éléments 1 et 2
3. Effacez les éléments 3 et 4 en utilisant le slicing

## **Exercices de parcours**

### Exercice 13 : Parcours avec indices
Écrivez une fonction qui prend une liste et :
1. Affiche chaque élément avec son indice
2. Retourne une liste des éléments aux indices pairs
3. Échange les éléments deux à deux ([1,2,3,4] → [2,1,4,3])

### Exercice 14 : Parcours simultané de deux listes
Étant donné `a = [1, 2, 3]` et `b = ['a', 'b', 'c', 'd']` :
1. Affichez les paires (1,a), (2,b), (3,c)
2. Que faire si les listes n'ont pas la même longueur ?
3. Créez une liste `[(1,'a'), (2,'b'), (3,'c')]`

### Exercice 15 : Parcours avec conditions
Pour une liste de nombres :
1. Trouvez le maximum et son indice
2. Comptez les nombres positifs, négatifs et nuls
3. Créez deux listes : nombres pairs et nombres impairs

## **Exercices d'application**

### Exercice 16 : Statistiques des dés améliorées
1. Modifiez le programme des dés pour qu'il fonctionne avec un nombre variable de dés
2. Ajoutez le calcul de la moyenne et de l'écart-type
3. Affichez un histogramme texte des résultats

### Exercice 17 : Recherche d'éléments
1. Écrivez une fonction qui trouve toutes les occurrences d'un élément
2. Écrivez une fonction qui supprime toutes les occurrences d'un élément
3. Écrivez une fonction qui trouve les éléments communs à deux listes

### Exercice 18 : Manipulation de matrices
Pour une matrice représentée comme liste de listes :
1. Calculez la somme de tous les éléments
2. Calculez la somme de chaque ligne
3. Transposez la matrice (échangez lignes et colonnes)

## **Exercices de réflexion critique**

### Exercice 19 : Copies et références
Observez ce code :
```python
a = [1, 2, 3]
b = a
b[0] = 100
print(a)  # Que donne-t-il ?
```
1. Pourquoi `a` a-t-il changé ?
2. Comment faire une vraie copie d'une liste ?
3. Comparez `a = b`, `a = b[:]`, `a = list(b)`, `a = b.copy()`

### Exercice 20 : Efficacité des opérations
Pour chaque opération, estimez sa complexité temporelle :
1. Accéder à `liste[i]`
2. Vérifier si `x in liste`
3. Concaténer deux listes
4. Créer une tranche (slice)

### Exercice 21 : Listes vs autres structures
Quand utiliseriez-vous une liste plutôt que :
1. Un tuple (immuable) ?
2. Un ensemble (set, sans ordre, sans doublons) ?
3. Un dictionnaire (clés-valeurs) ?

## **Exercices créatifs**

### Exercice 22 : Crible d'Ératosthène avec listes
Implémentez le crible d'Ératosthène pour trouver les nombres premiers jusqu'à N :
1. Créez une liste de booléens initialisés à True
2. Marquez les multiples comme False
3. Extrayez les indices où c'est True

### Exercice 23 : Compression RLE simple
La compression RLE (Run-Length Encoding) code les suites d'éléments identiques.
Exemple : "aaabbbcc" → [(a,3), (b,3), (c,2)]
Implémentez RLE pour une liste quelconque.

### Exercice 24 : Jeu de la vie de Conway
Créez une version simplifiée du jeu de la vie :
1. Représentez la grille par une liste de listes de booléens
2. Appliquez les règles sur une génération
3. Affichez plusieurs générations successives

## **Exercice bonus : Mastermind avec listes**

### Exercice 25 : Jeu Mastermind
Reprenez l'exercice Mastermind en utilisant des listes :
1. Générez une combinaison secrète de 4 couleurs (liste)
2. Comparez avec la proposition du joueur (liste)
3. Donnez les indices (○ bien placé, ● mal placé)
4. Utilisez des listes pour suivre l'historique des tentatives

---

## **Consignes pédagogiques avancées**

### Pour chaque exercice :
1. **Testez les cas limites** : Listes vides, listes à un élément, types mélangés
2. **Mesurez les performances** : Utilisez `time.time()` pour les gros calculs
3. **Comparez les solutions** : Essayez plusieurs approches pour un même problème

### Concepts clés à maîtriser :
- **Mutabilité** : Les listes peuvent être modifiées après création
- **Indexation** : Accès direct à n'importe quel élément en O(1)
- **Slicing** : Extraction de sous-listes sans modification originale
- **Références** : Plusieurs variables peuvent pointer vers la même liste

### Erreurs courantes à éviter :
- Modifier une liste pendant qu'on la parcourt
- Confondre `=` (référence) et copie
- Oublier que les indices commencent à 0
- Utiliser `+` pour ajouter un élément (utilisez `append` à la place)

### Bonnes pratiques :
- Nommez les listes au pluriel (`items`, `nombres`, `utilisateurs`)
- Utilisez des listes en compréhension quand c'est approprié
- Préférez le parcours direct (`for x in liste`) quand l'indice n'est pas nécessaire
- Documentez les préconditions (liste non vide, etc.)

### Techniques de debug :
1. **Affichez les étapes intermédiaires** :
```python
print(f"Avant modification: {liste}")
# modification
print(f"Après modification: {liste}")
```

2. **Utilisez `assert` pour vérifier les invariants** :
```python
assert len(liste) > 0, "La liste ne doit pas être vide"
```

3. **Testez avec des petites données** :
Créez d'abord des exemples simples que vous pouvez vérifier mentalement.

**Le but** : Ces exercices vous préparent aux opérations plus avancées sur les listes (méthodes, tris, compréhensions). Prenez le temps de bien comprendre chaque concept avant de passer à la suite.