# Exercices sur les dictionnaires (dict) en Python

## Exercice 1 : Création et manipulation basique
1. Crée un dictionnaire représentant une personne avec : nom, âge, ville, métier
2. Affiche chaque clé et sa valeur avec une boucle
3. Modifie l'âge et ajoute une nouvelle clé "langage_prefere"
4. Crée un deuxième dictionnaire avec `dict()` et une compréhension de dictionnaire

## Exercice 2 : Opérations d'accès et d'appartenance
Pour le dictionnaire : `eleve = {"nom": "Alice", "notes": [15, 18, 12], "classe": "Terminale"}`
1. Accède à la deuxième note avec deux méthodes différentes
2. Vérifie si "nom" et "absent" sont des clés valides
3. Essaie d'accéder à une clé inexistante avec `[]` puis avec `.get()`
4. Compte le nombre de paires clé-valeur

## Exercice 3 : Gestion d'inventaire
Tu gères un magasin avec ces produits :
```
inventaire = {
    "pommes": {"quantite": 50, "prix": 1.2},
    "bananes": {"quantite": 30, "prix": 0.8},
    "oranges": {"quantite": 40, "prix": 1.0}
}
```
1. Ajoute 20 pommes et retire 15 bananes
2. Ajoute un nouveau produit "kiwis" avec quantité 25 et prix 1.5
3. Calcule la valeur totale de l'inventaire (quantité × prix pour chaque produit)
4. Trouve le produit avec la plus grande quantité en stock

## Exercice 4 : Compteur de fréquences
Écris une fonction qui :
1. Prend une chaîne de caractères
2. Retourne un dictionnaire avec le compte de chaque mot
3. Ignore la casse et la ponctuation
4. Affiche les 3 mots les plus fréquents

Teste avec : "Le chat chasse la souris. Le chat est rapide, la souris est petite."

## Exercice 5 : Fusion de dictionnaires
Soit :
- `d1 = {"a": 1, "b": 2, "c": 3}`
- `d2 = {"b": 4, "d": 5, "e": 6}`
- `d3 = {"c": 7, "f": 8}`

1. Fusionne-les pour que les valeurs de d2 et d3 écrasent celles de d1
2. Crée un dictionnaire qui somme les valeurs des clés communes
3. Trouve les clés qui sont dans exactement deux dictionnaires

## Exercice 6 : Annuaire téléphonique
Crée un annuaire qui stocke :
- Nom → {"tel": "0123456789", "email": "nom@example.com"}

Écris les fonctions :
1. Ajouter/modifier un contact
2. Rechercher un contact par nom
3. Lister tous les contacts par ordre alphabétique
4. Supprimer un contact
5. Rechercher tous les contacts contenant une chaîne dans leur nom

## Exercice 7 : Conversion de structures
Écris des fonctions qui convertissent :
1. Une liste de tuples [(clé, valeur), ...] en dictionnaire
2. Un dictionnaire en deux listes : une de clés, une de valeurs
3. Un dictionnaire en une liste de tuples (clé, valeur)
4. Un dictionnaire imbriqué en dictionnaire plat
   Ex: {"a": {"b": 1, "c": 2}} → {"a.b": 1, "a.c": 2}

## Exercice 8 : Analyse de données élèves
Soit une liste d'élèves :
```
eleves = [
    {"nom": "Alice", "notes": {"maths": 15, "francais": 18, "histoire": 12}},
    {"nom": "Bob", "notes": {"maths": 10, "francais": 14, "histoire": 16}},
    {"nom": "Charlie", "notes": {"maths": 17, "francais": 13, "histoire": 19}}
]
```

Calcule :
1. La moyenne de chaque élève
2. La moyenne de la classe par matière
3. L'élève avec la meilleure moyenne
4. La variance des notes par matière

## Exercice 9 : Validation de clés
Crée un dictionnaire de configuration avec des valeurs par défaut :
```
config_defaut = {"host": "localhost", "port": 8080, "debug": False, "log_level": "INFO"}
```
1. Permets à l'utilisateur de fournir un dictionnaire de configuration partielle
2. Fusionne avec les valeurs par défaut (les valeurs utilisateur prioritaires)
3. Valide que "port" est un entier entre 1 et 65535
4. Valide que "log_level" est dans ["DEBUG", "INFO", "WARNING", "ERROR"]

## Exercice 10 : Dictionnaire inversé
Écris une fonction qui :
1. Prend un dictionnaire {clé: valeur}
2. Retourne un nouveau dictionnaire {valeur: [clés]}
3. Gère les collisions (plusieurs clés avec la même valeur)
4. Teste avec {"a": 1, "b": 2, "c": 1, "d": 3}

## Exercice 11 : Cache simple
Implémente un cache LRU (Least Recently Used) simple :
1. Dictionnaire avec taille maximum
2. Quand on ajoute un élément et que le cache est plein, supprime le moins récemment utilisé
3. Met à jour l'ordre d'utilisation à chaque accès
4. Implémente les méthodes `get(clé)` et `put(clé, valeur)`

## Exercice 12 : Arbre de décision
Crée un système de questions/réponses avec un dictionnaire imbriqué :
```
arbre = {
    "question": "Aimes-tu les animaux ?",
    "oui": {
        "question": "Préfères-tu les chiens ou les chats ?",
        "chiens": {"message": "Tu es une personne fidèle !"},
        "chats": {"message": "Tu es indépendant !"}
    },
    "non": {
        "question": "Préfères-tu les plantes ?",
        "oui": {"message": "Tu as la main verte !"},
        "non": {"message": "Tu es difficile à contenter !"}
    }
}
```
Parcours l'arbre en posant les questions et en suivant les réponses.

## Exercice 13 : Statistiques de texte avancées
Pour un texte donné, calcule :
1. Fréquence de chaque lettre (ignore les espaces et ponctuation)
2. Longueur moyenne des mots
3. Les 10 mots les plus fréquents
4. Nombre de phrases (séparées par . ! ?)
5. Densité lexicale (mots uniques / total mots)

## Exercice 14 : Gestionnaire de tâches
Crée un gestionnaire de tâches avec :
```
taches = {
    1: {"description": "Faire les courses", "priorite": 2, "termine": False},
    2: {"description": "Apprendre Python", "priorite": 1, "termine": True},
    ...
}
```

Fonctions à implémenter :
1. Ajouter/supprimer une tâche
2. Marquer une tâche comme terminée
3. Lister les tâches par priorité
4. Calculer le pourcentage de tâches terminées
5. Rechercher des tâches par mot-clé

## Exercice 15 : Simulation de base de données
Simule une petite base de données de produits avec :
- Recherche par catégorie, prix, disponibilité
- Tri par différents critères
- Agrégations : prix moyen par catégorie, stock total
- Mise à jour en temps réel des stocks

---

**Conseils pédagogiques :**
1. Toujours vérifier l'existence d'une clé avant d'y accéder avec `[]`
2. Préférer `.get()` pour les accès sécurisés
3. Utiliser `.items()` pour itérer sur clé et valeur simultanément
4. Penser aux compréhensions de dictionnaires pour des transformations élégantes
5. Visualiser les dictionnaires imbriqués comme des arbres

**Points clés à maîtriser :**
- Les clés doivent être immuables (hashables)
- L'ordre d'insertion est préservé (Python 3.7+)
- Complexité O(1) pour la recherche par clé
- Possibilité d'avoir des valeurs de n'importe quel type
- Les méthodes principales : keys(), values(), items(), get(), update()

**Réflexions critiques :**
- Quand utiliser un dictionnaire vs une liste de tuples ?
- Comment gérer les collisions de hachage (théorie) ?
- Pourquoi les dictionnaires sont-ils si rapides pour la recherche ?
- Quelles sont les limites des dictionnaires (mémoire, performance) ?
- Comment sérialiser un dictionnaire pour le stockage ?

**Applications réelles :**
- Configuration d'applications
- Caches et mémoires temporaires
- Index de recherche
- Représentation d'objets JSON
- Tables de correspondance

**Exercice bonus :** 
Crée un mini-jeu de rôle avec des personnages représentés par des dictionnaires :
- Attributs : vie, force, défense, expérience
- Inventaire : liste d'objets avec leurs propriétés
- Compétences : dictionnaire de compétences avec leurs effets
- Système de combat basé sur ces attributs

Bon travail ! Les dictionnaires sont l'une des structures les plus utiles en Python. Maîtrise-les bien, car tu les utiliseras constamment dans des projets réels.