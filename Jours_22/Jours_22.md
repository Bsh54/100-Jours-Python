## Sérialisation et désérialisation d'objets

### Présentation de JSON

Dans les sections précédentes, nous avons vu comment sauvegarder des données textuelles et binaires dans des fichiers. Mais une question se pose : comment sauvegarder dans un fichier les données d'une liste ou d'un dictionnaire ? En Python, nous pouvons sauvegarder les données de notre programme au format JSON. JSON signifie "JavaScript Object Notation". À l'origine, il s'agissait d'une syntaxe littérale pour créer des objets en JavaScript, mais il est maintenant largement utilisé pour l'échange de données interlangages et multiplateformes. La raison de son utilisation est simple : sa structure est compacte et il s'agit de texte pur. Tout système d'exploitation et tout langage de programmation peut traiter du texte pur, ce qui constitue la **condition préalable pour réaliser un échange de données interlangages et multiplateformes**. Actuellement, JSON a largement remplacé XML (Extensible Markup Language) en tant que **standard de facto pour l'échange de données entre systèmes hétérogènes**. Vous pouvez trouver plus d'informations sur JSON sur le [site officiel de JSON](https://www.json.org/json-fr.html), qui propose également les outils ou bibliothèques tiers permettant de traiter le format de données JSON dans chaque langage.

```javascript
{
    "name": "Luo Hao",
    "age": 40,
    "friends": ["Wang Dachui", "Bai Yuanfang"],
    "cars": [
        {"brand": "BMW", "max_speed": 240},
        {"brand": "Benz", "max_speed": 280},
        {"brand": "Audi", "max_speed": 280}
    ]
}
```

L'exemple JSON ci-dessus ressemble beaucoup à un dictionnaire Python et prend en charge les structures imbriquées, comme un dictionnaire Python dont les valeurs peuvent être elles-mêmes des dictionnaires.

Les types de données utilisés en JSON (types de données JavaScript) et les types de données Python sont facilement mis en correspondance, comme le montrent les deux tableaux ci-dessous.

Tableau 1 : Types de données JavaScript (valeurs) correspondant aux types de données Python (valeurs)

| JSON | Python |
| --- | --- |
| `object` | `dict` |
| `array` | `list` |
| `string` | `str` |
| `number` (entier) | `int` |
| `number` (réel) | `float` |
| `boolean` (`true` / `false`) | `bool` (`True` / `False`) |
| `null` | `None` |

Tableau 2 : Types de données Python (valeurs) correspondant aux types de données JavaScript (valeurs)

| Python | JSON |
| --- | --- |
| `dict` | `object` |
| `list` / `tuple` | `array` |
| `str` | `string` |
| `int` / `float` | `number` |
| `bool` (`True` / `False`) | `boolean` (`true` / `false`) |
| `None` | `null` |

### Lecture et écriture de données au format JSON

En Python, pour convertir un dictionnaire au format JSON (sous forme de chaîne), on peut utiliser la fonction `dumps` du module `json`, comme illustré ci-dessous.

```python
import json

my_dict = {
    'name': 'Luo Hao',
    'age': 40,
    'friends': ['Wang Dachui', 'Bai Yuanfang'],
    'cars': [
        {'brand': 'BMW', 'max_speed': 240},
        {'brand': 'Audi', 'max_speed': 280},
        {'brand': 'Benz', 'max_speed': 280}
    ]
}
print(json.dumps(my_dict))
```

Exécutez le code ci-dessus. La sortie montre que les caractères chinois sont affichés sous forme d'encodage Unicode.

```json
{"name": "Luo Hao", "age": 40, "friends": ["Wang Dachui", "Bai Yuanfang"], "cars": [{"brand": "BMW", "max_speed": 240}, {"brand": "Audi", "max_speed": 280}, {"brand": "Benz", "max_speed": 280}]}
```

Pour convertir un dictionnaire au format JSON et l'écrire dans un fichier texte, il suffit de remplacer la fonction `dumps` par `dump` et de lui passer l'objet fichier, comme illustré ci-dessous.

```python
import json

my_dict = {
    'name': 'Luo Hao',
    'age': 40,
    'friends': ['Wang Dachui', 'Bai Yuanfang'],
    'cars': [
        {'brand': 'BMW', 'max_speed': 240},
        {'brand': 'Audi', 'max_speed': 280},
        {'brand': 'Benz', 'max_speed': 280}
    ]
}
with open('data.json', 'w') as file:
    json.dump(my_dict, file)
```

Exécutez le code ci-dessus pour créer le fichier `data.json`. Son contenu est identique à la sortie du code précédent.

Le module `json` comporte quatre fonctions importantes :

- `dump` - Sérialise un objet Python au format JSON dans un fichier
- `dumps` - Convertit un objet Python en une chaîne au format JSON
- `load` - Désérialise les données JSON d'un fichier en objet
- `loads` - Désérialise le contenu d'une chaîne en objet Python

Deux concepts apparaissent ici : la sérialisation et la désérialisation. Selon Wikipédia, "la sérialisation (en informatique) est le processus de transformation d'une structure de données ou d'un objet en un format qui peut être stocké ou transmis et reconstruit ultérieurement. Le processus inverse, qui consiste à extraire une structure de données d'une série d'octets, est la désérialisation."

Le code suivant lit le fichier `data.json` créé précédemment et reconvertit les données JSON en dictionnaire Python.

```python
import json

with open('data.json', 'r') as file:
    my_dict = json.load(file)
    print(type(my_dict))
    print(my_dict)
```

### Outil de gestion de paquets pip

Le module `json` de la bibliothèque standard Python n'est pas très performant pour la sérialisation et la désérialisation des données. Pour remédier à ce problème, on peut utiliser la bibliothèque tierce `ujson` pour remplacer `json`. Les bibliothèques tierces sont des modules Python qui ne sont pas développés en interne par une entreprise, ni issus de la bibliothèque standard officielle. Ces modules sont généralement développés par d'autres entreprises, organisations ou individus, d'où leur nom de bibliothèques tierces. Bien que la bibliothèque standard de Python fournisse déjà de nombreux modules pour faciliter le développement, l'écosystème d'un langage puissant est nécessairement florissant.

Lors de l'installation de l'interpréteur Python, pip est installé par défaut. Vous pouvez vérifier sa présence dans l'invite de commandes ou le terminal avec `pip --version`. Pip est l'outil de gestion de paquets de Python. Avec pip, vous pouvez rechercher, installer, désinstaller et mettre à jour des bibliothèques ou outils tiers Python. Sous macOS et Linux, utilisez pip3. Par exemple, pour installer `ujson` qui remplace le module `json`, utilisez la commande suivante.

```bash
pip install ujson
```

Par défaut, pip accède à `https://pypi.org/simple/` pour obtenir des données sur les bibliothèques tierces, mais l'accès à ce site depuis certaines régions peut être lent. Les utilisateurs peuvent utiliser le miroir fourni par Douban pour remplacer cette source de téléchargement par défaut, comme suit.

```bash
pip install ujson -i https://pypi.douban.com/simple/
```

Vous pouvez rechercher des bibliothèques tierces par nom avec la commande `pip search`, et afficher les bibliothèques tierces déjà installées avec `pip list`. Pour mettre à jour une bibliothèque tierce, utilisez `pip install -U` ou `pip install --upgrade`. Pour supprimer une bibliothèque tierce, utilisez la commande `pip uninstall`.

Rechercher la bibliothèque tierce `ujson`.

```bash
pip search ujson

micropython-cpython-ujson (0.2)  - MicroPython module ujson ported to CPython
pycopy-cpython-ujson (0.2)       - Pycopy module ujson ported to CPython
ujson (3.0.0)                    - Ultra fast JSON encoder and decoder for Python
ujson-bedframe (1.33.0)          - Ultra fast JSON encoder and decoder for Python
ujson-segfault (2.1.57)          - Ultra fast JSON encoder and decoder for Python. Continuing 
                                   development.
ujson-ia (2.1.1)                 - Ultra fast JSON encoder and decoder for Python (Internet 
                                   Archive fork)
ujson-x (1.37)                   - Ultra fast JSON encoder and decoder for Python
ujson-x-legacy (1.35.1)          - Ultra fast JSON encoder and decoder for Python
drf_ujson (1.2)                  - Django Rest Framework UJSON Renderer
drf-ujson2 (1.6.1)               - Django Rest Framework UJSON Renderer
ujsonDB (0.1.0)                  - A lightweight and simple database using ujson.
fast-json (0.3.2)                - Combines best parts of json and ujson for fast serialization
decimal-monkeypatch (0.4.3)      - Python 2 performance patches: decimal to cdecimal, json to 
                                   ujson for psycopg2
```

Afficher les bibliothèques tierces déjà installées.

```bash
pip list

Package                       Version
----------------------------- ----------
aiohttp                       3.5.4
alipay                        0.7.4
altgraph                      0.16.1
amqp                          2.4.2
...							  ...
```

Mettre à jour la bibliothèque tierce `ujson`.

```bash
pip install -U ujson
```

Supprimer la bibliothèque tierce `ujson`.

```bash
pip uninstall -y ujson
```

> **Note** : Pour mettre à jour pip lui-même, sous macOS, utilisez la commande `pip install -U pip`. Sous Windows, remplacez la commande par `python -m pip install -U --user pip`.

### Obtenir des données via une API réseau

Si nous voulons afficher des informations météorologiques, sur l'état du trafic, les vols, etc., dans notre programme, nous ne pouvons pas fournir ces informations nous-mêmes, nous devons donc utiliser des services de données en ligne. Actuellement, la grande majorité des services de données en ligne (ou API réseau) fournissent des données au format JSON via [HTTP](https://fr.wikipedia.org/wiki/Hypertext_Transfer_Protocol) ou HTTPS. Nous pouvons envoyer une requête HTTP à une URL spécifique (Uniform Resource Locator) via un programme Python. Cette URL est l'API réseau. Si la requête réussit, elle renvoie une réponse HTTP, et le corps du message de la réponse HTTP contient les données au format JSON dont nous avons besoin.

De nombreux sites proposent des interfaces API réseau, par exemple [Juhe Data](https://www.juhe.cn/), [Avatardata](http://www.avatardata.cn/), etc. Ces sites proposent des interfaces de données gratuites et payantes. Le site [{API}Search](http://apis.io/) propose des fonctionnalités similaires, que vous pouvez étudier si vous le souhaitez. L'exemple suivant montre comment utiliser la bibliothèque [`requests`](http://docs.python-requests.org/) (une bibliothèque tierce permettant d'accéder aux ressources réseau via HTTP) pour accéder à une API réseau, obtenir des actualités nationales et afficher les titres et les liens. Dans cet exemple, nous utilisons l'interface de données d'actualités nationales fournie par le site [Tianxing Data](https://www.tianapi.com/). L'APIKey doit être demandée sur le site. Après vous être inscrit sur le site Tianxing Data, une APIKey vous est automatiquement attribuée, mais pour accéder à l'interface et obtenir des données, vous devez lier une adresse e-mail ou un téléphone portable pour vérification, puis demander l'interface que vous souhaitez utiliser.

Python accède au réseau via les URL. Nous recommandons d'utiliser la bibliothèque tierce `requests`, qui est simple et puissante, mais doit être installée séparément.

```bash
pip install requests
```

Obtenir les actualités nationales et afficher les titres et les liens.

```python
import requests

resp = requests.get('http://api.tianapi.com/guonei/?key=APIKey&num=10')
if resp.status_code == 200:
    data_model = resp.json()
    for news in data_model['newslist']:
        print(news['title'])
        print(news['url'])
        print('-' * 60)
```

Le code ci-dessus envoie une requête à l'interface d'actualités nationales de Tianxing Data via la fonction `get` du module `requests`. Si aucun problème ne survient lors de la requête, la fonction `get` renvoie un objet `Response`. L'attribut `status_code` de cet objet représente le code d'état de la réponse HTTP. Si sa valeur est égale à `200` ou à une autre valeur commençant par `2`, alors notre requête a réussi. La méthode `json()` de l'objet `Response` peut directement convertir les données au format JSON renvoyées en dictionnaire Python, ce qui est très pratique.

> **Note** : L'APIKey dans le code ci-dessus doit être remplacée par votre propre APIKey obtenue sur le site Tianxing Data. Le site Tianxing Data propose de nombreuses interfaces API très intéressantes, par exemple : tri des déchets, interprétation des rêves, etc. Vous pouvez imiter le code ci-dessus pour appeler ces interfaces. Chaque interface dispose d'une documentation correspondante expliquant en détail comment l'utiliser.

### Résumé

En Python, pour réaliser la sérialisation et la désérialisation, en plus du module `json`, on peut également utiliser les modules `pickle` et `shelve`. Cependant, ces deux modules utilisent un protocole de sérialisation spécifique, de sorte que les données sérialisées ne peuvent être reconnues que par Python. Pour plus d'informations sur ces modules, les lecteurs intéressés peuvent consulter la documentation en ligne. Traiter les données au format JSON est clairement une compétence essentielle que tout programmeur doit maîtriser, car que ce soit pour accéder à des interfaces API réseau ou pour fournir des interfaces API réseau à d'autres, il est nécessaire de posséder des connaissances sur le traitement des données au format JSON.