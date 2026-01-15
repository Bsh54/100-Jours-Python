## Manipulation de fichiers PDF avec Python

PDF signifie Portable Document Format. Ces fichiers utilisent généralement l'extension `.pdf`. Dans le travail de développement quotidien, les tâches les plus courantes sont l'extraction de texte à partir de PDF et la génération de documents PDF à partir de contenu existant.

### Extraire du texte d'un PDF

En Python, vous pouvez utiliser la bibliothèque tierce `PyPDF2` pour lire des fichiers PDF. Installez-la avec la commande suivante.

```bash
pip install PyPDF2
```

`PyPDF2` ne peut pas extraire des images, des graphiques ou d'autres médias d'un document PDF, mais il peut extraire du texte et le retourner sous forme de chaîne Python.

```python
import PyPDF2

reader = PyPDF2.PdfReader('test.pdf')
for page in reader.pages:
    print(page.extract_text())
```

> **Remarque** : Les fichiers PDF utilisés dans ce chapitre peuvent être obtenus via le lien Baidu Netdisk suivant. Lien : https://pan.baidu.com/s/1rQujl5RQn9R7PadB2Z5g_g Code : e7b4.

Bien sûr, `PyPDF2` ne peut pas extraire du texte de n'importe quel document PDF. À ma connaissance, il n'existe pas de solution particulièrement bonne à ce problème, surtout lors de l'extraction de texte chinois. Il existe de nombreux articles en ligne expliquant comment extraire du texte de PDF. Je vous recommande de lire [《Trois outils puissants pour aider Python à extraire des informations de documents PDF》](https://cloud.tencent.com/developer/article/1395339) pour en savoir plus.

Vous pouvez également utiliser directement un outil en ligne de commande tiers pour extraire du texte d'un fichier PDF, comme suit.

```bash
pip install pdfminer.six
pdf2text.py test.pdf
```

### Rotation et superposition de pages

Dans le code ci-dessus, l'objet `PdfFileReader` est créé pour lire le document PDF. Sa méthode `getPage` peut obtenir une page spécifique du document PDF et retourner un objet `PageObject`. Les méthodes `rotateClockwise` et `rotateCounterClockwise` de l'objet `PageObject` permettent de faire pivoter la page dans le sens horaire et antihoraire. La méthode `addBlankPage` de l'objet `PageObject` permet d'ajouter une nouvelle page vierge. Voici le code correspondant.

```python
reader = PyPDF2.PdfReader('XGBoost.pdf')
writer = PyPDF2.PdfWriter()

for no, page in enumerate(reader.pages):
    if no % 2 == 0:
        new_page = page.rotate(-90)
    else:
        new_page = page.rotate(90)
    writer.add_page(new_page)

with open('temp.pdf', 'wb') as file_obj:
    writer.write(file_obj)
```

### Chiffrer un fichier PDF

L'objet `PdfFileWrite` de `PyPDF2` permet de chiffrer un document PDF. Si vous devez définir un mot de passe d'accès uniforme pour une série de documents PDF, l'utilisation d'un programme Python est très pratique.

```python
import PyPDF2

reader = PyPDF2.PdfReader('XGBoost.pdf')
writer = PyPDF2.PdfWriter()

for page in reader.pages:
    writer.add_page(page)
    
writer.encrypt('motdepasse')

with open('temp.pdf', 'wb') as file_obj:
    writer.write(file_obj)
```

### Ajout en lot de filigranes

L'objet `PageObject` mentionné précédemment a également une méthode `mergePage`, qui permet de superposer deux pages PDF. Grâce à cette opération, il est facile d'ajouter un filigrane à un fichier PDF. Par exemple, pour ajouter un filigrane au fichier "XGBoost.pdf", nous pouvons d'abord préparer un fichier PDF fournissant la page de filigrane, puis lire l'objet `PageObject` contenant le filigrane. Ensuite, nous parcourons chaque page du fichier "XGBoost.pdf", obtenons l'objet `PageObject` et utilisons la méthode `mergePage` pour fusionner la page de filigrane avec la page originale. Voici le code.

```python
reader1 = PyPDF2.PdfReader('XGBoost.pdf')
reader2 = PyPDF2.PdfReader('filigrane.pdf')
writer = PyPDF2.PdfWriter()
watermark_page = reader2.pages[0]

for page in reader1.pages:
    page.merge_page(watermark_page)
    writer.add_page(page)

with open('temp.pdf', 'wb') as file_obj:
    writer.write(file_obj)
```

Si vous le souhaitez, vous pouvez même utiliser des filigranes différents pour les pages paires et impaires. Réfléchissez à la manière de le faire.

### Créer un fichier PDF

La création de documents PDF nécessite la bibliothèque tierce `reportlab`. Installez-la comme suit.

```bash
pip install reportlab
```

Voici un exemple montrant l'utilisation de `reportlab`.

```python
from reportlab.lib.pagesizes import A4
from reportlab.pdfbase import pdfmetrics
from reportlab.pdfbase.ttfonts import TTFont
from reportlab.pdfgen import canvas

pdf_canvas = canvas.Canvas('resources/demo.pdf', pagesize=A4)
width, height = A4

# Dessin
image = canvas.ImageReader('resources/guido.jpg')
pdf_canvas.drawImage(image, 20, height - 395, 250, 375)

# Afficher la page courante
pdf_canvas.showPage()

# Enregistrer les fichiers de police
pdfmetrics.registerFont(TTFont('Font1', 'resources/fonts/Vera.ttf'))
pdfmetrics.registerFont(TTFont('Font2', 'resources/fonts/QingWaShiTouTi.ttf'))

# Écrire du texte
pdf_canvas.setFont('Font2', 40)
pdf_canvas.setFillColorRGB(0.9, 0.5, 0.3, 1)
pdf_canvas.drawString(width // 2 - 120, height // 2, 'Bonjour le monde !')
pdf_canvas.setFont('Font1', 40)
pdf_canvas.setFillColorRGB(0, 1, 0, 0.5)
pdf_canvas.rotate(18)
pdf_canvas.drawString(250, 250, 'hello, world!')

# Sauvegarder
pdf_canvas.save()
```

Si le code ci-dessus n'est pas très clair, ce n'est pas grave. Lorsque vous aurez vraiment besoin de créer des documents PDF avec Python, étudiez attentivement la [documentation officielle de reportlab](https://www.reportlab.com/docs/reportlab-userguide.pdf).

> **Remarque** : L'image et les polices utilisées dans le code ci-dessus peuvent être obtenues via le lien Baidu Netdisk suivant. Lien : https://pan.baidu.com/s/1rQujl5RQn9R7PadB2Z5g_g Code : e7b4.

### Résumé

Après avoir étudié le contenu ci-dessus, vous devriez maintenant savoir comment traiter des tâches comme la fusion de plusieurs fichiers PDF avec du code Python. Essayez par vous-même !