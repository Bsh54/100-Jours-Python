## Structure conditionnelle (branchement)

Jusqu'à présent, les programmes Python que nous avons écrits exécutent les instructions une par une, dans l'ordre séquentiel. Cette structure de code est appelée **structure séquentielle**. Cependant, la structure séquentielle seule ne peut pas résoudre tous les problèmes. Par exemple, imaginons que nous concevions un jeu où la condition pour passer le premier niveau est que le joueur obtienne 1000 points. Après le premier niveau, nous devons décider, en fonction du score du joueur, s'il passe au deuxième niveau ou si le jeu affiche "Game Over". Dans ce scénario, notre code se divise en deux branches, et une seule sera exécutée. Il existe de nombreux scénarios similaires. Nous appelons cette structure la **structure conditionnelle** ou **structure de sélection**. Prenez une minute, vous devriez pouvoir trouver au moins cinq exemples similaires !

### Utilisation de `if` et `else` pour construire une structure conditionnelle

En Python, les mots-clés les plus couramment utilisés pour construire une structure conditionnelle sont `if`, `elif` et `else`. Un **mot-clé** est un mot ayant une signification spéciale dans le langage de programmation, et il est évident que vous ne pouvez pas l'utiliser comme nom de variable. Bien sûr, nous n'utilisons pas toujours les trois mots-clés pour construire une structure conditionnelle. Illustrons cela par un exemple : écrivons un calculateur d'**indice de masse corporelle (IMC)**. L'IMC est un indicateur international couramment utilisé pour évaluer la corpulence et la santé d'une personne. La formule est la suivante. Généralement, on considère que $\small{18.5 \le IMC < 24}$ correspond à une fourchette normale, $\small{IMC < 18.5}$ indique une insuffisance pondérale, $\small{IMC \ge 24}$ indique un surpoids, et $\small{IMC \ge 27}$ entre dans la catégorie de l'obésité.

$$
IMC = \frac{poids}{taille^{2}}
$$

> **Remarque** : Dans la formule ci-dessus, le poids est en kilogrammes (kg) et la taille en mètres (m).

```python
"""
Calculateur d'IMC

Version : 1.0
Auteur : Shadrak BESSANH
"""
height = float(input('Taille (cm) : '))
weight = float(input('Poids (kg) : '))
bmi = weight / (height / 100) ** 2
print(f'{bmi = :.1f}')
if 18.5 <= bmi < 24:
    print('Vous avez une superbe silhouette !')
```

> **Astuce** : L'instruction `if` se termine par un `:` (deux-points saisis en mode de saisie anglais). Les caractères spéciaux comme `'`, `"`, `=`, `(`, `)` dans le programme doivent également être saisis en mode anglais, comme indiqué précédemment. De nombreux débutants négligent souvent ce point, et lors de l'exécution du code, ils voient une multitude de messages d'erreur. Bien sûr, en lisant attentivement les messages d'erreur, il est facile de découvrir où se trouve le problème, mais **il est fortement recommandé** de **basculer en mode de saisie anglais** lors de l'écriture du code, afin d'éviter de nombreux désagréments inutiles.

Dans le code ci-dessus, après le calcul et l'affichage de l'IMC, nous avons ajouté une structure conditionnelle. Si la condition $\small{18.5 \le IMC < 24}$ est remplie, le programme affiche "Vous avez une superbe silhouette !". Sinon, cette sortie n'apparaît pas. C'est ce que nous avons mentionné précédemment : le code peut avoir différents chemins d'exécution, et certaines lignes de code ne sont pas nécessairement exécutées. Après le mot-clé `if`, nous donnons une expression `18.5 <= bmi < 24`. Nous avons dit précédemment que les opérations relationnelles produisent des valeurs booléennes. Si la valeur booléenne après `if` est `True`, alors l'instruction `print('Vous avez une superbe silhouette !')`, indentée de quatre espaces sous `if`, sera exécutée. Testons d'abord le code ci-dessus avec quelques jeux de données, comme indiqué ci-dessous.

Premier jeu de données :

```
Taille (cm) : 175
Poids (kg) : 68
bmi = 22.2
Vous avez une superbe silhouette !
```

Deuxième jeu de données :

```
Taille (cm) : 175
Poids (kg) : 95
bmi = 31.0
```

Troisième jeu de données :

```
Taille (cm) : 175
Poids (kg) : 50
bmi = 16.3
```

Seul le premier jeu de données (taille et poids) donne un IMC compris entre 18,5 et 24, déclenchant ainsi la condition `if` et affichant "Vous avez une superbe silhouette". Il est important de noter que, contrairement à des langages comme C, C++ ou Java, Python n'utilise pas d'accolades pour délimiter les blocs de code, mais **utilise l'indentation pour représenter la structure hiérarchique du code**. Si plusieurs instructions doivent être exécutées lorsque la condition `if` est remplie, il suffit qu'elles aient la même indentation. En d'autres termes, plusieurs lignes d'instructions consécutives avec la même indentation appartiennent au même **bloc de code** et constituent un ensemble d'exécution. L'indentation peut utiliser n'importe quel nombre d'espaces, mais **on utilise généralement 4 espaces**. Il est fortement déconseillé **d'utiliser la touche Tab pour l'indentation**. Si vous avez cette habitude, vous pouvez configurer votre éditeur de code pour convertir automatiquement 1 tabulation en 4 espaces. De nombreux éditeurs de code prennent en charge cette fonctionnalité, et PyCharm est configuré ainsi par défaut. Autre point : dans des langages comme C, C++ ou Java, `18.5 <= bmi < 24` doit être écrit sous forme de deux conditions `bmi >= 18.5` et `bmi < 24`, reliées par l'opérateur ET. En Python, on peut aussi le faire ; par exemple, l'instruction `if` précédente pourrait être écrite `if bmi >= 18.5 and bmi < 24:`, mais ce n'est pas nécessaire. `if 18.5 <= bmi < 24:` n'est-il pas plus élégant ? Voici le code Java équivalent. Il n'est pas grave de ne pas comprendre le code Java, l'objectif est de sentir la différence de syntaxe avec Python.

```java
import java.util.Scanner;

class Test {

    public static void main(String[] args) {
        try (Scanner sc = new Scanner(System.in)) {
            System.out.print("Taille (cm): ");
            double height = sc.nextDouble();
            System.out.print("Poids (kg): ");
            double weight = sc.nextDouble();
            double bmi = weight / Math.pow(height / 100, 2);
            System.out.printf("bmi = %.1f\n", bmi);
            if (bmi >= 18.5 && bmi < 24) {
                System.out.println("Vous avez une superbe silhouette !");
            }
        }
    }
}
```

> **Remarque** : Le code Java ci-dessus correspond à la version 1.0 du calculateur d'IMC. Beaucoup de gens aiment Python pour une bonne raison : il résout souvent les mêmes problèmes avec moins de code.

Modifions maintenant légèrement le code précédent pour donner un message d'avertissement lorsque l'IMC ne satisfait pas $\small{18.5 \le IMC < 24}$. Nous pouvons ajouter un bloc `else` après le bloc `if`. Il sera exécuté lorsque la condition de l'instruction `if` n'est pas remplie, comme indiqué ci-dessous. Clairement, soit `print('Vous avez une superbe silhouette !')` sous `if`, soit `print('Votre silhouette n'est pas assez standard !')` sous `else` sera exécuté.

```python
"""
Calculateur d'IMC

Version : 1.1
Auteur : Shadrak BESSANH
"""
height = float(input('Taille (cm) : '))
weight = float(input('Poids (kg) : '))
bmi = weight / (height / 100) ** 2
print(f'{bmi = :.1f}')
if 18.5 <= bmi < 24:
    print('Vous avez une superbe silhouette !')
else:
    print('Votre silhouette n'est pas assez standard !')
```

Pour donner des informations plus précises, nous pouvons à nouveau modifier le code ci-dessus et ajouter plus de branches à la structure conditionnelle à l'aide du mot-clé `elif`, comme indiqué ci-dessous.

```python
"""
Calculateur d'IMC

Version : 1.2
Auteur : Shadrak BESSANH
"""
height = float(input('Taille (cm) : '))
weight = float(input('Poids (kg) : '))
bmi = weight / (height / 100) ** 2
print(f'{bmi = :.1f}')
if bmi < 18.5:
    print('Votre poids est insuffisant !')
elif bmi < 24:
    print('Vous avez une superbe silhouette !')
elif bmi < 27:
    print('Vous êtes en surpoids !')
elif bmi < 30:
    print('Vous êtes légèrement obèse !')
elif bmi < 35:
    print('Vous êtes modérément obèse !')
else:
    print('Vous êtes sévèrement obèse !')
```

Testons à nouveau le code ci-dessus avec les trois jeux de données précédents et voyons les résultats.

Premier jeu de données :

```
Taille (cm) : 175
Poids (kg) : 68
bmi = 22.2
Vous avez une superbe silhouette !
```

Deuxième jeu de données :

```
Taille (cm) : 175
Poids (kg) : 95
bmi = 31.0
Vous êtes modérément obèse !
```

Troisième jeu de données :

```
Taille (cm) : 175
Poids (kg) : 50
bmi = 16.3
Votre poids est insuffisant !
```

### Utilisation de `match` et `case` pour construire une structure conditionnelle

Python 3.10 a introduit une nouvelle façon de construire des structures conditionnelles, utilisant les mots-clés `match` et `case`, permettant de créer facilement des structures à plusieurs branches. La documentation officielle de Python, en présentant cette nouvelle syntaxe, donne un exemple intéressant de reconnaissance des codes d'état de réponse HTTP (affichant la description correspondante en fonction du code d'état HTTP). Si vous ne savez pas ce qu'est un code d'état HTTP, vous pouvez consulter la [documentation](https://developer.mozilla.org/fr/docs/Web/HTTP/Status) sur MDN. Modifions légèrement l'exemple de la documentation officielle pour expliquer cette syntaxe. Regardons d'abord le code implémenté avec la structure `if-else`.

```python
status_code = int(input('Code d'état de réponse : '))
if status_code == 400:
    description = 'Bad Request'
elif status_code == 401:
    description = 'Unauthorized'
elif status_code == 403:
    description = 'Forbidden'
elif status_code == 404:
    description = 'Not Found'
elif status_code == 405:
    description = 'Method Not Allowed'
elif status_code == 418:
    description = 'I am a teapot'
elif status_code == 429:
    description = 'Too many requests'
else:
    description = 'Unknown status Code'
print('Description du code d'état :', description)
```

Résultat de l'exécution :

```
Code d'état de réponse : 403
Description du code d'état : Forbidden
```

Voici le code implémenté avec la syntaxe `match-case`. Bien que le résultat soit identique, le code est plus simple et élégant.

```python
status_code = int(input('Code d'état de réponse : '))
match status_code:
    case 400: description = 'Bad Request'
    case 401: description = 'Unauthorized'
    case 403: description = 'Forbidden'
    case 404: description = 'Not Found'
    case 405: description = 'Method Not Allowed'
    case 418: description = 'I am a teapot'
    case 429: description = 'Too many requests'
    case _: description = 'Unknown Status Code'
print('Description du code d'état :', description)
```

> **Remarque** : L'instruction `case _` dans le code agit comme un caractère générique. Si aucune des branches précédentes ne correspond, le code exécutera `case _`. `case _` est optionnel ; toutes les structures conditionnelles n'ont pas besoin d'une option générique. Si `case _` est présent, il doit être placé à la fin de la structure conditionnelle. S'il y a d'autres branches après lui, elles seront inaccessibles.

Bien sûr, la syntaxe `match-case` offre de nombreuses fonctionnalités avancées. L'une d'elles est le **modèle de fusion** (merge pattern). Par exemple, si nous voulons regrouper les codes d'état `401`, `403` et `404` dans une branche, et `400` et `405` dans une autre branche, tout en laissant les autres inchangés, le code peut être écrit comme suit.

```python
status_code = int(input('Code d'état de réponse : '))
match status_code:
    case 400 | 405: description = 'Invalid Request'
    case 401 | 403 | 404: description = 'Not Allowed'
    case 418: description = 'I am a teapot'
    case 429: description = 'Too many requests'
    case _: description = 'Unknown Status Code'
print('Description du code d'état :', description)
```

Résultat de l'exécution :

```
Code d'état de réponse : 403
Description du code d'état : Not Allowed
```

### Applications des structures conditionnelles

#### Exemple 1 : Évaluation d'une fonction par morceaux

Étant donné la fonction par morceaux suivante, saisir `x` et calculer `y`.

$$
y = \begin{cases} 3x - 5, & (x \gt 1) \\\\ x + 2, & (-1 \le x \le 1) \\\\ 5x + 3, & (x \lt -1) \end{cases}
$$

```python
"""
Évaluation d'une fonction par morceaux

Version : 1.0
Auteur : Shadrak BESSANH
"""
x = float(input('x = '))
if x > 1:
    y = 3 * x - 5
elif x >= -1:
    y = x + 2
else:
    y = 5 * x + 3
print(f'{y = }')
```

Selon les besoins du développement, les structures conditionnelles peuvent être **imbriquées**. Autrement dit, dans les blocs de code `if`, `elif` ou `else` d'une structure conditionnelle, on peut introduire une nouvelle structure conditionnelle. Par exemple, si la condition `if` est remplie, cela signifie que le joueur a réussi le niveau, mais après avoir réussi, nous devons évaluer sa performance en fonction du nombre de trésors ou d'objets obtenus (par exemple, attribuer une, deux ou trois étoiles). Nous devons donc construire une nouvelle structure conditionnelle à l'intérieur du `if`. De même, nous pouvons construire de nouvelles branches dans `elif` et `else`. C'est ce qu'on appelle une **structure conditionnelle imbriquée**. Suivant cette idée, l'évaluation de la fonction par morceaux ci-dessus peut également être implémentée avec le code suivant.

```python
"""
Évaluation d'une fonction par morceaux

Version : 1.1
Auteur : Shadrak BESSANH
"""
x = float(input('x = '))
if x > 1:
    y = 3 * x - 5
else:
    if x >= -1:
        y = x + 2
    else:
        y = 5 * x + 3
print(f'{y = }')
```

> **Remarque** : Vous pouvez juger par vous-même laquelle des deux approches ci-dessus est préférable. Dans le "**[Zen de Python](https://fr.wikipedia.org/wiki/Zen_de_Python)**", il est dit : "**Flat is better than nested**". La raison pour laquelle le code "plat" est considéré comme meilleur est que si le code est imbriqué sur de nombreux niveaux, la lisibilité en est gravement affectée. Personnellement, je recommande donc la première approche.

#### Exemple 2 : Conversion d'une note sur 100 en une lettre

Objectif : Si la note saisie est supérieure ou égale à 90, afficher `A` ; si elle est comprise entre 80 (inclus) et 90 (exclus), afficher `B` ; entre 70 (inclus) et 80 (exclus), afficher `C` ; entre 60 (inclus) et 70 (exclus), afficher `D` ; en dessous de 60, afficher `E`.

```python
"""
Conversion d'une note sur 100 en note alphabétique

Version : 1.0
Auteur : Shadrak BESSANH
"""
score = float(input('Entrez la note : '))
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'E'
print(f'{grade = }')
```

#### Exemple 3 : Calcul du périmètre et de l'aire d'un triangle

Objectif : Saisir les longueurs des trois côtés. S'ils peuvent former un triangle, calculer le périmètre et l'aire ; sinon, afficher un message indiquant "Impossible de former un triangle".

```python
"""
Calcul du périmètre et de l'aire d'un triangle

Version : 1.0
Auteur : Shadrak BESSANH
"""
a = float(input('a = '))
b = float(input('b = '))
c = float(input('c = '))
if a + b > c and a + c > b and b + c > a:
    perimeter = a + b + c
    print(f'Périmètre : {perimeter}')
    s = perimeter / 2
    area = (s * (s - a) * (s - b) * (s - c)) ** 0.5
    print(f'Aire : {area}')
else:
    print('Impossible de former un triangle')
```

> **Remarque** : La condition `if` ci-dessus signifie que la somme de deux côtés quelconques est supérieure au troisième côté, ce qui est une condition nécessaire pour former un triangle. Lorsque cette condition est remplie, nous calculons et affichons le périmètre et l'aire. Ainsi, les cinq instructions sous `if` ont la même indentation ; elles forment un ensemble. Dès que la condition `if` est remplie, elles sont toutes exécutées. C'est le concept de bloc de code mentionné précédemment. De plus, la formule utilisée ci-dessus pour calculer l'aire du triangle s'appelle la **formule de Héron**. Supposons un triangle avec des côtés de longueurs $\small{a}$, $\small{b}$, $\small{c}$. Alors l'aire $\small{A}$ du triangle peut être obtenue par la formule $\small{A = \sqrt{s(s-a)(s-b)(s-c)}}$, où $s=\frac{a + b + c}{2}$ est le demi-périmètre.

### Résumé

En maîtrisant les structures conditionnelles et les structures de boucle en Python, nous pouvons résoudre de nombreux problèmes pratiques. Cette leçon vous a sans doute aidé à comprendre comment construire des structures conditionnelles. Dans la prochaine leçon, nous aborderons les structures de boucle. Après ces deux leçons, vous constaterez que vous pourrez écrire de nombreux codes intéressants. Continuez ainsi !