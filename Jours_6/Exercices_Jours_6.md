# Exercices sur les Structures de Boucle en Python

## **Exercices de compréhension fondamentale**

### Exercice 1 : Types de boucles
1. Quelle est la différence fondamentale entre `for` et `while` ?
2. Donnez un exemple concret où vous utiliseriez `for` et un autre où vous utiliseriez `while`.
3. Pourquoi Python n'a-t-il pas de boucle `do-while` comme d'autres langages ?

### Exercice 2 : La fonction `range()`
1. Quels sont les trois paramètres de `range()` et que signifient-ils ?
2. Pourquoi `range(5)` génère-t-il les nombres 0 à 4 et non 1 à 5 ?
3. Comment générer une séquence décroissante avec `range()` ?

### Exercice 3 : Variables de boucle
Pourquoi utilise-t-on `_` comme variable de boucle quand on n'a pas besoin de sa valeur ?
Est-ce juste une convention ou y a-t-il un avantage technique ?

## **Exercices sur les boucles for**

### Exercice 4 : Sommes variées
Écrivez des programmes qui calculent :
1. La somme des multiples de 3 entre 1 et 100
2. La somme des carrés de 1 à n (n saisi par l'utilisateur)
3. La factorielle d'un nombre n (n! = 1×2×3×...×n)

### Exercice 5 : Table de multiplication améliorée
Modifiez le programme de table de multiplication pour :
1. Afficher toutes les tables de 1 à 10 en une seule fois
2. Formater la sortie en colonnes alignées
3. Demander à l'utilisateur quelle table il veut voir

### Exercice 6 : Compréhensions de liste (introduction)
Les compréhensions de liste sont une syntaxe concise pour créer des listes. Par exemple :
```python
carrés = [x**2 for x in range(10)]
```
Utilisez cette syntaxe pour :
1. Créer une liste des nombres pairs de 0 à 50
2. Créer une liste des multiples de 5 entre 1 et 100
3. Créer une liste des cubes des nombres de 1 à 10

## **Exercices sur les boucles while**

### Exercice 7 : Validation d'entrée
Écrivez un programme qui :
1. Demande un nombre entre 1 et 10
2. Continue à demander tant que l'entrée n'est pas valide
3. Utilise `while` pour gérer les tentatives infructueuses

### Exercice 8 : Suite de Fibonacci
Écrivez un programme qui :
1. Demande un nombre n
2. Affiche les n premiers termes de la suite de Fibonacci
   (chaque terme est la somme des deux précédents : 0, 1, 1, 2, 3, 5, 8...)

### Exercice 9 : Approximation de π
Calculez π par la méthode de Monte-Carlo :
1. Générez des points aléatoires dans un carré de côté 1
2. Comptez combien tombent dans le quart de cercle unité
3. π ≈ 4 × (points dans le cercle) / (total points)
4. Arrêtez quand l'approximation est stable à 0.001 près

## **Exercices sur break et continue**

### Exercice 10 : Recherche dans une liste
Écrivez un programme qui :
1. Crée une liste de 20 nombres aléatoires entre 1 et 100
2. Demande un nombre à rechercher
3. Parcourt la liste avec une boucle et utilise `break` dès qu'il trouve le nombre
4. Affiche la position si trouvé, "non trouvé" sinon

### Exercice 11 : Filtrage avec continue
Écrivez un programme qui :
1. Parcourt les nombres de 1 à 100
2. Affiche seulement les nombres qui ne sont ni multiples de 3 ni multiples de 5
3. Utilise `continue` pour sauter les nombres à ignorer

### Exercice 12 : Menu interactif
Créez un menu qui :
```
1. Option 1
2. Option 2
3. Quitter
```
Le programme revient au menu après chaque option, sauf pour "Quitter" qui utilise `break`.

## **Exercices sur les boucles imbriquées**

### Exercice 13 : Triangle d'étoiles
Écrivez un programme qui affiche :
```
*
**
***
****
*****
```

Puis modifiez-le pour afficher :
```
    *
   ***
  *****
 *******
*********
```

### Exercice 14 : Tous les diviseurs
Écrivez un programme qui :
1. Pour chaque nombre de 1 à 100
2. Affiche le nombre et tous ses diviseurs
3. Utilise une boucle imbriquée pour tester chaque diviseur potentiel

### Exercice 15 : Combinaisons
Écrivez un programme qui affiche toutes les combinaisons de :
1. Deux dés (de 1 à 6) et leur somme
2. Lettres 'A', 'B', 'C' avec chiffres 1, 2, 3 (A1, A2, A3, B1...)

## **Exercices d'algorithmique**

### Exercice 16 : Nombres premiers améliorés
1. Modifiez le programme de test de primalité pour qu'il affiche tous les diviseurs s'il n'est pas premier
2. Ajoutez un compteur d'itérations pour comparer l'efficacité
3. Testez avec de grands nombres pour voir la différence

### Exercice 17 : PPCM (Plus Petit Commun Multiple)
Écrivez un programme qui calcule le PPCM de deux nombres en utilisant la relation :
PPCM(a, b) = a × b / PGCD(a, b)
Testez avec différents couples de nombres.

### Exercice 18 : Conjecture de Syracuse
Pour un nombre n, si n est pair : n = n/2, sinon : n = 3n + 1
La conjecture dit qu'on finit toujours par atteindre 1.
Écrivez un programme qui :
1. Prend un nombre n
2. Affiche la suite jusqu'à atteindre 1
3. Compte le nombre d'étapes

## **Exercices de réflexion critique**

### Exercice 19 : Complexité temporelle
Pour chaque algorithme suivant, estimez le nombre d'opérations en fonction de n :
1. Somme de 1 à n (boucle simple)
2. Test de primalité (version simple)
3. Test de primalité (version optimisée avec √n)
4. Table de multiplication n×n (boucles imbriquées)

### Exercice 20 : Boucles infinies intentionnelles
Quand est-il acceptable d'utiliser `while True:` avec `break` ?
Comparez ces deux structures :
```python
# Version 1
i = 0
while i < 10:
    # ...
    i += 1

# Version 2
i = 0
while True:
    if i >= 10:
        break
    # ...
    i += 1
```

## **Exercices créatifs**

### Exercice 21 : Jeu du plus ou moins amélioré
Améliorez le jeu de devinette :
1. Ajoutez un nombre maximum de tentatives (10)
2. Donnez des indices comme "très proche", "assez proche", "loin"
3. Ajoutez un mode deux joueurs
4. Gardez les scores dans un fichier

### Exercice 22 : Horloge numérique
Créez une horloge qui affiche :
```
HH:MM:SS
```
Et se met à jour chaque seconde.
Utilisez `time.sleep(1)` et des boucles imbriquées pour les heures, minutes, secondes.

### Exercice 23 : Crible d'Ératosthène
Implémentez l'algorithme du crible d'Ératosthène pour trouver tous les nombres premiers jusqu'à n :
1. Créez une liste de True de taille n+1
2. Pour i de 2 à √n, si i est premier, marquez tous ses multiples comme non-premiers
3. Affichez tous les nombres restants marqués comme premiers

## **Exercice bonus : Mastermind**

### Exercice 24 : Jeu Mastermind simplifié
Créez une version simplifiée du Mastermind :
1. L'ordinateur génère une combinaison de 4 chiffres (de 1 à 6)
2. Le joueur propose une combinaison
3. L'ordinateur répond avec :
   - ○ pour un chiffre correct bien placé
   - ● pour un chiffre correct mal placé
4. Le jeu continue jusqu'à ce que le joueur trouve ou dépasse 12 tentatives

---

## **Consignes pédagogiques**

1. **Tracez l'exécution** : Pour les exercices complexes, notez les valeurs des variables à chaque itération
2. **Testez les cas limites** : Que se passe-t-il avec n=0, n=1, ou des valeurs négatives ?
3. **Mesurez les performances** : Comparez différentes implémentations du même problème
4. **Dessinez les algorithmes** : Représentez les boucles avec des diagrammes

**Points clés à retenir** :
- `for` quand le nombre d'itérations est connu
- `while` quand ça dépend d'une condition
- `break` pour sortir, `continue` pour sauter
- Les boucles imbriquées multiplient la complexité

**Erreurs courantes à éviter** :
- Oublier de mettre à jour la variable de contrôle dans `while`
- Confondre `break` et `continue`
- Mauvaise indentation dans les boucles imbriquées
- Boucles infinies accidentelles

**Bonnes pratiques** :
- Nommez vos variables de boucle de manière significative
- Utilisez `_` quand la valeur n'est pas utilisée
- Évitez les boucles trop profondément imbriquées
- Commentez les algorithmes complexes

**Astuce de debug** : Ajoutez des `print()` temporaires dans vos boucles pour voir ce qui se passe :
```python
for i in range(5):
    print(f"Début itération, i = {i}")  # Debug
    # ... votre code ...
    print(f"Fin itération, i = {i}")    # Debug
```