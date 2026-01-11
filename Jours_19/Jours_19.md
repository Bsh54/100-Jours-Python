## Programmation Orientée Objet Avancée

Nous avons précédemment abordé les bases de la programmation orientée objet (POO) en Python. Dans cette section, nous continuons à explorer les concepts liés à la POO.

### Visibilité et Décorateurs de Propriétés

Dans de nombreux langages orientés objet, les attributs des objets sont généralement définis comme privés (private) ou protégés (protected), c'est-à-dire que leur accès direct n'est pas autorisé. Les méthodes des objets sont généralement publiques (public), car ce sont les messages que l'objet peut recevoir et l'interface d'appel exposée à l'extérieur. C'est ce qu'on appelle la visibilité d'accès. En Python, on peut indiquer la visibilité d'un attribut en le préfixant avec des underscores. Par exemple, `__name` indique un attribut privé, `_name` indique un attribut protégé, comme illustré ci-dessous.

```python
class Student:

    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    def study(self, course_name):
        print(f'{self.__name} étudie {course_name}.')


stu = Student('Wang Dachui', 20)
stu.study('Programmation Python')
print(stu.__name)  # AttributeError: 'Student' object has no attribute '__name'
```

La dernière ligne du code ci-dessus déclenche une exception `AttributeError` (erreur d'attribut) avec le message : `'Student' object has no attribute '__name'`. Ainsi, un attribut commençant par `__`, comme `__name`, est considéré comme privé et ne peut être accédé directement depuis l'extérieur de la classe. Cependant, à l'intérieur de la classe, la méthode `study` peut y accéder via `self.__name`. Il est important de noter que la plupart des utilisateurs de Python ne choisissent pas de rendre les attributs des objets privés ou protégés. Comme le dit l'adage : "**We are all consenting adults here**" (nous sommes tous des adultes consentants). Les adultes sont responsables de leurs actes, et il n'est pas nécessaire de restreindre la visibilité via le langage lui-même. En effet, beaucoup de programmeurs considèrent que **l'ouverture est préférable à la fermeture**. Rendre les attributs privés n'est pas essentiel. Ainsi, Python n'impose pas de restriction sémantique stricte. Si vous le souhaitez, vous pouvez toujours accéder à l'attribut privé `__name` via `stu._Student__name`. Les lecteurs intéressés peuvent essayer.

### Attributs Dynamiques

Python est un langage dynamique. Selon Wikipédia, un langage dynamique est "un langage dont la structure peut être modifiée à l'exécution, par exemple en ajoutant de nouvelles fonctions, objets, voire du code, ou en supprimant des fonctions existantes ou en modifiant la structure". Les langages dynamiques sont très flexibles. Actuellement, Python et JavaScript sont des langages dynamiques populaires, ainsi que PHP, Ruby, entre autres. En revanche, des langages comme C et C++ ne sont pas dynamiques.

En Python, nous pouvons ajouter dynamiquement des attributs à un objet, c'est un privilège de Python en tant que langage à typage dynamique, comme montré ci-dessous. Notez que les méthodes d'un objet sont essentiellement aussi des attributs. Si un message non reconnu est envoyé à un objet, l'exception `AttributeError` est levée.

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age


stu = Student('Wang Dachui', 20)
stu.sex = 'Homme'  # Ajoute dynamiquement l'attribut 'sex' à l'objet étudiant
```

Si vous ne souhaitez pas ajouter dynamiquement des attributs aux objets lors de leur utilisation, vous pouvez utiliser la propriété magique `__slots__` de Python. Pour la classe `Student`, vous pouvez spécifier `__slots__ = ('name', 'age')`. Ainsi, les objets de la classe `Student` ne pourront avoir que les attributs `name` et `age`. Toute tentative d'ajout dynamique d'un autre attribut provoquera une exception, comme illustré ci-dessous.

```python
class Student:
    __slots__ = ('name', 'age')

    def __init__(self, name, age):
        self.name = name
        self.age = age


stu = Student('Wang Dachui', 20)
# AttributeError: 'Student' object has no attribute 'sex'
stu.sex = 'Homme'
```

### Méthodes Statiques et de Classe

Jusqu'à présent, les méthodes que nous avons définies dans les classes étaient des méthodes d'instance, c'est-à-dire des messages que l'objet peut recevoir. En plus des méthodes d'instance, une classe peut également contenir des méthodes statiques et des méthodes de classe. Ces deux types de méthodes sont des messages envoyés à la classe elle-même, et il n'y a pas de différence fondamentale entre elles. Dans le monde de la POO, tout est objet. Les classes que nous définissons sont également des objets, et les méthodes statiques et de classe sont des messages envoyés à ces objets de classe. Mais quels types de messages sont directement envoyés à la classe ?

Prenons un exemple : définissons une classe `Triangle` qui crée un triangle à partir de la longueur de ses trois côtés et fournit des méthodes pour calculer son périmètre et son aire. Calculer le périmètre et l'aire sont clairement des méthodes de l'objet triangle. Cependant, lors de la création d'un objet triangle, les trois longueurs fournies ne garantissent pas nécessairement qu'un triangle peut être formé. Nous pouvons donc d'abord écrire une méthode pour vérifier si trois longueurs données peuvent constituer un triangle. Cette méthode n'est clairement pas une méthode d'instance, car au moment de son appel, l'objet triangle n'existe pas encore. Nous pouvons concevoir ce type de méthode comme statique ou de classe, c'est-à-dire qu'il s'agit de messages envoyés à la classe `Triangle`, et non à un objet triangle, comme illustré ci-dessous.

```python
class Triangle(object):
    """Triangle"""

    def __init__(self, a, b, c):
        """Méthode d'initialisation"""
        self.a = a
        self.b = b
        self.c = c

    @staticmethod
    def is_valid(a, b, c):
        """Vérifie si trois longueurs peuvent former un triangle (méthode statique)"""
        return a + b > c and b + c > a and a + c > b

    # @classmethod
    # def is_valid(cls, a, b, c):
    #     """Vérifie si trois longueurs peuvent former un triangle (méthode de classe)"""
    #     return a + b > c and b + c > a and a + c > b

    def perimeter(self):
        """Calcule le périmètre"""
        return self.a + self.b + self.c

    def area(self):
        """Calcule l'aire"""
        p = self.perimeter() / 2
        return (p * (p - self.a) * (p - self.b) * (p - self.c)) ** 0.5
```

Le code ci-dessus utilise le décorateur `staticmethod` pour déclarer que `is_valid` est une méthode statique de la classe `Triangle`. Pour déclarer une méthode de classe, utilisez le décorateur `classmethod` (comme indiqué dans les lignes 15 à 18 du code). Les méthodes statiques et de classe peuvent être appelées directement via `NomClasse.nom_methode`. La différence est que le premier paramètre d'une méthode de classe est l'objet classe lui-même, tandis qu'une méthode statique n'a pas ce paramètre. En résumé, **les méthodes d'instance, de classe et statiques peuvent toutes être appelées via "NomClasse.nom_methode". La différence réside dans le premier paramètre de la méthode : un objet instance, un objet classe, ou aucun objet recevant le message**. Une méthode statique pourrait souvent être écrite comme une fonction indépendante, car elle n'est pas liée à un objet spécifique.

Complément : nous pouvons ajouter un décorateur `property` (type intégré de Python) aux méthodes `perimeter` et `area` de la classe `Triangle`. Ainsi, `perimeter` et `area` deviennent des propriétés accessibles directement comme des attributs, et non plus via un appel de méthode. Le code modifié est présenté ci-dessous.

```python
class Triangle(object):
    """Triangle"""

    def __init__(self, a, b, c):
        """Méthode d'initialisation"""
        self.a = a
        self.b = b
        self.c = c

    @staticmethod
    def is_valid(a, b, c):
        """Vérifie si trois longueurs peuvent former un triangle (méthode statique)"""
        return a + b > c and b + c > a and a + c > b

    @property
    def perimeter(self):
        """Calcule le périmètre"""
        return self.a + self.b + self.c

    @property
    def area(self):
        """Calcule l'aire"""
        p = self.perimeter / 2
        return (p * (p - self.a) * (p - self.b) * (p - self.c)) ** 0.5


t = Triangle(3, 4, 5)
print(f'Périmètre: {t.perimeter}')
print(f'Aire: {t.area}')
```

### Héritage et Polymorphisme

Les langages de programmation orientés objet permettent de créer de nouvelles classes basées sur des classes existantes, réduisant ainsi la duplication de code. La classe fournissant l'héritage est appelée classe parent (superclasse, classe de base). La classe recevant l'héritage est appelée classe enfant (sous-classe, classe dérivée). Par exemple, si nous définissons une classe `Student` et une classe `Teacher`, nous constaterons une grande quantité de code redondant, car ces deux classes partagent des attributs et des comportements communs en tant qu'êtres humains. Dans ce cas, nous devrions d'abord définir une classe `Person`, puis en dériver les classes `Teacher` et `Student` via l'héritage, comme illustré ci-dessous.

```python
class Person:
    """Personne"""

    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def eat(self):
        print(f'{self.name} mange.')
    
    def sleep(self):
        print(f'{self.name} dort.')


class Student(Person):
    """Étudiant"""
    
    def __init__(self, name, age):
        super().__init__(name, age)
    
    def study(self, course_name):
        print(f'{self.name} étudie {course_name}.')


class Teacher(Person):
    """Enseignant"""

    def __init__(self, name, age, title):
        super().__init__(name, age)
        self.title = title
    
    def teach(self, course_name):
        print(f'{self.name} {self.title} enseigne {course_name}.')


stu1 = Student('Bai Yuanfang', 21)
stu2 = Student('Di Renjie', 22)
tea1 = Teacher('Wu Zetian', 35, 'Professeur associé')
stu1.eat()
stu2.sleep()
tea1.eat()
stu1.study('Programmation Python')
tea1.teach('Programmation Python')
stu2.study('Introduction à la science des données')
```

La syntaxe d'héritage consiste à spécifier la classe parent entre parenthèses après le nom de la classe lors de sa définition. Si aucune classe parent n'est spécifiée, la classe parent par défaut est la classe `object`. La classe `object` est la classe racine en Python, ce qui signifie que toutes les classes en héritent, directement ou indirectement. Python permet l'héritage multiple, c'est-à-dire qu'une classe peut avoir un ou plusieurs parents. Nous aborderons l'héritage multiple plus en détail ultérieurement. Dans la méthode d'initialisation d'une classe enfant, nous pouvons appeler la méthode d'initialisation de la classe parent via `super().__init__()`. La fonction `super` est une fonction intégrée de Python conçue spécifiquement pour obtenir l'objet parent de l'objet courant. Comme le montre le code ci-dessus, en plus d'hériter des attributs et méthodes de la classe parent, une classe enfant peut définir ses propres attributs et méthodes. Ainsi, une classe enfant possède plus de capacités que sa classe parent. En développement, il est courant de remplacer un objet parent par un objet enfant, un comportement connu sous le nom de "principe de substitution de Liskov" (Liskov Substitution Principle).

Après avoir hérité d'une méthode de la classe parent, une classe enfant peut la redéfinir (la réimplémenter). Différentes classes enfants peuvent fournir différentes implémentations de la même méthode parent. Lors de l'exécution du programme, une telle méthode manifestera un comportement polymorphe (appel de la même méthode, mais actions différentes). Le polymorphisme est l'aspect le plus subtil de la POO, et aussi le plus difficile à comprendre et à maîtriser pour les débutants. Nous illustrerons ce concept avec un exemple dédié dans le prochain chapitre.

### Résumé

Python est un langage à typage dynamique. Les objets en Python peuvent se voir attribuer dynamiquement des attributs. Les méthodes d'un objet sont aussi des attributs, sauf qu'ils correspondent à une fonction appelable. Dans le monde de la POO, **tout est objet**. Les classes que nous définissons sont également des objets, donc **les classes peuvent aussi recevoir des messages**, correspondant aux méthodes de classe ou statiques. Grâce à l'héritage, nous pouvons **créer de nouvelles classes à partir de classes existantes**, réutilisant ainsi le code des classes existantes.