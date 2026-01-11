# Exercices sur les ensembles (sets) en Python

## Exercice 1 : Création et propriétés de base
Écris un programme qui :
1. Crée un ensemble contenant les voyelles de l'alphabet français
2. Crée un ensemble à partir de la phrase "Le chat dort sur le tapis" (sépare les mots)
3. Crée un ensemble de nombres de 1 à 20 divisibles par 2 ou 3
4. Montre que les doublons sont automatiquement éliminés

## Exercice 2 : Comparaison avec les listes
Crée :
1. Une liste avec 1000 nombres aléatoires entre 1 et 100 (utilise `random.randint()`)
2. Un ensemble à partir de cette liste
Compare :
3. Leurs longueurs respectives
4. Le temps d'exécution pour vérifier si le nombre 50 est présent (utilise `time.time()`)
Réfléchis : pourquoi y a-t-il une différence de performance ?

## Exercice 3 : Opérations ensemblistes
Soit :
- A = {2, 4, 6, 8, 10, 12}
- B = {3, 6, 9, 12, 15}
- C = {x for x in range(1, 21) if x % 2 == 0}

Calcule et affiche :
1. A ∩ B (intersection)
2. A ∪ B (union)
3. A - B (différence)
4. B - A (différence)
5. A Δ B (différence symétrique)
6. (A ∪ B) ∩ C
7. Les éléments qui sont dans exactement deux des trois ensembles

## Exercice 4 : Applications pratiques
Écris des fonctions qui :
1. Retournent les lettres communes à deux mots
2. Retournent les lettres présentes dans un mot mais pas dans l'autre
3. Vérifient si deux phrases ont des mots en commun
4. Trouvent les amis communs entre deux personnes (représente les amis comme des ensembles)

## Exercice 5 : Validation de données
Un système enregistre des emails. Écris un programme qui :
1. Prend une liste d'emails (certains en double)
2. Les convertit en ensemble pour éliminer les doublons
3. Vérifie si un nouvel email est déjà présent
4. Ajoute un nouvel email seulement s'il n'existe pas déjà
5. Compte combien d'emails uniques ont été enregistrés

## Exercice 6 : Relations ensemblistes
Pour trois ensembles E, F, G, écris des tests qui vérifient :
1. Si E est inclus dans F
2. Si E et F sont disjoints
3. Si F est un sur-ensemble de G
4. Si E ∪ F = G
5. Si E ∩ F = ∅ (ensemble vide)

## Exercice 7 : Manipulation d'ensembles
Soit un ensemble S = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
Écris un programme qui :
1. Ajoute les nombres 11, 12, 13
2. Supprime les nombres pairs
3. Supprime un élément au hasard (avec `pop()`)
4. Essaie de supprimer le nombre 20 (utilise `discard()` et `remove()`, compare)
5. Vide complètement l'ensemble

## Exercice 8 : frozenset et immutabilité
1. Crée un frozenset avec les jours de la semaine
2. Essaie d'ajouter/supprimer un élément (observe l'erreur)
3. Crée un ensemble normal contenant plusieurs frozensets
4. Montre qu'on ne peut pas mettre un set dans un autre set
5. Utilise un frozenset comme clé dans un dictionnaire

## Exercice 9 : Problème des sous-ensembles
Pour un ensemble donné S = {1, 2, 3} :
1. Trouve tous les sous-ensembles possibles (ensemble des parties)
2. Trouve tous les sous-ensembles de taille 2
3. Vérifie qu'un ensemble a 2^n sous-ensembles (où n = |S|)
4. Génère tous les sous-ensembles d'un ensemble de 4 éléments

## Exercice 10 : Analyse de texte avancée
Écris une fonction qui prend deux textes et retourne :
1. L'ensemble des mots communs aux deux textes
2. L'ensemble des mots uniques à chaque texte
3. Le pourcentage de mots du texte 1 qui apparaissent dans le texte 2
4. Les mots qui apparaissent dans au moins un texte mais pas dans les deux

## Exercice 11 : Théorie des ensembles
Implémente les lois de De Morgan pour les ensembles :
Pour tous ensembles A, B ⊆ E (univers) :
1. ¬(A ∪ B) = ¬A ∩ ¬B (complément de l'union = intersection des compléments)
2. ¬(A ∩ B) = ¬A ∪ ¬B (complément de l'intersection = union des compléments)

Teste avec E = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

## Exercice 12 : Résolution de problèmes
Trois groupes d'étudiants :
- G1 = {Alice, Bob, Charlie, David} aiment les maths
- G2 = {Bob, Charlie, Eve, Frank} aiment la physique
- G3 = {Charlie, David, Eve, Grace} aiment l'informatique

Trouve :
1. Les étudiants qui aiment au moins deux matières
2. Les étudiants qui n'aiment que les maths
3. Les étudiants qui aiment exactement une matière
4. Les étudiants qui aiment toutes les matières

## Exercice 13 : Optimisation avec ensembles
Écris une fonction qui trouve :
1. Les diviseurs communs de deux nombres
2. Les nombres premiers entre 1 et n (en utilisant le crible d'Ératosthène avec des ensembles)
3. Les permutations uniques des lettres d'un mot (en utilisant des ensembles pour éliminer les doublons)

## Exercice 14 : Diagrammes de Venn
Crée une représentation textuelle de diagrammes de Venn pour trois ensembles.
Par exemple, pour A = {1, 2, 3}, B = {2, 3, 4}, C = {3, 4, 5} :
- Zone A seulement : {1}
- Zone A∩B seulement : {2}
- Zone A∩B∩C : {3}
- etc.

## Exercice 15 : Application complexe
Un système de recommandation utilise les ensembles pour représenter :
- Les films vus par chaque utilisateur
- Les genres préférés de chaque utilisateur
- Les films disponibles par genre

Écris des fonctions qui :
1. Trouvent des films à recommander (films non vus dans les genres préférés)
2. Trouvent des amis avec des goûts similaires (intersection des genres ou films)
3. Calculent la similarité entre deux utilisateurs (Jaccard index = |A∩B|/|A∪B|)

---

**Conseils méthodologiques :**
1. Visualise les ensembles comme des cercles qui peuvent s'intersecter
2. Utilise des diagrammes de Venn pour les problèmes complexes
3. Pense aux analogies avec les opérations booléennes (AND, OR, XOR, NOT)
4. Teste toujours les cas limites : ensemble vide, ensembles disjoints, ensembles égaux
5. Compare systématiquement les performances avec les listes

**Points clés à retenir :**
- Les ensembles garantissent l'unicité des éléments
- Les ensembles ne sont pas ordonnés (pas d'indexation)
- Les tests d'appartenance (`in`) sont très rapides sur les ensembles
- Les ensembles sont mutables (sauf `frozenset`)
- Les éléments doivent être hashables (typiquement immuables)

**Réflexion critique :**
- Quand utiliser une liste vs un ensemble ?
- Pourquoi les ensembles ne peuvent-ils pas contenir de listes ?
- Dans quels cas réels les opérations ensemblistes sont-elles utiles ?
- Comment l'implémentation par hachage affecte-t-elle les performances ?

Bon travail sur ces exercices ! Les ensembles sont un outil puissant souvent sous-utilisé par les débutants.