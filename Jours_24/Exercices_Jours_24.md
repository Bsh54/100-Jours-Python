# Exercices sur la manipulation de fichiers Excel - Partie 1

## Exercice 1 - Compréhension des concepts
Explique avec tes propres mots :
1. Pourquoi Python a-t-il besoin de bibliothèques tierces pour manipuler Excel ?
2. Quelles sont les différences entre `xlrd`/`xlwt` et `openpyxl` ?
3. Qu'est-ce qu'un classeur, une feuille, une cellule dans Excel ?
4. Pourquoi les dates dans Excel sont-elles stockées différemment des autres nombres ?

## Exercice 2 - Analyse de l'API
À partir du code d'exemple, réponds aux questions :
1. Comment `xlrd` représente-t-il différents types de données dans les cellules ?
2. Quelle est la différence entre `row_values()` et `row_slice()` ?
3. Comment gérer les cellules fusionnées avec `xlrd` ?
4. Que fait `xlrd.xldate_as_tuple(value, 0)` et pourquoi le deuxième paramètre ?

## Exercice 3 - Création de classeur
Crée un programme qui génère un fichier Excel `budget.xls` avec :
1. Deux feuilles : "Dépenses" et "Revenus"
2. Dans "Dépenses" : colonnes Date, Catégorie, Montant, Description
3. Dans "Revenus" : colonnes Date, Source, Montant, Fréquence
4. 10 lignes de données aléatoires par feuille
5. Une ligne "TOTAL" à la fin de chaque feuille avec somme des montants

## Exercice 4 - Style avancé
Reprends l'exemple des scores et améliore le style :
1. En-têtes avec fond bleu clair, police blanche en gras
2. Notes < 60 en rouge, notes >= 90 en vert
3. Bordures fines noires sur toutes les cellules
4. Hauteur de ligne de 25px pour les données, 30px pour l'en-tête
5. Alignement centré pour toutes les cellules

## Exercice 5 - Calculs avec formules
Crée un fichier Excel `ventes.xls` pour un magasin :
1. Colonnes : Produit, PrixUnitaire, Quantité, Total
2. 15 produits différents
3. Utilise une formule Excel pour calculer Total = PrixUnitaire * Quantité
4. Ajoute en bas : Moyenne des prix, Somme des quantités, Somme des totaux (avec formules)
5. Ajoute une colonne "Remise" avec formule conditionnelle : 10% si Quantité > 100

## Exercice 6 - Conversion de formats
Écris un programme qui :
1. Lit un fichier CSV contenant des données d'étudiants
2. Convertit en fichier Excel avec mise en forme
3. Crée une feuille par département/filière
4. Ajoute des graphiques (si possible avec `xlwt`/`xlrd`)
5. Calcule les statistiques par feuille (moyennes, écarts-types)

## Exercice 7 - Fusion de données
Écris un script qui fusionne plusieurs fichiers Excel :
1. Tous les fichiers ont la même structure
2. Fusionne les données dans un nouveau classeur
3. Conserve les styles originaux ou applique un style unifié
4. Gère les doublons (mêmes ID ou clés)
5. Produit un rapport de fusion (nombre de lignes par fichier source)

## Exercice 8 - Validation de données
Crée un validateur pour fichiers Excel qui vérifie :
1. Types de données cohérents par colonne
2. Plages de valeurs acceptables (ex: âge entre 0 et 120)
3. Formats de dates valides
4. Références croisées (clés étrangères entre feuilles)
5. Formules non cassées (pas de références à des cellules supprimées)

## Exercice 9 - Automatisation de rapport
Imagine que tu dois générer un rapport mensuel :
1. Lit les données brutes depuis plusieurs fichiers Excel
2. Nettoie les données (valeurs manquantes, incohérentes)
3. Calcule les KPI (indicateurs clés de performance)
4. Génère un classeur avec :
   - Feuille "Résumé" avec tableaux de bord
   - Feuille "Détails" avec données agrégées
   - Feuille "Graphiques" avec visualisations
5. Applique un template de style corporate

## Exercice 10 - Projet : Gestion de stocks
Crée un système de gestion de stocks avec Excel :
1. **Structure** : Produit, Référence, QuantitéStock, SeuilMin, PrixAchat, PrixVente
2. **Mouvements** : Entrées (achats), Sorties (ventes), Ajustements
3. **Alertes** : Couleurs conditionnelles pour stocks bas
4. **Calculs** : Valeur du stock, Marge, Rotation
5. **Rapports** : Journal des mouvements, État des stocks, Statistiques

**Questions de réflexion :**
- Comment gérer les accès concurrents si plusieurs personnes modifient le même fichier ?
- Quelle stratégie pour les sauvegardes et versioning des fichiers Excel ?
- Comment optimiser les performances avec des fichiers très gros (>100 000 lignes) ?
- Quelles sont les limites de `xlwt`/`xlrd` par rapport à une vraie base de données ?

---

**Exercices bonus :**
1. Crée un template Excel avec styles prédéfinis et utilise-le pour générer des rapports
2. Implémente un système de logs qui enregistre toutes les modifications apportées
3. Écris un script qui extrait toutes les formules d'un classeur Excel
4. Crée un convertisseur Excel vers HTML (tableau web stylé)

**Scénarios complexes :**
1. Un fichier a des formules qui référencent d'autres fichiers
2. Les données sont sur plusieurs feuilles avec relations entre elles
3. Tu dois gérer des fuseaux horaires différents dans les dates
4. Le fichier utilise des macros (VBA) que tu dois préserver

**Conseils pédagogiques :**
- Teste avec différents formats de dates (américain, européen, etc.)
- Essaie d'ouvrir tes fichiers générés dans différents logiciels (Excel, LibreOffice, Google Sheets)
- Mesure les temps d'exécution avec des fichiers de différentes tailles
- Documente les limitations que tu découvres (types de graphiques non supportés, etc.)