# Exercices sur les expressions régulières en Python

## Exercice 1 - Compréhension des concepts
Explique avec tes propres mots :
1. Quelle est la différence entre `match()`, `search()` et `fullmatch()` ?
2. Pourquoi utiliser des "raw strings" (chaînes brutes) avec les regex ?
3. Que sont les groupes de capture et à quoi servent-ils ?
4. Quelle est la différence entre les quantificateurs gourmands et non gourmands ?

## Exercice 2 - Métacaractères et classes
Pour chaque expression régulière, décris ce qu'elle correspond :
1. `^[A-Z][a-z]*\s\d{1,2},?\s\d{4}$`
2. `\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b`
3. `(?i)password\s*[:=]\s*(\S+)`
4. `<!--.*?-->`
5. `(?<=@)\w+(?=\.)`

## Exercice 3 - Validation de données
Écris des regex pour valider :
1. Une adresse email (format basique)
2. Une date au format JJ/MM/AAAA (avec validation des jours/mois)
3. Un code postal français (5 chiffres)
4. Un numéro de téléphone français (format international ou national)
5. Un mot de passe (8+ caractères, majuscule, minuscule, chiffre, caractère spécial)
6. Une URL HTTP/HTTPS
7. Un numéro de sécurité sociale français (format simplifié)
8. Un identifiant Python valide (lettre ou _ suivi de lettres/chiffres/_)

## Exercice 4 - Extraction de données
Écris un programme qui extrait d'un texte :
1. Toutes les adresses emails
2. Toutes les URLs
3. Tous les hashtags (#mot) et mentions (@utilisateur)
4. Tous les montants d'argent (ex: 12,50 €, $15.99, 100EUR)
5. Tous les numéros de page (ex: Page 12, p. 45, pp. 67-69)

## Exercice 5 - Nettoyage de texte
Crée un nettoyeur de texte qui :
1. Supprime les balises HTML mais conserve le texte
2. Normalise les espaces (supprime les espaces multiples, tabulations)
3. Supprime la ponctuation excessive (!!! ??? ...,)
4. Formate les nombres (ex: 1,000,000 → 1000000)
5. Extrait seulement les phrases complètes (terminées par . ! ?)

## Exercice 6 - Analyse de logs
Écris un analyseur de logs Apache/Nginx qui :
1. Extrait l'IP, la date, la méthode HTTP, l'URL, le code de statut
2. Identifie les requêtes suspectes (SQL injection patterns)
3. Compte les requêtes par IP
4. Trouve les URLs les plus fréquentes
5. Détecte les erreurs (codes 4xx, 5xx)

## Exercice 7 - Template engine simple
Crée un moteur de templates basique :
1. Remplace `{{ variable }}` par une valeur
2. Supporte les boucles `{% for item in list %}...{% endfor %}`
3. Supporte les conditions `{% if condition %}...{% endif %}`
4. Gère l'échappement HTML automatique
5. Permet l'inclusion de templates

## Exercice 8 - Parser de mini-langage
Développe un parser pour un langage de configuration simple :
```
# Commentaire
server {
    port 8080;
    host "localhost";
    routes {
        "/home" -> "index.html";
        "/api/*" -> "api_handler";
    }
}
```
Le parser doit valider la syntaxe et produire un dictionnaire Python.

## Exercice 9 - Recherche avancée
Implémente une recherche de texte avec :
1. Opérateurs booléens (AND, OR, NOT)
2. Recherche de phrases exactes (guillemets)
3. Wildcards (* pour plusieurs caractères, ? pour un caractère)
4. Proximité (mots à N mots de distance)
5. Recherche insensible à la casse et aux accents

## Exercice 10 - Projet : Validateur de code
Crée un validateur de code Python qui :
1. Vérifie les imports valides
2. Détecte les variables non utilisées
3. Identifie les fonctions trop longues (> 50 lignes)
4. Cherche les patterns anti-patterns (ex: `== True`)
5. Valide les docstrings (présence, format)
6. Extrait les TODOs et FIXMEs des commentaires

**Questions de réflexion :**
- Quand faut-il utiliser une regex vs un parser dédié ?
- Comment optimiser une regex pour de grandes quantités de texte ?
- Quelles sont les limites des regex (ex: HTML nesting) ?
- Comment déboguer une regex complexe ?

---

**Scénarios complexes :**
1. Extraction de tables depuis du texte semi-structuré
2. Détection de langage naturel simple
3. Normalisation de dates dans différents formats
4. Analyse de fichiers CSV avec guillemets et échappements

**Optimisation :**
- Compare `findall()` vs `finditer()` pour la mémoire
- Teste la compilation de regex vs usage direct
- Mesure l'impact des lookaheads/lookbehinds sur la performance

**Bonnes pratiques :**
- Documente tes regex avec des commentaires et des exemples
- Utilise des groupes nommés pour la clarté
- Teste avec des cas limites et des inputs malveillants
- Évite les backtracking catastrophiques

**Défis techniques :**
1. Implémente une regex pour les nombres en lettres (ex: "cent vingt-trois")
2. Crée un système de recherche/replace avec callback
3. Développe un validateur de JSON basique avec regex
4. Écris un tokenizer pour un langage simple

**Sécurité :**
- Comment éviter les attaques ReDoS (Regular Expression Denial of Service) ?
- Comment valider les inputs utilisateur de manière sûre ?
- Quelles regex sont dangereuses et pourquoi ?

**Tests :**
- Crée une suite de tests pour tes regex (cas positifs et négatifs)
- Utilise des property-based tests pour trouver des cas limites
- Teste avec du texte Unicode (emojis, caractères spéciaux)

**Applications réelles :**
- Analyse de logs système
- Nettoyage de données avant import
- Validation de formulaires web
- Extraction d'information depuis des documents
- Recherche dans une base de code