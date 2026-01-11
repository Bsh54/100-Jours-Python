# Exercices sur la Pratique des Structures Conditionnelles et de Boucle

## **Exercices de décomposition et reconstruction**

### Exercice 1 : Analyse du code - Nombres premiers
Pour le programme des nombres premiers inférieurs à 100 :
1. Pourquoi vérifie-t-on seulement jusqu'à `int(num ** 0.5) + 1` ?
2. Combien d'itérations totales fait ce programme (pour tous les nombres de 2 à 99) ?
3. Comment pourriez-vous optimiser ce code pour qu'il soit plus rapide ?

### Exercice 2 : Fibonacci pas à pas
Tracez l'exécution de la suite de Fibonacci pour les 5 premiers termes :
```
Itération 1: a=0, b=1 → a,b = 1,1 → print(1)
Itération 2: a=1, b=1 → a,b = 1,2 → print(1)
Itération 3: a=1, b=2 → a,b = 2,3 → print(2)
...
```
Pourquoi commence-t-on avec `a=0, b=1` au lieu de `a=1, b=1` ?

### Exercice 3 : Inversion d'entier détaillée
Pour `num = 12345`, suivez chaque itération de la boucle :
```
Itération 1: num=12345, reversed_num=0 → reversed_num=5, num=1234
Itération 2: num=1234, reversed_num=5 → reversed_num=54, num=123
...
```
Expliquez mathématiquement pourquoi `reversed_num * 10 + num % 10` fonctionne.

## **Exercices sur les nombres spéciaux**

### Exercice 4 : Nombres parfaits
Un nombre parfait est un nombre égal à la somme de ses diviseurs propres (excluant lui-même).
Par exemple : 6 = 1 + 2 + 3, 28 = 1 + 2 + 4 + 7 + 14.
Écrivez un programme qui trouve tous les nombres parfaits inférieurs à 10000.

### Exercice 5 : Nombres amicaux
Deux nombres sont dits amicaux si la somme des diviseurs propres du premier est égale au second, et vice versa.
Exemple : 220 et 284 (diviseurs de 220 : 1+2+4+5+10+11+20+22+44+55+110 = 284, diviseurs de 284 : 1+2+4+71+142 = 220).
Trouvez toutes les paires amicales inférieures à 10000.

### Exercice 6 : Nombre d'Armstrong généralisé
Écrivez un programme qui trouve tous les nombres d'Armstrong (narcissiques) à n chiffres, pour n de 1 à 7.
Attention : 153 = 1³ + 5³ + 3³ (3 chiffres), 1634 = 1⁴ + 6⁴ + 3⁴ + 4⁴ (4 chiffres).

## **Exercices de recherche exhaustive**

### Exercice 7 : Équation diophantienne
Résolvez l'équation : 3x + 5y + 7z = 100
Trouvez tous les triplets (x, y, z) d'entiers positifs ou nuls qui satisfont cette équation.

### Exercice 8 : Problème des pièces de monnaie
Avec des pièces de 2€, 5€ et 10€, combien de façons existe-t-il de faire 50€ ?
Écrivez un programme qui compte toutes les combinaisons possibles.

### Exercice 9 : Carré magique 3×3
Un carré magique 3×3 contient les nombres 1 à 9 tels que chaque ligne, colonne et diagonale ait la même somme.
Écrivez un programme qui trouve tous les carrés magiques 3×3 possibles (en ignorant les rotations et symétries).

## **Exercices d'optimisation algorithmique**

### Exercice 10 : Crible d'Ératosthène
Implémentez le crible d'Ératosthène pour trouver tous les nombres premiers jusqu'à 1 000 000.
Comparez son efficacité avec la méthode de division essayale (l'exemple 1).

### Exercice 11 : Mémoïsation Fibonacci
Écrivez une version de Fibonacci qui utilise la mémoïsation (stocker les résultats déjà calculés) pour éviter les calculs redondants.
Testez pour n=100 (avec la méthode récursive simple, c'est impossible !).

### Exercice 12 : Recherche binaire vs linéaire
Comparez ces deux méthodes pour rechercher un élément dans une liste triée de 1 000 000 éléments.
Quelle est la complexité en pire cas de chaque méthode ?

## **Exercices de simulation et jeux**

### Exercice 13 : Pierre-Papier-Ciseaux
Simulez 1000 parties de Pierre-Papier-Ciseaux entre deux joueurs qui choisissent aléatoirement.
Calculez les statistiques : fréquences de chaque choix, pourcentage de matchs nuls.

### Exercice 14 : Marche aléatoire
Simulez une marche aléatoire en 1D : un point part de 0, à chaque étape il avance de +1 ou -1 avec probabilité 1/2.
Après 1000 pas, quelle est la position moyenne sur 10000 simulations ?

### Exercice 15 : Paradoxe des anniversaires
Simulez le paradoxe des anniversaires : dans un groupe de n personnes, quelle est la probabilité qu'au moins deux personnes aient la même date d'anniversaire ?
Testez pour n=23, n=30, n=50. Comparez avec la formule théorique.

## **Exercices de création de motifs**

### Exercice 16 : Triangle de Pascal
Affichez les 10 premières lignes du triangle de Pascal :
```
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
...
```

### Exercice 17 : Spirale numérique
Générez une spirale carrée de nombres :
```
21 22 23 24 25
20  7  8  9 10
19  6  1  2 11
18  5  4  3 12
17 16 15 14 13
```
Pour une taille n×n donnée.

### Exercice 18 : Fractale simple - Triangle de Sierpinski
Créez une approximation ASCII du triangle de Sierpinski sur 8 niveaux.

## **Exercices sur la validation et robustesse**

### Exercice 19 : Gestion des erreurs CRAPS
Améliorez le jeu CRAPS pour :
1. Gérer les entrées invalides (mise non numérique, négative, etc.)
2. Ajouter une limite de tours maximum (ex: 100 tours)
3. Permettre au joueur de quitter à tout moment

### Exercice 20 : Benchmark de performances
Écrivez trois versions du calcul de la somme des nombres premiers inférieurs à n :
1. Version naïve (double boucle)
2. Version optimisée (√n)
3. Version crible
Mesurez le temps d'exécution pour n=10000, n=100000.

## **Exercices de réflexion critique**

### Exercice 21 : Quand ne pas utiliser les boucles
Certains problèmes peuvent être résolus sans boucles explicites. Par exemple :
- Somme de 1 à n : n(n+1)/2
- Somme des carrés : n(n+1)(2n+1)/6
Donnez d'autres exemples où une formule mathématique est préférable à une boucle.

### Exercice 22 : Lire le Zen de Python
Le Zen de Python dit : "Flat is better than nested."
À partir des exemples de cette leçon, donnez un cas où des boucles imbriquées sont nécessaires et un cas où elles pourraient être évitées.

### Exercice 23 : Complexité et limites
Pour le problème des cent poulets :
- Version 1.0 : environ 21×34×34 = 24,276 itérations
- Version 1.1 : environ 21×34 = 714 itérations
Que se passe-t-il si on avait 1000 animaux et 1000 pièces au lieu de 100 ?

## **Projet final intégratif**

### Exercice 24 : Jeu du Blackjack simplifié
Créez un jeu de Blackjack avec ces règles simplifiées :
1. Un jeu de 52 cartes, valeurs : 2-10 = valeur nominale, J/Q/K = 10, As = 1 ou 11
2. Le joueur et le croupier reçoivent 2 cartes chacun (une du croupier cachée)
3. Le joueur peut demander des cartes supplémentaires ("hit") ou s'arrêter ("stand")
4. Le croupier tire jusqu'à atteindre au moins 17
5. Gagne celui le plus proche de 21 sans dépasser

Fonctionnalités à implémenter :
- Gestion du capital (mises)
- Option "doubler"
- Statistiques de parties
- Interface texte claire

---

## **Consignes pédagogiques avancées**

### Pour chaque exercice :
1. **Planifiez avant de coder** : Écrivez l'algorithme en français d'abord
2. **Testez progressivement** : Commencez avec de petites valeurs pour vérifier
3. **Analysez la complexité** : Estimez le nombre d'opérations
4. **Cherchez des optimisations** : Y a-t-il une meilleure approche ?

### Compétences à développer :
- **Décomposition** : Diviser un problème complexe en sous-problèmes
- **Reconnaissance de patterns** : Voir des structures récurrentes
- **Optimisation** : Réduire le nombre d'opérations inutiles
- **Validation** : Tester tous les cas possibles

### Checklist de qualité du code :
- [ ] Noms de variables significatifs
- [ ] Commentaires pour les parties complexes
- [ ] Gestion des cas limites
- [ ] Code lisible (indentation, espaces)
- [ ] Pas de redondance

### Journal d'apprentissage recommandé :
Pour chaque exercice, notez :
1. Temps passé à planifier vs coder
2. Difficultés rencontrées
3. Solutions trouvées
4. Ce que vous avez appris

**Rappel** : La maîtrise vient de la pratique. Ces exercices sont difficiles intentionnellement. Si vous bloquez :
1. Prenez une pause
2. Essayez de résoudre un sous-problème plus simple
3. Cherchez des exemples similaires
4. Demandez de l'aide sur des points spécifiques

**Le but n'est pas de tout réussir du premier coup, mais de développer votre capacité à résoudre des problèmes complexes.**