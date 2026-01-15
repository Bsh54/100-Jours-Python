## Manipulation de fichiers Word et PowerPoint avec Python

Dans le travail quotidien, de nombreuses tâches simples et répétitives pourraient être confiées à un programme Python. Par exemple, générer en masse plusieurs fichiers Word ou PowerPoint à partir de fichiers modèles. Word est le traitement de texte développé par Microsoft, que tout le monde connaît probablement. De nombreux documents officiels dans le travail quotidien sont rédigés et édités avec Word. Actuellement, l'extension de fichier Word utilisée est généralement `.docx`. PowerPoint est le logiciel de présentation développé par Microsoft, membre de la suite Office. Il est largement utilisé par les professionnels, les enseignants, les étudiants, etc., et est souvent appelé "diapositives". En Python, vous pouvez utiliser la bibliothèque tierce `python-docx` pour manipuler Word, et `python-pptx` pour générer des PowerPoint.

### Manipulation de documents Word

Nous pouvons d'abord installer la bibliothèque tierce `python-docx` avec la commande suivante.

```bash
pip install python-docx
```

Selon la [documentation officielle](https://python-docx.readthedocs.io/en/latest/), nous pouvons utiliser le code suivant pour générer un document Word simple.

```python
from docx import Document
from docx.shared import Cm, Pt

from docx.document import Document as Doc

# Créer un objet Doc représentant le document Word
document = Document()  # type: Doc
# Ajouter un titre principal
document.add_heading('Apprendre Python avec plaisir', 0)
# Ajouter un paragraphe
p = document.add_paragraph('Python est un langage de programmation très populaire, il est')
run = p.add_run('simple')
run.bold = True
run.font.size = Pt(18)
p.add_run(' et ')
run = p.add_run('élégant')
run.font.size = Pt(18)
run.underline = True
p.add_run('.')

# Ajouter un titre de niveau 1
document.add_heading('Titre, niveau 1', level=1)
# Ajouter un paragraphe avec style
document.add_paragraph('Citation intense', style='Intense Quote')
# Ajouter une liste non ordonnée
document.add_paragraph(
    'premier élément de la liste non ordonnée', style='List Bullet'
)
document.add_paragraph(
    'deuxième élément de la liste non ordonnée', style='List Bullet'
)
# Ajouter une liste ordonnée
document.add_paragraph(
    'premier élément de la liste ordonnée', style='List Number'
)
document.add_paragraph(
    'deuxième élément de la liste ordonnée', style='List Number'
)

# Ajouter une image (assurez-vous que le chemin et l'image existent)
document.add_picture('resources/guido.jpg', width=Cm(5.2))

# Ajouter un saut de section
document.add_section()

records = (
    ('Luo Hao', 'M', '1995-5-5'),
    ('Sun Meili', 'F', '1992-2-2')
)
# Ajouter un tableau
table = document.add_table(rows=1, cols=3)
table.style = 'Dark List'
hdr_cells = table.rows[0].cells
hdr_cells[0].text = 'Nom'
hdr_cells[1].text = 'Sexe'
hdr_cells[2].text = 'Date de naissance'
# Ajouter des lignes au tableau
for name, sex, birthday in records:
    row_cells = table.add_row().cells
    row_cells[0].text = name
    row_cells[1].text = sex
    row_cells[2].text = birthday

# Ajouter un saut de page
document.add_page_break()

# Enregistrer le document
document.save('demo.docx')
```

> **Remarque** : Le commentaire `# type: Doc` à la ligne 7 du code ci-dessus est destiné à obtenir des suggestions de complétion de code dans PyCharm. Sans cela, PyCharm ne peut pas fournir de suggestions pour l'objet `Doc` dans la suite du code si le type de données spécifique n'est pas connu.

Exécutez le code ci-dessus et ouvrez le document Word généré. Le résultat ressemblera à l'image ci-dessous.

Pour un fichier Word existant, nous pouvons parcourir tous ses paragraphes et récupérer leur contenu avec le code suivant.

```python
from docx import Document
from docx.document import Document as Doc

doc = Document('resources/certificat_de_depart.docx')  # type: Doc
for no, p in enumerate(doc.paragraphs):
    print(no, p.text)
```

> **Remarque** : Si vous avez besoin du fichier Word mentionné dans le code ci-dessus, vous pouvez l'obtenir via le lien Baidu Netdisk suivant. Lien : https://pan.baidu.com/s/1rQujl5RQn9R7PadB2Z5g_g Code : e7b4.

Le contenu lu est le suivant.

```
0 
1 C E R T I F I C A T  D E  D E P A R T
2 
3 Je soussigné(e) certifie que Wang Dachui, numéro de carte d'identité : 100200199512120001, a travaillé dans notre unité du 7 août 2018 au 28 juin 2020, dans le département développement en tant qu'ingénieur de développement Java, sans comportement inapproprié pendant son emploi. Pour des raisons personnelles, son contrat de travail a pris fin le 28 juin 2020. Tous les frais financiers ont été réglés et les formalités de rupture de la relation de travail ont été effectuées. Aucun litige relatif au travail n'existe entre les deux parties.
4 
5 En foi de quoi, le présent certificat est délivré.
6 
7 
8 Nom de l'entreprise (sceau) : Chengdu Fengcheche Technology Co., Ltd.
9    			28 juin 2020
```

À ce stade, de nombreux lecteurs ont probablement réalisé que nous pouvons créer un modèle à partir du certificat de départ ci-dessus, en remplaçant les informations telles que le nom, le numéro d'identité, les dates d'entrée et de départ par des espaces réservés. En remplaçant ces espaces réservés, nous pouvons écrire les informations correspondantes en fonction des besoins réels, générant ainsi des documents Word en masse.

Suivant cette idée, nous éditions d'abord un fichier modèle pour le certificat de départ, comme illustré ci-dessous.

Ensuite, nous lisons ce fichier, remplaçons les espaces réservés par les informations réelles, et générons un nouveau document Word, comme suit.

```python
from docx import Document
from docx.document import Document as Doc

# Enregistrer les informations réelles dans une liste sous forme de dictionnaires
employees = [
    {
        'name': 'Luo Hao',
        'id': '100200198011280001',
        'sdate': '1er mars 2008',
        'edate': '29 février 2012',
        'department': 'Développement de produits',
        'position': 'Architecte',
        'company': 'Chengdu Huawei Technologies Co., Ltd.'
    },
    {
        'name': 'Wang Dachui',
        'id': '510210199012125566',
        'sdate': '1er janvier 2019',
        'edate': '30 avril 2021',
        'department': 'Développement de produits',
        'position': 'Développeur Python',
        'company': 'Chengdu Gudao Technology Co., Ltd.'
    },
    {
        'name': 'Li Yuanfang',
        'id': '2102101995103221599',
        'sdate': '10 mai 2020',
        'edate': '5 mars 2021',
        'department': 'Développement de produits',
        'position': 'Développeur Java',
        'company': 'Tongcheng Enterprise Management Group Co., Ltd.'
    },
]
# Parcourir la liste pour générer des documents Word en masse
for emp_dict in employees:
    # Lire le fichier modèle de certificat de départ
    doc = Document('resources/certificat_de_depart_modele.docx')  # type: Doc
    # Parcourir tous les paragraphes à la recherche des espaces réservés
    for p in doc.paragraphs:
        if '{' not in p.text:
            continue
        # Ne pas modifier directement le contenu du paragraphe, sinon le style sera perdu
        # Il faut donc parcourir les éléments du paragraphe et effectuer un remplacement
        for run in p.runs:
            if '{' not in run.text:
                continue
            # Remplacer l'espace réservé par le contenu réel
            start, end = run.text.find('{'), run.text.find('}')
            key, place_holder = run.text[start + 1:end], run.text[start:end + 1]
            run.text = run.text.replace(place_holder, emp_dict[key])
    # Enregistrer un document Word pour chaque personne
    doc.save(f'{emp_dict["name"]}_certificat_de_depart.docx')
```

Exécutez le code ci-dessus. Trois documents Word seront générés dans le répertoire courant, comme illustré ci-dessous.

### Générer des PowerPoint

Nous devons d'abord installer la bibliothèque tierce `python-pptx` avec la commande suivante.

```bash
pip install python-pptx
```

Manipuler le contenu de PowerPoint avec Python n'étant pas un scénario d'application très courant, je ne vais pas m'étendre ici. Les lecteurs intéressés peuvent consulter la [documentation officielle de python-pptx](https://python-pptx.readthedocs.io/en/latest/). Je ne vais montrer qu'un exemple de code issu de la documentation officielle.

```python
from pptx import Presentation

# Créer un objet présentation
pres = Presentation()

# Ajouter une diapositive en utilisant une mise en page de titre
title_slide_layout = pres.slide_layouts[0]
slide = pres.slides.add_slide(title_slide_layout)
# Obtenir le titre et le sous-titre
title = slide.shapes.title
subtitle = slide.placeholders[1]
# Éditer le titre et le sous-titre
title.text = "Bienvenue à Python"
subtitle.text = "La vie est courte, j'utilise Python"

# Ajouter une diapositive avec une mise en page à puces
bullet_slide_layout = pres.slide_layouts[1]
slide = pres.slides.add_slide(bullet_slide_layout)
# Obtenir toutes les formes sur la diapositive
shapes = slide.shapes
# Obtenir le titre et le corps
title_shape = shapes.title
body_shape = shapes.placeholders[1]
# Éditer le titre
title_shape.text = 'Introduction'
# Éditer le contenu du corps
tf = body_shape.text_frame
tf.text = 'Histoire de Python'
# Ajouter un paragraphe de niveau 1
p = tf.add_paragraph()
p.text = 'Fin 1989'
p.level = 1
# Ajouter un paragraphe de niveau 2
p = tf.add_paragraph()
p.text = 'Guido a commencé à écrire l\'interpréteur pour Python.'
p.level = 2

# Enregistrer la présentation
pres.save('test.pptx')
```

Exécutez le code ci-dessus. Le fichier PowerPoint généré ressemblera à l'image ci-dessous.

### Résumé

Résoudre les problèmes d'automatisation bureautique avec des programmes Python est vraiment impressionnant. Cela nous libère des tâches fastidieuses et ennuyeuses. Écrire ce genre de code, c'est faire quelque chose d'utile une fois pour toutes. Même si le processus d'écriture du code n'est pas toujours agréable, utiliser ces codes devrait l'être.