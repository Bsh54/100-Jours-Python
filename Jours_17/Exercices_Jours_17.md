# Exercices sur les Décorateurs et la Récursivité

## Exercice 1 - Compréhension de Base des Décorateurs
Écrivez un décorateur simple `compteur_appels` qui enregistre le nombre de fois qu'une fonction a été appelée. Le décorateur doit afficher "Appel n°X" à chaque appel de la fonction décorée.

## Exercice 2 - Décorateur avec Paramètres
Créez un décorateur `repetition(n)` qui prend un paramètre `n` et fait en sorte que la fonction décorée s'exécute `n` fois lorsqu'elle est appelée une seule fois.

## Exercice 3 - Décorateur pour Valider les Entrées
Concevez un décorateur `valider_entiers_positifs` qui vérifie que tous les arguments positionnels passés à une fonction sont des entiers positifs. Si un argument n'est pas un entier positif, le décorateur doit lever une ValueError avec un message approprié.

## Exercice 4 - Chaînage de Décorateurs
Créez deux décorateurs:
1. `majuscules` qui transforme le résultat d'une fonction en majuscules si c'est une chaîne
2. `ajouter_prefixe(prefixe)` qui ajoute un préfixe donné au résultat

Testez les en les appliquant à une fonction `dire_bonjour(nom)` dans différents ordres. Que remarquez-vous?

## Exercice 5 - Décorateur pour Mesurer la Mémoire
Écrivez un décorateur `mesurer_memoire` qui affiche la quantité de mémoire utilisée avant et après l'exécution d'une fonction. Vous pouvez utiliser le module `sys` pour obtenir la mémoire utilisée.

## Exercice 6 - Récursivité: Calcul de Puissance
Implémentez une fonction récursive `puissance_recursive(x, n)` qui calcule x^n (x à la puissance n) pour n entier positif. Pensez à la condition de terminaison et à la formule de récurrence.

## Exercice 7 - Récursivité: Parcours d'Arbre de Dossiers
Écrivez une fonction récursive `afficher_arborescence(chemin, niveau=0)` qui affiche l'arborescence complète d'un dossier (noms des fichiers et sous-dossiers) avec une indentation correspondant à la profondeur. Quelle est la condition de terminaison naturelle ici?

## Exercice 8 - Récursivité vs Itération
Prenez la fonction Fibonacci récursive naïve (sans cache) et:
1. Analysez pourquoi elle est si lente pour des valeurs comme 40
2. Comptez combien d'appels récursifs sont faits pour fib(10)
3. Proposez une version récursive plus efficace sans utiliser de décorateur de cache

## Exercice 9 - Décorateur pour Journaliser
Créez un décorateur `journaliser(fichier_log)` qui:
- Enregistre dans un fichier la date, l'heure, le nom de la fonction et ses arguments
- Enregistre aussi la valeur de retour ou les exceptions levées
- Gère proprement l'ouverture et fermeture du fichier

## Exercice 10 - Récursivité sur les Listes
Écrivez une fonction récursive `aplatir(liste)` qui prend une liste pouvant contenir d'autres listes (imbriquées à n'importe quelle profondeur) et retourne une liste plate de tous les éléments. Par exemple, `aplatir([1, [2, [3, 4], 5]])` doit retourner `[1, 2, 3, 4, 5]`.

---

## Questions de Réflexion Critique

1. Dans quels cas les décorateurs sont-ils préférables à l'héritage de classes? Quand est-ce l'inverse?
2. Pourquoi Python limite-t-il la profondeur de récursion par défaut? Quels sont les risques de modifier cette limite?
3. Comment un décorateur peut-il affecter la signature (docstring, annotations de type, etc.) d'une fonction? Comment y remédier?
4. Quels sont les avantages et inconvénients des solutions récursives par rapport aux solutions itératives en Python?
5. Pourrait-on implémenter les décorateurs sans les fermetures (closures)? Pourquoi les fermetures sont-elles essentielles?
6. En quoi la récursivité terminale (tail recursion) diffère-t-elle de la récursivité classique? Python l'optimise-t-il?
7. Comment tester proprement une fonction décorée? Quelles sont les difficultés spécifiques?
8. Quels seraient les impacts sur la pile d'appels si une fonction récursive n'avait pas de condition de terminaison valide?
9. Comment les décorateurs pourraient-ils être utilisés dans un framework web comme Flask ou Django?
10. Pourquoi `functools.lru_cache` améliore-t-il tant les performances de la fonction Fibonacci récursive? Quel est son coût en mémoire?

---

## Défis Avancés (Optionnels)

1. Implémentez un décorateur `singleton` qui garantit qu'une classe n'a qu'une seule instance.
2. Créez un décorateur `retry(n, exceptions)` qui réessaie une fonction jusqu'à n fois quand certaines exceptions sont levées.
3. Écrivez une fonction récursive qui résout le problème des Tours de Hanoï.
4. Conceivez un décorateur `memoize` personnalisé (sans utiliser `lru_cache`) qui met en cache les résultats d'une fonction.
5. Implémentez un décorateur qui transforme une fonction récursive en version itérative automatiquement.

---

**Conseils pédagogiques:**
- Testez chaque exercice avec des cas simples d'abord
- Utilisez `print()` pour visualiser le flux d'exécution
- Dessinez des diagrammes de pile pour les fonctions récursives
- Comparez toujours plusieurs solutions au même problème
- Mesurez les performances (temps et mémoire) pour prendre des décisions éclairées