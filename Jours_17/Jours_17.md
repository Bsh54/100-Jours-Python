## Application Avancée des Fonctions

Dans le chapitre précédent, nous avons exploré les fonctions d'ordre supérieur en Python, et vous avez certainement acquis une compréhension plus approfondie de la définition et de l'application des fonctions. Dans ce chapitre, nous continuons à vous présenter des connaissances liées aux fonctions : une caractéristique syntaxique distinctive de Python, le décorateur, et l'appel récursif des fonctions.

### Décorateurs

En Python, un décorateur est une construction syntaxique qui permet **"d'embellir une autre fonction et de lui fournir des capacités supplémentaires"**. Un décorateur est lui-même une fonction qui prend comme paramètre la fonction à décorer et qui retourne une fonction dotée de fonctionnalités d'embellissement. D'après cette description, vous l'aurez deviné : un décorateur est une fonction d'ordre supérieur, car son paramètre et sa valeur de retour sont tous deux des fonctions. Cependant, le concept de décorateur reste souvent déroutant pour les débutants en programmation. Illustrons d'abord son utilité par un exemple simple.

Supposons que nous ayons deux fonctions, `download` et `upload`, pour respectivement télécharger et uploader des fichiers, comme montré ci-dessous.

```python
import random
import time


def download(filename):
    """Télécharge un fichier."""
    print(f'Début du téléchargement de {filename}.')
    time.sleep(random.random() * 6)
    print(f'{filename} téléchargé.')

    
def upload(filename):
    """Upload un fichier."""
    print(f'Début de l\'upload de {filename}.')
    time.sleep(random.random() * 8)
    print(f'{filename} uploadé.')

    
download('MySQL_from_drop_to_run.avi')
upload('Python_from_beginner_to_master.pdf')
```

> **Note** : Le code ci-dessus simule le temps nécessaire pour télécharger et uploader des fichiers en mettant en pause l'exécution pour une durée aléatoire, sans effectuer de véritable transfert réseau. Implémenter un vrai téléchargement/upload réseau en Python est également très simple, nous aborderons ces connaissances plus tard.

Nous avons maintenant un nouveau besoin : nous souhaitons connaître le temps exact pris par l'appel aux fonctions `download` et `upload`. Comment pouvons-nous réaliser cela ? Beaucoup d'entre vous ont probablement pensé à enregistrer un timestamp au début de l'exécution de la fonction et un autre à la fin, puis à soustraire les deux pour calculer la durée, comme montré ci-dessous.

```python
start = time.time()
download('MySQL_from_drop_to_run.avi')
end = time.time()
print(f'Temps écoulé : {end - start:.2f} secondes')
start = time.time()
upload('Python_from_beginner_to_master.pdf')
end = time.time()
print(f'Temps écoulé : {end - start:.2f} secondes')
```

Avec le code ci-dessus, nous pouvons enregistrer la durée des opérations, mais remarquez que le code pour enregistrer les temps, calculer et afficher la durée est du code répété. Tout développeur expérimenté le sait : **le code répété est la source de tous les maux**. Existe-t-il un moyen, sans écrire de code redondant, d'enregistrer le temps d'exécution des fonctions d'une manière simple et élégante ? En Python, les décorateurs sont la meilleure solution à ce type de problème. Grâce à la syntaxe des décorateurs, nous pouvons encapsuler le code de chronométrage, qui n'a pas de lien direct avec la logique métier originale (upload/téléchargement), dans une fonction. Si les fonctions `upload` et `download` ont besoin de mesurer le temps, nous appliquons simplement le décorateur à ces deux fonctions. Puisqu'un décorateur est une fonction d'ordre supérieur prenant et retournant des fonctions, nommons-le temporairement `record_time`. Sa structure générale devrait ressembler au code ci-dessous.

```python
def record_time(func):
    
    def wrapper(*args, **kwargs):
        
        result = func(*args, **kwargs)
        
        return result
    
    return wrapper
```

Notez que le paramètre `func` de la fonction `record_time` représente la fonction à décorer. La fonction `wrapper` définie à l'intérieur est la fonction dotée des capacités d'embellissement : elle exécute la fonction décorée `func` et doit finalement retourner la valeur de retour produite par cette exécution. J'ai laissé deux lignes vides aux lignes 4 et 6 dans le code ci-dessus, ce qui signifie que nous pouvons y ajouter du code pour implémenter des fonctionnalités supplémentaires. La fonction `record_time` retournera finalement cette fonction `wrapper` qui remplacera la fonction originale `func`. Ainsi, lorsque la fonction originale `func` est décorée par `record_time`, l'appeler revient en réalité à appeler `wrapper`, ce qui lui confère les capacités supplémentaires. Les paramètres de `wrapper` sont spéciaux : puisque `wrapper` doit remplacer `func` mais que nous ne savons pas quels paramètres `func` accepte, nous utilisons les paramètres variables `*args` et `**kwargs` pour tout récupérer, puis nous les transmettons intacts lors de l'appel à `func`. Soulignons également que Python permet la définition imbriquée de fonctions, comme nous l'avons fait en définissant `wrapper` à l'intérieur de `record_time`, une opération qui n'est pas supportée dans de nombreux langages de programmation.

Une fois cette structure comprise, nous pouvons intégrer la fonctionnalité de chronométrage dans ce décorateur, comme illustré ci-dessous.

```python
import time


def record_time(func):

    def wrapper(*args, **kwargs):
        # Enregistre le temps de début avant d'exécuter la fonction décorée
        start = time.time()
        # Exécute la fonction décorée et récupère sa valeur de retour
        result = func(*args, **kwargs)
        # Enregistre le temps de fin après l'exécution de la fonction décorée
        end = time.time()
        # Calcule et affiche le temps d'exécution de la fonction décorée
        print(f'Temps d\'exécution de {func.__name__} : {end - start:.2f} secondes')
        # Retourne la valeur de retour de la fonction décorée
        return result
    
    return wrapper
```

Écrire un décorateur demande un certain effort, mais c'est une opération efficace et réutilisable. Désormais, chaque fois que nous aurons besoin de mesurer le temps d'exécution d'une fonction, il suffira d'appliquer le décorateur ci-dessus. Il existe deux façons d'utiliser cette fonction décoratrice. La première est d'appeler directement la fonction décoratrice, de lui passer la fonction à décorer et d'utiliser sa valeur de retour pour remplacer la fonction originale. Ainsi, lors de l'appel, la fonction bénéficiera déjà des capacités supplémentaires fournies par le décorateur (enregistrement du temps d'exécution). Essayez le code ci-dessous pour comprendre.

```python
download = record_time(download)
upload = record_time(upload)
download('MySQL_from_drop_to_run.avi')
upload('Python_from_beginner_to_master.pdf')
```

En Python, il existe une **syntaxe sucrée** plus pratique pour utiliser les décorateurs. On peut utiliser `@nom_du_décorateur` placé directement au-dessus de la fonction à décorer. L'effet est identique au code précédent. Voici le code complet pour illustrer la définition et l'utilisation des décorateurs.

```python
import random
import time


def record_time(func):

    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f'Temps d\'exécution de {func.__name__} : {end - start:.2f} secondes')
        return result

    return wrapper


@record_time
def download(filename):
    print(f'Début du téléchargement de {filename}.')
    time.sleep(random.random() * 6)
    print(f'{filename} téléchargé.')


@record_time
def upload(filename):
    print(f'Début de l\'upload de {filename}.')
    time.sleep(random.random() * 8)
    print(f'{filename} uploadé.')


download('MySQL_from_drop_to_run.avi')
upload('Python_from_beginner_to_master.pdf')
```

Dans le code ci-dessus, nous avons ajouté le décorateur aux fonctions `download` et `upload` via la syntaxe sucrée. Les fonctions `download` et `upload` décorées sont en réalité la fonction `wrapper` retournée par notre décorateur. Les appeler revient à appeler `wrapper`, d'où la fonctionnalité d'enregistrement du temps d'exécution.

Si, à certains endroits du code, nous souhaitons désactiver l'effet du décorateur et exécuter la fonction originale, un travail supplémentaire est nécessaire lors de la définition du décorateur. La fonction `wraps` du module `functools` de la bibliothèque standard de Python est également un décorateur. En l'appliquant à la fonction `wrapper`, elle nous aide à préserver la fonction originale avant décoration. Ainsi, pour annuler l'effet du décorateur, nous pouvons accéder à la fonction originale via l'attribut `__wrapped__` de la fonction décorée.

```python
import random
import time

from functools import wraps


def record_time(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f'Temps d\'exécution de {func.__name__} : {end - start:.2f} secondes')
        return result

    return wrapper


@record_time
def download(filename):
    print(f'Début du téléchargement de {filename}.')
    time.sleep(random.random() * 6)
    print(f'{filename} téléchargé.')


@record_time
def upload(filename):
    print(f'Début de l\'upload de {filename}.')
    time.sleep(random.random() * 8)
    print(f'{filename} uploadé.')


# Appeler les fonctions décorées enregistrera le temps d'exécution
download('MySQL_from_drop_to_run.avi')
upload('Python_from_beginner_to_master.pdf')
# Désactiver l'effet du décorateur pour ne pas enregistrer le temps
download.__wrapped__('MySQL_Crash_Course.pdf')
upload.__wrapped__('Python_Journey.pdf')
```

**Le décorateur lui-même peut également être paramétré**, c'est-à-dire qu'il peut être personnalisé via des arguments passés par l'appelant. Nous expliquerons ce point plus en détail lorsque nous en aurons besoin.

### Appel Récursif

Python permet la définition imbriquée de fonctions, l'appel mutuel entre fonctions, et même l'appel direct ou indirect d'une fonction par elle-même. Une fonction qui s'appelle elle-même est dite récursive. À quoi sert l'appel récursif ? En réalité, de nombreux problèmes sont définis de manière récursive. Par exemple, la factorielle que nous avons vue précédemment : la factorielle d'un entier non négatif `N` est `N` multiplié par la factorielle de `N-1`, c'est-à-dire $\small{N! = N \times (N-1)!}$. La définition fait apparaître le concept de factorielle des deux côtés, c'est donc une définition récursive. Par conséquent, nous pouvons utiliser l'appel récursif pour écrire une fonction calculant la factorielle, comme montré ci-dessous.

```python
def fac(num):
    if num in (0, 1):
        return 1
    return num * fac(num - 1)
```

Dans le code ci-dessus, la fonction `fac` s'appelle elle-même, c'est un appel récursif. La condition `if` à la ligne 2 est la **condition de terminaison** de la récursion, définissant quand arrêter les appels récursifs. Pour le calcul de la factorielle, si nous atteignons la factorielle de `0` ou `1`, nous arrêtons la récursion et retournons directement `1`. L'expression `num * fac(num - 1)` à la ligne 4 est la **formule de récurrence**, c'est-à-dire la définition récursive de la factorielle. Analysons brièvement le processus d'exécution pour `fac(5)`.

```python
# Les appels récursifs s'empilent (push sur la pile)
# 5 * fac(4)
# 5 * (4 * fac(3))
# 5 * (4 * (3 * fac(2)))
# 5 * (4 * (3 * (2 * fac(1))))
# La récursion s'arrête, les fonctions se dépilent (pop)
# 5 * (4 * (3 * (2 * 1)))
# 5 * (4 * (3 * 2))
# 5 * (4 * 6)
# 5 * 24
# 120
print(fac(5))    # 120
```

Notez que les appels de fonction utilisent une structure de données en mémoire appelée **"pile"** (stack) pour sauvegarder le contexte d'exécution courant. À la fin de l'appel, la pile permet de restaurer le contexte précédent. Une pile est une structure de données **LIFO** (Last In, First Out), ce qui signifie que la première fonction empilée sera la dernière à retourner, et la dernière fonction empilée sera la première à retourner. Par exemple, si une fonction `a` appelle une fonction `b`, qui elle-même appelle une fonction `c`, alors la première fonction empilée est `a`, et la première fonction dépilée est `c`. Chaque nouvel appel de fonction ajoute une **trame de pile** (stack frame) à la pile, cette trame sauvegardant le contexte d'exécution actuel. Chaque retour de fonction retire une trame de pile. Généralement, l'espace mémoire réservé à la pile est limité. Par conséquent, si les appels récursifs sont trop nombreux, cela peut provoquer un **débordement de pile** (stack overflow). Il est donc crucial de **s'assurer que la récursion converge rapidement**. Essayez d'exécuter `fac(5000)` ; vous devriez obtenir une erreur `RecursionError` avec le message : `maximum recursion depth exceeded in comparison` (dépassement de la profondeur de récursion maximale), ce qui correspond à un débordement de pile.

Avec l'interpréteur Python officiel (CPython), la profondeur maximale par défaut de la pile d'appels est fixée à `1000` niveaux. Au-delà, l'erreur `RecursionError` se produit. Il est possible d'utiliser la fonction `setrecursionlimit` du module `sys` pour modifier cette limite, mais cela n'est pas recommandé. Il vaut mieux garantir une convergence rapide de la récursion, ou envisager d'utiliser une boucle itérative à la place.

Prenons un autre exemple précédemment évoqué : la génération de la suite de Fibonacci. Les deux premiers termes de la suite de Fibonacci sont `1`. À partir du troisième terme, chaque terme est la somme des deux termes précédents, ce qui peut s'écrire `f(n) = f(n - 1) + f(n - 2)`. C'est clairement une définition récursive, nous pouvons donc utiliser la fonction récursive suivante pour calculer le `n`-ième nombre de Fibonacci.

```python
def fib1(n):
    if n in (1, 2):
        return 1
    return fib1(n - 1) + fib1(n - 2)


for i in range(1, 21):
    print(fib1(i))
```

Attention : bien que le code ci-dessus pour calculer les nombres de Fibonacci semble simple et clair, ses performances sont médiocres. Essayez de modifier le second paramètre de la fonction `range` dans la boucle `for` en `51`, pour afficher les 50 premiers nombres de Fibonacci, et observez le temps nécessaire. Vous pouvez partager le temps d'exécution dans les commentaires. Réfléchissez aux raisons de cette lenteur. Il est clair qu'une approche itérative utilisant une boucle est bien meilleure, comme montré ci-dessous.

```python
def fib2(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```

De plus, nous pouvons optimiser le code récursif ci-dessus en utilisant la fonction `lru_cache` du module `functools` de la bibliothèque standard de Python. `lru_cache` est une fonction décoratrice. En l'appliquant à la fonction `fib1`, elle met en cache les résultats d'exécution, évitant ainsi un grand nombre de calculs redondants lors des appels récursifs. Cela améliore considérablement les performances. Essayez d'afficher les 50 premiers nombres de Fibonacci avec le décorateur et comparez le temps d'exécution !

```python
from functools import lru_cache


@lru_cache()
def fib1(n):
    if n in (1, 2):
        return 1
    return fib1(n - 1) + fib1(n - 2)


for i in range(1, 51):
    print(i, fib1(i))
```

> **Note** : `lru_cache` est un décorateur paramétrable, c'est pourquoi la syntaxe `@lru_cache()` à la ligne 4 comprend des parenthèses. `lru_cache` a un paramètre important nommé `maxsize`, qui définit la taille du cache. Sa valeur par défaut est 128.

### Résumé

Les décorateurs sont une caractéristique syntaxique distinctive de Python. **Ils permettent d'améliorer des fonctions existantes**, une technique de programmation très utile. D'autre part, l'appel récursif de fonctions permet de simplifier certains problèmes complexes au niveau du code. Cependant, **il faut absolument faire attention à la condition de terminaison et à la formule de récurrence**. Trouver une formule de récurrence est la condition préalable à l'utilisation de la récursion, et la condition de terminaison garantit que la récursion s'arrêtera. Les appels de fonction utilisent l'espace pile en mémoire pour sauvegarder et restaurer le contexte. Cet espace est généralement très limité. Par conséquent, **si la récursion ne converge pas rapidement, elle risque de provoquer un débordement de pile, entraînant un plantage du programme**.