# Exercices sur la Programmation Orientée Objet

## Exercice 1 - Création de classe basique
Créez une classe `Livre` avec les attributs `titre`, `auteur` et `annee_publication`. Ajoutez une méthode `description()` qui retourne une chaîne formatée avec ces informations.

## Exercice 2 - Méthode d'initialisation
Étendez la classe `Livre` pour qu'elle accepte également `nombre_pages` et `genre` dans son constructeur. Ajoutez une méthode `est_long()` qui retourne `True` si le livre a plus de 300 pages.

## Exercice 3 - Encapsulation pratique
Créez une classe `CompteBancaire` avec:
- Un attribut privé `__solde` (utilisez le double underscore)
- Des méthodes `deposer(montant)` et `retirer(montant)`
- Une méthode `get_solde()` pour consulter le solde
- Empêchez les retraits si le solde serait négatif

## Exercice 4 - Méthodes spéciales (magiques)
Implémentez les méthodes spéciales suivantes pour la classe `Livre`:
- `__str__`: pour affichage convivial
- `__eq__`: pour comparer deux livres (même titre et auteur)
- `__repr__`: pour représentation technique

## Exercice 5 - Composition d'objets
Créez une classe `Bibliotheque` qui contient une liste de livres. Ajoutez des méthodes pour:
- Ajouter un livre
- Retirer un livre par titre
- Chercher tous les livres d'un auteur
- Compter le nombre total de pages

## Exercice 6 - Classe avec logique métier
Créez une classe `Cercle` avec:
- Un attribut `rayon`
- Des méthodes pour calculer l'aire et le périmètre
- Une méthode `contient_point(x, y)` qui vérifie si un point (x,y) est à l'intérieur du cercle centré à l'origine
- Une méthode `agrandir(facteur)` qui multiplie le rayon

## Exercice 7 - Gestion d'état
Créez une classe `Thermostat` qui:
- A une température cible et une température actuelle
- Peut être en mode "chauffage" ou "climatisation"
- A une méthode `tick()` qui simule le passage du temps et ajuste la température actuelle vers la cible
- Affiche son état (ex: "Chauffage: 20°C -> 22°C")

## Exercice 8 - Relation entre classes
Créez deux classes:
1. `Etudiant` avec nom, identifiant et liste de cours suivis
2. `Cours` avec nom, professeur et capacité maximale

Ajoutez une méthode `inscrire(etudiant)` à la classe `Cours` qui gère l'inscription, vérifie la capacité, et met à jour la liste des cours de l'étudiant.

## Exercice 9 - Validation dans le constructeur
Créez une classe `Date` qui représente une date (jour, mois, année). Validez dans le constructeur:
- Le mois entre 1 et 12
- Le jour valide pour le mois donné (ignorez les années bissextiles pour simplifier)
- L'année positive
Lancez une `ValueError` si la date est invalide.

## Exercice 10 - Système complet simple
Créez un système de gestion de commandes avec:
- `Client`: nom, adresse
- `Produit`: nom, prix, quantité en stock
- `Commande`: client, liste de produits avec quantités, date
- `Magasin`: gère les stocks, passe les commandes, calcule les totaux

Ajoutez une méthode `passer_commande(client, produits_dict)` à `Magasin` qui vérifie les stocks et crée une commande.

---

## Questions de Réflexion Critique

1. Pourquoi Python utilise-t-il `self` explicite plutôt qu'un `this` implicite comme Java/C++? Quels sont les avantages et inconvénients?

2. Quand faut-il utiliser une classe vs un simple dictionnaire ou dataclass? Quels critères utilisez-vous pour décider?

3. Pourquoi Python permet-il d'ajouter dynamiquement des attributs aux objets (`obj.nouvel_attribut = valeur`)? Est-ce une bonne pratique?

4. Quelle est la différence entre `__init__` et `__new__`? Quand utiliser l'un plutôt que l'autre?

5. Comment l'encapsulation en Python (avec `_` et `__`) diffère-t-elle de langages comme Java? Pourquoi Python est-il moins strict?

6. Que se passe-t-il en mémoire quand vous créez 1000 instances d'une classe? Comment Python gère cela?

7. Pourquoi les méthodes d'instance reçoivent-elles automatiquement `self`? Pourrait-on avoir des méthodes sans `self`?

8. Comment les classes Python gèrent-elles l'héritage multiple? Quels problèmes cela peut-il causer?

9. Quelle est la relation entre classe et type en Python? (`type(instance)`, `instance.__class__`, `type.__bases__`)

10. Quand utiliser `@classmethod` vs `@staticmethod` vs méthode d'instance? Donnez des exemples concrets.

---

## Défis Avancés (Optionnels)

1. Implémentez une classe `Vecteur` avec surcharge d'opérateurs (`+`, `-`, `*`, `==`, `len()`, `[]`).

2. Créez une classe `Singleton` qui garantit qu'une seule instance peut exister, peu importe combien de fois on tente de l'instancier.

3. Implémentez un décorateur `@property` personnalisé qui ajoute la validation quand on assigne une valeur.

4. Créez un système de plugins où différentes classes peuvent s'enregistrer pour gérer différents types de fichiers.

5. Implémentez le pattern Observateur: une classe `Observable` et plusieurs classes `Observateur` qui réagissent aux changements.

---

## Analyse de Code

Considérez ce code:
```python
class Mystere:
    def __init__(self):
        self.data = []
    
    def ajouter(self, x):
        self.data.append(x)
        return self
    
    def __add__(self, autre):
        result = Mystere()
        result.data = self.data + autre.data
        return result
```

1. Quel pattern de conception est utilisé avec la méthode `ajouter`?
2. Que fait `__add__`? Comment l'utiliser?
3. Que se passe-t-il si on fait `m1 = Mystere(); m2 = m1; m1.ajouter(5); print(m2.data)`?
4. Comment améliorer cette classe?

---

**Conseils pédagogiques:**
- Dessinez des diagrammes UML simples pour chaque exercice
- Testez les cas limites (valeurs nulles, négatives, limites)
- Comparez votre code POO avec une version procédurale équivalente
- Utilisez `pdb` ou le débogueur pour inspecter les objets en mémoire
- Écrivez des tests unitaires pour chaque classe
- Réfléchissez à la cohésion et au couplage de vos classes