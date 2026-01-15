## Traitement d'images avec Python

### Notions de base

1. **Couleurs**. Si vous avez déjà peint avec des pigments, vous savez probablement qu'en mélangeant le rouge, le jaune et le bleu, on peut obtenir d'autres couleurs. En effet, ces trois couleurs sont les couleurs primaires en art, des couleurs fondamentales qui ne peuvent être décomposées. En informatique, nous pouvons superposer des lumières rouge, verte et bleue dans différentes proportions pour créer d'autres couleurs. Ainsi, ces trois couleurs sont les couleurs primaires additives en lumière. Dans les systèmes informatiques, une couleur est généralement représentée par une valeur RGB ou RGBA (où A représente le canal Alpha, qui détermine la transparence du pixel à travers l'image).

   | Nom         | Valeur RGB        | Nom         | Valeur RGB      |
   | :---------- | :---------------- | :---------- | :-------------- |
   | Blanc       | (255, 255, 255)   | Rouge       | (255, 0, 0)     |
   | Vert        | (0, 255, 0)       | Bleu        | (0, 0, 255)     |
   | Gris        | (128, 128, 128)   | Jaune       | (255, 255, 0)   |
   | Noir        | (0, 0, 0)         | Violet      | (128, 0, 128)   |

2. **Pixels**. Pour une image représentée par une séquence numérique, la plus petite unité est un petit carré de couleur unique sur l'image. Ces petits carrés ont une position précise et une valeur de couleur attribuée. La couleur et la position de ces petits carrés déterminent l'apparence finale de l'image. Ce sont des unités indivisibles, généralement appelées pixels (picture elements). Chaque image contient un certain nombre de pixels, qui déterminent la taille à laquelle l'image apparaît à l'écran. Si vous aimez prendre des photos ou des selfies, le terme pixel ne vous est pas étranger.

### Traiter des images avec Pillow

Pillow est un fork issu de la célèbre bibliothèque de traitement d'images Python PIL. Avec Pillow, vous pouvez effectuer diverses opérations telles que la compression et le traitement d'images. Installez Pillow avec la commande suivante.

```bash
pip install pillow
```

La classe la plus importante dans Pillow est `Image`. Vous pouvez lire une image via la fonction `open` du module `Image` et obtenir un objet de type `Image`.

1. Lire et afficher une image

   ```python
   from PIL import Image
   
   # Lire l'image pour obtenir un objet Image
   image = Image.open('guido.jpg')
   # Obtenir le format de l'image via l'attribut format de l'objet Image
   print(image.format)  # JPEG
   # Obtenir les dimensions de l'image via l'attribut size de l'objet Image
   print(image.size)    # (500, 750)
   # Obtenir le mode de l'image via l'attribut mode de l'objet Image
   print(image.mode)    # RGB
   # Afficher l'image via la méthode show de l'objet Image
   image.show()
   ```

2. Rogner une image

   ```python
   # Rogner l'image en spécifiant la zone de rognage via la méthode crop de l'objet Image
   image.crop((80, 20, 310, 360)).show()
   ```

3. Générer une miniature

   ```python
   # Générer une miniature de dimensions spécifiées via la méthode thumbnail de l'objet Image
   image.thumbnail((128, 128))
   image.show()
   ```

4. Redimensionner et coller une image

   ```python
   # Lire la photo de Luo Hao pour obtenir un objet Image
   luohao_image = Image.open('luohao.png')
   # Lire la photo de Guido pour obtenir un objet Image
   guido_image = Image.open('guido.jpg')
   # Découper la tête de Guido depuis sa photo
   guido_head = guido_image.crop((80, 20, 310, 360))
   width, height = guido_head.size
   # Utiliser la méthode resize de l'objet Image pour modifier les dimensions de l'image
   # Utiliser la méthode paste de l'objet Image pour coller la tête de Guido sur la photo de Luo Hao
   luohao_image.paste(guido_head.resize((int(width / 1.5), int(height / 1.5))), (172, 40))
   luohao_image.show()
   ```

5. Rotation et retournement

   ```python
   image = Image.open('guido.jpg')
   # Utiliser la méthode rotate de l'objet Image pour faire pivoter l'image
   image.rotate(45).show()
   # Utiliser la méthode transpose de l'objet Image pour retourner l'image
   # Image.FLIP_LEFT_RIGHT - retournement horizontal
   # Image.FLIP_TOP_BOTTOM - retournement vertical
   image.transpose(Image.FLIP_TOP_BOTTOM).show()
   ```

6. Manipuler les pixels

   ```python
   for x in range(80, 310):
       for y in range(20, 360):
           # Modifier le pixel spécifié de l'image via la méthode putpixel de l'objet Image
           image.putpixel((x, y), (128, 128, 128))
   image.show()
   ```

7. Effets de filtre

   ```python
   from PIL import ImageFilter
   
   # Appliquer un filtre à l'image via la méthode filter de l'objet Image
   # Le module ImageFilter contient de nombreux filtres prédéfinis et permet également de créer des filtres personnalisés
   image.filter(ImageFilter.CONTOUR).show()
   ```

### Dessiner avec Pillow

Pillow dispose d'un module appelé `ImageDraw`. La fonction `Draw` de ce module renvoie un objet `ImageDraw`. Grâce aux méthodes `arc`, `line`, `rectangle`, `ellipse`, `polygon`, etc., de l'objet `ImageDraw`, vous pouvez dessiner des arcs, des lignes, des rectangles, des ellipses, des polygones, etc., sur l'image. Vous pouvez également ajouter du texte à l'image via la méthode `text` de cet objet.

Pour dessiner une image comme celle ci-dessus, voici le code complet.

```python
import random

from PIL import Image, ImageDraw, ImageFont


def random_color():
    """Générer une couleur aléatoire"""
    red = random.randint(0, 255)
    green = random.randint(0, 255)
    blue = random.randint(0, 255)
    return red, green, blue


width, height = 800, 600
# Créer une image 800*600 avec un fond blanc
image = Image.new(mode='RGB', size=(width, height), color=(255, 255, 255))
# Créer un objet ImageDraw
drawer = ImageDraw.Draw(image)
# Obtenir un objet ImageFont en spécifiant la police et la taille
font = ImageFont.truetype('Kongxin.ttf', 32)
# Dessiner du texte via la méthode text de l'objet ImageDraw
drawer.text((300, 50), 'Hello, world!', fill=(255, 0, 0), font=font)
# Dessiner deux lignes diagonales via la méthode line de l'objet ImageDraw
drawer.line((0, 0, width, height), fill=(0, 0, 255), width=2)
drawer.line((width, 0, 0, height), fill=(0, 0, 255), width=2)
xy = width // 2 - 60, height // 2 - 60, width // 2 + 60, height // 2 + 60
# Dessiner un rectangle via la méthode rectangle de l'objet ImageDraw
drawer.rectangle(xy, outline=(255, 0, 0), width=2)
# Dessiner des ellipses via la méthode ellipse de l'objet ImageDraw
for i in range(4):
    left, top, right, bottom = 150 + i * 120, 220, 310 + i * 120, 380
    drawer.ellipse((left, top, right, bottom), outline=random_color(), width=8)
# Afficher l'image
image.show()
# Sauvegarder l'image
image.save('result.png')
```

> **Remarque** : Le fichier de police utilisé dans le code ci-dessus doit être préparé par vos soins. Choisissez un fichier de police que vous aimez et placez-le dans le répertoire du code.

### Résumé

Pour développer en Python, en plus de Pillow pour traiter les images, vous pouvez utiliser la bibliothèque OpenCV, plus puissante, pour le traitement graphique et d'images. OpenCV (**Open** Source **C**omputer **V**ision Library) est une bibliothèque de vision par ordinateur multiplateforme, utilisée pour développer des programmes de traitement d'images en temps réel, de vision par ordinateur et de reconnaissance de formes. Dans notre travail quotidien, de nombreuses tâches fastidieuses peuvent être traitées par des programmes Python. Le but de la programmation est de permettre à l'ordinateur de nous aider à résoudre des problèmes, réduisant ainsi le travail répétitif et ennuyeux. Grâce à ce chapitre, vous avez probablement ressenti le plaisir de dessiner et de modifier des images avec des programmes Python. En réalité, Python peut faire bien plus que cela. Continuez votre apprentissage.