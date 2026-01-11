# Exercices sur les Variables en Python

## **Exercices de compréhension**

### Exercice 1 : Fondamentaux
Quelle est la différence fondamentale entre la mémoire interne (RAM) et la mémoire externe dans le contexte de l'exécution d'un programme Python ?

### Exercice 2 : Concept de variable
En vos propres mots, expliquez pourquoi on appelle "variable" un espace mémoire qui stocke des données. Qu'est-ce qui est "variable" exactement ?

### Exercice 3 : Représentation binaire
Si toutes les données sont stockées en binaire dans l'ordinateur, pourquoi Python nous permet-il d'écrire `100` (décimal), `0b100` (binaire) et `0x100` (hexadécimal) ?

### Exercice 4 : Architecture von Neumann
L'explication mentionne que l'architecture von Neumann sépare la mémoire et le processeur. Quel serait le problème si cette séparation n'existait pas ?

## **Exercices sur les types de données**

### Exercice 5 : Identification de types
Pour chaque valeur suivante, déterminez son type sans exécuter de code :
1. `3.14159`
2. `"3.14159"`
3. `True`
4. `0b1010`
5. `1.23e-4`
6. `"False"`

### Exercice 6 : Notation scientifique
Convertissez ces nombres en notation scientifique :
1. `1234567.89`
2. `0.000000123`
3. `-987.65`

### Exercice 7 : Conversions de base
Sans exécuter de code, que pensez-vous que donneront ces conversions ?
1. `int("1010", base=2)`
2. `int("FF", base=16)`
3. `int("77", base=8)`

### Exercice 8 : Caractères et codes
1. Quel code Unicode obtiendriez-vous pour la lettre 'A' ?
2. Quel caractère correspond au code 65 ?
3. Pourquoi `chr()` et `ord()` sont-elles des fonctions importantes ?

## **Exercices sur le nommage des variables**

### Exercice 9 : Validité des noms
Parmi ces noms de variables, lesquels sont valides en Python ? Pourquoi ?
1. `ma_variable`
2. `2nd_variable`
3. `_variable_privée`
4. `variable!`
5. `maVariable`
6. `if`
7. `variable123`

### Exercice 10 : Sensibilité à la casse
Soit le code suivant :
```python
Variable = 10
variable = 20
VARIABLE = 30
```
Combien de variables différentes sont créées ? Justifiez.

### Exercice 11 : Noms significatifs
Pour chaque situation, proposez un nom de variable significatif :
1. Stocker l'âge d'une personne
2. Stocker le prix total d'un panier d'achats
3. Stocker si un utilisateur est connecté
4. Stocker le nom complet d'un étudiant

## **Exercices de réflexion critique**

### Exercice 12 : Conversion booléenne
Pourquoi `bool("hello")` retourne `True` alors que `bool("")` retourne `False` ?
Quelle règle générale pouvez-vous déduire pour la conversion des chaînes en booléens ?

### Exercice 13 : Perte de données
Que se passe-t-il quand on convertit `123.987` en `int` ? Pourquoi Python se comporte-t-il ainsi ?
Est-ce que cette perte d'information est toujours souhaitable ?

### Exercice 14 : Variables et mémoire
Quand vous écrivez `x = 10` en Python, que se passe-t-il exactement dans la mémoire de l'ordinateur ?

## **Exercices de mise en pratique**

### Exercice 15 : Déclaration et affichage
Écrivez un programme qui :
1. Déclare 4 variables de types différents (int, float, str, bool)
2. Affiche chaque variable avec son type

### Exercice 16 : Opérations mixtes
Que se passe-t-il quand vous additionnez :
1. Un `int` et un `float` ?
2. Un `str` et un `int` ?
3. Un `bool` et un `int` ?

(Formulez des hypothèses avant de tester)

### Exercice 17 : Conversions en chaîne
Pourquoi `str(True)` donne `"True"` et pas `"1"` ?
Quelle est la différence entre `str(123)` et `"123"` ?

### Exercice 18 : Variables et réaffectation
Observez ce code :
```python
x = 10
print(x)
x = "maintenant je suis une chaîne"
print(x)
```
Est-ce normal qu'une variable change de type en cours de programme ?
Quels sont les avantages et inconvénients de cette caractéristique de Python ?

## **Exercices de synthèse**

### Exercice 19 : Le cycle d'une variable
Tracez le cycle de vie complet d'une variable en Python, depuis sa déclaration jusqu'à sa destruction.
Qu'est-ce qui déclenche la "destruction" d'une variable ?

### Exercice 20 : Variables vs. Constantes
Python n'a pas de constantes au niveau du langage. Comment pourriez-vous simuler une constante ?
Pourquoi certaines langues ont-elles des constantes alors que Python n'en a pas ?

---

## **Consignes pour travailler ces exercices**

1. **Réfléchissez avant de coder** : Pour chaque exercice, notez d'abord votre réponse théorique
2. **Testez vos hypothèses** : Créez un fichier Python pour vérifier vos réponses
3. **Analysez les erreurs** : Si vous vous trompez, comprenez pourquoi
4. **Documentez vos découvertes** : Prenez des notes sur ce que vous apprenez

**Astuce pédagogique** : Ces exercices sont conçus pour faire des liens entre :
- La théorie (comment fonctionne un ordinateur)
- La syntaxe (comment écrire en Python)
- La sémantique (ce que le code signifie réellement)

Le but n'est pas seulement de savoir écrire `x = 10`, mais de comprendre ce que représente cette ligne à tous les niveaux.