## Application de la Programmation Orientée Objet

La programmation orientée objet (POO) est relativement facile à comprendre pour les débutants, mais difficile à appliquer. Bien que nous ayons résumé la méthode en trois étapes (définir la classe, créer l'objet, envoyer des messages à l'objet), il est plus facile à dire qu'à faire. **De nombreux exercices de programmation** et **la lecture de code de qualité** sont probablement les deux choses les plus utiles à ce stade. Continuons avec des cas classiques pour analyser les concepts de la POO, tout en reliant les connaissances Python acquises précédemment.

### Exemple 1 : Jeu de cartes.

> **Note** : Pour simplifier, notre jeu de cartes comporte 52 cartes (sans jokers). Le jeu doit distribuer les 52 cartes à 4 joueurs, chaque joueur recevant 13 cartes, triées par couleur (pique, cœur, trèfle, carreau) et par valeur ascendante. Les autres fonctionnalités ne sont pas implémentées pour l'instant.

En utilisant l'approche POO, nous devons d'abord identifier les objets à partir des besoins du problème et en déduire les classes correspondantes, ainsi que leurs attributs et comportements. Cela n'est pas particulièrement difficile : nous pouvons extraire les noms et verbes de la description. Les noms représentent généralement les objets ou leurs attributs, tandis que les verbes représentent leurs comportements. Dans un jeu de cartes, il devrait y avoir au moins trois types d'objets : la carte, le jeu de cartes et le joueur. Ces trois classes ne sont pas isolées. Les relations entre classes peuvent être grossièrement divisées en **relation is-a (héritage)**, **relation has-a (association)** et **relation use-a (dépendance)**. Clairement, le jeu de cartes et la carte ont une relation has-a, car un jeu de cartes a (has-a) 52 cartes. Le joueur et la carte ont à la fois une relation d'association et de dépendance, car le joueur a (has-a) des cartes et utilise (use-a) les cartes.

Les attributs d'une carte sont évidents : la couleur et la valeur. Nous pourrions utiliser les nombres de 0 à 3 pour représenter les quatre couleurs, mais cela rendrait le code peu lisible, car la correspondance entre pique, cœur, trèfle, carreau et les nombres 0 à 3 ne serait pas claire. Si une variable ne peut prendre qu'un nombre limité de valeurs, nous pouvons utiliser une énumération. Contrairement à des langages comme C ou Java, Python n'a pas de mot-clé pour déclarer un type énuméré, mais nous pouvons créer un type énuméré en héritant de la classe `Enum` du module `enum`, comme illustré ci-dessous.

```python
from enum import Enum


class Suite(Enum):
    """Couleur (énumération)"""
    SPADE, HEART, CLUB, DIAMOND = range(4)
```

Le code ci-dessus montre que définir un type énuméré revient à définir des constantes symboliques, telles que `SPADE`, `HEART`, etc. Chaque constante symbolique a une valeur associée. Ainsi, au lieu d'utiliser le nombre 0 pour représenter le pique, nous utilisons `Suite.SPADE`. De même, au lieu de 3 pour le carreau, nous utilisons `Suite.DIAMOND`. Notez que les constantes symboliques sont préférables aux constantes littérales, car leur signification est compréhensible pour quiconque lit l'anglais, améliorant ainsi la lisibilité du code. Les types énumérés en Python sont itérables, c'est-à-dire qu'ils peuvent être placés dans une boucle `for-in` pour extraire successivement chaque constante symbolique et sa valeur associée, comme montré ci-dessous.

```python
for suite in Suite:
    print(f'{suite}: {suite.value}')
```

Ensuite, nous pouvons définir la classe `Card`.

```python
class Card:
    """Carte"""

    def __init__(self, suite, face):
        self.suite = suite
        self.face = face

    def __repr__(self):
        suites = '♠♥♣♦'
        faces = ['', 'A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K']
        return f'{suites[self.suite.value]}{faces[self.face]}'  # Retourne la couleur et la valeur de la carte
```

Testons la classe `Card` avec le code suivant.

```python
card1 = Card(Suite.SPADE, 5)
card2 = Card(Suite.HEART, 13)
print(card1)  # ♠5 
print(card2)  # ♥K
```

Définissons maintenant la classe `Poker`.

```python
import random


class Poker:
    """Jeu de cartes"""

    def __init__(self):
        self.cards = [Card(suite, face) 
                      for suite in Suite
                      for face in range(1, 14)]  # Liste de 52 cartes
        self.current = 0  # Attribut pour suivre la position de distribution

    def shuffle(self):
        """Mélanger les cartes"""
        self.current = 0
        random.shuffle(self.cards)  # Utilise la fonction shuffle du module random pour un mélange aléatoire

    def deal(self):
        """Distribuer une carte"""
        card = self.cards[self.current]
        self.current += 1
        return card

    @property
    def has_next(self):
        """Vérifie s'il reste des cartes à distribuer"""
        return self.current < len(self.cards)
```

Testons la classe `Poker` avec le code suivant.

```python
poker = Poker()
print(poker.cards)  # Cartes avant mélange
poker.shuffle()
print(poker.cards)  # Cartes après mélange
```

Définissons la classe `Player`.

```python
class Player:
    """Joueur"""

    def __init__(self, name):
        self.name = name
        self.cards = []  # Cartes en main du joueur

    def get_one(self, card):
        """Prendre une carte"""
        self.cards.append(card)

    def arrange(self):
        """Trier les cartes en main"""
        self.cards.sort()
```

Créons quatre joueurs et distribuons les cartes.

```python
poker = Poker()
poker.shuffle()
players = [Player('Dong Xie'), Player('Xi Du'), Player('Nan Di'), Player('Bei Gai')]
# Distribuer les cartes à tour de rôle, 13 cartes par joueur
for _ in range(13):
    for player in players:
        player.get_one(poker.deal())
# Chaque joueur trie ses cartes et affiche son nom et sa main
for player in players:
    player.arrange()
    print(f'{player.name}: ', end='')
    print(player.cards)
```

L'exécution du code ci-dessus provoquera une exception à `player.arrange()`, car la méthode `arrange` de `Player` utilise `sort` pour trier les cartes en main. Le tri nécessite de comparer deux objets `Card`, et l'opérateur `<` ne peut pas être appliqué directement au type `Card`, d'où l'exception `TypeError` avec le message : `'<' not supported between instances of 'Card' and 'Card'`.

Pour résoudre ce problème, nous pouvons modifier légèrement la classe `Card` pour permettre la comparaison directe de deux objets `Card` avec `<`. La technique utilisée s'appelle la **surcharge d'opérateur**. En Python, pour surcharger l'opérateur `<`, nous devons ajouter une méthode magique nommée `__lt__`. Évidemment, `lt` dans `__lt__` est l'abréviation de "less than". De même, la méthode magique `__gt__` correspond à l'opérateur `>`, `__le__` à `<=`, `__ge__` à `>=`, `__eq__` à `==`, et `__ne__` à `!=`.

La classe `Card` modifiée est présentée ci-dessous.

```python
class Card:
    """Carte"""

    def __init__(self, suite, face):
        self.suite = suite
        self.face = face

    def __repr__(self):
        suites = '♠♥♣♦'
        faces = ['', 'A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K']
        return f'{suites[self.suite.value]}{faces[self.face]}'
    
    def __lt__(self, other):
        if self.suite == other.suite:
            return self.face < other.face   # Même couleur, comparer les valeurs
        return self.suite.value < other.suite.value   # Couleurs différentes, comparer les valeurs des couleurs
```

>**Note :** Vous pouvez essayer de développer un simple jeu de cartes, comme le Black Jack (21), en vous basant sur le code ci-dessus. Les règles peuvent être trouvées en ligne.

### Exemple 2 : Système de calcul de salaire.

> **Exigence :** Une entreprise a trois types d'employés : directeur de département, programmeur et vendeur. Concevoir un système de calcul de salaire qui calcule le salaire mensuel des employés en fonction des informations fournies. Le salaire mensuel du directeur de département est fixe à 15000 €. Le programmeur est payé à l'heure, à 200 € de l'heure. Le salaire du vendeur est composé d'un salaire de base de 1800 € plus une commission de 5% sur les ventes.

En analysant les besoins, nous voyons que le directeur de département, le programmeur et le vendeur sont tous des employés, partageant des attributs et des comportements communs. Nous pouvons donc d'abord concevoir une classe parent `Employee`, puis en dériver les trois sous-classes par héritage. Il est clair que nous ne créerons pas d'objets de la classe `Employee`, car nous avons besoin d'objets employés concrets. Cette classe peut donc être conçue comme une classe abstraite destinée uniquement à l'héritage. Python n'a pas de mot-clé pour définir une classe abstraite, mais nous pouvons utiliser la métaclasse `ABCMeta` du module `abc`. Le concept de métaclasse n'est pas détaillé ici, mais vous pouvez simplement suivre l'exemple.

```python
from abc import ABCMeta, abstractmethod


class Employee(metaclass=ABCMeta):
    """Employé"""

    def __init__(self, name):
        self.name = name

    @abstractmethod
    def get_salary(self):
        """Calculer le salaire mensuel"""
        pass
```

Dans la classe `Employee` ci-dessus, la méthode `get_salary` calcule le salaire mensuel, mais comme le type d'employé n'est pas encore déterminé, cette méthode ne peut être implémentée. Pour les méthodes temporairement non implémentables, nous utilisons le décorateur `abstractmethod` pour les déclarer comme méthodes abstraites. Une **méthode abstraite est une méthode déclarée mais non implémentée**, dont la déclaration force les sous-classes à la redéfinir. Le code suivant montre comment dériver les sous-classes `Manager`, `Programmer`, `Salesman` de la classe `Employee` et comment elles redéfinissent la méthode abstraite parent.

```python
class Manager(Employee):
    """Directeur de département"""

    def get_salary(self):
        return 15000.0


class Programmer(Employee):
    """Programmeur"""

    def __init__(self, name, working_hour=0):
        super().__init__(name)
        self.working_hour = working_hour

    def get_salary(self):
        return 200 * self.working_hour


class Salesman(Employee):
    """Vendeur"""

    def __init__(self, name, sales=0):
        super().__init__(name)
        self.sales = sales

    def get_salary(self):
        return 1800 + self.sales * 0.05
```

Les classes `Manager`, `Programmer` et `Salesman` héritent toutes de `Employee` et redéfinissent chacune la méthode `get_salary`. **Redéfinir signifie que la sous-classe réimplémente une méthode existante de la classe parent**. Notez que `get_salary` diffère dans chaque sous-classe, donc cette méthode manifestera un **comportement polymorphe** lors de l'exécution. Le polymorphisme signifie simplement qu'un **même appel de méthode** provoque **des actions différentes selon l'objet sous-classe**.

Complétons le système de calcul de salaire avec le code ci-dessous. Comme le programmeur et le vendeur nécessitent respectivement la saisie des heures travaillées et du chiffre d'affaires du mois, nous utilisons la fonction intégrée `isinstance` pour vérifier le type de l'objet employé. La fonction `type` mentionnée précédemment peut aussi identifier le type d'un objet, mais `isinstance` est plus puissante car elle peut déterminer si un objet est d'un type sous-classe dans une hiérarchie d'héritage. En simplifiant, `type` correspond à une correspondance exacte du type, tandis qu'`isinstance` correspond à une correspondance approximative.

```python
emps = [Manager('Liu Bei'), Programmer('Zhuge Liang'), Manager('Cao Cao'), Programmer('Xun Yu'), Salesman('Zhang Liao')]
for emp in emps:
    if isinstance(emp, Programmer):
        emp.working_hour = int(input(f'Entrez les heures travaillées ce mois par {emp.name}: '))
    elif isinstance(emp, Salesman):
        emp.sales = float(input(f'Entrez les ventes ce mois de {emp.name}: '))
    print(f'Le salaire de {emp.name} ce mois est: {emp.get_salary():.2f}€')
```

### Résumé

La pensée orientée objet est excellente et correspond au mode de pensée humain normal. Cependant, maîtriser l'abstraction, l'encapsulation, l'héritage et le polymorphisme en POO nécessite une accumulation et une maturation sur le long terme. Cela ne peut se faire du jour au lendemain, car l'acquisition des connaissances est un processus graduel.