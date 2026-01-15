## Lecture et écriture de fichiers et gestion des exceptions

Dans le développement pratique, on rencontre souvent des scénarios nécessitant la persistance des données. La persistance désigne le transfert des données d'un support de stockage ne permettant pas une conservation à long terme (généralement la mémoire) vers un support de stockage permettant une conservation à long terme (généralement le disque dur). La méthode la plus directe et la plus simple pour implémenter la persistance des données consiste à sauvegarder les données dans des **fichiers** via le **système de fichiers**.

Le **système de fichiers** d'un ordinateur est une méthode de stockage et d'organisation des données informatiques qui facilite l'accès et la recherche des données. Il utilise les concepts abstraits logiques de **fichier** et d'**arborescence de répertoires** pour remplacer les concepts de blocs de données des périphériques physiques comme les disques durs, les CD, les clés USB, etc. Lorsque l'utilisateur utilise le système de fichiers pour sauvegarder des données, il n'a pas besoin de se soucier du bloc de données physique sur le disque où les données sont réellement enregistrées, il lui suffit de se souvenir du chemin et du nom de ce fichier. Avant d'écrire de nouvelles données, l'utilisateur n'a pas besoin de se soucier des blocs de données inutilisés sur le disque. La gestion de l'espace de stockage sur le disque (allocation et libération) est automatiquement effectuée par le système de fichiers. L'utilisateur a seulement besoin de se souvenir dans quel fichier les données ont été écrites.

### Ouvrir et fermer un fichier

Avec un système de fichiers, nous pouvons très facilement lire et écrire des données via des fichiers. En Python, il est très simple d'effectuer des opérations sur les fichiers. Nous pouvons utiliser la fonction intégrée `open` pour ouvrir un fichier. Lors de l'utilisation de la fonction `open`, nous pouvons spécifier des informations telles que le **nom du fichier**, le **mode d'ouverture** et l'**encodage des caractères** via les paramètres de la fonction, puis procéder aux opérations de lecture et d'écriture sur le fichier. Le mode d'ouverture mentionné ici fait référence au type de fichier à ouvrir (fichier texte ou fichier binaire) et à l'opération à effectuer (lecture, écriture ou ajout), comme détaillé dans le tableau ci-dessous.

| Mode | Signification |
| --- | --- |
| `'r'` | Lecture (par défaut) |
| `'w'` | Écriture (tronque le contenu existant) |
| `'x'` | Écriture, génère une exception si le fichier existe déjà |
| `'a'` | Ajout, écrit le contenu à la fin du fichier existant |
| `'b'` | Mode binaire |
| `'t'` | Mode texte (par défaut) |
| `'+'` | Mise à jour (lecture et écriture) |

Lors de l'utilisation de la fonction `open`, si le fichier ouvert est un fichier texte, l'encodage des caractères utilisé pour lire et écrire le fichier peut être spécifié via le paramètre `encoding`. Si les concepts d'encodage des caractères et de jeu de caractères ne sont pas compris, vous pouvez consulter l'article sur les jeux de caractères et l'encodage, qui ne sera pas détaillé ici.

Si l'ouverture du fichier par la fonction `open` réussit, un objet fichier est retourné. Via cet objet, nous pouvons réaliser les opérations de lecture et d'écriture. Si l'ouverture échoue, la fonction `open` déclenche une exception, comme expliqué plus loin. Pour fermer un fichier ouvert, on peut utiliser la méthode `close` de l'objet fichier, ce qui permet de libérer le fichier une fois les opérations terminées.

### Lire et écrire un fichier texte

Lors de l'ouverture d'un fichier texte avec la fonction `open`, il faut spécifier le nom du fichier et définir le mode d'ouverture sur `'r'` (c'est la valeur par défaut si non spécifié). Si un encodage doit être précisé, on peut utiliser le paramètre `encoding`. S'il n'est pas spécifié, la valeur par défaut est None, et l'encodage par défaut du système d'exploitation sera utilisé pour lire le fichier. Il est important de noter que si l'encodage utilisé lors de la sauvegarde du fichier ne correspond pas à celui spécifié par le paramètre `encoding`, il peut y avoir un échec de lecture dû à l'impossibilité de décoder certains caractères.

L'exemple suivant montre comment lire un fichier texte brut (généralement un fichier composé uniquement de l'encodage natif des caractères, sans éléments de contrôle de style, lisible directement par un simple éditeur de texte).

```python
file = open('Poème.txt', 'r', encoding='utf-8')
print(file.read())
file.close()
```

Outre l'utilisation de la méthode `read` de l'objet fichier pour lire le fichier, on peut utiliser une boucle `for-in` pour lire ligne par ligne, ou la méthode `readlines` pour lire le fichier ligne par ligne dans une liste, comme montré ci-dessous.

```python
file = open('Poème.txt', 'r', encoding='utf-8')
for line in file:
    print(line, end='')
file.close()

file = open('Poème.txt', 'r', encoding='utf-8')
lines = file.readlines()
for line in lines:
    print(line, end='')
file.close()
```

Pour écrire du contenu dans un fichier, on peut utiliser `w` ou `a` comme mode d'ouverture. Le premier tronque le contenu existant avant d'écrire le nouveau, le second ajoute le nouveau contenu à la fin du fichier existant.

```python
file = open('Poème.txt', 'a', encoding='utf-8')
file.write('\nTitre : Poème')
file.write('\nAuteur : Auteur')
file.write('\nDate : Mars 1977')
file.close()
```

### Mécanisme de gestion des exceptions

Notez que dans le code ci-dessus, si le fichier spécifié dans la fonction `open` n'existe pas ou ne peut pas être ouvert, une exception se produira, provoquant l'arrêt du programme. Pour rendre le code robuste et tolérant aux fautes, nous pouvons **utiliser le mécanisme d'exception de Python pour traiter de manière appropriée le code susceptible de rencontrer des problèmes à l'exécution**. Python utilise cinq mots-clés liés aux exceptions : `try`, `except`, `else`, `finally` et `raise`. Examinons d'abord le code ci-dessous, puis présentons l'utilisation de ces mots-clés.

```python
file = None
try:
    file = open('Poème.txt', 'r', encoding='utf-8')
    print(file.read())
except FileNotFoundError:
    print('Impossible d\'ouvrir le fichier spécifié !')
except LookupError:
    print('Encodage inconnu spécifié !')
except UnicodeDecodeError:
    print('Erreur de décodage lors de la lecture du fichier !')
finally:
    if file:
        file.close()
```

En Python, nous pouvons placer le code susceptible de provoquer des exceptions à l'exécution dans un bloc `try`. Après `try`, on peut ajouter un ou plusieurs blocs `except` pour capturer les exceptions et les traiter en conséquence. Par exemple, dans le code ci-dessus, l'absence de fichier déclenche `FileNotFoundError`, un encodage inconnu déclenche `LookupError`, et une lecture avec un encodage incompatible déclenche `UnicodeDecodeError`. Ainsi, nous avons trois blocs `except` pour gérer ces trois situations d'exception différentes. Après `except`, on peut aussi ajouter un bloc `else`, qui est exécuté si aucune exception ne se produit dans le bloc `try`. Le code dans `else` n'est pas soumis à la capture d'exceptions, donc si une exception s'y produit, le programme s'arrêtera et rapportera l'erreur. Enfin, nous utilisons le bloc `finally` pour fermer le fichier ouvert et libérer les ressources externes acquises par le programme. Le code du bloc `finally` est toujours exécuté, que le programme se termine normalement ou anormalement, y compris en cas d'appel à la fonction `exit` du module `sys` (car `exit` provoque en réalité une exception `SystemExit`). Ainsi, nous appelons le bloc `finally` "bloc de code toujours exécuté", et il est idéal pour libérer les ressources externes.

Python intègre de nombreux types d'exceptions. Outre ceux utilisés ci-dessus et ceux rencontrés précédemment, il existe de nombreux autres types d'exceptions, dont la hiérarchie d'héritage est la suivante.

```
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- StopAsyncIteration
      +-- ArithmeticError
      |    +-- FloatingPointError
      |    +-- OverflowError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- BufferError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- IndexError
      |    +-- KeyError
      +-- MemoryError
      +-- NameError
      |    +-- UnboundLocalError
      +-- OSError
      |    +-- BlockingIOError
      |    +-- ChildProcessError
      |    +-- ConnectionError
      |    |    +-- BrokenPipeError
      |    |    +-- ConnectionAbortedError
      |    |    +-- ConnectionRefusedError
      |    |    +-- ConnectionResetError
      |    +-- FileExistsError
      |    +-- FileNotFoundError
      |    +-- InterruptedError
      |    +-- IsADirectoryError
      |    +-- NotADirectoryError
      |    +-- PermissionError
      |    +-- ProcessLookupError
      |    +-- TimeoutError
      +-- ReferenceError
      +-- RuntimeError
      |    +-- NotImplementedError
      |    +-- RecursionError
      +-- SyntaxError
      |    +-- IndentationError
      |         +-- TabError
      +-- SystemError
      +-- TypeError
      +-- ValueError
      |    +-- UnicodeError
      |         +-- UnicodeDecodeError
      |         +-- UnicodeEncodeError
      |         +-- UnicodeTranslateError
      +-- Warning
           +-- DeprecationWarning
           +-- PendingDeprecationWarning
           +-- RuntimeWarning
           +-- SyntaxWarning
           +-- UserWarning
           +-- FutureWarning
           +-- ImportWarning
           +-- UnicodeWarning
           +-- BytesWarning
           +-- ResourceWarning
```

D'après cette hiérarchie, toutes les exceptions en Python sont des sous-types de `BaseException`, qui a quatre sous-classes directes : `SystemExit`, `KeyboardInterrupt`, `GeneratorExit` et `Exception`. `SystemExit` indique que l'interpréteur demande une sortie, `KeyboardInterrupt` est l'interruption de l'exécution par l'utilisateur (Ctrl+C), `GeneratorExit` signale une exception dans un générateur. Il n'est pas nécessaire de bien comprendre ces exceptions pour l'instant. Notons la classe `Exception`, qui est le parent des types d'exceptions courants ; de nombreuses exceptions en héritent directement ou indirectement. Si les types d'exceptions intégrés à Python ne suffisent pas aux besoins de l'application, nous pouvons définir des types d'exceptions personnalisés, qui doivent également hériter directement ou indirectement de la classe `Exception`, et peuvent redéfinir ou ajouter des méthodes si nécessaire.

En Python, le mot-clé `raise` peut être utilisé pour déclencher une exception (lancer un objet d'exception), et l'appelant peut capturer et traiter l'exception via la structure `try...except...`. Par exemple, dans une fonction, si les conditions d'exécution ne sont pas remplies, on peut déclencher une exception pour informer l'appelant du problème. L'appelant peut ensuite capturer et traiter l'exception pour permettre au code de se rétablir. Voici un exemple de définition et de déclenchement d'une exception.

```python
class InputError(ValueError):
    """Type d'exception personnalisé"""
    pass


def fac(num):
    """Calcul de la factorielle"""
    if num < 0:
        raise InputError('Seuls les entiers non négatifs peuvent être utilisés pour le calcul factoriel')
    if num in (0, 1):
        return 1
    return num * fac(num - 1)
```

Pour appeler la fonction de factorielle `fac`, on capture l'exception d'erreur d'entrée via la structure `try...except...` et on affiche l'objet exception (message d'erreur). Si l'entrée est correcte, on calcule la factorielle et on termine le programme.

```python
flag = True
while flag:
    num = int(input('n = '))
    try:
        print(f'{num}! = {fac(num)}')
        flag = False
    except InputError as err:
        print(err)
```

### Syntaxe du gestionnaire de contexte

Pour les objets fichiers retournés par la fonction `open`, on peut également utiliser la syntaxe du gestionnaire de contexte `with` pour que la méthode `close` de l'objet fichier soit automatiquement exécutée une fois les opérations terminées. Cela rend le code plus simple et élégant, car il n'est plus nécessaire d'écrire un bloc `finally` pour fermer le fichier et libérer les ressources. Il est important de noter que tous les objets ne peuvent pas être utilisés avec la syntaxe de contexte `with` ; seuls les objets conformes au **protocole de gestionnaire de contexte** (ayant les méthodes magiques `__enter__` et `__exit__`) peuvent l'utiliser. Le module `contextlib` de la bibliothèque standard Python fournit également un support pour cette syntaxe, qui sera expliqué plus tard.

Voici le code réécrit avec la syntaxe de contexte `with`.

```python
try:
    with open('Poème.txt', 'r', encoding='utf-8') as file:
        print(file.read())
except FileNotFoundError:
    print('Impossible d\'ouvrir le fichier spécifié !')
except LookupError:
    print('Encodage inconnu spécifié !')
except UnicodeDecodeError:
    print('Erreur de décodage lors de la lecture du fichier !')
```

### Lecture et écriture de fichiers binaires

La lecture et l'écriture de fichiers binaires sont similaires aux opérations sur les fichiers texte, mais il faut noter que lors de l'ouverture d'un fichier avec `open`, le mode de lecture est `'rb'` et le mode d'écriture est `'wb'`. De plus, pour les fichiers texte, la valeur de retour de `read` et les paramètres de `write` sont des objets `str` (chaînes de caractères), tandis que pour les fichiers binaires, ce sont des objets de type `bytes` (séquences d'octets). Le code suivant réalise une copie d'un fichier image nommé `guido.jpg` du répertoire courant vers un fichier nommé `nouvelle_image.jpg`.

```python
try:
    with open('guido.jpg', 'rb') as file1:
        data = file1.read()
    with open('nouvelle_image.jpg', 'wb') as file2:
        file2.write(data)
except FileNotFoundError:
    print('Le fichier spécifié ne peut pas être ouvert.')
except IOError:
    print('Erreur lors de la lecture/écriture du fichier.')
print('Exécution du programme terminée.')
```

Si le fichier image à copier est très volumineux, lire tout son contenu en mémoire d'un coup peut consommer beaucoup de mémoire. Pour réduire l'utilisation de la mémoire, on peut passer un paramètre `size` à la méthode `read` pour spécifier le nombre d'octets à lire à chaque fois, et réaliser l'opération par lecture et écriture en boucle, comme montré ci-dessous.

```python
try:
    with open('guido.jpg', 'rb') as file1, open('nouvelle_image.jpg', 'wb') as file2:
        data = file1.read(512)
        while data:
            file2.write(data)
            data = file1.read()
except FileNotFoundError:
    print('Le fichier spécifié ne peut pas être ouvert.')
except IOError:
    print('Erreur lors de la lecture/écriture du fichier.')
print('Exécution du programme terminée.')
```

### Résumé

Grâce aux opérations de lecture et d'écriture de fichiers, nous pouvons réaliser la persistance des données. En Python, on peut obtenir un objet fichier via la fonction `open`, et utiliser les méthodes `read` et `write` de l'objet fichier pour lire et écrire. Un programme en cours d'exécution peut rencontrer des situations exceptionnelles imprévisibles, que l'on peut gérer en utilisant le mécanisme d'exception de Python. Celui-ci repose principalement sur cinq mots-clés : `try`, `except`, `else`, `finally` et `raise`. Les instructions `except` après `try` ne sont pas obligatoires, `finally` non plus, mais l'un des deux est nécessaire. On peut avoir une ou plusieurs instructions `except`, qui seront évaluées dans l'ordre pour correspondre aux exceptions spécifiées. Si une exception est traitée, elle n'entrera pas dans les `except` suivants. Une instruction `except` peut capturer plusieurs types d'exceptions en utilisant un tuple. Si aucun type d'exception n'est spécifié après `except`, toutes les exceptions sont capturées par défaut. Après capture, on peut utiliser `raise` pour relancer l'exception, mais il est déconseillé de capturer et relancer la même exception. Il est également déconseillé de capturer toutes les exceptions sans comprendre la logique, car cela peut masquer des problèmes graves dans le programme. Enfin, il est important de souligner qu'**il ne faut pas utiliser le mécanisme d'exception pour gérer la logique métier normale ou contrôler le flux du programme**. En d'autres termes, il ne faut pas abuser du mécanisme d'exception, une erreur fréquente chez les débutants.