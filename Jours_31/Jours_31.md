## Python Avancé

### Concepts Clés

- **Compréhensions (List/Dict/Set Comprehensions)**

  ```Python
  prices = {
      'AAPL': 191.88,
      'GOOG': 1186.96,
      'IBM': 149.24,
      'ORCL': 48.44,
      'ACN': 166.89,
      'FB': 208.09,
      'SYMC': 21.29
  }
  # Créer un nouveau dictionnaire avec les actions dont le prix > 100
  prices2 = {key: value for key, value in prices.items() if value > 100}
  print(prices2)
  ```

  > **Note :** Les compréhensions peuvent être utilisées pour générer des listes, des ensembles et des dictionnaires.

- **Piège des listes imbriquées**

  ```Python
  names = ['Guan Yu', 'Zhang Fei', 'Zhao Yun', 'Ma Chao', 'Huang Zhong']
  courses = ['Chinois', 'Mathématiques', 'Anglais']
  # Saisir les notes de 5 étudiants dans 3 matières
  # ERREUR - Voir http://pythontutor.com/visualize.html#mode=edit
  # scores = [[None] * len(courses)] * len(names)
  scores = [[None] * len(courses) for _ in range(len(names))]
  for row, name in enumerate(names):
      for col, course in enumerate(courses):
          scores[row][col] = float(input(f'Veuillez saisir la note de {name} en {course}: '))
          print(scores)
  ```

  [Python Tutor](http://pythontutor.com/) - VISUALISEZ LE CODE ET OBTENEZ DE L'AIDE EN DIRECT

- **Module `heapq` (Tri par tas)**

  ```Python
  """
  Trouver les N plus grands ou plus petits éléments d'une liste
  Structure de tas (tas max / tas min)
  """
  import heapq
  
  list1 = [34, 25, 12, 99, 87, 63, 58, 78, 88, 92]
  list2 = [
      {'name': 'IBM', 'shares': 100, 'price': 91.1},
      {'name': 'AAPL', 'shares': 50, 'price': 543.22},
      {'name': 'FB', 'shares': 200, 'price': 21.09},
      {'name': 'HPQ', 'shares': 35, 'price': 31.75},
      {'name': 'YHOO', 'shares': 45, 'price': 16.35},
      {'name': 'ACME', 'shares': 75, 'price': 115.65}
  ]
  print(heapq.nlargest(3, list1))
  print(heapq.nsmallest(3, list1))
  print(heapq.nlargest(2, list2, key=lambda x: x['price']))
  print(heapq.nlargest(2, list2, key=lambda x: x['shares']))
  ```

- **Module `itertools`**

  ```Python
  """
  Module d'outils d'itération
  """
  import itertools
  
  # Générer toutes les permutations de 'ABCD'
  itertools.permutations('ABCD')
  # Générer toutes les combinaisons de 3 éléments parmi 'ABCDE'
  itertools.combinations('ABCDE', 3)
  # Produit cartésien de 'ABCD' et '123'
  itertools.product('ABCD', '123')
  # Séquence infinie cyclique de ('A', 'B', 'C')
  itertools.cycle(('A', 'B', 'C'))
  ```

- **Module `collections`**

  Classes utilitaires courantes :

  - `namedtuple` : Tuple nommé. C'est une usine à classes qui prend un nom de type et une liste d'attributs pour créer une classe.
  - `deque` : File doublement chaînée (double-ended queue), une alternative aux listes. Les listes Python sont implémentées sur des tableaux, tandis que `deque` est une liste chaînée double. Ainsi, pour ajouter/supprimer des éléments en tête ou en queue, `deque` offre de meilleures performances avec une complexité asymptotique O(1).
  - `Counter` : Sous-classe de `dict`. Les clés sont les éléments, les valeurs sont leurs nombres d'occurrences. Sa méthode `most_common()` aide à obtenir les éléments les plus fréquents.
  - `OrderedDict` : Sous-classe de `dict`. Il conserve l'ordre d'insertion des paires clé-valeur, combinant le comportement d'un dictionnaire et d'une liste.
  - `defaultdict` : Similaire à un dictionnaire, mais permet d'obtenir une valeur par défaut pour une clé via une usine (callable). C'est plus efficace que la méthode `setdefault()` des dictionnaires standards.

  ```Python
  """
  Trouver l'élément le plus fréquent dans une séquence
  """
  from collections import Counter
  
  words = [
      'look', 'into', 'my', 'eyes', 'look', 'into', 'my', 'eyes',
      'the', 'eyes', 'the', 'eyes', 'the', 'eyes', 'not', 'around',
      'the', 'eyes', "don't", 'look', 'around', 'the', 'eyes',
      'look', 'into', 'my', 'eyes', "you're", 'under'
  ]
  counter = Counter(words)
  print(counter.most_common(3))
  ```

### Structures de données et algorithmes

- **Algorithme** : Méthode et étapes pour résoudre un problème.
- **Évaluer la qualité d'un algorithme** : Complexité temporelle asymptotique et complexité spatiale asymptotique.
- **Notation Grand O pour la complexité temporelle asymptotique** :
  - O(c) - Complexité constante - Filtre de Bloom / Stockage par hachage
  - O(log₂n) - Complexité logarithmique - Recherche dichotomique (binary search)
  - O(n) - Complexité linéaire - Recherche séquentielle / Tri par comptage
  - O(n*log₂n) - Complexité quasi-linéaire - Algorithmes de tri avancés (tri fusion, tri rapide)
  - O(n²) - Complexité quadratique - Algorithmes de tri simples (tri par sélection, tri par insertion, tri à bulles)
  - O(n³) - Complexité cubique - Algorithme de Floyd / Multiplication de matrices
  - O(2ⁿ) - Complexité exponentielle (géométrique) - Tours de Hanoï
  - O(n!) - Complexité factorielle - Problème du voyageur de commerce (NPC)

- **Algorithmes de tri (sélection, bulles, fusion) et de recherche (séquentielle, dichotomique)**

  ```Python
  def select_sort(items, comp=lambda x, y: x < y):
      """Tri par sélection simple"""
      items = items[:]
      for i in range(len(items) - 1):
          min_index = i
          for j in range(i + 1, len(items)):
              if comp(items[j], items[min_index]):
                  min_index = j
          items[i], items[min_index] = items[min_index], items[i]
      return items
  ```

  ```Python
  def bubble_sort(items, comp=lambda x, y: x > y):
      """Tri à bulles"""
      items = items[:]
      for i in range(len(items) - 1):
          swapped = False
          for j in range(len(items) - 1 - i):
              if comp(items[j], items[j + 1]):
                  items[j], items[j + 1] = items[j + 1], items[j]
                  swapped = True
          if not swapped:
              break
      return items
  ```

  ```Python
  def bubble_sort(items, comp=lambda x, y: x > y):
      """Tri à bulles amélioré (cocktail shaker sort)"""
      items = items[:]
      for i in range(len(items) - 1):
          swapped = False
          for j in range(len(items) - 1 - i):
              if comp(items[j], items[j + 1]):
                  items[j], items[j + 1] = items[j + 1], items[j]
                  swapped = True
          if swapped:
              swapped = False
              for j in range(len(items) - 2 - i, i, -1):
                  if comp(items[j - 1], items[j]):
                      items[j], items[j - 1] = items[j - 1], items[j]
                      swapped = True
          if not swapped:
              break
      return items
  ```

  ```Python
  def merge(items1, items2, comp=lambda x, y: x < y):
      """Fusion (combiner deux listes triées en une liste triée)"""
      items = []
      index1, index2 = 0, 0
      while index1 < len(items1) and index2 < len(items2):
          if comp(items1[index1], items2[index2]):
              items.append(items1[index1])
              index1 += 1
          else:
              items.append(items2[index2])
              index2 += 1
      items += items1[index1:]
      items += items2[index2:]
      return items
  
  def merge_sort(items, comp=lambda x, y: x < y):
      return _merge_sort(list(items), comp)
  
  def _merge_sort(items, comp):
      """Tri fusion"""
      if len(items) < 2:
          return items
      mid = len(items) // 2
      left = _merge_sort(items[:mid], comp)
      right = _merge_sort(items[mid:], comp)
      return merge(left, right, comp)
  ```

  ```Python
  def seq_search(items, key):
      """Recherche séquentielle"""
      for index, item in enumerate(items):
          if item == key:
              return index
      return -1
  ```

  ```Python
  def bin_search(items, key):
      """Recherche dichotomique"""
      start, end = 0, len(items) - 1
      while start <= end:
          mid = (start + end) // 2
          if key > items[mid]:
              start = mid + 1
          elif key < items[mid]:
              end = mid - 1
          else:
              return mid
      return -1
  ```

- **Algorithmes courants** :

  - **Force brute (Exhaustive Search)** : Énumère toutes les possibilités jusqu'à trouver la solution.
  - **Algorithme glouton (Greedy)** : À chaque étape, fait le choix localement optimal, sans viser nécessairement la solution optimale globale, pour trouver rapidement une solution satisfaisante.
  - **Diviser pour régner (Divide and Conquer)** : Divise un problème complexe en sous-problèmes similaires plus petits, jusqu'à ce qu'ils soient directement solubles, puis combine leurs solutions.
  - **Retour sur trace (Backtracking)** : Explore systématiquement les possibilités. Si une voie mène à une impasse ou n'est pas optimale, on revient en arrière (backtrack) pour essayer une autre possibilité.
  - **Programmation dynamique (Dynamic Programming)** : Résout des sous-problèmes, stocke leurs solutions pour éviter les recalculs, et combine ces solutions pour résoudre le problème initial.

  **Exemple de force brute :** Problème des cent poulets et cent pièces ; Problème des cinq pêcheurs et des poissons.

  ```Python
  # Un coq coûte 5 pièces, une poule 3 pièces, trois poussins 1 pièce.
  # Acheter 100 volailles avec 100 pièces. Combien de coqs, poules, poussins ?
  for x in range(20):
      for y in range(33):
          z = 100 - x - y
          if 5 * x + 3 * y + z // 3 == 100 and z % 3 == 0:
              print(x, y, z)
  
  # Cinq pêcheurs A, B, C, D, E attrapent des poissons de nuit et s'endorment.
  # A se réveille le premier, divise les poissons en 5 parts égales, jette le surplus de 1, prend sa part.
  # B se réveille ensuite, fait de même (divise le reste en 5, jette 1, prend sa part).
  # C, D, E font de même successivement. Quel est le nombre minimal de poissons ?
  fish = 6
  while True:
      total = fish
      enough = True
      for _ in range(5):
          if (total - 1) % 5 == 0:
              total = (total - 1) // 5 * 4
          else:
              enough = False
              break
      if enough:
          print(fish)
          break
      fish += 5
  ```

  **Exemple d'algorithme glouton :** Supposons qu'un voleur ait un sac à dos d'une capacité de 20 kg. Il entre dans une maison et trouve les objets suivants. Il ne peut pas tout prendre. Il doit décider quoi prendre pour maximiser la valeur.

  |   Nom   | Prix ($) | Poids (kg) |
  | :-----: | :------: | :--------: |
  |  Ordinateur  |    200    |     20     |
  | Radio |     20    |     4      |
  | Horloge |    175    |     10     |
  |  Vase   |     50    |     2      |
  |  Livre  |     10    |     1      |
  | Peinture |     90    |     9      |

  ```Python
  """
  Algorithme glouton : À chaque étape, choisit l'option localement optimale.
  Entrée :
  20 6
  Ordinateur 200 20
  Radio 20 4
  Horloge 175 10
  Vase 50 2
  Livre 10 1
  Peinture 90 9
  """
  class Thing(object):
      """Objet"""
  
      def __init__(self, name, price, weight):
          self.name = name
          self.price = price
          self.weight = weight
  
      @property
      def value(self):
          """Ratio valeur/poids"""
          return self.price / self.weight
  
  def input_thing():
      """Saisir les informations d'un objet"""
      name_str, price_str, weight_str = input().split()
      return name_str, int(price_str), int(weight_str)
  
  def main():
      """Fonction principale"""
      max_weight, num_of_things = map(int, input().split())
      all_things = []
      for _ in range(num_of_things):
          all_things.append(Thing(*input_thing()))
      all_things.sort(key=lambda x: x.value, reverse=True)
      total_weight = 0
      total_price = 0
      for thing in all_things:
          if total_weight + thing.weight <= max_weight:
              print(f'Le voleur prend {thing.name}')
              total_weight += thing.weight
              total_price += thing.price
      print(f'Valeur totale : {total_price}$')
  
  if __name__ == '__main__':
      main()
  ```

  **Exemple de diviser pour régner :** [Tri rapide (QuickSort)](https://fr.wikipedia.org/wiki/Tri_rapide).

  ```Python
  """
  Tri rapide - Choisir un pivot, partitionner les éléments (plus petits à gauche, plus grands à droite)
  """
  def quick_sort(items, comp=lambda x, y: x <= y):
      items = list(items)[:]
      _quick_sort(items, 0, len(items) - 1, comp)
      return items
  
  def _quick_sort(items, start, end, comp):
      if start < end:
          pos = _partition(items, start, end, comp)
          _quick_sort(items, start, pos - 1, comp)
          _quick_sort(items, pos + 1, end, comp)
  
  def _partition(items, start, end, comp):
      pivot = items[end]
      i = start - 1
      for j in range(start, end):
          if comp(items[j], pivot):
              i += 1
              items[i], items[j] = items[j], items[i]
      items[i + 1], items[end] = items[end], items[i + 1]
      return i + 1
  ```

  **Exemple de retour sur trace :** [Problème du cavalier (Knight's Tour)](https://fr.wikipedia.org/wiki/Probl%C3%A8me_du_cavalier).

  ```Python
  """
  Retour sur trace récursif : Explore les possibilités. Si une voie échoue, revient en arrière.
  Problèmes classiques : Tour du cavalier, Huit dames, Chercher un chemin dans un labyrinthe.
  """
  import sys
  import time
  
  SIZE = 5
  total = 0
  
  def print_board(board):
      for row in board:
          for col in row:
              print(str(col).center(4), end='')
          print()
  
  def patrol(board, row, col, step=1):
      if row >= 0 and row < SIZE and \
          col >= 0 and col < SIZE and \
          board[row][col] == 0:
          board[row][col] = step
          if step == SIZE * SIZE:
              global total
              total += 1
              print(f'Solution {total}: ')
              print_board(board)
          patrol(board, row - 2, col - 1, step + 1)
          patrol(board, row - 1, col - 2, step + 1)
          patrol(board, row + 1, col - 2, step + 1)
          patrol(board, row + 2, col - 1, step + 1)
          patrol(board, row + 2, col + 1, step + 1)
          patrol(board, row + 1, col + 2, step + 1)
          patrol(board, row - 1, col + 2, step + 1)
          patrol(board, row - 2, col + 1, step + 1)
          board[row][col] = 0
  
  def main():
      board = [[0] * SIZE for _ in range(SIZE)]
      patrol(board, SIZE - 1, SIZE - 1)
  
  if __name__ == '__main__':
      main()
  ```

  **Exemple de programmation dynamique :** Somme maximale d'une sous-liste contiguë.

  > **Note :** Une sous-liste est définie par des indices consécutifs. Les éléments sont des entiers (positifs, négatifs ou nuls). Le programme prend une liste en entrée et affiche la somme maximale d'une sous-liste contiguë.
  > Exemples :
  > Entrée : 1 -2 3 5 -3 2
  > Sortie : 8
  > Entrée : 0 -2 3 5 -1 2
  > Sortie : 9
  > Entrée : -9 -2 -3 -5 -3
  > Sortie : -2

  ```Python
  def main():
      items = list(map(int, input().split()))
      overall = partial = items[0]
      for i in range(1, len(items)):
          partial = max(items[i], partial + items[i])
          overall = max(partial, overall)
      print(overall)
  
  if __name__ == '__main__':
      main()
  ```

  > **Note :** Une approche naïve avec deux boucles imbriquées aurait une complexité de O(N²). L'approche par programmation dynamique ci-dessus, utilisant seulement deux variables supplémentaires, réduit la complexité à O(N).

### Utilisation des fonctions

- **Traiter les fonctions comme des "citoyens de première classe"**
  - Une fonction peut être assignée à une variable.
  - Une fonction peut être passée en argument à une autre fonction.
  - Une fonction peut être renvoyée par une autre fonction.

- **Utilisation des fonctions d'ordre supérieur (`filter`, `map` et leurs alternatives)**

  ```Python
  items1 = list(map(lambda x: x ** 2, filter(lambda x: x % 2, range(1, 10))))
  items2 = [x ** 2 for x in range(1, 10) if x % 2]
  ```

- **Paramètres positionnels, paramètres variables (`*args`), paramètres nommés (`**kwargs`), paramètres nommés obligatoires (keyword-only arguments)**

- **Métadonnées des paramètres (lisibilité du code)**

- **Fonctions anonymes et fonctions en ligne (`lambda`)**

- **Fermetures (closures) et portée des variables (scope)**
  - Ordre de recherche des variables LEGB (Local > Enclosing > Global > Built-in)
  - Mots-clés `global` et `nonlocal`
    - `global` : Déclare ou utilise une variable globale.
    - `nonlocal` : Déclare l'utilisation d'une variable d'une portée englobante (doit exister).

- **Fonctions décoratrices (appliquer et annuler un décorateur)**

  Exemple : Décorateur pour mesurer le temps d'exécution.

  ```Python
  from time import time
  from functools import wraps
  
  def record_time(func):
      """Décorateur personnalisé pour enregistrer le temps"""
      
      @wraps(func)
      def wrapper(*args, **kwargs):
          start = time()
          result = func(*args, **kwargs)
          print(f'{func.__name__}: {time() - start} secondes')
          return result
          
      return wrapper
  ```

  Pour un décorateur paramétrable (non couplé à `print`) :

  ```Python
  from functools import wraps
  from time import time
  
  def record(output):
      """Décorateur paramétrable"""
      
      def decorate(func):
          
          @wraps(func)
          def wrapper(*args, **kwargs):
              start = time()
              result = func(*args, **kwargs)
              output(func.__name__, time() - start)
              return result
              
          return wrapper
      
      return decorate
  ```

  ```Python
  from functools import wraps
  from time import time
  
  class Record():
      """Définir un décorateur via une classe"""
  
      def __init__(self, output):
          self.output = output
  
      def __call__(self, func):
  
          @wraps(func)
          def wrapper(*args, **kwargs):
              start = time()
              result = func(*args, **kwargs)
              self.output(func.__name__, time() - start)
              return result
  
          return wrapper
  ```

  > **Note :** Grâce au décorateur `@wraps`, on peut accéder à la fonction originale via `func.__wrapped__` pour "annuler" le décorateur.

  Exemple : Implémenter le pattern Singleton avec un décorateur.

  ```Python
  from functools import wraps
  
  def singleton(cls):
      """Décorateur de classe (Singleton)"""
      instances = {}
  
      @wraps(cls)
      def wrapper(*args, **kwargs):
          if cls not in instances:
              instances[cls] = cls(*args, **kwargs)
          return instances[cls]
  
      return wrapper
  
  @singleton
  class President:
      """Président (classe Singleton)"""
      pass
  ```

  > **Note :** Le code ci-dessus utilise une fermeture. Il n'est pas *thread-safe*. Pour une version *thread-safe* :

  ```Python
  from functools import wraps
  from threading import RLock
  
  def singleton(cls):
      """Décorateur Singleton thread-safe"""
      instances = {}
      locker = RLock()
  
      @wraps(cls)
      def wrapper(*args, **kwargs):
          if cls not in instances:
              with locker:
                  if cls not in instances:
                      instances[cls] = cls(*args, **kwargs)
          return instances[cls]
  
      return wrapper
  ```

  > **Note :** Le code utilise la syntaxe `with` pour la gestion du verrou, car un objet verrou est un gestionnaire de contexte (implémente `__enter__` et `__exit__`). On effectue d'abord une vérification sans verrou pour la performance, puis une vérification avec verrou.

### Concepts de la programmation orientée objet

- **Les trois piliers : Encapsulation, Héritage, Polymorphisme**

  Exemple : Système de calcul de salaire.

  ```Python
  """
  Système de paie - Un manager gagne 15000 par mois, un programmeur 200 de l'heure, un vendeur 1800 de base + 5% des ventes.
  """
  from abc import ABCMeta, abstractmethod
  
  class Employee(metaclass=ABCMeta):
      """Employé (classe abstraite)"""
  
      def __init__(self, name):
          self.name = name
  
      @abstractmethod
      def get_salary(self):
          """Calculer le salaire mensuel (méthode abstraite)"""
          pass
  
  class Manager(Employee):
      """Manager"""
  
      def get_salary(self):
          return 15000.0
  
  class Programmer(Employee):
      """Programmeur"""
  
      def __init__(self, name, working_hour=0):
          self.working_hour = working_hour
          super().__init__(name)
  
      def get_salary(self):
          return 200.0 * self.working_hour
  
  class Salesman(Employee):
      """Vendeur"""
  
      def __init__(self, name, sales=0.0):
          self.sales = sales
          super().__init__(name)
  
      def get_salary(self):
          return 1800.0 + self.sales * 0.05
  
  class EmployeeFactory:
      """Usine à employés (pattern Factory - découple le créateur de l'objet)"""
  
      @staticmethod
      def create(emp_type, *args, **kwargs):
          """Créer un employé"""
          all_emp_types = {'M': Manager, 'P': Programmer, 'S': Salesman}
          cls = all_emp_types[emp_type.upper()]
          return cls(*args, **kwargs) if cls else None
  
  def main():
      """Fonction principale"""
      emps = [
          EmployeeFactory.create('M', 'Cao Cao'),
          EmployeeFactory.create('P', 'Xun Yu', 120),
          EmployeeFactory.create('P', 'Guo Jia', 85),
          EmployeeFactory.create('S', 'Dian Wei', 123000),
      ]
      for emp in emps:
          print(f'{emp.name}: {emp.get_salary():.2f} €')
  
  if __name__ == '__main__':
      main()
  ```

- **Relations entre classes**
  - Relation **is-a** : Héritage
  - Relation **has-a** : Association / Agrégation / Composition
  - Relation **use-a** : Dépendance

  Exemple : Jeu de cartes.

  ```Python
  """
  Conseil : Les constantes symboliques sont préférables aux littéraux. Les énumérations sont le meilleur choix.
  """
  from enum import Enum, unique
  import random
  
  @unique
  class Suite(Enum):
      """Couleurs"""
      SPADE, HEART, CLUB, DIAMOND = range(4)
  
      def __lt__(self, other):
          return self.value < other.value
  
  class Card:
      """Carte"""
  
      def __init__(self, suite, face):
          self.suite = suite
          self.face = face
  
      def show(self):
          """Afficher la carte"""
          suites = ['♠', '♥', '♣', '♦']
          faces = ['', 'A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'V', 'D', 'R']
          return f'{suites[self.suite.value]}{faces[self.face]}'
  
      def __repr__(self):
          return self.show()
  
  class Poker:
      """Jeu de cartes"""
  
      def __init__(self):
          self.index = 0
          self.cards = [Card(suite, face)
                        for suite in Suite
                        for face in range(1, 14)]
  
      def shuffle(self):
          """Battre les cartes (mélanger aléatoirement)"""
          random.shuffle(self.cards)
          self.index = 0
  
      def deal(self):
          """Distribuer une carte"""
          card = self.cards[self.index]
          self.index += 1
          return card
  
      @property
      def has_more(self):
          return self.index < len(self.cards)
  
  class Player:
      """Joueur"""
  
      def __init__(self, name):
          self.name = name
          self.cards = []
  
      def get_one(self, card):
          """Prendre une carte"""
          self.cards.append(card)
  
      def sort(self, comp=lambda card: (card.suite, card.face)):
          """Trier ses cartes"""
          self.cards.sort(key=comp)
  
  def main():
      """Fonction principale"""
      poker = Poker()
      poker.shuffle()
      players = [Player('Est'), Player('Ouest'), Player('Sud'), Player('Nord')]
      while poker.has_more:
          for player in players:
                  player.get_one(poker.deal())
      for player in players:
          player.sort()
          print(player.name, end=': ')
          print(player.cards)
  
  if __name__ == '__main__':
      main()
  ```

  > **Note :** Le code utilise des caractères Emoji pour les couleurs. Ils peuvent ne pas s'afficher sur certains systèmes.

- **Copie d'objets (copie profonde vs copie superficielle)**

- **Garbage collection (ramasse-miettes), références circulaires et références faibles (weak references)**

  Python utilise une gestion automatique de la mémoire basée sur le **comptage de références**, aidée par le **marquage-nettoyage (mark-and-sweep)** et la **collecte par générations (generational garbage collection)**.

  ```C
  typedef struct _object {
      /* Compteur de références */
      int ob_refcnt;
      /* Pointeur vers le type */
      struct _typeobject *ob_type;
  } PyObject;
  ```

  ```C
  /* Incrémenter le compteur */
  #define Py_INCREF(op)   ((op)->ob_refcnt++)
  /* Décrémenter le compteur */
  #define Py_DECREF(op) \
      if (--(op)->ob_refcnt != 0) \
          ; \
      else \
          __Py_Dealloc((PyObject *)(op))
  ```

  Situations où le compteur de références **+1** :
  - Objet créé, ex: `a = 23`
  - Objet référencé, ex: `b = a`
  - Objet passé en argument à une fonction, ex: `f(a)`
  - Objet stocké dans un conteneur, ex: `list1 = [a, a]`

  Situations où le compteur de références **-1** :
  - L'alias de l'objet est explicitement détruit, ex: `del a`
  - L'alias est assigné à un nouvel objet, ex: `a = 24`
  - Un objet quitte sa portée (variable locale d'une fonction)
  - Le conteneur est détruit ou l'objet est supprimé du conteneur

  Les références circulaires peuvent causer des **fuites de mémoire**. Pour y remédier, Python utilise "marquage-nettoyage" et "collecte par générations". À la création, un objet appartient à la génération 0. S'il survit à un cycle de GC, il passe à la génération 1, puis éventuellement à la génération 2.

  ```Python
  # Une référence circulaire cause une fuite mémoire - Python utilise aussi marquage-nettoyage et collecte par générations.
  # Avant Python 3.6, redéfinir __del__ dans un cycle pouvait empêcher sa résolution.
  # Pour éviter les cycles, on peut utiliser des références faibles (weak references).
  list1 = []
  list2 = []
  list1.append(list2)
  list2.append(list1)
  ```

  Le garbage collection est déclenché dans ces cas :
  - Appel explicite à `gc.collect()`
  - Les compteurs internes du module `gc` atteignent un seuil
  - Le programme se termine

  Si deux objets dans un cycle définissent `__del__`, le module `gc` ne les détruit pas (problème d'ordre d'appel). Ce problème est résolu depuis Python 3.6.

  On peut aussi utiliser le module `weakref` pour créer des références faibles et éviter les cycles.

- **Attributs et méthodes magiques (cf. *Python Magic Method Guide*)**

  Questions à considérer :
  - Un objet personnalisé peut-il utiliser des opérateurs ?
  - Peut-on mettre un objet personnalisé dans un `set` ? La déduplication fonctionne-t-elle ?
  - Un objet personnalisé peut-il être une clé de dictionnaire ?
  - Un objet personnalisé peut-il être utilisé avec la syntaxe `with` (gestionnaire de contexte) ?

- **Mixin**

  Exemple : Dictionnaire personnalisé n'autorisant l'assignation que si la clé n'existe pas.

  ```Python
  class SetOnceMappingMixin:
      """Mixin personnalisé"""
      __slots__ = ()
  
      def __setitem__(self, key, value):
          if key in self:
              raise KeyError(str(key) + ' déjà défini')
          return super().__setitem__(key, value)
  
  class SetOnceDict(SetOnceMappingMixin, dict):
      """Dictionnaire personnalisé"""
      pass
  
  my_dict = SetOnceDict()
  try:
      my_dict['username'] = 'jackfrued'
      my_dict['username'] = 'hellokitty'
  except KeyError:
      pass
  print(my_dict)
  ```

- **Métaprogrammation et métaclasses**

  Les objets sont créés par des classes. Les classes sont créées par des métaclasses. Les métaclasses fournissent les métadonnées pour créer une classe. Toutes les classes héritent (directement ou indirectement) de `object`. Toutes les métaclasses héritent de `type`.

  Exemple : Implémenter le Singleton avec une métaclasse.

  ```Python
  import threading
  
  class SingletonMeta(type):
      """Métaclasse personnalisée"""
  
      def __init__(cls, *args, **kwargs):
          cls.__instance = None
          cls.__lock = threading.RLock()
          super().__init__(*args, **kwargs)
  
      def __call__(cls, *args, **kwargs):
          if cls.__instance is None:
              with cls.__lock:
                  if cls.__instance is None:
                      cls.__instance = super().__call__(*args, **kwargs)
          return cls.__instance
  
  class President(metaclass=SingletonMeta):
      """Président (classe Singleton)"""
      pass
  ```

- **Principes de conception orientée objet (SOLID)**
  - **Principe de responsabilité unique (SRP)** - Une classe a une seule raison de changer.
  - **Principe ouvert/fermé (OCP)** - Les entités logicielles doivent être ouvertes à l'extension, fermées à la modification.
  - **Principe d'inversion des dépendances (DIP)** - Programmer vers des abstractions, pas des implémentations (moins contraignant en Python).
  - **Principe de substitution de Liskov (LSP)** - Un objet d'un sous-type doit pouvoir remplacer un objet du type parent.
  - **Principe de ségrégation des interfaces (ISP)** - Préférer des interfaces spécifiques et fines plutôt que des interfaces larges et génériques.
  - **Principe de composition sur l'héritage (CARP)** - Préférer la composition à l'héritage pour réutiliser le code.
  - **Principe de connaissance minimale (LoD / Loi de Déméter)** - Ne pas envoyer de messages à des objets indirectement liés.

  > **Note :** Les lettres en gras forment l'acronyme **SOLID**.

- **Design Patterns GoF**
  - **Créationnels** : Singleton, Fabrique (Factory), Constructeur (Builder), Prototype.
  - **Structurels** : Adaptateur (Adapter), Façade, Proxy.
  - **Comportementaux** : Itérateur (Iterator), Observateur (Observer), État (State), Stratégie (Strategy).

  Exemple : Algorithme de hachage interchangeable (Pattern Stratégie).

  ```Python
  class StreamHasher:
      """Générateur de condensat (hash)"""
  
      def __init__(self, alg='md5', size=4096):
          self.size = size
          alg = alg.lower()
          self.hasher = getattr(__import__('hashlib'), alg.lower())()
  
      def __call__(self, stream):
          return self.to_digest(stream)
  
      def to_digest(self, stream):
          """Générer un condensat hexadécimal"""
          for buf in iter(lambda: stream.read(self.size), b''):
              self.hasher.update(buf)
          return self.hasher.hexdigest()
  
  def main():
      """Fonction principale"""
      hasher1 = StreamHasher()
      with open('Python-3.7.6.tgz', 'rb') as stream:
          print(hasher1.to_digest(stream))
      hasher2 = StreamHasher('sha1')
      with open('Python-3.7.6.tgz', 'rb') as stream:
          print(hasher2(stream))
  
  if __name__ == '__main__':
      main()
  ```

### Itérateurs et générateurs

- **Itérateur** : Objet qui implémente le protocole d'itération.
  - Python n'a pas de mot-clé comme `protocol` ou `interface`.
  - Les protocoles sont représentés par des méthodes magiques.
  - `__iter__` et `__next__` constituent le protocole d'itération.

  ```Python
  class Fib(object):
      """Itérateur"""
      
      def __init__(self, num):
          self.num = num
          self.a, self.b = 0, 1
          self.idx = 0
     
      def __iter__(self):
          return self
  
      def __next__(self):
          if self.idx < self.num:
              self.a, self.b = self.b, self.a + self.b
              self.idx += 1
              return self.a
          raise StopIteration()
  ```

- **Générateur** : Version simplifiée syntaxiquement d'un itérateur (mot-clé `yield`).

  ```Python
  def fib(num):
      """Générateur"""
      a, b = 0, 1
      for _ in range(num):
          a, b = b, a + b
          yield a
  ```

- **Générateur évoluant en coroutine**

  Un objet générateur peut recevoir des données via la méthode `send()`. Ces données deviennent la valeur de l'expression `yield` dans la fonction génératrice. Ainsi, un générateur peut être utilisé comme une coroutine, c'est-à-dire une sous-routine permettant une collaboration (coopération).

  ```Python
  def calc_avg():
      """Calcul de moyenne en flux continu"""
      total, counter = 0, 0
      avg_value = None
      while True:
          value = yield avg_value
          total, counter = total + value, counter + 1
          avg_value = total / counter
  
  gen = calc_avg()
  next(gen)  # Initialisation
  print(gen.send(10))
  print(gen.send(20))
  print(gen.send(30))
  ```

### Programmation concurrente

Trois approches en Python : **Multithreading**, **Multiprocessing**, **I/O asynchrone**. Avantages : amélioration des performances et de l'expérience utilisateur. Inconvénients : développement et débogage plus complexes.

- **Multithreading** : Le module `threading` fournit la classe `Thread` ainsi que `Lock`, `Condition`, `Event`, `Semaphore`, `Barrier`. Le **GIL (Global Interpreter Lock)** empêche l'exécution simultanée de bytecode Python par plusieurs threads (nécessaire pour CPython car sa gestion de mémoire n'est pas *thread-safe*). Le GIL limite l'utilisation des cœurs multiples avec les threads.

  ```Python
  """
  Question d'entretien : Différence entre processus et thread ?
  Processus - Unité d'allocation mémoire par le système d'exploitation. Un processus peut contenir un ou plusieurs threads.
  Thread - Unité d'allocation du temps CPU par le système d'exploitation.
  Programmation concurrente :
  1. Améliorer les performances - Exécuter en parallèle les parties indépendantes du programme.
  2. Améliorer l'expérience utilisateur - Éviter que des opérations longues ne bloquent l'interface.
  """
  import glob
  import os
  import threading
  
  from PIL import Image
  
  PREFIX = 'thumbnails'
  
  def generate_thumbnail(infile, size, format='PNG'):
      """Générer une miniature pour un fichier image donné"""
      file, ext = os.path.splitext(infile)
      file = file[file.rfind('/') + 1:]
      outfile = f'{PREFIX}/{file}_{size[0]}_{size[1]}.{ext}'
      img = Image.open(infile)
      img.thumbnail(size, Image.ANTIALIAS)
      img.save(outfile, format)
  
  def main():
      """Fonction principale"""
      if not os.path.exists(PREFIX):
          os.mkdir(PREFIX)
      for infile in glob.glob('images/*.png'):
          for size in (32, 64, 128):
              # Créer et démarrer un thread
              threading.Thread(
                  target=generate_thumbnail,
                  args=(infile, (size, size))
              ).start()
  
  if __name__ == '__main__':
      main()
  ```

  Concurrence d'accès à une ressource partagée.

  ```Python
  """
  Un programme multithread sans concurrence pour les ressources est simple.
  Quand plusieurs threads accèdent à une ressource critique sans protection, cela cause des incohérences.
  Ressource critique : Ressource partagée et compétitionnée par plusieurs threads.
  """
  import time
  import threading
  
  from concurrent.futures import ThreadPoolExecutor
  
  class Account(object):
      """Compte bancaire"""
  
      def __init__(self):
          self.balance = 0.0
          self.lock = threading.Lock()
  
      def deposit(self, money):
          # Protéger la ressource critique avec un verrou
          with self.lock:
              new_balance = self.balance + money
              time.sleep(0.001)  # Simuler un traitement
              self.balance = new_balance
  
  def main():
      """Fonction principale"""
      account = Account()
      # Créer un pool de threads
      pool = ThreadPoolExecutor(max_workers=10)
      futures = []
      for _ in range(100):
          future = pool.submit(account.deposit, 1)
          futures.append(future)
      # Arrêter le pool
      pool.shutdown()
      for future in futures:
          future.result()
      print(account.balance)
  
  if __name__ == '__main__':
      main()
  ```

  Exemple plus avancé : 5 threads déposent de l'argent, 5 threads en retirent. Si le solde est insuffisant, le thread de retrait attend. On utilise `Condition` pour la synchronisation.

  ```Python
  """
  Plusieurs threads sur une ressource - Protection par verrou (Lock/RLock)
  Plusieurs threads sur plusieurs ressources (threads > ressources) - Sémaphore (Semaphore)
  Ordonnancement de threads - Mettre en pause / Réveiller - Condition
  """
  from concurrent.futures import ThreadPoolExecutor
  from random import randint
  from time import sleep
  
  import threading
  
  class Account:
      """Compte bancaire"""
  
      def __init__(self, balance=0):
          self.balance = balance
          lock = threading.RLock()
          self.condition = threading.Condition(lock)
  
      def withdraw(self, money):
          """Retirer de l'argent"""
          with self.condition:
              while money > self.balance:
                  self.condition.wait()
              new_balance = self.balance - money
              sleep(0.001)
              self.balance = new_balance
  
      def deposit(self, money):
          """Déposer de l'argent"""
          with self.condition:
              new_balance = self.balance + money
              sleep(0.001)
              self.balance = new_balance
              self.condition.notify_all()
  
  def add_money(account):
      while True:
          money = randint(5, 10)
          account.deposit(money)
          print(threading.current_thread().name,
                ':', money, '====>', account.balance)
          sleep(0.5)
  
  def sub_money(account):
      while True:
          money = randint(10, 30)
          account.withdraw(money)
          print(threading.current_thread().name,
                ':', money, '<====', account.balance)
          sleep(1)
  
  def main():
      account = Account()
      with ThreadPoolExecutor(max_workers=15) as pool:
          for _ in range(5):
              pool.submit(add_money, account)
          for _ in range(10):
              pool.submit(sub_money, account)
  
  if __name__ == '__main__':
      main()
  ```

- **Multiprocessing** : Contourne efficacement le GIL. La classe principale est `Process`. Le module `multiprocessing` propose des équivalents aux outils de `threading`. Pour le partage de données entre processus, on peut utiliser des tuyaux (pipes), des sockets, ou la classe `Queue` (basée sur des pipes et des verrous). Exemple :

  ```Python
  """
  Utilisation du multiprocessing et des pools de processus.
  Le multithreading ne peut exploiter les cœurs multiples à cause du GIL.
  Pour les tâches intensives en calcul, privilégier le multiprocessing.
  Exécution : time python3 exemple.py
  Résultat réel : 11.512s
  Temps utilisateur : 39.319s (environ 4x le temps réel, car 4 cœurs utilisés).
  """
  import concurrent.futures
  import math
  
  PRIMES = [
      1116281,
      1297337,
      104395303,
      472882027,
      533000389,
      817504243,
      982451653,
      112272535095293,
      112582705942171,
      112272535095293,
      115280095190773,
      115797848077099,
      1099726899285419
  ] * 5
  
  def is_prime(n):
      """Vérifier si un nombre est premier"""
      if n % 2 == 0:
          return False
  
      sqrt_n = int(math.floor(math.sqrt(n)))
      for i in range(3, sqrt_n + 1, 2):
          if n % i == 0:
              return False
      return True
  
  def main():
      """Fonction principale"""
      with concurrent.futures.ProcessPoolExecutor() as executor:
          for number, prime in zip(PRIMES, executor.map(is_prime, PRIMES)):
              print('%d est premier : %s' % (number, prime))
  
  if __name__ == '__main__':
      main()
  ```

  > **Point clé : Comparaison Multithreading / Multiprocessing.**
  >
  > Utiliser le **multithreading** quand :
  > 1. Le programme maintient beaucoup d'état partagé (mutables). Les listes, dictionnaires et ensembles Python sont *thread-safe*, donc le coût est faible.
  > 2. Le programme passe beaucoup de temps en I/O, avec peu de calcul parallèle et une consommation mémoire modérée.
  >
  > Utiliser le **multiprocessing** quand :
  > 1. Le programme exécute des tâches intensives en calcul (manipulation de bytecode, traitement de données, calcul scientifique).
  > 2. Les entrées peuvent être divisées en blocs traitables en parallèle, et les résultats fusionnés.
  > 3. La consommation mémoire n'est pas un frein et le programme ne dépend pas fortement de l'I/O (fichiers, sockets).

- **Programmation asynchrone (Async I/O)** : Les tâches sont sélectionnées dans une file d'attente et exécutées de manière coopérative par un planificateur (scheduler). L'ordre d'exécution n'est pas garanti. Python 3 supporte l'asynchrone via le module `asyncio` et les mots-clés `async` et `await` (officiels depuis Python 3.7).

  ```Python
  """
  Async I/O - async / await
  """
  import asyncio
  
  def num_generator(m, n):
      """Générateur de nombres dans un intervalle"""
      yield from range(m, n + 1)
  
  async def prime_filter(m, n):
      """Filtre de nombres premiers"""
      primes = []
      for i in num_generator(m, n):
          flag = True
          for j in range(2, int(i ** 0.5 + 1)):
              if i % j == 0:
                  flag = False
                  break
          if flag:
              print('Premier =>', i)
              primes.append(i)
  
          await asyncio.sleep(0.001)  # Point d'arrêt pour coopération
      return tuple(primes)
  
  async def square_mapper(m, n):
      """Calculateur de carrés"""
      squares = []
      for i in num_generator(m, n):
          print('Carré =>', i * i)
          squares.append(i * i)
  
          await asyncio.sleep(0.001)
      return squares
  
  def main():
      """Fonction principale"""
      loop = asyncio.get_event_loop()
      future = asyncio.gather(prime_filter(2, 100), square_mapper(1, 100))
      future.add_done_callback(lambda x: print(x.result()))
      loop.run_until_complete(future)
      loop.close()
  
  if __name__ == '__main__':
      main()
  ```

  > **Note :** `get_event_loop()` obtient la boucle d'événements par défaut. `asyncio.gather()` exécute des coroutines concurrentes et renvoie un *future*. `add_done_callback()` ajoute un rappel. `run_until_complete()` bloque jusqu'à la fin.

  La bibliothèque tierce `aiohttp` fournit un client et serveur HTTP asynchrones, compatibles avec `asyncio`. Exemple de récupération asynchrone de titres de pages web :

  ```Python
  import asyncio
  import re
  
  import aiohttp
  
  PATTERN = re.compile(r'\<title\>(?P<title>.*)\<\/title\>')
  
  async def fetch_page(session, url):
      async with session.get(url, ssl=False) as resp:
          return await resp.text()
  
  async def show_title(url):
      async with aiohttp.ClientSession() as session:
          html = await fetch_page(session, url)
          print(PATTERN.search(html).group('title'))
  
  def main():
      urls = ('https://www.python.org/',
              'https://git-scm.com/',
              'https://www.jd.com/',
              'https://www.taobao.com/',
              'https://www.douban.com/')
      loop = asyncio.get_event_loop()
      cos = [show_title(url) for url in urls]
      loop.run_until_complete(asyncio.wait(cos))
      loop.close()
  
  if __name__ == '__main__':
      main()
  ```

  > **Point clé : Comparaison Async I/O / Multiprocessing.**
  >
  > Utiliser `asyncio` quand :
  > - Le programme n'a pas besoin de vrai parallélisme, mais repose sur de l'I/O asynchrone et des callbacks.
  > - Il y a beaucoup d'attentes (sleep, I/O). Idéal pour les serveurs web sans besoin de traitement en temps réel.

  D'autres bibliothèques pour le parallélisme : `joblib`, `PyMP`, etc.
  Pour améliorer l'extensibilité et la concurrence, on peut faire de la **montée en puissance verticale** (améliorer un nœud) ou **horizontale** (ajouter des nœuds). Les files d'attente de messages (message queues) permettent de découpler les applications, agissant comme une extension distribuée de `Queue`. Le standard AMQP (Advanced Message Queuing Protocol) est très répandu (implémentations : Apache ActiveMQ, RabbitMQ).
  Pour l'**asynchronisation des tâches**, on peut utiliser **Celery**, une file d'attente distribuée en Python, utilisant un broker de messages comme RabbitMQ ou Redis.