# Exercices sur les chaînes de caractères en Python

## Exercice 1 : Définitions de base
Écris un programme qui :
1. Crée une chaîne contenant ton nom et prénom
2. Crée une chaîne sur plusieurs lignes contenant ton adresse
3. Affiche les deux chaînes précédentes
4. Affiche la longueur de chacune d'elles

## Exercice 2 : Caractères d'échappement
Crée une chaîne qui affichera exactement ceci à l'écran :
```
Le chemin est : C:\Users\Documents\Python\test.txt
Elle a dit : "Bonjour à tous !"
Et il a répondu : 'Salut !'
```

## Exercice 3 : Chaînes brutes et encodage
1. Crée une chaîne brute contenant : `\n\t\x61\b`
2. Crée une chaîne normale contenant les mêmes caractères
3. Compare les résultats des deux avec la fonction `print()`
4. Explique mentalement pourquoi les affichages sont différents

## Exercice 4 : Opérations de base
Soit les chaînes : `s1 = "Python"`, `s2 = "est"`, `s3 = "génial"`
1. Concatène-les pour former : "Python est génial !!!"
2. Répète "Hi" 5 fois avec un espace entre chaque
3. Vérifie si "thon" est dans `s1`
4. Compare `s1` et `"python"` (minuscule)

## Exercice 5 : Indexation et slicing
Pour la chaîne `s = "abcdefghijklmnopqrstuvwxyz"` :
1. Affiche le 5ème caractère
2. Affiche les 5 derniers caractères
3. Affiche tous les caractères de position paire (0, 2, 4...)
4. Affiche la chaîne à l'envers
5. Extrais "jkl" de trois manières différentes

## Exercice 6 : Parcours et transformation
Écris une fonction qui :
1. Prend une chaîne en paramètre
2. Parcourt chaque caractère
3. Remplace toutes les voyelles par des étoiles (*)
4. Retourne la nouvelle chaîne

Teste avec : "Hello World" → "H*ll* W*rld"

## Exercice 7 : Méthodes de recherche
Pour la phrase : `phrase = "Le chat noir dort sur le canapé rouge"`
1. Trouve la position du mot "noir"
2. Cherche "chien" (quelle méthode utiliser ?)
3. Vérifie si la phrase commence par "Le"
4. Vérifie si elle se termine par "e"
5. Compte combien de fois apparaît la lettre "e"

## Exercice 8 : Nettoyage et formatage
Soit l'entrée utilisateur : `input_str = "   Pierre.DUPONT@gmail.com   "`
1. Nettoie les espaces superflus
2. Convertis l'email en minuscules
3. Formate l'affichage : "Email nettoyé : pierre.dupont@gmail.com"
4. Ajuste le nom "DUPONT" pour qu'il soit en "Dupont" uniquement

## Exercice 9 : Découpage et reconstruction
Pour la chaîne : `data = "nom:Martin;age:30;ville:Paris;profession:Ingénieur"`
1. Découpe la chaîne pour obtenir chaque paire clé-valeur
2. Crée un dictionnaire avec ces données
3. Recrée une chaîne similaire mais avec "|" comme séparateur
4. Extrais uniquement la valeur associée à "ville"

## Exercice 10 : Analyse de texte
Écris un programme qui analyse une phrase et affiche :
1. Le nombre de mots
2. Le mot le plus long
3. La lettre la plus fréquente
4. Si c'est une question (se termine par "?")
5. Le pourcentage de lettres majuscules

Teste avec : "Python est-il un langage de programmation puissant ? OUI !"

## Exercice 11 : Encodage et manipulation
1. Crée une chaîne avec ton prénom et un caractère spécial (é, è, à, etc.)
2. Encode-la en UTF-8 puis en ISO-8859-1
3. Compare les représentations bytes
4. Décode chaque version et explique les différences si nécessaire

## Exercice 12 : Challenge créatif
Crée un générateur de "pyramide de lettres" :
Pour "PYTHON", affiche :
```
P
PY
PYT
PYTH
PYTHO
PYTHON
PYTHO
PYTH
PYT
PY
P
```

## Exercice 13 : Validation de données
Écris des fonctions qui vérifient :
1. Si une chaîne est un palindrome (se lit pareil dans les deux sens)
2. Si une chaîne est un numéro de téléphone français valide
3. Si un mot de passe est fort (min 8 caractères, majuscule, minuscule, chiffre)
4. Si une adresse email a un format valide

## Exercice 14 : Algorithmie avec chaînes
Implémente l'algorithme de chiffrement de César :
- Décaler chaque lettre de n positions dans l'alphabet
- Gérer le débordement (z → a)
- Conserver la casse et les autres caractères

Teste avec "Hello World!" et un décalage de 3 → "Khoor Zruog!"

## Exercice 15 : Application réelle
Simule le traitement d'un fichier CSV sous forme de chaîne :
```
"id,nom,prix,quantité
1,ordinateur,800,5
2,souris,25,30
3,clavier,45,15"
```

Extrais et calcule :
1. Le prix total du stock
2. Le produit le plus cher
3. La liste des produits avec moins de 10 unités

---

**Conseils pour travailler ces exercices :**
- Teste chaque ligne de code pour bien comprendre
- Utilise `print()` pour voir les résultats intermédiaires
- Fais des schémas mentaux pour les index et slices
- Compare différentes méthodes pour arriver au même résultat
- Documente tes découvertes et difficultés

**Objectifs pédagogiques :**
- Manipuler les chaînes de caractères de manière fluide
- Choisir la bonne méthode pour chaque problème
- Comprendre l'immutabilité des chaînes
- Maîtriser l'encodage des caractères
- Développer une intuition pour le traitement de texte

Bon travail ! Ces exercices couvrent les concepts essentiels des chaînes en Python.