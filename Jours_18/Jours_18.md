## Introduction à la Programmation Orientée Objet

La programmation orientée objet (POO) est un **paradigme de programmation** très populaire. Un paradigme de programmation fait référence à la **méthodologie de conception des programmes**, c'est-à-dire la manière dont les programmeurs perçoivent et comprennent les programmes, ainsi que leur façon d'écrire du code.

Dans les cours précédents, nous avons dit que **"un programme est un ensemble d'instructions"**. Lors de l'exécution, les instructions du programme sont traduites en une ou plusieurs commandes exécutées par le CPU (Unité Centrale de Traitement). Pour simplifier la conception des programmes, nous avons introduit les fonctions, qui permettent de **regrouper du code relativement indépendant et fréquemment réutilisé**. Lorsque ce code est nécessaire, il suffit d'appeler la fonction. Si une fonction devient trop complexe et lourde, nous pouvons la **diviser en plusieurs sous-fonctions** pour réduire la complexité du système.

Remarquez-vous que programmer consiste essentiellement à écrire du code en suivant le mode de fonctionnement de l'ordinateur pour lui faire accomplir des tâches ? Cependant, le mode de fonctionnement de l'ordinateur diffère du mode de pensée humain normal. Si programmer oblige à abandonner le mode de pensée humain pour s'adapter à la machine, une grande partie du plaisir de la programmation disparaît. Je ne dis pas qu'il est impossible d'écrire du code en suivant le fonctionnement de l'ordinateur, mais lorsqu'il s'agit de développer un système complexe, cette approche peut rendre le code excessivement compliqué, entraînant des difficultés considérables dans le développement et la maintenance.

Avec l'augmentation de la complexité des logiciels, écrire un code correct et fiable devient une tâche extrêmement ardue. C'est pourquoi beaucoup pensent que "le développement de logiciels est l'activité humaine la plus complexe pour transformer le monde". Comment décrire des systèmes complexes et résoudre des problèmes complexes avec des programmes est devenu une question que tous les programmeurs doivent considérer. Le langage Smalltalk, apparu dans les années 70, a donné de l'espoir aux développeurs de logiciels en introduisant un nouveau paradigme de programmation : la programmation orientée objet. Dans le monde de la POO, **les données du programme et les fonctions qui les manipulent forment un tout logique**, que nous appelons **objet**. **Les objets peuvent recevoir des messages**. La méthode pour résoudre les problèmes consiste à **créer des objets et à leur envoyer toutes sortes de messages**. Grâce à la transmission de messages, plusieurs objets dans le programme peuvent collaborer, permettant ainsi de construire des systèmes complexes et de résoudre des problèmes réels. Bien sûr, les prémices de la POO remontent au langage Simula, encore plus ancien, mais ce n'est pas le point central de notre discussion.

> **Note :** Aujourd'hui, de nombreux langages de programmation de haut niveau prennent en charge la POO. Cependant, la POO n'est pas une "balle magique" résolvant tous les problèmes du développement logiciel. Actuellement, il n'existe pas de "balle magique" dans l'industrie du logiciel. Pour approfondir cette question, vous pouvez consulter l'article de Frederick Brooks, père du système IBM360, "No Silver Bullet—Essence and Accident in Software Engineering", ou le classique de l'ingénierie logicielle "The Mythical Man-Month".

### Classes et Objets

Pour résumer la POO en une phrase, je pense que la formulation suivante est particulièrement pertinente et précise.

> **Programmation Orientée Objet :** Regrouper un ensemble de données et les méthodes pour les manipuler en **objets**, classer les objets ayant le même comportement dans des **classes**, masquer les détails internes des objets via **l'encapsulation**, réaliser la spécialisation et la généralisation des classes via **l'héritage**, et implémenter une répartition dynamique basée sur le type d'objet via **le polymorphisme**.

Cette phrase peut ne pas être facile à comprendre pour les débutants, mais je peux d'abord mettre en évidence quelques mots-clés : **objet**, **classe**, **encapsulation**, **héritage**, **polymorphisme**.

Parlons d'abord des termes classe et objet. En POO, **une classe est un concept abstrait, un objet est un concept concret**. Nous extrayons les caractéristiques communes d'un groupe d'objets pour former une classe. Par exemple, nous parlons souvent de "l'être humain", un concept abstrait. Chacun d'entre nous est une existence concrète sous ce concept abstrait, c'est-à-dire un objet. En résumé, **une classe est le plan et le modèle d'un objet, un objet est une instance d'une classe, une entité capable de recevoir des messages**.

Dans le monde de la POO, **tout est objet**, **les objets ont des attributs et des comportements**, **chaque objet est unique** et **tout objet appartient à une classe**. Les attributs d'un objet sont ses caractéristiques statiques, son comportement est sa caractéristique dynamique. Selon cette définition, si nous extrayons les attributs et comportements communs d'objets partageant des caractéristiques similaires, nous pouvons définir une classe.

### Définir une Classe

En Python, nous pouvons utiliser le mot-clé `class` suivi du nom de la classe pour définir une classe. L'indentation détermine le bloc de code de la classe, comme pour la définition d'une fonction. Dans le bloc de code de la classe, nous écrivons des fonctions. Nous avons dit qu'une classe est un concept abstrait ; ces fonctions représentent donc l'extraction des caractéristiques dynamiques communes à un groupe d'objets. Les fonctions écrites dans une classe sont généralement appelées **méthodes**. Les méthodes sont le comportement de l'objet, c'est-à-dire les messages qu'il peut recevoir. Le premier paramètre d'une méthode est généralement `self`, qui représente l'objet lui-même recevant le message.

```python
class Student:

    def study(self, course_name):
        print(f'L\'étudiant étudie {course_name}.')

    def play(self):
        print(f'L\'étudiant joue.')
```

### Créer et Utiliser des Objets

Après avoir défini une classe, nous pouvons créer des objets en utilisant la syntaxe du constructeur, comme montré ci-dessous.

```python
stu1 = Student()
stu2 = Student()
print(stu1)    # <__main__.Student object at 0x10ad5ac50>
print(stu2)    # <__main__.Student object at 0x10ad5acd0> 
print(hex(id(stu1)), hex(id(stu2)))    # 0x10ad5ac50 0x10ad5acd0
```

La syntaxe consistant à placer des parenthèses après le nom de la classe est la syntaxe du constructeur. Le code ci-dessus crée deux objets étudiants, l'un assigné à la variable `stu1`, l'autre à `stu2`. Lorsque nous imprimons les variables `stu1` et `stu2` avec la fonction `print`, nous voyons l'adresse mémoire de l'objet (au format hexadécimal), identique à la valeur obtenue avec la fonction `id` pour l'identifiant de l'objet. Nous pouvons maintenant dire que nos variables sauvegardent en réalité une adresse logique (position) d'un objet en mémoire. Grâce à cette adresse logique, nous pouvons localiser l'objet en mémoire. Ainsi, une instruction d'assignation comme `stu3 = stu2` ne crée pas un nouvel objet, elle se contente de sauvegarder l'adresse d'un objet existant dans une nouvelle variable.

Essayons maintenant d'envoyer des messages aux objets, c'est-à-dire d'appeler leurs méthodes. Dans la classe `Student` définie précédemment, nous avons créé deux méthodes, `study` et `play`. Le premier paramètre de chaque méthode, `self`, représente l'objet étudiant recevant le message. Le deuxième paramètre de la méthode `study` est le nom du cours étudié. En Python, il existe deux façons d'envoyer un message à un objet, comme illustré dans le code suivant.

```python
# Appeler la méthode via "Classe.méthode"
# Le premier paramètre est l'objet recevant le message
# Le deuxième paramètre est le nom du cours
Student.study(stu1, 'Programmation Python')    # L'étudiant étudie Programmation Python.
# Appeler la méthode via "objet.méthode"
# L'objet avant le point est celui recevant le message
# Il suffit de passer le deuxième paramètre (nom du cours)
stu1.study('Programmation Python')             # L'étudiant étudie Programmation Python.

Student.play(stu2)                             # L'étudiant joue.
stu2.play()                                    # L'étudiant joue. 
```

### Méthode d'Initialisation

Vous avez peut-être remarqué que les objets étudiants créés précédemment avaient un comportement mais pas d'attributs. Pour définir des attributs pour un objet étudiant, nous pouvons modifier la classe `Student` en lui ajoutant une méthode nommée `__init__`. Lorsque nous appelons le constructeur de la classe `Student` pour créer un objet, de l'espace mémoire est d'abord alloué pour stocker l'objet étudiant, puis la méthode `__init__` est exécutée automatiquement pour initialiser cette mémoire, c'est-à-dire pour y placer les données. Ainsi, en ajoutant la méthode `__init__` à la classe `Student`, nous pouvons spécifier des attributs pour l'objet étudiant et leur assigner des valeurs initiales. C'est pourquoi la méthode `__init__` est souvent appelée méthode d'initialisation.

Modifions légèrement la classe `Student` ci-dessus pour ajouter deux attributs à l'objet étudiant : `name` (nom) et `age` (âge).

```python
class Student:
    """Étudiant"""

    def __init__(self, name, age):
        """Méthode d'initialisation"""
        self.name = name
        self.age = age

    def study(self, course_name):
        """Étudier"""
        print(f'{self.name} étudie {course_name}.')

    def play(self):
        """Jouer"""
        print(f'{self.name} joue.')
```

Modifiez le code précédent de création d'objets et d'envoi de messages, puis exécutez-le à nouveau pour observer les changements.

```python
# Appeler le constructeur de la classe Student pour créer des objets et passer les paramètres d'initialisation
stu1 = Student('Luo Hao', 44)
stu2 = Student('Wang Dachui', 25)
stu1.study('Programmation Python')    # Luo Hao étudie Programmation Python.
stu2.play()                          # Wang Dachui joue.
```

### Les Piliers de la POO

La programmation orientée objet repose sur trois piliers, les trois mots-clés que nous avons soulignés précédemment : **encapsulation**, **héritage** et **polymorphisme**. Les deux derniers concepts seront détaillés dans le prochain cours. Concentrons-nous d'abord sur l'encapsulation. Ma compréhension de l'encapsulation est : **masquer tous les détails d'implémentation qui peuvent l'être, n'exposer que des interfaces d'appel simples**. Les méthodes d'objet que nous définissons dans une classe sont une forme d'encapsulation. Cette encapsulation nous permet, après avoir créé un objet, d'exécuter le code de la méthode simplement en envoyant un message à l'objet. Autrement dit, nous utilisons la méthode en ne connaissant que son nom et ses paramètres (vue externe de la méthode), sans connaître les détails de son implémentation interne (vue interne de la méthode).

Prenons un exemple : si je veux qu'un robot me verse un verre d'eau, sans utiliser la POO ni aucune encapsulation, je devrais envoyer une série d'instructions au robot : se lever, tourner à gauche, avancer de 5 pas, prendre le verre devant, se retourner, avancer de 10 pas, se pencher, poser le verre, appuyer sur le bouton de distribution d'eau, attendre 10 secondes, relâcher le bouton, reprendre le verre, tourner à droite, avancer de 5 pas, poser le verre, etc. Imaginez la complexité ! Selon l'approche POO, nous pouvons encapsuler l'action de verser de l'eau dans une méthode du robot. Lorsque nous avons besoin que le robot nous serve de l'eau, il suffit d'envoyer le message "verse de l'eau" à l'objet robot. N'est-ce pas bien mieux ?

Dans de nombreux cas, la POO se résume à une approche en trois étapes. Première étape : définir la classe. Deuxième étape : créer l'objet. Troisième étape : envoyer des messages à l'objet. Bien sûr, parfois la première étape n'est pas nécessaire, car la classe que nous voulons utiliser existe peut-être déjà. Nous avons dit précédemment que les `list`, `set`, `dict` intégrés à Python sont en réalité des classes. Si nous devons créer des objets liste, ensemble ou dictionnaire, nous n'avons pas besoin de définir une classe personnalisée. Certaines classes ne sont pas directement fournies par la bibliothèque standard de Python mais proviennent de code tiers ; l'installation et l'utilisation de code tiers seront abordées dans des cours ultérieurs. Dans certains cas particuliers, nous utilisons des objets dits "intégrés". Cela signifie que les étapes 1 et 2 ne sont pas nécessaires, car la classe existe déjà et l'objet a déjà été créé. Il suffit d'envoyer des messages à l'objet ; c'est ce qu'on appelle le "prêt à l'emploi".

### Exemples de POO

#### Exemple 1 : Horloge

> **Exigence :** Définir une classe décrivant une horloge numérique, offrant les fonctionnalités d'avancement et d'affichage de l'heure.

```python
import time


# Définir la classe Horloge
class Clock:
    """Horloge numérique"""

    def __init__(self, hour=0, minute=0, second=0):
        """Méthode d'initialisation
        :param hour: Heure
        :param minute: Minute
        :param second: Seconde
        """
        self.hour = hour
        self.min = minute
        self.sec = second

    def run(self):
        """Faire avancer l'horloge"""
        self.sec += 1
        if self.sec == 60:
            self.sec = 0
            self.min += 1
            if self.min == 60:
                self.min = 0
                self.hour += 1
                if self.hour == 24:
                    self.hour = 0

    def show(self):
        """Afficher l'heure"""
        return f'{self.hour:0>2d}:{self.min:0>2d}:{self.sec:0>2d}'


# Créer un objet horloge
clock = Clock(23, 59, 58)
while True:
    # Envoyer un message à l'objet horloge pour lire l'heure
    print(clock.show())
    # Mettre en pause pendant 1 seconde
    time.sleep(1)
    # Envoyer un message à l'objet horloge pour la faire avancer
    clock.run()
```

#### Exemple 2 : Point dans le plan

> **Exigence :** Définir une classe décrivant un point dans le plan, fournissant une méthode pour calculer la distance à un autre point.

```python
class Point:
    """Point dans le plan"""

    def __init__(self, x=0, y=0):
        """Méthode d'initialisation
        :param x: Abscisse
        :param y: Ordonnée
        """
        self.x, self.y = x, y

    def distance_to(self, other):
        """Calculer la distance à un autre point
        :param other: L'autre point
        """
        dx = self.x - other.x
        dy = self.y - other.y
        return (dx * dx + dy * dy) ** 0.5

    def __str__(self):
        return f'({self.x}, {self.y})'


p1 = Point(3, 5)
p2 = Point(6, 9)
print(p1)  # Appelle la méthode magique __str__ de l'objet
print(p2)
print(p1.distance_to(p2))
```

### Résumé

La programmation orientée objet est un paradigme de programmation très populaire. Il en existe d'autres, comme la **programmation impérative** et la **programmation fonctionnelle**. Comme le monde réel est constitué d'objets, et que les objets sont des entités pouvant recevoir des messages, **la POO correspond mieux au mode de pensée humain habituel**. Une classe est abstraite, un objet est concret. Avec une classe, on peut créer des objets ; avec des objets, on peut recevoir des messages. Telle est la base de la POO. Le processus de définition d'une classe est un processus d'abstraction. Trouver les attributs communs des objets relève de l'abstraction des données ; trouver les méthodes communes relève de l'abstraction du comportement. Le processus d'abstraction est subjectif : abstraire un même groupe d'objets peut donner des résultats différents selon les personnes.