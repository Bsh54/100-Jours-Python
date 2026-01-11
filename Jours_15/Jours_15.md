## Applications pratiques des fonctions

### Exemple 1 : Code de vérification aléatoire

Concevoir une fonction qui génère un code de vérification aléatoire composé de chiffres et de lettres (majuscules et minuscules). La longueur doit être paramétrable.

```python
import random
import string

TOUS_CARACTERES = string.digits + string.ascii_letters


def generer_code(*, longueur_code=4):
    """
    Génère un code de vérification de longueur spécifiée.
    
    :param longueur_code: Longueur du code (4 caractères par défaut).
    :return: Chaîne aléatoire composée de chiffres et de lettres.
    """
    return ''.join(random.choices(TOUS_CARACTERES, k=longueur_code))
```

> **Note 1** : Le module `string` fournit des constantes utiles :
> - `string.digits` est la chaîne `'0123456789'`.
> - `string.ascii_letters` est la chaîne `'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'`.
>
> **Note 2** : Le module `random` offre deux fonctions de tirage aléatoire :
> - `sample` : tirage **sans remise** (les éléments tirés ne se répètent pas).
> - `choices` : tirage **avec remise** (les éléments peuvent se répéter).
> Le premier argument est la population (séquence), l'argument `k` est la taille de l'échantillon. Pour `choices`, `k` est un **argument nommé obligatoire** (*keyword-only argument*), il faut donc l'appeler comme `k=valeur`.

Testons la fonction en générant 5 codes :

```python
for _ in range(5):
    print(generer_code())
```

Sortie possible :
```
59tZ
QKU5
izq8
IBBb
jIfX
```

Ou avec une longueur personnalisée :

```python
for _ in range(5):
    print(generer_code(longueur_code=6))
```

Sortie possible :
```
FxJucw
HS4H9G
0yyXfz
x7fohf
ReO22w
```

> **Note** : Le paramètre `longueur_code` de notre fonction est un **argument nommé obligatoire** (grâce à `*` dans la signature). Comme il a une valeur par défaut (`4`), on peut l'omettre. Si on souhaite fournir une valeur, il **faut** spécifier le nom du paramètre : `longueur_code=6`.

### Exemple 2 : Vérifier si un nombre est premier

Écrire une fonction qui détermine si un entier supérieur à 1 est un nombre premier (nombre premier = divisible uniquement par 1 et par lui-même). Si un entier $N > 1$ est premier, alors il n'a aucun diviseur (facteur) entre 2 et $N-1$.

```python
def est_premier(num: int) -> bool:
    """
    Vérifie si un entier positif est premier.
    
    :param num: Entier supérieur à 1.
    :return: `True` si num est premier, sinon `False`.
    """
    if num <= 1:
        return False
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            return False
    return True
```

> **Note 1** : La syntaxe `num: int` dans les paramètres est une **annotation de type** (*type hint*). Elle n'affecte pas l'exécution mais améliore la lisibilité et peut être utilisée par des outils d'analyse statique. De même, `-> bool` indique que la fonction retourne un booléen.
>
> **Note 2** : Il n'est pas nécessaire de tester tous les diviseurs jusqu'à `num - 1`. Si `num` n'a pas de diviseur inférieur ou égal à sa racine carrée, alors il n'en a aucun au-delà. Cela améliore significativement les performances.

### Exemple 3 : PGCD et PPCM

Concevoir des fonctions pour calculer le **Plus Grand Commun Diviseur (PGCD)** et le **Plus Petit Commun Multiple (PPCM)** de deux entiers positifs.

- Le PGCD de $x$ et $y$ est le plus grand entier qui divise à la fois $x$ et $y$.
- Si $x$ et $y$ sont premiers entre eux, leur PGCD est 1.
- Le PPCM de $x$ et $y$ est le plus petit entier divisible par $x$ et $y$.
- Si $x$ et $y$ sont premiers entre eux, leur PPCM est $x \times y$.

Il est préférable de créer deux fonctions distinctes pour ces deux opérations.

```python
def pgcd(x: int, y: int) -> int:
    """Calcule le Plus Grand Commun Diviseur (algorithme d'Euclide)."""
    while y % x != 0:
        x, y = y % x, x
    return x


def ppcm(x: int, y: int) -> int:
    """Calcule le Plus Petit Commun Multiple."""
    return x * y // pgcd(x, y)
```

> **Note** : Les fonctions peuvent s'appeler mutuellement. Ici, `ppcm` appelle `pgcd` pour calculer le PPCM via la formule : $\text{PPCM}(x, y) = \frac{x \times y}{\text{PGCD}(x, y)}$.

### Exemple 4 : Statistiques descriptives

Supposons que nos données d'échantillon soient stockées dans une liste. Créons des fonctions pour calculer les principales statistiques descriptives :

- Moyenne arithmétique (mean)
- Médiane (median)
- Étendue (range)
- Variance (variance)
- Écart-type (standard deviation)
- Coefficient de variation (coefficient of variation)

Formules :

**Moyenne de l'échantillon** :
$$
\bar{x} = \frac{\sum_{i=1}^{n}x_{i}}{n} = \frac{x_{1}+x_{2}+\cdots +x_{n}}{n}
$$

**Variance de l'échantillon** (estimateur sans biais) :
$$
s^2 = \frac {\sum_{i=1}^{n}(x_i - \bar{x})^2} {n-1}
$$

**Écart-type de l'échantillon** :
$$
s = \sqrt{\frac{\sum_{i=1}^{n}(x_i - \bar{x})^2}{n-1}}
$$

**Coefficient de variation** :
$$
CV = \frac{s}{\bar{x}}
$$

```python
def etendue(donnees):
    """Étendue (différence entre maximum et minimum)."""
    return max(donnees) - min(donnees)


def moyenne(donnees):
    """Moyenne arithmétique."""
    return sum(donnees) / len(donnees)


def mediane(donnees):
    """Médiane."""
    temp, taille = sorted(donnees), len(donnees)
    if taille % 2 != 0:
        return temp[taille // 2]
    else:
        return (temp[taille // 2 - 1] + temp[taille // 2]) / 2


def variance(donnees, ddof=1):
    """
    Variance.
    
    :param ddof: Degrés de liberté (Delta Degrees of Freedom).
                 ddof=1 pour un échantillon (variance sans biais).
                 ddof=0 pour une population.
    """
    x_bar = moyenne(donnees)
    temp = [(num - x_bar) ** 2 for num in donnees]
    return sum(temp) / (len(temp) - ddof)


def ecart_type(donnees, ddof=1):
    """Écart-type (racine carrée de la variance)."""
    return variance(donnees, ddof) ** 0.5


def coeff_variation(donnees, ddof=1):
    """Coefficient de variation."""
    return ecart_type(donnees, ddof) / moyenne(donnees)


def resume_statistique(donnees):
    """Affiche un résumé des statistiques descriptives."""
    print(f'Moyenne : {moyenne(donnees)}')
    print(f'Médiane : {mediane(donnees)}')
    print(f'Étendue : {etendue(donnees)}')
    print(f'Variance : {variance(donnees)}')
    print(f'Écart-type : {ecart_type(donnees)}')
    print(f'Coefficient de variation : {coeff_variation(donnees)}')
```

> **Note 1** : La **médiane** est la valeur qui sépare l'échantillon en deux parties égales. Si le nombre d'éléments $n$ est impair, c'est l'élément central après tri (position $\frac{n+1}{2}$). Si $n$ est pair, c'est la moyenne des deux éléments centraux (positions $\frac{n}{2}$ et $\frac{n}{2}+1$).
>
> **Note 2** : Les fonctions `variance` et `ecart_type` ont un paramètre `ddof` (degrés de liberté). Par défaut `ddof=1` pour calculer la variance/écart-type d'un **échantillon** (estimateur sans biais). Pour la variance/écart-type d'une **population** entière, utilisez `ddof=0`.
>
> **Note 3** : La fonction `resume_statistique` assemble toutes les fonctions précédentes pour afficher un résumé. Python possède un module standard `statistics` qui fournit ces fonctionnalités (et bien d'autres).

### Exemple 5 : Générateur de tirages de loterie (Loto)

Reprenons l'exemple du générateur de combinaisons aléatoires pour le Loto (vu précédemment). Refactorisons-le en séparant la génération et l'affichage dans deux fonctions distinctes, puis générons N tirages.

```python
"""
Générateur de combinaisons aléatoires pour le Loto

Auteur: 骆昊
Version: 1.3
"""
import random

NUMEROS_ROUGES = list(range(1, 34))   # 1 à 33 inclus
NUMEROS_BLEUS = list(range(1, 17))    # 1 à 16 inclus


def generer_tirage():
    """
    Génère une combinaison aléatoire.
    
    :return: Liste de 6 numéros rouges (triés) + 1 numéro bleu.
    """
    numeros_choisis = random.sample(NUMEROS_ROUGES, 6)
    numeros_choisis.sort()
    numeros_choisis.append(random.choice(NUMEROS_BLEUS))
    return numeros_choisis


def afficher_tirage(numeros):
    """
    Affiche une combinaison de manière formatée.
    
    :param numeros: Liste de numéros (6 rouges + 1 bleu).
    """
    for num in numeros[:-1]:  # Les 6 premiers (rouges)
        print(f'\033[031m{num:02d}\033[0m', end=' ')
    print(f'\033[034m{numeros[-1]:02d}\033[0m')  # Le dernier (bleu)


n = int(input('Combien de tirages générer ? '))
for _ in range(n):
    afficher_tirage(generer_tirage())
```

> **Note** : Observez la ligne `afficher_tirage(generer_tirage())`. D'abord, `generer_tirage()` est appelée et retourne une liste. Cette liste est **immédiatement** passée comme argument à `afficher_tirage()`. Ce style de code est clair et concis. Après cette refactorisation, la logique est bien séparée :
> - `generer_tirage()` : responsable de la création des données.
> - `afficher_tirage()` : responsable de la présentation.
>
> En tant qu'utilisateur de ces fonctions, vous n'avez pas besoin de connaître leur implémentation interne. Vous savez simplement que `generer_tirage()` vous donne une combinaison et que `afficher_tirage()` l'affiche. C'est le principe d'**abstraction**, essentiel dans la programmation et lorsque vous utilisez des bibliothèques tierces.

### Résumé

Lorsque vous écrivez du code, surtout dans des projets professionnels, ayez le réflexe d'**encapsuler les fonctionnalités indépendantes et réutilisables dans des fonctions**. Cela permet à vous-même et à votre équipe de les réutiliser facilement, évitant ainsi la duplication et le travail fastidieux. Une bonne décomposition en fonctions rend le code plus lisible, plus maintenable et plus testable.