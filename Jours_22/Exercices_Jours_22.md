# Exercices sur la sérialisation JSON et les API réseaux

## Exercice 1 - Compréhension des concepts
Explique avec tes propres mots :
1. Quelle est la différence entre JSON et XML comme formats d'échange de données ?
2. Quels sont les avantages de JSON par rapport à un format binaire personnalisé ?
3. Qu'est-ce que la sérialisation et la désérialisation, et pourquoi sont-elles importantes ?
4. Comment JSON représente-t-il les structures de données complexes (listes imbriquées, dictionnaires dans des dictionnaires) ?

## Exercice 2 - Correspondance des types de données
Pour chaque paire ci-dessous, indique si elle peut être convertie directement par `json.dumps()` sans erreur, et si non, explique pourquoi :

1. `{"nom": "Alice", "âge": 25}` → ?
2. `{"date": datetime.datetime.now()}` → ?
3. `{1: "un", 2: "deux"}` → ?
4. `[True, False, None]` → ?
5. `{("x", "y"): (1, 2)}` → ?
6. `{frozenset([1, 2]): "ensemble"}` → ?

## Exercice 3 - Lecture/écriture JSON
Écris un programme qui :
1. Crée un dictionnaire représentant un livre avec :
   - Titre
   - Auteur
   - Année de publication
   - Liste de chapitres (chaque chapitre est un dict avec titre et nombre de pages)
   - Prix
2. Écrit ce dictionnaire dans un fichier `livre.json`
3. Relit le fichier et calcule :
   - Le nombre total de pages
   - Le prix moyen par page

## Exercice 4 - Manipulation de JSON
Écris une fonction `filtrer_donnees(json_file, critere)` qui :
1. Charge un fichier JSON contenant une liste d'objets
2. Filtre les objets selon un critère donné (ex: âge > 18, ville = "Paris")
3. Sauvegarde le résultat filtré dans un nouveau fichier JSON
4. Gère les erreurs (fichier inexistant, JSON mal formé, clés manquantes)

## Exercice 5 - Comparaison de bibliothèques
Recherche et compare 3 bibliothèques JSON pour Python (`json`, `ujson`, `orjson`, `simplejson`). Pour chaque bibliothèque :
1. Avantages principaux
2. Inconvénients
3. Cas d'utilisation recommandés
4. Compatibilité avec les types Python

## Exercice 6 - API REST simple
Imagine que tu dois créer une API REST pour une bibliothèque. Définis :
1. 3 endpoints minimum avec leur méthode HTTP et leur fonction
2. Le schéma JSON pour un livre
3. Les réponses possibles (succès, erreurs) avec leurs codes HTTP
4. Comment gérer les opérations CRUD (Create, Read, Update, Delete)

## Exercice 7 - Consommation d'API
Écris un programme qui utilise l'API OpenWeatherMap (ou une API publique similaire) pour :
1. Demander une ville à l'utilisateur
2. Faire une requête à l'API pour obtenir la météo
3. Afficher les informations de manière lisible
4. Sauvegarder les données dans un fichier JSON avec timestamp
5. Gérer les erreurs (ville inexistante, problèmes réseau, quota dépassé)

## Exercice 8 - Transformation de données
Tu reçois des données au format CSV et tu dois les convertir en JSON. Écris un programme qui :
1. Lit un fichier CSV avec colonnes : nom, email, département, salaire
2. Convertit en structure JSON organisée par département
3. Calcule des statistiques par département (moyenne des salaires, nombre d'employés)
4. Produit deux fichiers : `employes_par_departement.json` et `statistiques.json`

## Exercice 9 - Gestion de cache
Pour éviter de faire trop d'appels API, implémente un système de cache :
1. Avant de faire un appel API, vérifie si les données sont dans un fichier cache
2. Le cache expire après 1 heure
3. Structure du cache : fichier JSON avec timestamp et données
4. Gère plusieurs endpoints différents dans le même cache

## Exercice 10 - Projet complet : Gestionnaire de recettes
Conçois un système de gestion de recettes de cuisine avec :
1. **Structure de données** : Définis le schéma JSON pour une recette
2. **CRUD** : Fonctions pour ajouter, lire, modifier, supprimer des recettes
3. **Recherche** : Recherche par ingrédients, temps de préparation, difficulté
4. **Import/Export** : Export en JSON et import depuis d'autres formats
5. **API** : Interface simple pour interagir avec le système

**Questions de réflexion :**
- Comment valider le schéma JSON des recettes ?
- Comment gérer les versions du schéma si tu veux ajouter de nouveaux champs ?
- Comment optimiser la recherche dans une grande collection de recettes ?
- Quelles mesures de sécurité mettre en place si l'API est exposée sur internet ?

---

**Conseils pédagogiques :**
- Expérimente avec différentes APIs publiques (elles ont souvent des limites de requêtes gratuites)
- Compare JSON avec d'autres formats comme YAML, TOML, ou XML
- Réfléchis à la validation des données JSON (avec `jsonschema` par exemple)
- Considère la performance : quand utiliser `json.loads()` vs `json.load()` ?