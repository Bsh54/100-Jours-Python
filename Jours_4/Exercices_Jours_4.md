Voici 10 exercices condensés qui couvrent les points essentiels des opérateurs en Python :

---

### **Exercice 1 : Priorité des opérateurs**
Sans exécuter de code, quel est le résultat de `2 + 3 * 4 ** 2 / 8 - 1` ?
1. Suivez la table de priorité pour calculer étape par étape.
2. Ajoutez des parenthèses pour représenter l'ordre réel des opérations.

### **Exercice 2 : Division entière et reste**
Soit `a = 17` et `b = 5` :
1. Que donne `a / b`, `a // b` et `a % b` ?
2. Quelle relation mathématique lie ces trois résultats ?
3. Pourquoi `-7 // 2` donne `-4` et non `-3` ?

### **Exercice 3 : Opérateurs d'affectation composés**
Pour chacune des expressions suivantes, réécrivez-la sans opérateur composé :
1. `a **= 3`
2. `x //= y + 2`
3. `b %= c * 2 - 1`

### **Exercice 4 : Comparaisons et types**
Que se passe-t-il quand on compare :
1. Un entier avec un flottant : `5 == 5.0`
2. Un booléen avec un entier : `True == 1`
3. Une chaîne avec un nombre : `"10" == 10`
Formulez des hypothèses avant de tester.

### **Exercice 5 : Opérateurs logiques et évaluation paresseuse**
Soit le code suivant :
```python
def fonction_lente():
    print("Fonction exécutée")
    return True

x = False and fonction_lente()
y = True or fonction_lente()
```
1. Combien de fois voyez-vous "Fonction exécutée" s'afficher ?
2. Expliquez pourquoi.

### **Exercice 6 : L'opérateur morse (walrus operator)**
1. Pourquoi `print(a = 10)` provoque une erreur alors que `print(a := 10)` fonctionne ?
2. Donnez un exemple pratique où l'opérateur morse est utile dans une condition.

### **Exercice 7 : Conversion de température**
Écrivez un programme qui :
1. Convertit des Celsius en Fahrenheit (formule : `F = C × 9/5 + 32`).
2. Demande à l'utilisateur s'il veut convertir de C vers F ou de F vers C.
3. Vérifie que la température entrée n'est pas inférieure au zéro absolu.

### **Exercice 8 : Année bissextile améliorée**
1. Modifiez l'exemple donné en cours pour qu'il affiche "2024 est une année bissextile" au lieu de juste `True`.
2. Ajoutez une vérification que l'année est supérieure à 1582.
3. Gérez le cas où l'utilisateur entre autre chose qu'un nombre entier.

### **Exercice 9 : Les dangers de la comparaison de flottants**
1. Pourquoi `0.1 + 0.2 == 0.3` donne `False` en Python ?
2. Comment devrait-on comparer des nombres à virgule flottante pour éviter les problèmes ?
3. Quelle est la différence entre `is` et `==` ? Donnez un exemple où `a == b` est `True` mais `a is b` est `False`.

### **Exercice 10 : Calculatrice de formes géométriques**
Créez un programme qui :
1. Demande à l'utilisateur de choisir entre cercle, rectangle ou triangle.
2. Selon le choix, demande les dimensions nécessaires.
3. Calcule et affiche le périmètre et l'aire.
4. Utilise `math.pi` pour une meilleure précision.

