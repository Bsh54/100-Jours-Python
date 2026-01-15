# Exercices sur la manipulation de fichiers Word et PowerPoint

## Exercice 1 - Compréhension des concepts
Explique avec tes propres mots :
1. Qu'est-ce qu'un "espace réservé" (placeholder) dans un document Word ?
2. Quelle est la différence entre un paragraphe (`paragraph`) et un "run" dans `python-docx` ?
3. Pourquoi est-il préférable de manipuler les `runs` plutôt que le texte directement ?
4. Comment les styles sont-ils gérés dans Word et comment les reproduire en Python ?

## Exercice 2 - Analyse de structure
À partir du code d'exemple, réponds aux questions :
1. Comment accéder à différents types de contenus dans un document Word ?
2. Quelle est la différence entre `add_paragraph()` et `add_run()` ?
3. Comment gérer les tableaux et leurs cellules ?
4. Comment ajouter des images avec des dimensions spécifiques ?

## Exercice 3 - Génération de documents simples
Crée un programme qui génère un rapport Word avec :
1. Page de titre avec titre, auteur, date
2. Table des matières automatique
3. 3 sections avec titres hiérarchiques
4. Listes à puces et numérotées
5. Tableau de données avec en-têtes
6. Images avec légendes
7. En-têtes et pieds de page personnalisés

## Exercice 4 - Template avancé
Crée un template de contrat avec :
1. En-tête avec logo et informations de l'entreprise
2. Sections variables : client, dates, montants, conditions
3. Clauses conditionnelles (certaines sections apparaissent seulement si certaines conditions sont remplies)
4. Signatures avec espaces pour dates et noms
5. Annexes avec numérotation automatique
6. Styles professionnels (polices, marges, interlignes)

## Exercice 5 - Traitement de documents existants
Écris un programme qui :
1. Lit un dossier contenant des documents Word
2. Extrait des informations spécifiques (ex: dates, noms, montants)
3. Génère un rapport consolidé en Excel
4. Identifie les documents qui ne suivent pas le format attendu
5. Renomme les fichiers selon un schéma standard

## Exercice 6 - Conversion et extraction
Crée un convertisseur qui :
1. Extrait tout le texte d'un document Word en conservant la structure
2. Convertit les tableaux Word en CSV
3. Extrait toutes les images et les sauvegarde avec des noms significatifs
4. Génère un fichier Markdown à partir du Word
5. Compare deux versions d'un document et montre les différences

## Exercice 7 - PowerPoint dynamique
Génère une présentation PowerPoint pour un rapport mensuel :
1. Diapositive de titre avec logo
2. Diapositive d'agenda automatique
3. Diapositives de données avec graphiques (utilisation de placeholders)
4. Transition entre diapositives
5. Animations sur les éléments (si supportées par `python-pptx`)
6. Notes du présentateur

## Exercice 8 - Fusion de données PowerPoint
Écris un programme qui :
1. Prend un template PowerPoint avec des placeholders
2. Remplit avec des données depuis une base de données ou un fichier CSV
3. Génère une présentation par client/projet
4. Personnalise les couleurs et images selon le client
5. Exporte également un PDF de la présentation

## Exercice 9 - Système de génération de documents
Conçois un système qui génère :
1. Une offre commerciale (Word)
2. La présentation associée (PowerPoint)
3. Le contrat (Word)
4. Le bon de commande (Excel)
À partir d'une seule source de données, avec cohérence entre tous les documents.

## Exercice 10 - Projet complet : Gestionnaire de documentation
Crée un système de gestion de documentation technique :
1. **Templates** : Pour différents types de documents (spécifications, manuels, rapports)
2. **Versioning** : Suivi des modifications, comparaison entre versions
3. **Approval workflow** : Génération de documents pour review, tracking des approbations
4. **Publication** : Génération de PDF, HTML, et versions imprimables
5. **Recherche** : Indexation du contenu pour recherche full-text

**Questions de réflexion :**
- Comment gérer les références croisées entre documents ?
- Quelle stratégie pour la gestion des images et ressources externes ?
- Comment assurer la cohérence quand plusieurs personnes génèrent des documents ?
- Comment versionner les templates eux-mêmes ?

---

**Scénarios complexes :**
1. Un document doit inclure des formules mathématiques complexes
2. Besoin de générer des documents en plusieurs langues
3. Les documents contiennent des liens hypertextes internes et externes
4. Nécessité de générer des documents accessibles (conformes aux normes d'accessibilité)

**Optimisation :**
- Comment générer 1000+ documents rapidement ?
- Comment minimiser la taille des fichiers générés ?
- Comment gérer la mémoire avec de très gros documents ?

**Bonnes pratiques :**
- Structure ton code avec des classes pour différents types de documents
- Utilise des fichiers de configuration pour les templates et styles
- Logge les erreurs et les documents générés
- Crée des tests unitaires pour les fonctions de génération

**Défis techniques :**
1. Implémente un système de "mail merge" avancé avec conditions et boucles
2. Crée un générateur de CV qui s'adapte au template choisi
3. Développe un convertisseur Word → PowerPoint (extraction des titres et points clés)
4. Crée un éditeur de documents collaboratif en ligne avec génération de Word/PDF