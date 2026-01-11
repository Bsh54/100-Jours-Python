# Exercices sur la POO Avancée

## Exercice 1 - Gestion des attributs privés
Créez une classe `CompteBancaire` avec:
- Attributs privés: `__numero_compte`, `__solde`
- Méthode publique: `deposer(montant)`, `retirer(montant)`, `afficher_solde()`
- Propriété: `solde` en lecture seule pour accéder au solde
- Essayez d'accéder à `__solde` depuis l'extérieur puis via `_CompteBancaire__solde`

## Exercice 2 - Utilisation de `__slots__`
Créez une classe `Point3D` avec `__slots__` pour limiter les attributs à `x`, `y`, `z`:
- Empêchez l'ajout dynamique d'attributs
- Implémentez une méthode `distance_a(autre_point)`
- Comparez la mémoire utilisée avec/sans `__slots__` avec `sys.getsizeof()`

## Exercice 3 - Méthodes statiques et de classe
Créez une classe `Geometrie` avec:
- Une méthode statique `distance(p1, p2)` calculant la distance entre deux points
- Une méthode de classe `creer_cercle(cls, centre, rayon)` retournant une instance de `Cercle`
- Une propriété de classe `pi = 3.1415926535`

## Exercice 4 - Propriétés avec validation
Créez une classe `Personne` avec:
- Attribut privé `__age`
- Propriété `age` avec getter, setter (valide: 0 <= age <= 150)
- Propriété `est_majeur` en lecture seule retournant True si age >= 18
- Propriété `annee_naissance` calculée à partir de l'âge actuel

## Exercice 5 - Héritage et redéfinition
Créez une hiérarchie `Animal`:
- Classe mère `Animal` avec `nom`, `age`, méthode `parler()` (générique)
- Classes filles `Chien`, `Chat`, `Oiseau` redéfinissant `parler()`
- Méthode `vieillir()` dans Animal, redéfinie dans `Chien` (vieillit 7x plus vite)

## Exercice 6 - Polymorphisme
Créez une interface `Forme` avec méthode abstraite `aire()`. Implémentez:
- `Carre(cote)`
- `Cercle(rayon)`  
- `Rectangle(largeur, hauteur)`

Puis écrivez une fonction `trier_formes(formes)` qui trie par aire décroissante.

## Exercice 7 - Héritage multiple
Créez trois classes:
- `Volant` avec méthode `voler()`
- `Nageant` avec méthode `nager()`
- `Marchant` avec méthode `marcher()`

Puis créez `Canard` qui hérite des trois et peut faire toutes les actions.

## Exercice 8 - Méta-programmation avec `__getattr__`
Créez une classe `Proxy` qui:
- Enveloppe un objet quelconque
- Redirige tous les appels d'attributs vers l'objet enveloppé
- Logge chaque accès avec `print(f"Accès à {nom_attr}")`
- Gère les attributs inexistants gracieusement

## Exercice 9 - Design Pattern Observateur
Implémentez le pattern Observateur:
- Classe `Sujet` avec `attach(observateur)`, `detach(observateur)`, `notify()`
- Classe `Observateur` avec méthode `update(sujet)`
- Classe `DonneesMeteo` (Sujet) qui notifie quand la température change

## Exercice 10 - Surcharge complète d'opérateurs
Créez une classe `Vecteur2D` avec:
- `__add__`, `__sub__`, `__mul__` (produit scalaire et multiplication par scalaire)
- `__eq__`, `__lt__` (compare la norme)
- `__len__` (retourne 2)
- `__getitem__` (accès indexé: vecteur[0] = x, vecteur[1] = y)
- `__str__`, `__repr__`

---

## Questions de Réflexion Critique

1. Pourquoi Python utilise-t-il `_NomClasse__attribut` pour les attributs privés? Quel est le mécanisme de "name mangling"?

2. Quand utiliser `__slots__`? Quels sont les avantages performances vs limitations?

3. Quelle est la différence entre `@property` et un simple getter/setter? Quand faut-il utiliser l'un ou l'autre?

4. Comment le polymorphisme en Python diffère-t-il des langages à typage statique comme Java?

5. Quels problèmes peuvent survenir avec l'héritage multiple? Comment Python les résout-il avec le MRO?

6. Pourquoi `super()` est-elle importante avec l'héritage multiple? Que se passe-t-il sans elle?

7. Comment `__getattr__` et `__getattribute__` diffèrent-ils? Quand utiliser chacun?

8. Quels sont les risques des attributs dynamiques? Comment les éviter en production?

9. Comment tester proprement les classes avec attributs privés? Faut-il tester les attributs privés?

10. Quelle est la philosophie Pythonique "We are all consenting adults"? Comment cela influence-t-il la conception?

---

## Défis Avancés (Optionnels)

1. Implémentez un ORM simple avec gestion automatique des propriétés basée sur les types.

2. Créez un système de plugins avec classes enregistrées dynamiquement via décorateurs.

3. Implémentez le pattern Composite avec `__add__` pour combiner des formes.

4. Créez une classe `LazyProxy` qui ne charge ses données que lors du premier accès.

5. Implémentez une méta-classe qui ajoute automatiquement des méthodes de sérialisation.

---

## Analyse de Code

```python
class A:
    def __init__(self):
        self.public = "public"
        self._protected = "protected"
        self.__private = "private"
    
    def show(self):
        print(self.public, self._protected, self.__private)

class B(A):
    def __init__(self):
        super().__init__()
        self.__private = "B's private"  # Différent de A.__private
    
    def show_b(self):
        print(self.public, self._protected, self.__private)

a = A()
b = B()
print("A:", a.public, a._protected, a._A__private)
print("B:", b.public, b._protected, b._B__private, b._A__private)
a.show()
b.show()
b.show_b()
```

Questions:
1. Combien d'attributs privés différents existent? Quels sont leurs noms réels?
2. Pourquoi `b.show()` affiche-t-il la valeur privée de A?
3. Comment éviter la confusion avec les attributs privés dans l'héritage?
4. Que se passe-t-il si on essaie `print(b.__private)`?

---

## Projet Final

Créez un système de gestion de bibliothèque avec:
- `Livre`: ISBN, titre, auteur, année, statut (disponible/emprunté)
- `Membre`: ID, nom, liste des livres empruntés, limite d'emprunt
- `Bibliothecaire`: peut ajouter/supprimer des livres, enregistrer des membres
- `Bibliotheque`: singleton gérant tous les livres et membres
- `SystemeEmprunt`: gère les emprunts/retours avec validation

Contraintes:
- Utilisez propriétés avec validation
- Héritage approprié
- Méthodes statiques/de classe là où pertinent
- Gestion d'erreurs avec exceptions personnalisées
- Polymorphisme pour différents types de documents (livre, magazine, DVD)

---

**Conseils pédagogiques:**
- Utilisez `dir()` pour explorer les attributs réels des objets
- Dessinez les diagrammes de classe UML
- Testez chaque exercice avec des cas limites
- Comparez avec des implémentations procédurales équivalentes
- Utilisez le module `inspect` pour explorer les classes
- Pratiquez le refactoring pour améliorer la conception
- Écrivez des tests unitaires avant le code (TDD)
- Documentez avec des docstrings et type hints