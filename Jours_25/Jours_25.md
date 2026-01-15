## Lecture et écriture de fichiers Excel en Python - Partie 2

### Présentation d'Excel

Excel est un logiciel de feuille de calcul développé par Microsoft pour les systèmes d'exploitation Windows et macOS. Grâce à son interface intuitive, ses excellentes fonctionnalités de calcul et ses outils de graphiques, ainsi qu'à son marketing réussi, Excel est depuis longtemps le logiciel de traitement de données le plus populaire pour les ordinateurs personnels. Bien sûr, Excel a également de nombreux concurrents, tels que Google Sheets, LibreOffice Calc, Numbers, etc., qui sont essentiellement compatibles avec Excel, du moins capables de lire et d'écrire les versions plus récentes de fichiers Excel, mais ce n'est pas le sujet principal ici. Maîtriser l'utilisation de Python pour manipuler des fichiers Excel peut rendre les tâches d'automatisation du travail quotidien plus faciles et agréables. De plus, dans de nombreux projets commerciaux, l'importation et l'exportation de fichiers Excel sont des fonctionnalités particulièrement courantes.

Dans ce chapitre, nous continuons à expliquer comment manipuler des fichiers Excel avec une autre bibliothèque tierce, `openpyxl`. Il faut d'abord l'installer.

```bash
pip install openpyxl
```

L'avantage de `openpyxl` est que, lorsque nous ouvrons un fichier Excel, nous pouvons à la fois le lire et y écrire, et la facilité d'utilisation est meilleure qu'avec `xlwt` et `xlrd`. De plus, pour l'édition des styles et les calculs de formules, utiliser `openpyxl` est beaucoup plus simple que les méthodes expliquées dans le chapitre précédent. `openpyxl` prend également en charge les tableaux croisés dynamiques et l'insertion de graphiques, entre autres fonctionnalités très puissantes. Il est important de souligner à nouveau que `openpyxl` ne prend pas en charge la manipulation des fichiers Excel antérieurs à Office 2007.

### Lire un fichier Excel

Par exemple, dans le dossier courant, il y a un fichier Excel nommé "Données d'actions d'Alibaba 2020.xlsx". Pour lire et afficher son contenu, vous pouvez utiliser le code ci-dessous.

```python
import datetime

import openpyxl

# Charger un classeur ---> Workbook
wb = openpyxl.load_workbook('Données d'actions d'Alibaba 2020.xlsx')
# Obtenir les noms des feuilles de calcul
print(wb.sheetnames)
# Obtenir une feuille de calcul ---> Worksheet
sheet = wb.worksheets[0]
# Obtenir la plage des cellules
print(sheet.dimensions)
# Obtenir le nombre de lignes et de colonnes
print(sheet.max_row, sheet.max_column)

# Obtenir la valeur d'une cellule spécifique
print(sheet.cell(3, 3).value)
print(sheet['C3'].value)
print(sheet['G255'].value)

# Obtenir plusieurs cellules (tuple imbriqué)
print(sheet['A2:C5'])

# Lire les données de toutes les cellules
for row_ch in range(2, sheet.max_row + 1):
    for col_ch in 'ABCDEFG':
        value = sheet[f'{col_ch}{row_ch}'].value
        if type(value) == datetime.datetime:
            print(value.strftime('%Y年%m月%d日'), end='\t')
        elif type(value) == int:
            print(f'{value:<10d}', end='\t')
        elif type(value) == float:
            print(f'{value:.4f}', end='\t')
        else:
            print(value, end='\t')
    print()
```

> **Remarque** : Le fichier Excel "Données d'actions d'Alibaba 2020.xlsx" utilisé dans le code ci-dessus peut être obtenu via le lien Baidu Netdisk fourni à la fin. Lien : https://pan.baidu.com/s/1rQujl5RQn9R7PadB2Z5g_g Code : e7b4.

Il est important de noter que `openpyxl` offre deux façons d'obtenir une cellule spécifique. L'une est via la méthode `cell`. Attention, les indices de ligne et de colonne de cette méthode commencent à `1`, pour respecter les habitudes des utilisateurs d'Excel. L'autre est via l'opérateur d'indexation, en spécifiant les coordonnées de la cellule, par exemple `C3`, `G255`, pour obtenir la cellule correspondante. Ensuite, via l'attribut `value` de l'objet cellule, vous pouvez obtenir la valeur de la cellule. Grâce au code ci-dessus, vous avez probablement remarqué que vous pouvez obtenir plusieurs cellules via une opération de slice comme `sheet['A2:C5']` ou `sheet['A2':'C5']`. Cette opération renvoie un tuple imbriqué, ce qui équivaut à obtenir plusieurs lignes et colonnes.

### Écrire dans un fichier Excel

Utilisons maintenant `openpyxl` pour écrire dans un fichier Excel.

```python
import random

import openpyxl

# Étape 1 : Créer un classeur (Workbook)
wb = openpyxl.Workbook()

# Étape 2 : Ajouter une feuille de calcul (Worksheet)
sheet = wb.active
sheet.title = 'Résultats finaux'

titles = ('Nom', 'Chinois', 'Mathématiques', 'Anglais')
for col_index, title in enumerate(titles):
    sheet.cell(1, col_index + 1, title)

names = ('Guan Yu', 'Zhang Fei', 'Zhao Yun', 'Ma Chao', 'Huang Zhong')
for row_index, name in enumerate(names):
    sheet.cell(row_index + 2, 1, name)
    for col_index in range(2, 5):
        sheet.cell(row_index + 2, col_index, random.randrange(50, 101))

# Étape 4 : Enregistrer le classeur
wb.save('Tableau des résultats d'examen.xlsx')
```

### Ajuster les styles et calculs avec formules

Lors de l'utilisation d'`openpyxl` pour manipuler Excel, si vous souhaitez ajuster le style d'une cellule, vous pouvez le faire directement via les attributs de l'objet cellule (`Cell`). Les attributs de l'objet cellule incluent la police (`font`), l'alignement (`alignment`), les bordures (`border`), etc. Pour plus de détails, référez-vous à la [documentation officielle d'openpyxl](https://openpyxl.readthedocs.io/en/stable/index.html). Lors de l'utilisation d'`openpyxl`, si vous avez besoin d'effectuer des calculs avec formules, vous pouvez le faire exactement comme dans Excel. Voici le code correspondant.

```python
import openpyxl
from openpyxl.styles import Font, Alignment, Border, Side

# Alignement
alignment = Alignment(horizontal='center', vertical='center')
# Style de bordure
side = Side(color='ff7f50', style='mediumDashed')

wb = openpyxl.load_workbook('Tableau des résultats d'examen.xlsx')
sheet = wb.worksheets[0]

# Ajuster la hauteur des lignes et la largeur des colonnes
sheet.row_dimensions[1].height = 30
sheet.column_dimensions['E'].width = 120

sheet['E1'] = 'Moyenne'
# Définir la police
sheet.cell(1, 5).font = Font(size=18, bold=True, color='ff1493', name='KaiTi')
# Définir l'alignement
sheet.cell(1, 5).alignment = alignment
# Définir les bordures de la cellule
sheet.cell(1, 5).border = Border(left=side, top=side, right=side, bottom=side)
for i in range(2, 7):
    # Calcul de la moyenne de chaque étudiant avec une formule
    sheet[f'E{i}'] = f'=average(B{i}:D{i})'
    sheet.cell(i, 5).font = Font(size=12, color='4169e1', italic=True)
    sheet.cell(i, 5).alignment = alignment

wb.save('Tableau des résultats d'examen.xlsx')
```

### Générer des graphiques statistiques

Avec la bibliothèque `openpyxl`, vous pouvez insérer directement des graphiques statistiques dans Excel. La méthode est globalement la même que pour insérer un graphique dans Excel. Vous pouvez créer un objet graphique d'un type spécifié, puis configurer le graphique via les propriétés de cet objet. Le plus important est de lier les données au graphique, c'est-à-dire ce que représente l'axe horizontal, ce que représente l'axe vertical, et les valeurs spécifiques. Enfin, vous pouvez ajouter l'objet graphique à la feuille de calcul. Voici le code correspondant.

```python
from openpyxl import Workbook
from openpyxl.chart import BarChart, Reference

wb = Workbook(write_only=True)
sheet = wb.create_sheet()

rows = [
    ('Catégorie', 'Groupe de vente A', 'Groupe de vente B'),
    ('Téléphone', 40, 30),
    ('Tablette', 50, 60),
    ('Ordinateur portable', 80, 70),
    ('Périphériques', 20, 10),
]

# Ajouter des lignes à la feuille de calcul
for row in rows:
    sheet.append(row)

# Créer un objet graphique
chart = BarChart()
chart.type = 'col'
chart.style = 10
# Définir le titre du graphique
chart.title = 'Graphique des ventes'
# Définir le titre de l'axe vertical du graphique
chart.y_axis.title = 'Quantité vendue'
# Définir le titre de l'axe horizontal du graphique
chart.x_axis.title = 'Catégorie de produit'
# Définir la plage des données
data = Reference(sheet, min_col=2, min_row=1, max_row=5, max_col=3)
# Définir la plage des catégories
cats = Reference(sheet, min_col=1, min_row=2, max_row=5)
# Ajouter des données au graphique
chart.add_data(data, titles_from_data=True)
# Définir les catégories du graphique
chart.set_categories(cats)
chart.shape = 4
# Ajouter le graphique à la cellule spécifiée de la feuille de calcul
sheet.add_chart(chart, 'A10')

wb.save('demo.xlsx')
```

Exécutez le code ci-dessus et ouvrez le fichier Excel généré. Le résultat ressemblera à l'image ci-dessous.

### Résumé

Maîtriser la manipulation de fichiers Excel avec Python permet de résoudre de nombreuses tâches fastidieuses de traitement de feuilles de calcul Excel dans le travail quotidien. Les cas les plus courants sont la fusion de plusieurs fichiers Excel ayant le même format de données en un seul fichier, et l'extraction de données spécifiques à partir de plusieurs fichiers ou feuilles Excel. Si le volume de données est important ou si le traitement des données est complexe, nous recommandons d'utiliser l'une des bibliothèques d'analyse de données Python, comme pandas.