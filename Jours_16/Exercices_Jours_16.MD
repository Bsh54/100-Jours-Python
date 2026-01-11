# Exercices sur l'utilisation avancée des fonctions

## Exercice 1 : Fonctions d'ordre supérieur personnalisées
1. Écris une fonction `appliquer_a_tous(fonction, liste)` qui applique `fonction` à chaque élément
2. Écris une fonction `filtrer_selon(condition, liste)` qui filtre selon `condition`
3. Écris une fonction `reduire_par(fonction, liste, initial)` qui réduit la liste
4. Teste avec des lambdas pour :
   - Doubler tous les éléments
   - Garder les nombres > 5
   - Faire le produit de tous les éléments

## Exercice 2 : Composition de fonctions
1. Écris une fonction `composer(f, g)` qui retourne h(x) = f(g(x))
2. Écris une fonction `composer_plusieurs(*fonctions)` qui compose n fonctions
3. Écris une fonction `appliquer_en_chaîne(x, *fonctions)` qui applique f1(f2(...fn(x)))
4. Teste avec :
   - f(x) = x+1, g(x) = x*2 → h(3) = (3*2)+1 = 7
   - Chaîne : carré, +5, racine → √(x² + 5)

## Exercice 3 : Fabrique de fonctions
1. Écris une fonction `creer_multiplicateur(n)` qui retourne une fonction multipliant par n
2. Écris une fonction `creer_comparateur(sens)` qui retourne une fonction max ou min
3. Écris une fonction `creer_formateur(format_str)` qui retourne une fonction formatant selon le format
4. Utilise ces fabriques pour créer et utiliser plusieurs fonctions spécialisées

## Exercice 4 : Fonctions avec état (closures)
1. Écris une fonction `compteur()` qui retourne une fonction incrémentant un compteur interne
2. Écris une fonction `memoire_valeurs()` qui retourne une fonction stockant les valeurs déjà calculées
3. Écris une fonction `make_adder(x)` qui retourne une fonction ajoutant x à son argument
4. Teste que chaque closure maintient son état propre

## Exercice 5 : Currying et application partielle
1. Écris une fonction `curry(fonction)` qui transforme f(a,b,c) en f(a)(b)(c)
2. Écris une fonction `appliquer_partiellement(fonction, *args_fixes)` qui fixe certains arguments
3. Compare avec `functools.partial`
4. Utilise pour créer des fonctions spécialisées à partir de fonctions générales

## Exercice 6 : Map-Reduce personnalisé
1. Implémente ton propre `map_reduce(data, mapper, reducer)` 
2. `mapper` transforme chaque élément en paire (clé, valeur)
3. `reducer` agrège les valeurs par clé
4. Teste pour compter les mots d'un texte :
   - mapper : (mot, 1) pour chaque mot
   - reducer : somme des 1 par mot

## Exercice 7 : Trieurs génériques
1. Écris une fonction `trier_par(liste, cle)` où `cle` est une fonction retournant une valeur de tri
2. Écris une fonction `trier_surplusieurs_criteres(liste, *cles)` qui trie par plusieurs clés
3. Écris une fonction `trier_selon_priorite(liste, priorites)` où priorites est un dict {valeur: rang}
4. Teste avec des listes d'objets complexes (tuples, dicts)

## Exercice 8 : Pipeline de traitement
1. Écris une fonction `pipeline(*etapes)` qui retourne une fonction appliquant toutes les étapes
2. Chaque étape est une fonction prenant un argument et retournant une valeur
3. Écris des étapes génériques : `filtrer(condition)`, `transformer(fonction)`, `valider(condition)`
4. Crée un pipeline pour nettoyer une liste de nombres : enlever None, convertir en int, garder >0

## Exercice 9 : Décorateurs simples
1. Écris un décorateur `chronometrer` qui mesure et affiche le temps d'exécution
2. Écris un décorateur `memoriser` qui cache les résultats (memoization)
3. Écris un décorateur `valider_arguments(*validations)` qui valide les types des arguments
4. Écris un décorateur `logger` qui loggue les appels et retours

## Exercice 10 : Système d'événements
1. Écris une fonction `creer_gestionnaire_evenements()` qui retourne un objet avec :
   - `on(nom, handler)` pour enregistrer un handler
   - `emit(nom, *args)` pour déclencher un événement
   - `off(nom, handler)` pour retirer un handler
2. Teste avec des événements comme "click", "data", "error"
3. Ajoute la possibilité de handlers asynchrones

---

**Conseils pédagogiques :**
1. Commence par écrire les versions non-génériques, puis généralise
2. Utilise des exemples concrets pour comprendre chaque concept
3. Teste avec des fonctions simples avant de passer aux complexes
4. Visualise le flux de données (entrée → transformation → sortie)

**Concepts clés à maîtriser :**
- First-class functions : fonctions comme valeurs
- Higher-order functions : fonctions qui manipulent des fonctions
- Closures : fonctions avec état capturé
- Currying : transformation f(a,b) → f(a)(b)
- Composition : combinaison de fonctions

**Applications pratiques :**
- Callbacks dans les interfaces graphiques
- Middleware dans les frameworks web
- Strategies dans les design patterns
- Transformations de données en ETL

**Pièges courants :**
- Variables capturées par les closures (effet de lié tardif)
- État mutable dans les closures
- Performance des lambdas complexes
- Lisibilité excessive des fonctions imbriquées

**Exercices de réflexion :**
1. Quelle est la différence entre `partial` et une closure ?
2. Quand utiliser une lambda vs une fonction nommée ?
3. Comment déboguer une chaîne de fonctions composées ?
4. Quelles sont les limites des fonctions d'ordre supérieur ?

**Projet d'intégration :**
Crée un mini-framework de traitement de données avec :
1. Des fonctions de transformation génériques
2. Un système de pipeline configurable
3. Des décorateurs pour logging et validation
4. Un système de plugins par fonctions

**Évaluation :**
Pour chaque exercice, vérifie :
- La fonction est-elle réutilisable ?
- La signature est-elle claire ?
- Gère-t-elle les cas d'erreur ?
- Les performances sont-elles acceptables ?

**Astuces :**
- Utilise `functools.wraps` pour préserver les métadonnées des fonctions décorées
- Les lambdas ne peuvent contenir que des expressions, pas des statements
- `partial` peut fixer des arguments positionnels ou nommés
- Les closures capturent les variables par référence, pas par valeur

**Pour aller plus loin :**
- Foncteurs et monades (concepts fonctionnels avancés)
- Programmation fonctionnelle réactive
- Évaluation paresseuse avec générateurs
- Méta-programmation avec des fonctions