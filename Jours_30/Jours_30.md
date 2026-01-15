## Application des expressions régulières

### Connaissances sur les expressions régulières

Lors de l'écriture de programmes pour traiter des chaînes de caractères, il est fréquent de rencontrer le besoin de rechercher dans un texte des chaînes conformes à certaines règles. Les expressions régulières sont des outils permettant de décrire ces règles. En d'autres termes, nous pouvons utiliser des expressions régulières pour définir des modèles de correspondance de chaînes, c'est-à-dire comment vérifier si une chaîne comporte une partie correspondant à un certain modèle, ou extraire d'une chaîne la partie correspondant à un modèle, ou encore la remplacer.

Prenons un exemple simple : si vous avez déjà utilisé la recherche de fichiers sous Windows et spécifié des noms de fichiers avec des caractères génériques (`*` et `?`), alors les expressions régulières sont similaires à des outils de correspondance de texte, mais elles sont plus puissantes que les caractères génériques. Elles peuvent décrire vos besoins plus précisément, mais bien sûr, l'inconvénient est qu'écrire une expression régulière est beaucoup plus complexe que d'utiliser des caractères génériques, car tout ce qui vous apporte des avantages nécessite un coût correspondant.

Prenons un autre exemple : nous obtenons une chaîne d'un certain endroit (peut-être un fichier texte ou une nouvelle sur Internet) et nous souhaitons trouver les numéros de téléphone portable et les numéros de téléphone fixe dans cette chaîne. Bien sûr, nous pouvons définir que les numéros de téléphone portable sont des nombres à 11 chiffres (attention, il ne s'agit pas de nombres aléatoires à 11 chiffres, car vous n'avez jamais vu un numéro de téléphone portable comme "25012345678"), et que les numéros de téléphone fixe suivent un modèle comme "indicatif régional - numéro". Sans utiliser d'expressions régulières, cette tâche serait assez fastidieuse. Initialement, les ordinateurs étaient créés pour effectuer des calculs mathématiques, traitant principalement des valeurs numériques. Aujourd'hui, une grande partie des informations que nous traitons quotidiennement sont des données textuelles, et nous souhaitons que l'ordinateur puisse reconnaître et traiter du texte conforme à certains modèles, d'où l'importance des expressions régulières. Aujourd'hui, presque tous les langages de programmation offrent un support pour les opérations sur les expressions régulières. Python prend en charge les opérations sur les expressions régulières via le module `re` de sa bibliothèque standard.

Pour les connaissances sur les expressions régulières, vous pouvez lire un article de blog très célèbre intitulé [《Tutoriel d'introduction aux expressions régulières en 30 minutes》](https://deerchao.net/tutorials/regex/regex.htm). Après avoir lu cet article, vous pourrez comprendre le tableau ci-dessous, qui résume brièvement certains symboles de base dans les expressions régulières.

| Symbole        | Explication                                           | Exemple               | Remarques                                                               |
| -------------- | ----------------------------------------------------- | --------------------- | ----------------------------------------------------------------------- |
| `.`            | Correspond à n'importe quel caractère                 | `b.t`                 | Peut correspondre à bat / but / b#t / b1t, etc.                         |
| `\w`           | Correspond aux lettres, chiffres et tirets bas       | `b\wt`                | Peut correspondre à bat / b1t / b_t, etc.<br>Mais ne correspond pas à b#t |
| `\s`           | Correspond aux caractères blancs (\r, \n, \t, etc.)  | `love\syou`           | Peut correspondre à "love you"                                          |
| `\d`           | Correspond aux chiffres                               | `\d\d`                | Peut correspondre à 01 / 23 / 99, etc.                                  |
| `\b`           | Correspond à la limite d'un mot                       | `\bThe\b`             |                                                                         |
| `^`            | Correspond au début de la chaîne                      | `^The`                | Peut correspondre aux chaînes commençant par "The"                      |
| `$`            | Correspond à la fin de la chaîne                      | `.exe$`               | Peut correspondre aux chaînes se terminant par ".exe"                   |
| `\W`           | Correspond aux caractères non lettres/chiffres/tiret bas | `b\Wt`                | Peut correspondre à b#t / b@t, etc.<br>Mais ne correspond pas à but / b1t / b_t, etc. |
| `\S`           | Correspond aux caractères non blancs                  | `love\Syou`           | Peut correspondre à love#you, etc.<br>Mais ne correspond pas à "love you" |
| `\D`           | Correspond aux caractères non chiffres                | `\d\D`                | Peut correspondre à 9a / 3# / 0F, etc.                                  |
| `\B`           | Correspond à la limite non d'un mot                   | `\Bio\B`              |                                                                         |
| `[]`           | Correspond à un seul caractère d'un ensemble          | `[aeiou]`             | Peut correspondre à n'importe quelle voyelle                            |
| `[^]`          | Correspond à un seul caractère non dans l'ensemble    | `[^aeiou]`            | Peut correspondre à n'importe quelle consonne                           |
| `*`            | Correspond 0 fois ou plus                             | `\w*`                 |                                                                         |
| `+`            | Correspond 1 fois ou plus                             | `\w+`                 |                                                                         |
| `?`            | Correspond 0 ou 1 fois                                | `\w?`                 |                                                                         |
| `{N}`          | Correspond exactement N fois                          | `\w{3}`               |                                                                         |
| `{M,}`         | Correspond au moins M fois                            | `\w{3,}`              |                                                                         |
| `{M,N}`        | Correspond entre M et N fois                          | `\w{3,6}`             |                                                                         |
| `\|`           | Alternative                                           | `foo\|bar`            | Peut correspondre à "foo" ou "bar"                                      |
| `(?#)`         | Commentaire                                           |                       |                                                                         |
| `(exp)`        | Correspond à exp et capture dans un groupe nommé automatiquement |                       |                                                                         |
| `(?<name>exp)` | Correspond à exp et capture dans un groupe nommé "name" |                       |                                                                         |
| `(?:exp)`      | Correspond à exp mais ne capture pas le texte         |                       |                                                                         |
| `(?=exp)`      | Correspond à la position avant exp                    | `\b\w+(?=ing)`        | Peut correspondre à "danc" dans "I'm dancing"                           |
| `(?<=exp)`     | Correspond à la position après exp                    | `(?<=\bdanc)\w+\b`    | Peut correspondre au premier "ing" dans "I love dancing and reading"    |
| `(?!exp)`      | Correspond à une position qui n'est pas suivie de exp |                       |                                                                         |
| `(?<!exp)`     | Correspond à une position qui n'est pas précédée de exp |                       |                                                                         |
| `*?`           | Répétition non gourmande : répète le moins possible   | `a.*b`<br>`a.*?b`     | Appliqué à "aabab", le premier correspond à "aabab", le second à "aab" et "ab" |
| `+?`           | Répétition non gourmande de 1 ou plusieurs fois       |                       |                                                                         |
| `??`           | Répétition non gourmande de 0 ou 1 fois               |                       |                                                                         |
| `{M,N}?`       | Répétition non gourmande de M à N fois                |                       |                                                                         |
| `{M,}?`        | Répétition non gourmande d'au moins M fois            |                       |                                                                         |

> **Remarque :** Si le caractère à correspondre est un caractère spécial dans l'expression régulière, vous pouvez utiliser `\` pour l'échapper. Par exemple, pour correspondre à un point, écrivez `\.` car `.` seul correspond à n'importe quel caractère. De même, pour correspondre à des parenthèses, écrivez `\(` et `\)`, sinon elles seront interprétées comme un groupe dans l'expression régulière.

### Support des expressions régulières en Python

Python fournit le module `re` pour prendre en charge les opérations liées aux expressions régulières. Voici les fonctions principales du module `re`.

| Fonction                                           | Description                                                                 |
| -------------------------------------------------- | --------------------------------------------------------------------------- |
| `compile(pattern, flags=0)`                        | Compile une expression régulière et retourne un objet expression régulière  |
| `match(pattern, string, flags=0)`                  | Essaie de faire correspondre l'expression régulière au début de la chaîne ; retourne un objet de correspondance en cas de succès, sinon `None` |
| `search(pattern, string, flags=0)`                 | Recherche la première occurrence du motif dans la chaîne ; retourne un objet de correspondance en cas de succès, sinon `None` |
| `split(pattern, string, maxsplit=0, flags=0)`      | Divise la chaîne en utilisant le motif comme séparateur ; retourne une liste |
| `sub(pattern, repl, string, count=0, flags=0)`     | Remplace les occurrences du motif par la chaîne de remplacement ; `count` contrôle le nombre de remplacements |
| `fullmatch(pattern, string, flags=0)`              | Version complète de `match` (correspondance de début à fin)                 |
| `findall(pattern, string, flags=0)`                | Trouve toutes les occurrences du motif dans la chaîne ; retourne une liste de chaînes |
| `finditer(pattern, string, flags=0)`               | Trouve toutes les occurrences du motif dans la chaîne ; retourne un itérateur |
| `purge()`                                          | Vide le cache des expressions régulières compilées implicitement            |
| `re.I` / `re.IGNORECASE`                           | Indicateur pour ignorer la casse                                            |
| `re.M` / `re.MULTILINE`                            | Indicateur pour le mode multiligne                                          |

> **Remarque :** Les fonctions du module `re` mentionnées ci-dessus peuvent également être remplacées par des méthodes d'objets d'expression régulière (`Pattern`). Si une expression régulière doit être utilisée plusieurs fois, il est plus judicieux de la compiler d'abord avec la fonction `compile` pour créer un objet d'expression régulière.

Voici une série d'exemples montrant comment utiliser les expressions régulières en Python.

#### Exemple 1 : Vérifier la validité d'un nom d'utilisateur et d'un numéro QQ, et fournir les messages d'erreur correspondants.

```python
"""
Exigences : le nom d'utilisateur doit être composé de lettres, chiffres ou tirets bas, avec une longueur entre 6 et 20 caractères. Le numéro QQ doit être un nombre de 5 à 12 chiffres, ne commençant pas par 0.
"""
import re

username = input('Veuillez entrer un nom d'utilisateur : ')
qq = input('Veuillez entrer un numéro QQ : ')
# Le premier paramètre de match est une chaîne ou un objet d'expression régulière.
# Le deuxième paramètre est la chaîne à comparer avec l'expression régulière.
m1 = re.match(r'^[0-9a-zA-Z_]{6,20}$', username)
if not m1:
    print('Veuillez entrer un nom d'utilisateur valide.')
# fullmatch exige que la chaîne corresponde exactement à l'expression régulière.
# Ainsi, nous n'avons pas inclus les symboles de début et de fin.
m2 = re.fullmatch(r'[1-9]\d{4,11}', qq)
if not m2:
    print('Veuillez entrer un numéro QQ valide.')
if m1 and m2:
    print('Les informations que vous avez entrées sont valides !')
```

> **Conseil :** Dans le code ci-dessus, nous avons utilisé la syntaxe de "chaîne brute" (en ajoutant `r` devant la chaîne). Une "chaîne brute" signifie que chaque caractère dans la chaîne conserve sa signification littérale, en d'autres termes, il n'y a pas de caractères d'échappement. Comme les expressions régulières contiennent de nombreux métacaractères et nécessitent des échappements, sans les chaînes brutes, nous devrions écrire les barres obliques inverses comme `\\`. Par exemple, `\d` (correspondant à un chiffre) devrait être écrit `\\d`, ce qui est non seulement moins pratique à écrire, mais aussi plus difficile à lire.

#### Exemple 2 : Extraire les numéros de téléphone portable d'un texte.

L'image ci-dessous montre les préfixes de numéros de téléphone portable proposés par les trois opérateurs chinois jusqu'à fin 2017.

```python
import re

# Créer un objet d'expression régulière, utilisant les assertions avant/arrière pour s'assurer que le numéro de téléphone n'est pas précédé ou suivi d'un chiffre.
pattern = re.compile(r'(?<=\D)1[34578]\d{9}(?=\D)')
sentence = '''Important : répétez 8130123456789 fois, mon numéro de téléphone est 13512346789,
pas 15600998765, ni 110 ou 119. Le numéro de téléphone de Wang Dachui est 15600998765.'''
# Méthode 1 : Trouver toutes les correspondances et les stocker dans une liste.
tels_list = re.findall(pattern, sentence)
for tel in tels_list:
    print(tel)
print('-------- Ligne de séparation élégante --------')

# Méthode 2 : Récupérer les objets de correspondance via un itérateur et obtenir leur contenu.
for temp in pattern.finditer(sentence):
    print(temp.group())
print('-------- Ligne de séparation élégante --------')

# Méthode 3 : Utiliser search avec une position de départ pour trouver toutes les correspondances.
m = pattern.search(sentence)
while m:
    print(m.group())
    m = pattern.search(sentence, m.end())
```

> **Remarque :** L'expression régulière ci-dessus pour les numéros de téléphone portable chinois n'est pas optimale, car les numéros commençant par 14 ne sont que 145 ou 147, et l'expression régulière ne prend pas cela en compte. Une meilleure expression régulière pour les numéros de téléphone portable chinois serait : `(?<=\D)(1[38]\d{9}|14[57]\d{8}|15[0-35-9]\d{8}|17[678]\d{8})(?=\D)`. Il semble qu'il existe maintenant des numéros commençant par 19 et 16 en Chine, mais cela ne fait pas partie de nos considérations pour le moment.

#### Exemple 3 : Remplacer le contenu indésirable dans une chaîne.

```python
import re

sentence = 'Oh, merde ! Es-tu stupide ? Va te faire foutre.'
purified = re.sub('foutre|merde|[stu][pid]+',
                  '*', sentence, flags=re.IGNORECASE)
print(purified)  # Oh, * ! Es-tu * ? *.
```

> **Remarque :** Les fonctions liées aux expressions régulières du module `re` ont toutes un paramètre `flags`, qui représente les indicateurs de correspondance. Vous pouvez spécifier si la correspondance doit ignorer la casse, être multiligne, afficher des informations de débogage, etc. Si vous devez spécifier plusieurs valeurs pour `flags`, vous pouvez utiliser l'opérateur OU au niveau des bits (`|`), par exemple `flags=re.I | re.M`.

#### Exemple 4 : Diviser une longue chaîne.

```python
import re

poem = 'La lumière de la lune devant la fenêtre, je soupçonne que c'est du givre sur le sol. Je lève la tête pour regarder la lune, je baisse la tête pour penser à mon pays natal.'
sentences_list = re.split(r'[，。]', poem)
sentences_list = [sentence for sentence in sentences_list if sentence]
for sentence in sentences_list:
    print(sentence)
```

### Résumé

Les expressions régulières sont extrêmement puissantes pour le traitement et la correspondance de chaînes de caractères. À travers les exemples ci-dessus, vous avez probablement ressenti le potentiel des expressions régulières. Bien sûr, écrire une expression régulière n'est pas facile pour un débutant, mais la pratique rend parfait. N'hésitez pas à essayer. Il existe un [outil de test d'expressions régulières en ligne](https://c.runoob.com/front-end/854) qui peut vous aider dans une certaine mesure.