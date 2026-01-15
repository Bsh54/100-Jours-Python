# Exercices sur la manipulation de fichiers Excel - Partie 2

## Exercice 1 - Comparaison des bibliothèques
Compare `xlrd`/`xlwt` et `openpyxl` sur ces points :
1. Support des formats (.xls vs .xlsx)
2. Performances en lecture/écriture
3. Richesse des fonctionnalités (styles, graphiques, formules)
4. Facilité d'utilisation et courbe d'apprentissage
5. Maintenance et communauté

## Exercice 2 - Manipulation de cellules
Écris un programme qui :
1. Crée un classeur avec 5 feuilles différentes
2. Dans chaque feuille, remplit une grille 10x10 avec des nombres aléatoires
3. Utilise les 3 méthodes d'accès aux cellules : `cell()`, notation `['A1']`, itération
4. Compare les temps d'exécution de chaque méthode
5. Modifie les valeurs selon une règle (ex: carré du nombre si pair)

## Exercice 3 - Styles complexes
Crée un template Excel professionnel avec :
1. En-tête avec logo (texte stylisé) et date de génération
2. Pied de page avec numéro de page et nom du fichier
3. Tableau avec bandes de couleur alternées (zebra stripes)
4. Cellules conditionnelles : couleurs selon les valeurs
5. Bordures personnalisées (épaisseurs et couleurs différentes)
6. Police et taille variables selon l'importance des données

## Exercice 4 - Formules avancées
Génère un fichier de gestion de projet avec :
1. Tâches avec : Nom, Début, Fin, Durée, Responsable, % complété
2. Formules automatiques : Durée = Fin - Début
3. Calcul de la durée totale du projet
4. Indicatrice de retard (couleur rouge si Fin > aujourd'hui et % < 100)
5. Tableau de bord avec : % total, tâches en retard, prochain échéancier
6. Utilise des fonctions Excel comme `TODAY()`, `IF()`, `SUMIF()`

## Exercice 5 - Graphiques dynamiques
Crée un rapport de ventes avec :
1. Données mensuelles sur 2 ans
2. 3 graphiques différents : histogramme, courbe, camembert
3. Graphiques qui se mettent à jour quand les données changent
4. Légendes, titres, axes personnalisés
5. Positionnement précis des graphiques dans la feuille
6. Combinaison de types de graphiques (ex: courbe + histogramme)

## Exercice 6 - Template et génération de documents
Développe un système de génération de factures :
1. Template Excel avec zones variables (client, date, produits)
2. Script Python qui remplace les variables par les vraies données
3. Calcul automatique des totaux, TVA, remises
4. Génération d'un PDF à partir du Excel (recherche comment faire)
5. Sauvegarde des données dans une base pour historique

## Exercice 7 - Fusion de données complexe
Écris un programme qui :
1. Lit 5 fichiers Excel avec des structures différentes
2. Normalise les données (noms de colonnes, formats, unités)
3. Fusionne dans un classeur structuré avec onglets
4. Crée des liens entre les onglets (formules de référence)
5. Génère un rapport de consolidation avec graphiques croisés

## Exercice 8 - Validation et nettoyage
Crée un outil de préparation de données qui :
1. Détecte les doublons et propose des actions (fusion, suppression)
2. Identifie les valeurs aberrantes (outliers) selon des règles métier
3. Comble les valeurs manquantes (moyenne, médiane, valeur par défaut)
4. Standardise les formats (dates, nombres, textes)
5. Génère un rapport des modifications apportées

## Exercice 9 - Tableaux croisés dynamiques
Explore les capacités d'`openpyxl` pour :
1. Créer un tableau croisé dynamique simple
2. Configurer les champs (lignes, colonnes, valeurs)
3. Appliquer des filtres et tris
4. Exporter les données du tableau croisé
5. Quelles sont les limitations par rapport à Excel natif ?

## Exercice 10 - Projet : Tableau de bord interactif
Crée un tableau de bord complet pour une petite entreprise :
1. **Données** : Import depuis CSV/JSON/API
2. **Traitement** : Nettoyage, agrégation, calculs
3. **Visualisation** : 5 graphiques minimum avec actualisation
4. **Interactivité** : Filtres par dates, catégories (avec validations de données)
5. **Export** : PDF, HTML, envoi par email automatique
6. **Planification** : Exécution quotidienne via tâche planifiée

**Questions de réflexion :**
- Quand utiliser Python + Excel vs Power BI / Tableau ?
- Comment gérer la confidentialité des données dans les fichiers Excel ?
- Quelle architecture pour une application qui génère des rapports Excel à grande échelle ?
- Comment tester une application qui génère des fichiers Excel ?

---

**Scénarios avancés :**
1. Un fichier doit être généré avec 100 000 lignes et rester utilisable
2. Les graphiques doivent utiliser une palette de couleurs spécifique à la marque
3. Le rapport doit être multilingue (en-têtes selon la langue de l'utilisateur)
4. Intégration avec des templates Word pour créer des rapports combinés

**Optimisation :**
- Mesure l'impact de différents styles sur la taille du fichier
- Teste la lecture/écriture en streaming pour les très gros fichiers
- Compare `openpyxl` en mode `read_only` et `write_only`
- Évalue l'utilisation mémoire avec différents volumes de données

**Bonnes pratiques :**
- Structure ton code en fonctions réutilisables
- Documente les formats d'entrée/sortie attendus
- Gère les erreurs gracieusement (fichier verrouillé, format incorrect)
- Crée des logs pour tracer l'exécution des générations

**Défis techniques :**
1. Implémente une fonction qui crée un onglet avec un calendrier mensuel
2. Génère un diagramme de Gantt à partir de données de projet
3. Crée un système de versioning pour les fichiers générés
4. Développe un comparateur de fichiers Excel qui montre les différences visuellement