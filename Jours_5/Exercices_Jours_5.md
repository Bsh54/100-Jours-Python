# Exercices sur les Structures Conditionnelles en Python (version condensée)

### **Exercice 1 : Fondamentaux des conditions**
1. Quelle est la différence entre une structure séquentielle et une structure conditionnelle ?
2. Pourquoi Python utilise-t-il l'indentation plutôt que des accolades ?

### **Exercice 2 : Structure if-elif-else**
Écrivez un programme qui demande l'âge et affiche :
- "Enfant" si moins de 12 ans
- "Adolescent" entre 12 et 17 ans
- "Adulte" entre 18 et 64 ans
- "Senior" à partir de 65 ans

### **Exercice 3 : Opérateur ternaire**
Réécrivez ces codes avec l'opérateur ternaire :
```python
# Version 1
if temperature > 30:
    vetement = "short"
else:
    vetement = "pantalon"

# Version 2
if note >= 10:
    resultat = "reçu"
else:
    resultat = "ajourné"
```

### **Exercice 4 : Conversion if-elif vers match-case**
Convertissez ce code en utilisant `match-case` :
```python
jour = int(input("Numéro du jour (1-7) : "))
if jour == 1:
    nom = "Lundi"
elif jour == 2:
    nom = "Mardi"
# ... jusqu'à 7
else:
    nom = "Invalide"
```

### **Exercice 5 : Calculateur d'IMC amélioré**
Écrivez un programme qui :
1. Calcule l'IMC (poids / taille²)
2. Affiche la catégorie : Maigreur (<18.5), Normal (18.5-24.9), Surpoids (25-29.9), Obésité (≥30)
3. Ajoute des conseils personnalisés selon la catégorie

### **Exercice 6 : Solveur d'équation du second degré**
Écrivez un programme qui :
1. Demande les coefficients a, b, c de ax² + bx + c = 0
2. Calcule le discriminant Δ = b² - 4ac
3. Affiche les solutions selon les cas (Δ>0, Δ=0, Δ<0, a=0)

### **Exercice 7 : Éviter l'imbrication excessive**
Le code suivant est trop imbriqué. Réécrivez-le de façon plus claire :
```python
if connexion_etablie:
    if utilisateur_valide:
        if mot_de_passe_correct:
            if compte_actif:
                print("Bienvenue !")
            else:
                print("Compte désactivé")
        else:
            print("Mot de passe incorrect")
    else:
        print("Utilisateur inconnu")
else:
    print("Pas de connexion")
```

### **Exercice 8 : Conditions booléennes**
1. Simplifiez ces expressions : `not (a or not b)` et `(a and b) or (a and not b)`
2. Identifiez les redondances dans : `if x > 0 and x != 0:`

### **Exercice 9 : Système d'authentification**
Créez un programme qui :
1. Demande un nom d'utilisateur et un mot de passe
2. Vérifie contre des valeurs prédéfinies
3. Affiche des messages différents pour chaque cas d'erreur
4. Gère le cas où l'utilisateur laisse un champ vide

### **Exercice 10 : Jeu d'aventure texte**
Créez un jeu d'aventure avec plusieurs choix :
```
Vous êtes dans une forêt.
1. Aller à gauche
2. Aller à droite
3. Rester sur place
```
Utilisez des structures conditionnelles pour créer au moins 3 scénarios différents.

