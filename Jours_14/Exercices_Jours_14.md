# Exercices sur les fonctions et modules en Python

## Exercice 1 : Définition et appel de fonctions basiques
1. Écris une fonction `carre(x)` qui retourne le carré d'un nombre
2. Écris une fonction `est_pair(n)` qui retourne `True` si n est pair, `False` sinon
3. Écris une fonction `bonjour(nom)` qui affiche "Bonjour, [nom] !"
4. Appelle ces trois fonctions avec différents arguments

## Exercice 2 : Factorielle et combinaisons
1. Écris une fonction `factorielle(n)` qui calcule n! (utilise une boucle)
2. Écris une fonction `coefficient_binomial(n, k)` qui calcule C(n,k) = n!/(k!(n-k)!)
3. Teste avec C(5,2) = 10 et C(7,3) = 35
4. Que se passe-t-il si n < k ? Corrige ta fonction pour retourner 0 dans ce cas

## Exercice 3 : Arguments avec valeurs par défaut
Écris une fonction `calculer_prix(prix_unitaire, quantite=1, tva=20.0)` qui :
1. Calcule le prix HT (prix_unitaire × quantité)
2. Calcule le prix TTC (HT × (1 + TVA/100))
3. Retourne les deux valeurs (HT, TTC)
4. Teste avec différents appels :
   - `calculer_prix(10)` → (10, 12)
   - `calculer_prix(10, 3)` → (30, 36)
   - `calculer_prix(10, tva=5.5)` → (10, 10.55)

## Exercice 4 : Arguments positionnels et nommés
Écris une fonction `format_date(jour, mois, annee, separateur='/'` qui :
1. Retourne une date formatée : "jour/mois/année" (sur deux chiffres pour jour et mois)
2. Les paramètres jour, mois, annee doivent être positionnels uniquement (utilise `/`)
3. Le paramètre separateur doit être nommé uniquement (utilise `*`)
4. Teste : `format_date(5, 12, 2023)` → "05/12/2023"
5. Teste : `format_date(5, 12, 2023, separateur='-')` → "05-12-2023"

## Exercice 5 : Arguments variables (*args et **kwargs)
1. Écris une fonction `moyenne(*nombres)` qui calcule la moyenne d'un nombre quelconque de nombres
2. Écris une fonction `decrire_personne(**infos)` qui affiche "Personne :" puis chaque clé-valeur
3. Combine les deux : `stats(nom, *notes, **details)` qui affiche le nom, la moyenne des notes, et les détails
4. Teste avec différents nombres d'arguments

## Exercice 6 : Portée des variables
Écris un programme qui illustre la différence entre :
1. Variables globales
2. Variables locales
3. Le mot-clé `global`
4. Le mot-clé `nonlocal` (pour fonctions imbriquées)

Crée des exemples qui montrent :
- Quand une variable locale masque une globale
- Comment modifier une globale depuis une fonction
- Comment une fonction imbriquée accède aux variables de la fonction parente

## Exercice 7 : Modules personnalisés
Crée trois fichiers :
1. `geometrie.py` avec des fonctions `aire_cercle(r)`, `perimetre_cercle(r)`, `aire_rectangle(L,l)`
2. `statistiques.py` avec des fonctions `moyenne(liste)`, `mediane(liste)`, `ecart_type(liste)`
3. `main.py` qui importe et utilise les fonctions des deux modules de différentes façons :
   - Import complet avec alias
   - Import spécifique de fonctions
   - Import avec renommage

## Exercice 8 : Documentation et tests
Écris une fonction `resoudre_equation_second_degre(a, b, c)` qui :
1. Résout ax² + bx + c = 0
2. Retourne :
   - 2 solutions si Δ > 0
   - 1 solution si Δ = 0
   - None si Δ < 0
3. Ajoute une docstring complète avec :
   - Description
   - Paramètres
   - Retour
   - Exemples
4. Teste avec au moins 3 cas : Δ>0, Δ=0, Δ<0

## Exercice 9 : Fonctions d'ordre supérieur
Écris des fonctions qui :
1. `appliquer_fonction(liste, fonction)` : applique une fonction à chaque élément
2. `filtrer(liste, condition)` : retourne les éléments qui satisfont une condition
3. `composer(f, g)` : retourne une nouvelle fonction h(x) = f(g(x))
4. Utilise ces fonctions avec :
   - `carre(x)` et `est_pair(x)` de l'exercice 1
   - `lambda x: x*2` (fonction anonyme)

## Exercice 10 : Gestion des erreurs
Écris une fonction `calcul_risque(montant, taux, duree)` qui :
1. Calcule les intérêts d'un placement : montant × (1 + taux)^duree
2. Gère les erreurs avec `try/except` :
   - TypeError si les arguments ne sont pas numériques
   - ValueError si taux < -1 ou duree < 0
   - Division par zero si taux = -1
3. Retourne le résultat ou un message d'erreur approprié
4. Teste avec des arguments valides et invalides

---

**Conseils pédagogiques :**
1. Nomme toujours tes fonctions avec des verbes d'action
2. Une fonction doit faire une seule chose, mais la faire bien
3. Documente toujours tes fonctions avec des docstrings
4. Teste tes fonctions avec des cas limites
5. Réfléchis à la réutilisabilité de tes fonctions

**Points clés à maîtriser :**
- Syntaxe de définition : `def nom_fonction(parametres):`
- Valeur de retour : `return` (ou implicite `None`)
- Portée des variables : locale vs globale
- Types d'arguments : positionnels, nommés, avec défaut, variables
- Importation de modules : `import`, `from ... import`, alias

**Pièges courants :**
- Modifier une liste passée en paramètre (effet de bord)
- Utiliser une valeur mutable comme défaut (ex: `def f(x=[])`)
- Confusion entre `return` et `print`
- Oublier les parenthèses dans l'appel

**Réflexions avancées :**
- Quand utiliser une fonction vs une méthode ?
- Qu'est-ce qu'une fonction pure (sans effet de bord) ?
- Comment optimiser les appels récursifs ?
- Qu'est-ce que la mémoïsation et quand l'utiliser ?

**Bonnes pratiques :**
- Une fonction ne devrait pas dépasser 20 lignes
- Utilise des type hints pour clarifier les types attendus
- Écris des tests unitaires pour tes fonctions importantes
- Pense à la lisibilité : nommage clair, logique simple

**Pour aller plus loin :**
- Fonctions génératrices (`yield`)
- Décorateurs
- Fonctions lambda
- Récursion vs itération