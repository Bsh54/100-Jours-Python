## Lecture et écriture de fichiers Excel en Python - Partie 1

### Présentation d'Excel

Excel est un logiciel de feuille de calcul développé par Microsoft pour les systèmes d'exploitation Windows et macOS. Grâce à son interface intuitive, ses excellentes fonctionnalités de calcul et ses outils de graphiques, ainsi qu'à son marketing réussi, Excel est depuis longtemps le logiciel de traitement de données le plus populaire pour les ordinateurs personnels. Bien sûr, Excel a également de nombreux concurrents, tels que Google Sheets, LibreOffice Calc, Numbers, etc., qui sont essentiellement compatibles avec Excel, du moins capables de lire et d'écrire les versions plus récentes de fichiers Excel, mais ce n'est pas le sujet principal ici. Maîtriser l'utilisation de Python pour manipuler des fichiers Excel peut rendre les tâches d'automatisation du travail quotidien plus faciles et agréables. De plus, dans de nombreux projets commerciaux, l'importation et l'exportation de fichiers Excel sont des fonctionnalités particulièrement courantes.

Python nécessite des bibliothèques tierces pour manipuler Excel. Pour être compatible avec les versions d'Excel antérieures à 2007, c'est-à-dire les fichiers Excel au format `xls`, vous pouvez utiliser les bibliothèques tierces `xlrd` et `xlwt`. La première permet de lire les fichiers Excel, la seconde d'écrire dans les fichiers Excel. Pour les versions plus récentes d'Excel, c'est-à-dire les fichiers Excel au format `xlsx`, vous pouvez utiliser la bibliothèque `openpyxl`. Bien sûr, cette bibliothèque ne permet pas seulement de manipuler Excel, mais aussi d'autres fichiers de feuille de calcul basés sur Office Open XML.

Dans ce chapitre, nous expliquons d'abord comment manipuler des fichiers Excel avec `xlwt` et `xlrd`. Vous pouvez commencer par installer ces deux bibliothèques tierces ainsi que le module utilitaire `xlutils` avec la commande suivante.

```bash
pip install xlwt xlrd xlutils
```

### Lire un fichier Excel

Par exemple, supposons qu'il y ait un fichier Excel nommé "Données d'actions d'Alibaba 2020.xls" dans le dossier courant. Pour lire et afficher son contenu, vous pouvez utiliser le code ci-dessous.

```python
import xlrd

# Utilisez la fonction open_workbook du module xlrd pour ouvrir le fichier Excel spécifié et obtenir un objet Book (classeur)
wb = xlrd.open_workbook('Données d'actions d'Alibaba 2020.xls')
# La méthode sheet_names de l'objet Book permet d'obtenir tous les noms de feuilles
sheetnames = wb.sheet_names()
print(sheetnames)
# Obtenez l'objet Sheet (feuille de calcul) via le nom de feuille spécifié
sheet = wb.sheet_by_name(sheetnames[0])
# Obtenez le nombre de lignes et de colonnes de la feuille via les attributs nrows et ncols de l'objet Sheet
print(sheet.nrows, sheet.ncols)
for row in range(sheet.nrows):
    for col in range(sheet.ncols):
        # Obtenez l'objet Cell (cellule) spécifié via la méthode cell de l'objet Sheet
        # Obtenez la valeur de la cellule via l'attribut value de l'objet Cell
        value = sheet.cell(row, col).value
        # Effectuez un formatage des données pour toutes les lignes sauf la première
        if row > 0:
            # Convertissez le type xldate de la première colonne en tuple, puis formatez-le au format "année-mois-jour"
            if col == 0:
                # Le deuxième paramètre de la fonction xldate_as_tuple n'a que deux valeurs : 0 et 1
                # 0 représente une date basée sur 1900-01-01, 1 représente une date basée sur 1904-01-01
                value = xlrd.xldate_as_tuple(value, 0)
                value = f'{value[0]}年{value[1]:>02d}月{value[2]:>02d}日'
            # Traitez les autres colonnes de type number en nombres flottants avec deux décimales
            else:
                value = f'{value:.2f}'
        print(value, end='\t')
    print()
# Obtenez le type de données de la dernière cellule
# 0 - vide, 1 - chaîne, 2 - nombre, 3 - date, 4 - booléen, 5 - erreur
last_cell_type = sheet.cell_type(sheet.nrows - 1, sheet.ncols - 1)
print(last_cell_type)
# Obtenez les valeurs de la première ligne (liste)
print(sheet.row_values(0))
# Obtenez les données d'une plage de colonnes spécifique sur une ligne spécifiée (liste)
# Le premier paramètre est l'indice de ligne, les deuxième et troisième paramètres sont les indices de début (inclus) et de fin (exclus) de colonne
print(sheet.row_slice(3, 0, 5))
```

> **Remarque** : Le fichier Excel "Données d'actions d'Alibaba 2020.xls" utilisé dans le code ci-dessus peut être obtenu via le lien Baidu Netdisk fourni à la fin. Lien : https://pan.baidu.com/s/1rQujl5RQn9R7PadB2Z5g_g Code : e7b4.

Grâce au code ci-dessus, vous devriez maintenant comprendre comment lire un fichier Excel. Pour en savoir plus sur le module `xlrd`, vous pouvez consulter sa [documentation officielle](https://xlrd.readthedocs.io/en/latest/).

### Écrire dans un fichier Excel

Pour écrire dans un fichier Excel, vous pouvez créer un objet Workbook (classeur) à l'aide de la classe `Workbook` du module `xlwt`. La méthode `add_sheet` de l'objet Workbook permet d'ajouter une feuille de calcul. La méthode `write` de l'objet Worksheet permet d'écrire des données dans une cellule spécifique. Enfin, la méthode `save` de l'objet Workbook permet d'enregistrer le classeur dans un fichier spécifié ou en mémoire. Le code ci-dessous écrit les résultats d'examen de cinq élèves dans trois matières dans un fichier Excel.

```python
import random

import xlwt

student_names = ['Guan Yu', 'Zhang Fei', 'Zhao Yun', 'Ma Chao', 'Huang Zhong']
scores = [[random.randrange(50, 101) for _ in range(3)] for _ in range(5)]
# Créez un objet Workbook (classeur)
wb = xlwt.Workbook()
# Créez un objet Worksheet (feuille de calcul)
sheet = wb.add_sheet('Classe 1-2')
# Ajoutez les données d'en-tête
titles = ('Nom', 'Chinois', 'Mathématiques', 'Anglais')
for index, title in enumerate(titles):
    sheet.write(0, index, title)
# Écrivez les noms des élèves et les résultats d'examen dans les cellules
for row in range(len(scores)):
    sheet.write(row + 1, 0, student_names[row])
    for col in range(len(scores[row])):
        sheet.write(row + 1, col + 1, scores[row][col])
# Enregistrez le classeur Excel
wb.save('Tableau des résultats d'examen.xls')
```

### Ajuster le style des cellules

Lors de l'écriture dans un fichier Excel, nous pouvons également définir le style des cellules, principalement la police (Font), l'alignement (Alignment), les bordures (Border) et l'arrière-plan (Background). `xlwt` encapsule des classes correspondantes pour prendre en charge ces paramètres. Pour définir le style d'une cellule, vous devez d'abord créer un objet `XFStyle`, puis définir la police, l'alignement, les bordures, etc., via les propriétés de cet objet. Par exemple, dans l'exemple précédent, si vous souhaitez modifier la couleur d'arrière-plan des cellules d'en-tête en jaune, vous pouvez procéder comme suit.

```python
header_style = xlwt.XFStyle()
pattern = xlwt.Pattern()
pattern.pattern = xlwt.Pattern.SOLID_PATTERN
# 0 - noir, 1 - blanc, 2 - rouge, 3 - vert, 4 - bleu, 5 - jaune, 6 - rose, 7 - cyan
pattern.pattern_fore_colour = 5
header_style.pattern = pattern
titles = ('Nom', 'Chinois', 'Mathématiques', 'Anglais')
for index, title in enumerate(titles):
    sheet.write(0, index, title, header_style)
```

Si vous souhaitez définir une police spécifique pour l'en-tête, vous pouvez utiliser la classe `Font` et ajouter le code suivant.

```python
font = xlwt.Font()
# Nom de la police
font.name = 'KaiTi'
# Taille de la police (20 est l'unité de base, 18 représente 18px)
font.height = 20 * 18
# Utiliser le gras ou non
font.bold = True
# Utiliser l'italique ou non
font.italic = False
# Couleur de la police
font.colour_index = 1
header_style.font = font
```

> **Remarque** : Le nom de police (`font.name`) spécifié dans le code ci-dessus doit être une police disponible sur votre système local. Par exemple, sur mon ordinateur, la police "KaiTi" est disponible.

Si vous souhaitez que l'en-tête soit centré verticalement, vous pouvez utiliser le code suivant.

```python
align = xlwt.Alignment()
# Alignement vertical
align.vert = xlwt.Alignment.VERT_CENTER
# Alignement horizontal
align.horz = xlwt.Alignment.HORZ_CENTER
header_style.alignment = align
```

Si vous souhaitez ajouter une bordure pointillée jaune à l'en-tête, vous pouvez utiliser le code suivant.

```python
borders = xlwt.Borders()
props = (
    ('top', 'top_colour'), ('right', 'right_colour'),
    ('bottom', 'bottom_colour'), ('left', 'left_colour')
)
# Définissez le style et la couleur des bordures des quatre côtés via une boucle
for position, color in props:
    # Utilisez la fonction intégrée setattr pour attribuer dynamiquement une valeur à la propriété spécifiée de l'objet
    setattr(borders, position, xlwt.Borders.DASHED)
    setattr(borders, color, 5)
header_style.borders = borders
```

Pour ajuster la largeur des cellules (largeur de colonne) et la hauteur de l'en-tête (hauteur de ligne), vous pouvez procéder comme suit.

```python
# Définissez la hauteur de ligne à 40px
sheet.row(0).set_style(xlwt.easyxf(f'font:height {20 * 40}'))
titles = ('Nom', 'Chinois', 'Mathématiques', 'Anglais')
for index, title in enumerate(titles):
    # Définissez la largeur de colonne à 200px
    sheet.col(index).width = 20 * 200
    # Définissez les données et le style de la cellule
    sheet.write(0, index, title, header_style)
```

### Calcul avec formules

Pour le fichier "Données d'actions d'Alibaba 2020.xls" ouvert précédemment, si vous souhaitez calculer la moyenne du prix de clôture annuel (champ Close) et la somme du volume annuel (champ Volume), vous pouvez utiliser les formules Excel. Nous pouvons d'abord lire le fichier Excel avec `xlrd`, puis convertir le fichier Excel lu en un objet `Workbook` pour l'écriture à l'aide de la fonction `copy` fournie par la bibliothèque tierce `xlutils`. Lors de l'appel de la méthode `write`, vous pouvez écrire un objet `Formula` dans une cellule.

Le code pour effectuer des calculs avec formules est présenté ci-dessous.

```python
import xlrd
import xlwt
from xlutils.copy import copy

wb_for_read = xlrd.open_workbook('Données d'actions d'Alibaba 2020.xls')
sheet1 = wb_for_read.sheet_by_index(0)
nrows, ncols = sheet1.nrows, sheet1.ncols
wb_for_write = copy(wb_for_read)
sheet2 = wb_for_write.get_sheet(0)
sheet2.write(nrows, 4, xlwt.Formula(f'average(E2:E{nrows})'))
sheet2.write(nrows, 6, xlwt.Formula(f'sum(G2:G{nrows})'))
wb_for_write.save('Données d'actions d'Alibaba 2020 résumées.xls')
```

> **Remarque** : Le code ci-dessus présente quelques imperfections. Les lecteurs intéressés peuvent explorer par eux-mêmes et réfléchir à la manière de les résoudre.

### Résumé

Maîtriser la manipulation de fichiers Excel avec Python permet de résoudre de nombreuses tâches fastidieuses de traitement de feuilles de calcul Excel dans le travail quotidien. Les cas les plus courants sont la fusion de plusieurs fichiers Excel ayant le même format de données en un seul fichier, et l'extraction de données spécifiques à partir de plusieurs fichiers ou feuilles Excel. Bien sûr, pour traiter les données tabulaires, il peut être plus pratique d'utiliser l'une des bibliothèques d'analyse de données Python, comme pandas.