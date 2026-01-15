# Exercices sur le traitement d'images avec Python

## Exercice 1 - Concepts fondamentaux
Explique avec tes propres mots :
1. Quelle est la différence entre les couleurs primaires additives (lumière) et soustractives (pigments) ?
2. Comment fonctionne le modèle RGBA ? À quoi sert le canal Alpha ?
3. Qu'est-ce qu'un pixel ? Comment la résolution affecte-t-elle la qualité d'une image ?
4. Pourquoi les images JPEG et PNG ont-elles des tailles si différentes pour un même contenu ?

## Exercice 2 - Manipulation d'images basiques
Écris un programme qui :
1. Charge une image et affiche ses propriétés (format, taille, mode, etc.)
2. Crée 5 versions différentes de l'image :
   - Rogner le centre (50% de la largeur et hauteur)
   - Redimensionner à 25% de la taille originale
   - Convertir en niveaux de gris
   - Miroir horizontal
   - Rotation de 30 degrés
3. Crée une collage de ces 5 images dans une nouvelle image
4. Sauvegarde le résultat avec compression optimisée

## Exercice 3 - Analyse des pixels
Écris un analyseur d'image qui :
1. Calcule l'histogramme des couleurs (distribution des valeurs R, G, B)
2. Trouve la couleur la plus fréquente
3. Détecte si l'image est principalement claire ou sombre
4. Identifie les zones de forte variation de couleur (contours potentiels)
5. Génère une version "posterisée" avec seulement 8 couleurs

## Exercice 4 - Filtres personnalisés
Implémente ces filtres de traitement d'image :
1. **Sépia** : Conversion avec teinte sépia
2. **Flou gaussien** : Approche simple par moyenne des pixels voisins
3. **Détection de contours** : Mise en évidence des changements brusques de couleur
4. **Renforcement** : Augmentation du contraste local
5. **Pixel art** : Réduction du nombre de couleurs et agrandissement des pixels

## Exercice 5 - Watermarking intelligent
Crée un système d'ajout de watermark (filigrane) qui :
1. Place un logo/text en bas à droite avec transparence
2. Crée un watermark discret sur toute l'image (pattern répété)
3. Ajoute des métadonnées dans les pixels (stéganographie simple)
4. Génère un hash de l'image pour détecter les modifications
5. Applique le watermark à un dossier entier d'images

## Exercice 6 - Génération d'images
Utilise `ImageDraw` pour créer :
1. Un graphique à barres à partir de données numériques
2. Un calendrier mensuel avec mise en évidence des weekends
3. Une carte de visite personnalisée avec logo et coordonnées
4. Un diagramme de Gantt simple pour un projet
5. Un motif géométrique fractal (ex: triangle de Sierpinski)

## Exercice 7 - Traitement par lots
Développe un script de traitement par lots qui :
1. Lit tous les images d'un dossier et ses sous-dossiers
2. Redimensionne toutes les images à une taille maximale donnée
3. Convertit les formats (ex: tous les .jpg en .webp)
4. Optimise la compression sans perte notable de qualité
5. Génère un rapport avec statistiques (taille totale économisée, etc.)

## Exercice 8 - Reconnaissance simple
Implémente des fonctions de reconnaissance basique :
1. Détection de visages (via modèle simple ou cascade de Haar)
2. Lecture de code-barres / QR codes
3. OCR simple pour texte clair sur fond uniforme
4. Détection de couleurs dominantes dans des zones
5. Comparaison d'images pour trouver les plus similaires

## Exercice 9 - Montage photo
Crée un outil de montage qui permet :
1. D'ajouter plusieurs images dans un collage avec cadres
2. D'appliquer des filtres différents à chaque partie
3. D'ajouter du texte avec différentes polices et effets
4. De créer des memes avec texte en haut et en bas
5. D'exporter en différentes tailles pour réseaux sociaux

## Exercice 10 - Projet : Processeur d'images web
Conçois un système web de traitement d'images :
1. **Upload** : Interface pour uploader des images
2. **Édition** : Outils basiques (rogner, redimensionner, filtres)
3. **Batch** : Application d'opérations à plusieurs images
4. **Export** : Choix de format et qualité
5. **API** : Endpoint REST pour traitement automatique
6. **Stockage** : Gestion des images traitées avec métadonnées

**Questions de réflexion :**
- Comment optimiser le traitement pour les très grandes images ?
- Quelle stratégie pour la gestion des couleurs (espaces colorimétriques) ?
- Comment assurer la qualité lors de multiples modifications ?
- Quelles sont les implications légales du traitement d'images (droits d'auteur, visages) ?

---

**Scénarios avancés :**
1. Besoin de traiter des images en temps réel (flux vidéo)
2. Images médicales avec exigences de précision extrême
3. Images satellitaires de très grande taille
4. Conservation précise des couleurs pour l'impression professionnelle

**Optimisation :**
- Compare les performances de différentes opérations
- Teste l'utilisation mémoire avec différentes tailles d'images
- Implémente un cache pour les opérations coûteuses
- Utilise le parallélisme pour le traitement par lots

**Bonnes pratiques :**
- Structure ton code avec séparation claire des responsabilités
- Documente les algorithmes utilisés et leurs paramètres
- Crée des tests avec des images de référence
- Gère les erreurs gracieusement (fichiers corrompus, formats non supportés)

**Défis techniques :**
1. Implémente un algorithme de "content-aware resize" (redimensionnement intelligent)
2. Crée un générateur de mosaïques d'images (photo-mosaïque)
3. Développe un système de compression avec perte contrôlée
4. Implémente la détection de duplication d'images (même avec modifications)

**Sécurité :**
- Comment valider qu'une image n'est pas malveillante ?
- Comment protéger les images contre le vol ou la modification non autorisée ?
- Comment anonymiser les visaces dans les images automatiquement ?

**Intégration :**
- Comment intégrer avec des services cloud (AWS S3, Google Cloud Storage) ?
- Comment créer un pipeline de traitement d'images pour un site web ?
- Comment exposer les fonctionnalités via une interface en ligne de commande ?