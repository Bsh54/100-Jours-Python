# Exercices pour la compréhension des concepts Python avancés

## Exercice 1 - Compréhensions de dictionnaires et erreurs courantes
Soit le dictionnaire suivant :
```python
temperatures = {
    'Paris': 22.5,
    'Lyon': 25.8,
    'Marseille': 28.3,
    'Lille': 19.7,
    'Toulouse': 26.1,
    'Bordeaux': 24.9,
    'Nice': 27.5
}
```

1. Crée un nouveau dictionnaire contenant uniquement les villes où la température est supérieure à 25°C.
2. Quelle serait une erreur commune si tu essayais de modifier ce dictionnaire tout en l'itérant? Propose un exemple de code qui montrerait cette erreur.

## Exercice 2 - Piège des listes imbriquées
1. Explique avec tes propres mots pourquoi ce code est problématique :
```python
matrix = [[0] * 3] * 4
matrix[0][0] = 1
```

2. Dessine ou décris comment les références sont organisées en mémoire dans cet exemple.
3. Propose deux solutions correctes pour créer cette matrice.

## Exercice 3 - Utilisation de heapq
Soit une liste d'objets représentant des étudiants avec leurs notes :
```python
etudiants = [
    {'nom': 'Alice', 'note': 85, 'absences': 2},
    {'nom': 'Bob', 'note': 92, 'absences': 0},
    {'nom': 'Charlie', 'note': 78, 'absences': 3},
    {'nom': 'David', 'note': 88, 'absences': 1},
    {'nom': 'Eve', 'note': 95, 'absences': 2}
]
```

1. Trouve les 2 étudiants avec les meilleures notes.
2. Trouve les 2 étudiants avec le moins d'absences.
3. Que se passerait-il si tu essayais d'utiliser `heapq.nlargest()` directement sur la liste des dictionnaires sans spécifier de clé?

## Exercice 4 - Exploration du module itertools
1. Pour une compétition sportive avec 4 équipes (A, B, C, D), combien de matchs différents seraient possibles si chaque équipe joue contre toutes les autres exactement une fois?
2. Utilise `itertools.combinations` pour générer ces paires.
3. Si on voulait organiser un tournoi où l'ordre des matchs importe, quelle fonction d'`itertools` utiliserais-tu? Pourquoi?

## Exercice 5 - Comptage avec Counter
Analyse ce texte d'un livre pour enfants :
```python
texte = """
le petit chaperon rouge va chez sa grand-mère
elle apporte une galette et un pot de beurre
sur le chemin elle rencontre le loup
le loup a une grande bouche et de grandes dents
"""
```

1. Compte les 5 mots les plus fréquents (ignore la casse).
2. Quel problème pourrait survenir avec la ponctuation dans ce comptage?
3. Propose une méthode pour nettoyer le texte avant de compter.

## Exercice 6 - Algorithmes de tri comparés
1. Pour un tableau de 1000 éléments presque triés (seulement 10 éléments mal placés), quel algorithme de tri (sélection, bulles, fusion) serait le plus efficace? Justifie ta réponse.
2. Imaginons que tu dois trier une liste de 10 millions d'éléments en mémoire limitée. Quels facteurs considérerais-tu dans le choix de l'algorithme?
3. Donne un exemple concret où le tri par insertion serait préférable au tri rapide.

## Exercice 7 - Recherche dichotomique vs séquentielle
Tu dois chercher un mot dans un dictionnaire électronique contenant 1 million de mots.

1. En moyenne, combien de comparaisons seraient nécessaires avec une recherche séquentielle?
2. Combien avec une recherche dichotomique?
3. Quel est le prérequis pour utiliser une recherche dichotomique?
4. Donne un exemple où la recherche séquentielle pourrait être plus rapide que la recherche dichotomique.

## Exercice 8 - Analyse de complexité
Classe ces complexités du plus efficace au moins efficace pour n = 1000:
- O(1)
- O(log n)
- O(n)
- O(n log n)
- O(n²)
- O(n³)

1. Pour chaque complexité, donne un exemple d'opération qui aurait cette complexité.
2. Si un algorithme prend 1 seconde pour traiter 1000 éléments avec complexité O(n²), combien de temps prendrait-il pour 2000 éléments?

## Exercice 9 - Problème du sac à dos (glouton vs exhaustif)
Reprends le problème du sac à dos du voleur avec capacité 15kg et ces objets:

| Objet | Valeur | Poids |
|-------|--------|-------|
| A     | 60€    | 10kg  |
| B     | 100€   | 20kg  |
| C     | 120€   | 30kg  |
| D     | 40€    | 5kg   |
| E     | 50€    | 10kg  |

1. Quelle solution l'algorithme glouton (basé sur le ratio valeur/poids) proposerait-il?
2. Cette solution est-elle optimale? Pourquoi?
3. Quelle serait la complexité d'une solution par force brute?

## Exercice 10 - Gestion de la mémoire et références
Considère ce code:
```python
class Noeud:
    def __init__(self, valeur):
        self.valeur = valeur
        self.suivant = None

# Création d'une liste chaînée circulaire
a = Noeud(1)
b = Noeud(2)
c = Noeud(3)
a.suivant = b
b.suivant = c
c.suivant = a  # Référence circulaire
```

1. Que se passe-t-il quand on exécute `del a`, `del b`, `del c`?
2. Comment Python détecte-t-il et gère-t-il cette référence circulaire?
3. Quel mécanisme pourrait-on utiliser pour éviter ce problème si on voulait pouvoir supprimer des nœuds individuellement?

## Exercice 11 - Décorateurs et fermetures
1. Écris un décorateur qui limite le nombre d'appels à une fonction (par exemple, maximum 3 appels).
2. Explique pourquoi la variable de compteur doit être définie dans une portée englobante.
3. Que se passerait-il si tu utilisais `global` au lieu d'une fermeture?

## Exercice 12 - Programmation orientée objet avancée
Tu dois modéliser un système de bibliothèque avec:
- Des livres (titre, auteur, ISBN, disponible/emprunté)
- Des membres (nom, ID, livres empruntés)
- Des bibliothécaires (nom, ID)

1. Dessine le diagramme de classes avec leurs relations (héritage, association, etc.)
2. Quels design patterns pourraient être utiles? (Singleton pour la base de données? Factory pour créer des membres?)
3. Comment gérerais-tu l'emprunt multiple de livres par un membre?

## Exercice 13 - Itérateurs personnalisés
Crée un itérateur qui génère la suite de Fibonacci jusqu'à une limite donnée:
1. Implémente-le d'abord comme une classe avec `__iter__` et `__next__`.
2. Ré-implémente-le ensuite comme un générateur avec `yield`.
3. Compare les deux approches: avantages/inconvénients de chacune.

## Exercice 14 - Multithreading vs Multiprocessing
Tu dois traiter 1000 images:
- Opération: redimensionnement + application d'un filtre
- Chaque image prend ~0.1 seconde à traiter

1. Combien de temps prendrait le traitement séquentiel?
2. Si tu utilises 4 threads, quel serait le temps théorique minimum? Pourquoi ne serait-il pas atteint?
3. Si tu utilises 4 processus, quel serait l'avantage par rapport aux threads?
4. Dans quel cas choisirais-tu l'approche asynchrone?

## Exercice 15 - Test de compréhension globale
Conçois un système simple de gestion de commandes en ligne qui utilise:
- Des compréhensions pour filtrer les commandes
- Un algorithme de tri pour organiser les commandes par priorité
- Un décorateur pour logger les actions importantes
- Du multithreading pour traiter les commandes en parallèle
- Un itérateur pour parcourir l'historique des commandes

Décris brièvement comment chaque concept serait utilisé dans ce système.

---

**Conseils pédagogiques:**
- Pour chaque exercice, essaie d'abord de trouver la solution par toi-même
- Utilise Python Tutor pour visualiser l'exécution du code
- Teste différentes approches et compare leurs performances
- Documente tes réflexions et les problèmes rencontrés
- Discute tes solutions avec d'autres pour avoir des perspectives différentes