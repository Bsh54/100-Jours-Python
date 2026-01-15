## Lecture et écriture de fichiers CSV en Python

### Présentation des fichiers CSV

CSV (Comma Separated Values) signifie "valeurs séparées par des virgules". C'est un format de fichier simple et universel largement utilisé pour l'importation et l'exportation de données dans les applications (bases de données, feuilles de calcul, etc.) et pour l'échange de données entre systèmes hétérogènes. Comme les fichiers CSV sont des fichiers texte purs, ils peuvent être traités par n'importe quel système d'exploitation et langage de programmation. De nombreux langages de programmation offrent un support pour la lecture et l'écriture de fichiers CSV, ce qui explique pourquoi le format CSV est largement utilisé dans le traitement des données et la science des données.

Les fichiers CSV ont les caractéristiques suivantes :

1. Texte pur, utilisant un jeu de caractères (comme [ASCII](https://fr.wikipedia.org/wiki/ASCII), [Unicode](https://fr.wikipedia.org/wiki/Unicode), [GB2312](https://fr.wikipedia.org/wiki/GB2312), etc.) ;
2. Composé d'enregistrements (généralement un par ligne) ;
3. Chaque enregistrement est divisé en champs (colonnes) par un séparateur (comme une virgule, un point-virgule, une tabulation, etc.) ;
4. Tous les enregistrements ont la même séquence de champs.

Les fichiers CSV peuvent être ouverts et modifiés avec un éditeur de texte ou un outil comme un tableur Excel. Lorsque vous ouvrez un fichier CSV avec un tableur comme Excel, vous ne voyez même pas la différence entre un CSV et un fichier Excel. De nombreux systèmes de base de données prennent en charge l'exportation de données vers des fichiers CSV, ainsi que la lecture de données à partir de fichiers CSV pour les enregistrer dans la base de données, mais ce n'est pas le sujet principal de cette discussion.

### Écrire des données dans un fichier CSV

Supposons que nous ayons les résultats d'examens de cinq élèves dans trois matières à enregistrer dans un fichier CSV. Pour cela, nous pouvons utiliser le module `csv` de la bibliothèque standard de Python. La fonction `writer` de ce module renvoie un objet `csvwriter`, dont les méthodes `writerow` ou `writerows` permettent d'écrire des données dans un fichier CSV. Voici le code correspondant.

```python
import csv
import random

with open('scores.csv', 'w') as file:
    writer = csv.writer(file)
    writer.writerow(['Nom', 'Chinois', 'Mathématiques', 'Anglais'])
    names = ['Guan Yu', 'Zhang Fei', 'Zhao Yun', 'Ma Chao', 'Huang Zhong']
    for name in names:
        scores = [random.randrange(50, 101) for _ in range(3)]
        scores.insert(0, name)
        writer.writerow(scores)
```

Contenu du fichier CSV généré :

```
Nom,Chinois,Mathématiques,Anglais
Guan Yu,98,86,61
Zhang Fei,86,58,80
Zhao Yun,95,73,70
Ma Chao,83,97,55
Huang Zhong,61,54,87
```

Il est important de noter que la fonction `writer` ci-dessus, en plus de l'objet fichier dans lequel écrire les données, peut prendre un paramètre `dialect` qui indique le dialecte du fichier CSV, la valeur par défaut étant `excel`. De plus, on peut spécifier le séparateur (par défaut la virgule), le caractère d'encadrement des valeurs (par défaut les guillemets doubles) et le mode d'encadrement via les paramètres `delimiter`, `quotechar` et `quoting`. Le caractère d'encadrement est principalement utilisé lorsque les champs contiennent des caractères spéciaux, pour éviter toute ambiguïté. Vous pouvez essayer de modifier la ligne 5 du code ci-dessus comme suit, puis examiner le fichier CSV généré.

```python
writer = csv.writer(file, delimiter='|', quoting=csv.QUOTE_ALL)
```

Contenu du fichier CSV généré :

```
"Nom"|"Chinois"|"Mathématiques"|"Anglais"
"Guan Yu"|"88"|"64"|"65"
"Zhang Fei"|"76"|"93"|"79"
"Zhao Yun"|"78"|"55"|"76"
"Ma Chao"|"72"|"77"|"68"
"Huang Zhong"|"70"|"72"|"51"
```

### Lire des données à partir d'un fichier CSV

Pour lire le fichier CSV créé précédemment, on peut utiliser le code ci-dessous. La fonction `reader` du module `csv` crée un objet `csvreader`, qui est un itérateur permettant de lire les données du fichier via la fonction `next` ou une boucle `for-in`.

```python
import csv

with open('scores.csv', 'r') as file:
    reader = csv.reader(file, delimiter='|')
    for data_list in reader:
        print(reader.line_num, end='\t')
        for elem in data_list:
            print(elem, end='\t')
        print()
```

> **Remarque** : Dans le code ci-dessus, lorsqu'on itère sur l'objet `csvreader` avec une boucle `for`, on obtient à chaque fois un objet liste contenant tous les champs d'une ligne.

### Résumé

À l'avenir, si vous utilisez Python pour l'analyse de données, vous utiliserez probablement la bibliothèque tierce `pandas`, l'un des outils les plus puissants pour l'analyse de données en Python. `pandas` inclut les fonctions `read_csv` et `to_csv` pour lire et écrire des fichiers CSV. `read_csv` convertit les données lues en un objet `DataFrame`, qui est le type le plus important de la bibliothèque `pandas`, encapsulant une série de méthodes pour le traitement des données (nettoyage, transformation, agrégation, etc.). `to_csv` écrit les données d'un objet `DataFrame` dans un fichier CSV, permettant ainsi la persistance des données. Les fonctions `read_csv` et `to_csv` sont bien plus puissantes que les fonctions natives `csvreader` et `csvwriter`.