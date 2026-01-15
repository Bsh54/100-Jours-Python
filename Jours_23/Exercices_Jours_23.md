# Exercices sur les fichiers CSV en Python

## Exercice 1 - Compréhension des concepts
Explique avec tes propres mots :
1. Qu'est-ce qu'un fichier CSV et pourquoi est-il si largement utilisé ?
2. Quels sont les avantages et inconvénients du CSV par rapport à JSON ?
3. Pourquoi peut-on ouvrir un fichier CSV avec un éditeur de texte ET avec Excel ?
4. Qu'est-ce qu'un "dialecte" CSV et pourquoi existe-t-il différents dialectes ?

## Exercice 2 - Analyse de cas
Pour chaque scénario, indique si le CSV est un bon choix et explique pourquoi :
1. Sauvegarder les paramètres de configuration d'une application
2. Exporter 100 000 lignes de données depuis une base de données
3. Échanger des données entre un système Python et un système Java
4. Stocker des données avec des champs contenant des virgules et des sauts de ligne
5. Sauvegarder des données binaires (images, sons)

## Exercice 3 - Écriture CSV avancée
Écris un programme qui génère un fichier CSV `temperature.csv` avec :
1. Une ligne d'en-tête : Date, Ville, TempératureMin, TempératureMax, Précipitations
2. 30 jours de données aléatoires pour 3 villes différentes
3. Utilise un point-virgule comme séparateur
4. Encadre tous les champs avec des guillemets doubles
5. Ajoute une ligne de commentaire au début du fichier (commençant par #)

## Exercice 4 - Lecture avec traitement
Écris une fonction `analyser_scores(csv_file)` qui :
1. Lit le fichier `scores.csv` de l'exemple
2. Calcule la moyenne de chaque élève
3. Trouve la meilleure note par matière
4. Identifie l'élève avec la meilleure moyenne générale
5. Produit un rapport formaté et sauvegarde les statistiques dans un nouveau CSV

## Exercice 5 - Gestion des cas complexes
Comment gérerais-tu ces situations dans un fichier CSV ?
1. Un champ contient une virgule : "Paris, France"
2. Un champ contient des guillemets : `Il a dit "Bonjour"`
3. Un champ contient un saut de ligne : adresse sur plusieurs lignes
4. Les données contiennent des caractères Unicode : "Café", " naïve"
5. Le fichier a des en-têtes mais certaines lignes ont des colonnes manquantes

## Exercice 6 - Conversion de formats
Écris un programme qui :
1. Lit un fichier JSON contenant une liste d'utilisateurs
2. Convertit les données en CSV avec colonnes : id, nom, email, age, ville
3. Gère les utilisateurs optionnels (certains n'ont pas d'âge ou de ville)
4. Propose deux options de sortie : avec et sans en-têtes
5. Permet de choisir le séparateur (virgule, point-virgule, tabulation)

## Exercice 7 - Validation de données
Crée un validateur de fichiers CSV qui vérifie :
1. Toutes les lignes ont le même nombre de colonnes
2. Les types de données sont cohérents dans chaque colonne
3. Aucune ligne n'est complètement vide
4. Les dates sont dans un format valide
5. Les nombres sont dans des plages acceptables
Le programme doit produire un rapport d'erreurs détaillé.

## Exercice 8 - Comparaison CSV vs pandas
Recherche et compare :
1. Les fonctionnalités de base du module `csv` vs `pandas.read_csv()`
2. Quand utiliser l'un plutôt que l'autre
3. Les limitations du module `csv`
4. Les avantages de `pandas` pour l'analyse de données
5. Le coût en mémoire de chaque approche

## Exercice 9 - Fusion de fichiers CSV
Écris un programme qui fusionne plusieurs fichiers CSV :
1. Tous les fichiers ont les mêmes colonnes mais des données différentes
2. Certains fichiers peuvent avoir des colonnes supplémentaires
3. Gère les doublons (mêmes données dans plusieurs fichiers)
4. Produit un fichier consolidé avec statistiques (nombre de lignes fusionnées, etc.)
5. Option : fusionner seulement certaines colonnes spécifiées

## Exercice 10 - Projet : Gestionnaire de contacts
Crée un système de gestion de contacts avec CSV :
1. **Structure** : nom, prénom, téléphone, email, entreprise, tags
2. **CRUD** : ajouter, modifier, supprimer, rechercher des contacts
3. **Recherche** : par nom, entreprise, tags
4. **Import/Export** : depuis/vers JSON, vCard, autres CSV
5. **Statistiques** : nombre de contacts par entreprise, tags les plus utilisés

**Questions de réflexion :**
- Comment gérer les relations plusieurs-à-plusieurs (un contact avec plusieurs tags) en CSV ?
- Comment optimiser la recherche dans un gros fichier CSV ?
- Quelle stratégie pour éviter la corruption des données lors des modifications ?
- Comment versionner les données (suivi des modifications) ?

---

**Exercices bonus :**
1. Modifie l'exemple des scores pour utiliser `DictWriter` et `DictReader`. Quels sont les avantages ?
2. Crée un dialecte CSV personnalisé pour un format spécifique à ton domaine
3. Écris un script qui détecte automatiquement le séparateur et l'encodage d'un fichier CSV
4. Implémente une lecture "paresseuse" (lazy) pour les très gros fichiers CSV

**Conseils pédagogiques :**
- Expérimente avec différents séparateurs et caractères d'encadrement
- Essaie d'ouvrir tes fichiers CSV générés dans Excel, LibreOffice et un éditeur de texte
- Teste les limites : que se passe-t-il avec des données très volumineuses ?
- Compare la performance du module `csv` avec la lecture manuelle (split sur les virgules)