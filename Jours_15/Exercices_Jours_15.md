# Exercices sur les applications pratiques des fonctions

## Exercice 1 : Générateur de mots de passe sécurisés
1. Écris une fonction `generer_mot_de_passe(longueur=12)` qui génère un mot de passe aléatoire
2. Le mot de passe doit contenir au moins : 1 majuscule, 1 minuscule, 1 chiffre, 1 caractère spécial
3. La fonction doit valider que `longueur` est ≥ 8
4. Écris une fonction `force_mot_de_passe(mdp)` qui évalue la force (faible/moyen/fort)
5. Teste en générant 5 mots de passe et évalue leur force

## Exercice 2 : Analyse de nombres premiers
1. Écris une fonction `liste_premiers(n)` qui retourne tous les nombres premiers ≤ n
2. Écris une fonction `decomposition_facteurs_premiers(n)` qui retourne la décomposition (ex: 60 → [2, 2, 3, 5])
3. Écris une fonction `nombres_jumeaux(limite)` qui trouve les paires de premiers jumeaux (écart de 2)
4. Écris une fonction `est_premier_germain(p)` qui vérifie si p et 2p+1 sont premiers

## Exercice 3 : Calculs mathématiques avancés
1. Écris une fonction `suite_fibonacci(n)` qui retourne les n premiers termes
2. Écris une fonction `coefficients_binomiaux(n)` qui retourne la ligne n du triangle de Pascal
3. Écris une fonction `approximation_pi(iterations)` qui approxime π par la méthode Monte-Carlo
4. Écris une fonction `racine_nieme(x, n, precision=1e-10)` qui calcule √[n]{x} par la méthode de Newton

## Exercice 4 : Statistiques sur un fichier texte
1. Écris une fonction `statistiques_fichier(nom_fichier)` qui analyse un fichier texte et retourne :
   - Nombre total de caractères
   - Nombre de mots
   - Nombre de lignes
   - Mot le plus fréquent
   - Longueur moyenne des mots
2. Écris une fonction `frequences_lettres(nom_fichier)` qui retourne un dictionnaire des fréquences
3. Écris une fonction `mots_par_ligne(nom_fichier)` qui calcule la distribution des mots par ligne

## Exercice 5 : Gestionnaire de contacts amélioré
1. Écris une fonction `ajouter_contact(annuaire, nom, **infos)` qui ajoute un contact
2. Écris une fonction `rechercher_contacts(annuaire, **criteres)` qui recherche par critères multiples
3. Écris une fonction `exporter_contacts(annuaire, format='json')` qui exporte en JSON ou CSV
4. Écris une fonction `importer_contacts(fichier)` qui importe depuis un fichier
5. Crée un menu interactif qui utilise ces fonctions

## Exercice 6 : Calculatrice scientifique modulaire
Crée un module `calculatrice.py` avec :
1. `addition(*args)` - somme de n nombres
2. `soustraire(a, b)` - différence
3. `multiplier(*args)` - produit
4. `diviser(a, b)` - division avec gestion de division par zéro
5. `puissance(base, exposant)` - exponentiation
6. `logarithme(x, base=10)` - logarithme
7. `trigonometrie(angle, fonction='sin')` - sin/cos/tan
8. `convertir_unites(valeur, unite_source, unite_cible)` - conversions (ex: C→F)

## Exercice 7 : Jeu du pendu (hangman)
1. Écris une fonction `choisir_mot(liste_mots)` qui choisit un mot aléatoire
2. Écris une fonction `afficher_etat(mot_secret, lettres_trouvees)` qui affiche "_ _ a _"
3. Écris une fonction `verifier_lettre(lettre, mot_secret, lettres_trouvees, tentatives)`
4. Écris une fonction `jouer_partie()` qui orchestre le jeu complet
5. Ajoute un système de scores et de difficultés

## Exercice 8 : Compression RLE (Run-Length Encoding)
1. Écris une fonction `compresser_rle(texte)` qui encode : "AAABBBCC" → "3A3B2C"
2. Écris une fonction `decompresser_rle(texte_compresse)` qui décode
3. Écris une fonction `taux_compression(original, compresse)` qui calcule le ratio
4. Teste avec différents textes (répétitifs vs aléatoires)
5. Étends pour gérer les nombres dans le texte original

## Exercice 9 : Système de recommandation simple
1. Écris une fonction `similarite_jaccard(utilisateur1, utilisateur2)` calcule la similarité entre préférences
2. Écris une fonction `recommandations(utilisateur, historique, k=3)` trouve les k plus proches voisins
3. Écris une fonction `predire_notes(utilisateur, items, similarites)` prédit les notes pour nouveaux items
4. Teste avec un petit jeu de données de films/notes

## Exercice 10 : API météo simulée
Crée un module `meteo.py` qui simule une API météo :
1. `obtenir_temperature(ville, date)` retourne une température aléatoire plausible
2. `obtenir_previsions(ville, jours)` retourne des prévisions pour plusieurs jours
3. `convertir_unites(temperature, unite)` convertit °C ↔ °F ↔ K
4. `indice_confort(temperature, humidite)` calcule un indice de confort
5. `statistiques_mensuelles(ville, mois)` retourne stats historiques
6. Crée un programme principal qui utilise toutes ces fonctions

---

**Conseils pédagogiques :**
1. Commence par écrire les signatures des fonctions (nom, paramètres, retour)
2. Écris les docstrings AVANT d'écrire le code de la fonction
3. Teste chaque fonction isolément avant de les combiner
4. Utilise des jeux de tests variés (cas normaux, limites, erreurs)

**Bonnes pratiques :**
- Une fonction = une responsabilité
- Nomme les fonctions avec des verbes à l'infinitif
- Utilise des paramètres par défaut quand c'est pertinent
- Gère les erreurs avec `try/except`
- Retourne des résultats cohérents (même type, même structure)

**Concepts avancés à explorer :**
- Récursivité (factorielle, Fibonacci, tours de Hanoi)
- Fermetures (closures) et fonctions d'ordre supérieur
- Générateurs (`yield`) pour les séquences infinies
- Décorateurs pour ajouter des fonctionnalités

**Erreurs courantes à éviter :**
- Effets de bord non désirés (modifier les paramètres mutables)
- Variables globales dans les fonctions
- Code trop long ou trop complexe
- Gestion insuffisante des cas d'erreur

**Projets d'intégration :**
1. Calendrier perpétuel avec fonctions pour :
   - Jour de la semaine d'une date
   - Nombre de jours entre deux dates
   - Jours fériés d'une année
   - Calcul d'âge exact

2. Système de gestion de bibliothèque avec fonctions pour :
   - Ajouter/retirer des livres
   - Rechercher par critères
   - Gérer les emprunts
   - Statistiques d'utilisation

**Exercice bonus :** 
Crée un mini-framework de tests unitaires :
- `def test(fonction, entree, sortie_attendue)`
- `def test_avec_exception(fonction, entree, exception_attendue)`
- `def executer_tous_les_tests(tests)`
- Teste tes propres fonctions avec ce framework