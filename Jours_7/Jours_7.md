## Pratique des structures conditionnelles et de boucle

Grâce aux deux leçons précédentes, vous avez maintenant une compréhension initiale des structures conditionnelles et de boucle en Python. **Les structures conditionnelles et de boucle sont la base de la construction de la logique des programmes**. Leur importance ne fait aucun doute, mais pour les débutants, c'est également la partie la plus difficile. Beaucoup comprennent la syntaxe des structures conditionnelles et de boucle, mais lorsqu'ils rencontrent des problèmes pratiques, ils ne savent pas par où commencer ; **il est facile de comprendre le code d'autrui, mais il est difficile d'écrire son propre code similaire**. Si vous rencontrez les mêmes difficultés et perplexités, ne vous découragez surtout pas. C'est simplement parce que votre voyage en programmation ne fait que commencer, **votre quantité d'entraînement n'a pas encore atteint le niveau où vous pouvez écrire du code à volonté**. Il suffit de renforcer la pratique de la programmation, de produire des changements qualitatifs par l'accumulation quantitative, et ce problème finira par être résolu.

### Exemple 1 : Nombres premiers inférieurs à 100

> **Remarque** : Un nombre premier est un entier positif divisible uniquement par 1 et par lui-même (à l'exception de 1). Nous avons déjà écrit du code pour déterminer si un nombre est premier ; il s'agit ici d'une version améliorée.

```python
"""
Afficher les nombres premiers inférieurs à 100

Version : 1.0
Auteur : Shadrak BESSANH
"""
for num in range(2, 100):
    is_prime = True
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            is_prime = False
            break
    if is_prime:
        print(num)
```

### Exemple 2 : Suite de Fibonacci

Objectif : Afficher les 20 premiers termes de la suite de Fibonacci.

> **Remarque** : La **suite de Fibonacci** (également appelée *suite du nombre d'or*) est une suite d'entiers introduite par le mathématicien italien Leonardo Fibonacci dans son livre *Liber Abaci*, où il étudiait la croissance d'une population de lapins dans des conditions idéales. C'est pourquoi cette suite est souvent appelée "suite des lapins". La suite de Fibonacci est caractérisée par le fait que ses deux premiers termes sont 1, et chaque terme suivant est la somme des deux termes précédents. Selon cette règle, les 10 premiers termes de la suite de Fibonacci sont : `1, 1, 2, 3, 5, 8, 13, 21, 34, 55`. La suite de Fibonacci a des applications directes en physique moderne, en chimie, et dans l'étude des quasi-cristaux, entre autres.

```python
"""
Afficher les 20 premiers termes de la suite de Fibonacci

Version : 1.0
Auteur : Shadrak BESSANH
"""

a, b = 0, 1
for _ in range(20):
    a, b = b, a + b
    print(a)
```

> **Remarque** : Dans la boucle ci-dessus, `a, b = b, a + b` signifie attribuer la valeur de `b` à `a`, et la valeur de `a + b` à `b`. Grâce à cette formule de récurrence, nous obtenons successivement les termes de la suite de Fibonacci.

### Exemple 3 : Recherche des nombres narcissiques

Objectif : Trouver tous les nombres narcissiques compris entre 100 et 999.

> **Indication** : En théorie des nombres, un **nombre narcissique** (également appelé nombre d'Armstrong) est un entier non négatif à $\small{N}$ chiffres dont la somme des puissances $\small{N}$-ièmes de ses chiffres est égale au nombre lui-même. Par exemple : $\small{153 = 1^{3} + 5^{3} + 3^{3}}$, donc 153 est un nombre narcissique ; $\small{1634 = 1^{4} + 6^{4} + 3^{4} + 4^{4}}$, donc 1634 est également un nombre narcissique. Pour un nombre à trois chiffres, la clé est de le décomposer en centaines, dizaines et unités, puis de vérifier s'il satisfait la condition des nombres narcissiques. Cela peut être facilement réalisé en Python à l'aide des opérateurs `//` et `%`.

```python
"""
Trouver les nombres narcissiques entre 100 et 999

Version : 1.0
Auteur : Shadrak BESSANH
"""
for num in range(100, 1000):
    low = num % 10
    mid = num // 10 % 10
    high = num // 100
    if num == low ** 3 + mid ** 3 + high ** 3:
        print(num)
```

L'astuce ci-dessus utilisant `//` et `%` pour décomposer un nombre est très utile lors de l'écriture de code. Par exemple, pour inverser un entier positif dont nous ne connaissons pas le nombre de chiffres (par exemple, transformer 12389 en 98321), nous pouvons également utiliser ces deux opérations, comme illustré ci-dessous.

```python
"""
Inverser un entier positif

Version : 1.0
Auteur : Shadrak BESSANH
"""
num = int(input('num = '))
reversed_num = 0
while num > 0:
    reversed_num = reversed_num * 10 + num % 10
    num //= 10
print(reversed_num)
```

### Exemple 4 : Problème des cent poulets

> **Remarque** : Le problème des cent poulets est un problème mathématique posé par le mathématicien chinois Zhang Qiujian dans son livre *Suan Jing* : un coq coûte cinq pièces, une poule coûte trois pièces, et trois poussins coûtent une pièce. Avec cent pièces, achetez cent poulets. Combien de coqs, de poules et de poussins ? Traduit en langage moderne : un coq coûte 5 pièces, une poule coûte 3 pièces, et trois poussins coûtent 1 pièce. Avec 100 pièces, achetez 100 poulets. Combien y a-t-il de coqs, de poules et de poussins ?

```python
"""
Problème des cent poulets

Version : 1.0
Auteur : Shadrak BESSANH
"""
for x in range(0, 21):
    for y in range(0, 34):
        for z in range(0, 100, 3):
            if x + y + z == 100 and 5 * x + 3 * y + z // 3 == 100:
                print(f'Coqs : {x}, Poules : {y}, Poussins : {z}')
```

La méthode utilisée ci-dessus s'appelle la **méthode exhaustive** (ou **recherche exhaustive**). Cette méthode consiste à énumérer toutes les solutions possibles et à vérifier si chacune satisfait les conditions du problème, afin d'obtenir la solution. Dans le code ci-dessus, nous utilisons des boucles imbriquées. Supposons qu'il y ait `x` coqs ; clairement, `x` varie de 0 à 20. Supposons qu'il y ait `y` poules ; `y` varie de 0 à 33. Supposons qu'il y ait `z` poussins ; `z` varie de 0 à 99 et doit être un multiple de 3. Ainsi, nous définissons la condition pour 100 poulets : `x + y + z == 100`, et la condition pour 100 pièces : `5 * x + 3 * y + z // 3 == 100`. Lorsque les deux conditions sont simultanément satisfaites, nous avons la bonne réponse, que nous affichons avec `print`. Cette méthode peut sembler lourde, mais pour un ordinateur doté d'une grande puissance de calcul, c'est généralement une approche viable, voire une bonne option, tant que la solution existe.

En fait, le code ci-dessus peut être amélioré. Puisque nous avons supposé qu'il y a `x` coqs et `y` poules, le nombre de poussins doit être `100 - x - y`. En réduisant une condition, nous pouvons transformer les trois boucles `for-in` imbriquées en deux boucles imbriquées. Le nombre d'itérations diminue, ce qui améliore significativement l'efficacité du code, comme illustré ci-dessous.

```python
"""
Problème des cent poulets

Version : 1.1
Auteur : Shadrak BESSANH
"""
for x in range(0, 21):
    for y in range(0, 34):
        z = 100 - x - y
        if z % 3 == 0 and 5 * x + 3 * y + z // 3 == 100:
            print(f'Coqs : {x}, Poules : {y}, Poussins : {z}')
```

> **Remarque** : La condition `z % 3 == 0` dans le code ci-dessus garantit que le nombre de poussins est un multiple de 3.

### Exemple 5 : Jeu de dés CRAPS

> **Remarque** : CRAPS, également appelé "craps", est un jeu de dés très populaire dans les casinos de Las Vegas. Le jeu utilise deux dés, et les joueurs lancent les dés pour obtenir des points. Les règles simplifiées sont les suivantes : si le joueur obtient un 7 ou un 11 au premier lancer, il gagne ; s'il obtient un 2, un 3 ou un 12 au premier lancer, la banque gagne ; pour tout autre point, le jeu continue, le joueur relance les dés. Si le joueur obtient un 7, la banque gagne ; s'il obtient le même point que lors du premier lancer, le joueur gagne ; pour tout autre point, le joueur continue à lancer les dés jusqu'à ce qu'un vainqueur soit déterminé. Pour ajouter du plaisir au code, nous supposons que le joueur commence avec une mise de 1000 unités. Avant chaque tour, le joueur mise. S'il gagne, il reçoit un gain égal à sa mise ; si la banque gagne, il perd sa mise. Le jeu se termine lorsque le joueur fait faillite (il perd toute sa mise).

```python
"""
Jeu de dés CRAPS

Version : 1.0
Auteur : Shadrak BESSANH
"""
import random

money = 1000
while money > 0:
    print(f'Votre capital total est de : {money} unités')
    # La mise doit être supérieure à 0 et inférieure ou égale au capital du joueur
    while True:
        debt = int(input('Placez votre mise : '))
        if 0 < debt <= money:
            break
    # Simuler le lancer de deux dés en ajoutant deux nombres aléatoires uniformément distribués entre 1 et 6
    first_point = random.randrange(1, 7) + random.randrange(1, 7)
    print(f'\nLe joueur a obtenu {first_point}')
    if first_point == 7 or first_point == 11:
        print('Le joueur gagne !\n')
        money += debt
    elif first_point == 2 or first_point == 3 or first_point == 12:
        print('La banque gagne !\n')
        money -= debt
    else:
        # Si le premier lancer ne donne pas de vainqueur, le joueur doit relancer les dés
        while True:
            current_point = random.randrange(1, 7) + random.randrange(1, 7)
            print(f'Le joueur a obtenu {current_point}')
            if current_point == 7:
                print('La banque gagne !\n')
                money -= debt
                break
            elif current_point == first_point:
                print('Le joueur gagne !\n')
                money += debt
                break
print('Vous avez fait faillite, le jeu est terminé !')
```

### Résumé

Les structures conditionnelles et de boucle sont extrêmement importantes ; elles sont la base de la construction de la logique des programmes. **Il est essentiel de pratiquer intensivement pour les maîtriser parfaitement**. Vous pouvez prendre le jeu CRAPS décrit ci-dessus comme référence : si vous pouvez écrire ce code sans difficulté, alors vous maîtrisez déjà bien les structures conditionnelles et de boucle.