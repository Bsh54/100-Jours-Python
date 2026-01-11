# Exercices sur l'Application de la POO

## Exercice 1 - Système de gestion de bibliothèque
Créez un système de bibliothèque avec:
- `Document`: classe abstraite avec `titre`, `auteur`, méthode abstraite `emprunter()`
- `Livre`: hérite de Document, ajoute `isbn`, `nombre_pages`
- `DVD`: hérite de Document, ajoute `duree`, `realisateur`
- `Membre`: avec `nom`, `liste_documents_empruntes`, `limite_emprunts`
- `Bibliotheque`: singleton qui gère tous les documents et membres

Ajoutez un système d'emprunt/retour avec validation.

## Exercice 2 - Jeu d'échecs simplifié
Créez un échiquier 8x8 avec:
- `Piece`: classe abstraite avec `couleur` (BLANC/NOIR), position, méthode abstraite `mouvements_valides()`
- Sous-classes: `Pion`, `Tour`, `Cavalier`, `Fou`, `Dame`, `Roi` avec leurs règles de mouvement
- `Echiquier`: gère la position des pièces, vérifie les collisions
- `JeuEchecs`: orchestre le jeu, tours alternés, détection d'échec

## Exercice 3 - Système de réservation de billets
Créez un système pour un cinéma/théâtre:
- `Evenement`: spectacle, film, concert avec `nom`, `date`, `heure`, `capacité`
- `Siege`: avec `numero`, `rangee`, `categorie` (standard, VIP)
- `Reservation`: avec `client`, `evenement`, `liste_sieges`, `prix_total`
- `SystemeReservation`: gère la disponibilité, calcule les prix, applique les promotions

## Exercice 4 - Simulation de réseau social
Créez un réseau social minimal:
- `Utilisateur`: avec `nom`, `email`, `amis` (liste d'autres utilisateurs), `publications`
- `Publication`: avec `contenu`, `date`, `auteur`, `likes`, `commentaires`
- `Commentaire`: avec `contenu`, `date`, `auteur`
- `ReseauSocial`: gère les utilisateurs, suggestions d'amis, fil d'actualité

## Exercice 5 - Système de gestion de commandes e-commerce
Créez un système complet:
- `Client`: avec `nom`, `adresse`, `historique_commandes`
- `Produit`: avec `nom`, `prix`, `stock`, `categorie`
- `Commande`: avec `client`, `liste_produits_quantites`, `statut` (en attente, expédiée, livrée)
- `Panier`: avec `client`, `produits_selectionnes`
- `SystemePaiement`: abstrait, avec sous-classes `CarteCredit`, `PayPal`, `Virement`

## Exercice 6 - Jeu de rôle (RPG) simple
Créez un jeu de rôle textuel:
- `Personnage`: avec `nom`, `points_vie`, `force`, `defense`, `inventaire`
- `Arme` et `Armure`: classes avec attributs de bonus
- `Monstre`: avec `points_vie`, `attaque`, `loot` (liste d'objets)
- `Salle`: avec `description`, `monstres`, `objets`, `sorties` (autres salles)
- `Jeu`: gère la navigation, combats, inventaire

## Exercice 7 - Calculateur d'impôts
Créez un système de calcul d'impôts:
- `Contribuable`: avec `revenu_annuel`, `situation_familiale`, `nombre_enfants`
- `Deduction`: abstraite, avec sous-classes `DeductionLogement`, `DeductionFamille`, etc.
- `TrancheImposition`: avec `min`, `max`, `taux`
- `CalculateurImpot`: applique les tranches, déductions, calcule le net

## Exercice 8 - Système de gestion de tâches (Todo List)
Créez un système avancé:
- `Tache`: avec `titre`, `description`, `date_echeance`, `priorite`, `statut`
- `Projet`: avec `nom`, `liste_taches`, `membres_equipe`
- `Utilisateur`: avec `taches_assignees`, `projets`
- `SystemeNotification`: notifie des échéances, changements de statut
- `Filtre`: pour filtrer les tâches par priorité, date, etc.

## Exercice 9 - Simulateur de banque
Créez un système bancaire:
- `Compte`: abstrait, avec sous-classes `CompteCourant`, `CompteEpargne`, `CompteEntreprise`
- `Transaction`: avec `montant`, `date`, `type` (dépôt, retrait, virement)
- `Client`: avec `liste_comptes`, `informations_personnelles`
- `Banque`: avec `liste_clients`, `taux_interet_epargne`
- `SystemeSecurite`: détecte les activités suspectes

## Exercice 10 - Système de réservation de voyages
Créez un système complet:
- `Destination`: avec `ville`, `pays`, `attractions`
- `Hotel`: avec `nom`, `etoiles`, `chambres_disponibles`, `prix_nuit`
- `Vol`: avec `compagnie`, `numero`, `depart`, `arrivee`, `prix`
- `Voyage`: combine `hotel`, `vol`, `activites`
- `ReservationVoyage`: avec `client`, `voyage`, `date_depart`, `date_retour`
- `AgentVoyage`: système qui suggère des voyages basés sur le budget/préférences

---

## Questions de Réflexion Critique

1. Quand utiliser une classe abstraite vs une interface? Python n'a pas d'interfaces formelles - comment les simuler?

2. Comment gérer les relations circulaires entre classes (ex: A a une liste de B, B a une référence à A)?

3. Quand utiliser l'héritage vs la composition? Donnez des exemples où la composition est meilleure.

4. Comment éviter le "God Object" anti-pattern (une classe qui fait trop de choses)?

5. Quelle est la différence entre `isinstance()` et `type()`? Quand utiliser chacun?

6. Comment gérer la persistance des objets (sauvegarde/chargement depuis fichier/BDD)?

7. Comment tester efficacement les hiérarchies de classes complexes?

8. Quels sont les avantages/inconvénients des singletons? Comment les implémenter proprement?

9. Comment gérer les versions différentes d'objets (migration de schéma)?

10. Quand faut-il utiliser le pattern Factory vs construire les objets directement?

---

## Défis Avancés (Optionnels)

1. Implémentez un moteur de règles d'entreprise avec classes `Regle`, `Condition`, `Action`.

2. Créez un système de workflow avec `Etat`, `Transition`, `Workflow`.

3. Implémentez un système de cache distribé avec `NoeudCache`, `Strategy` (LRU, FIFO).

4. Créez un ORM complet avec relations 1-N, N-N, héritage, requêtes.

5. Implémentez un système d'événements distribués avec `Producteur`, `Consommateur`, `Message`.

---

## Projet Intégrateur

Créez un système de gestion d'université avec:
- `Personne` → `Etudiant`, `Professeur`, `Administratif`
- `Cours` avec `prerequis`, `credits`, `horaire`
- `Departement` avec `liste_cours`, `liste_professeurs`
- `Inscription` gère les inscriptions aux cours avec validation des prérequis
- `Notes` avec système de calcul de moyenne, mentions
- `EmploiDuTemps` génère automatiquement les horaires sans conflits
- `SystemePaiement` gère les frais de scolarité
- `Bibliotheque` avec système de prêt de livres
- `Cantine` avec gestion des repas, menus

Contraintes:
- Utilisez au moins 3 design patterns différents
- Implémentez la sérialisation JSON pour sauvegarder l'état
- Gestion d'erreurs complète avec exceptions personnalisées
- Interface en ligne de commande ou web simple
- Tests unitaires pour chaque classe importante

---

**Conseils pédagogiques:**
- Commencez par dessiner les diagrammes de classe UML
- Identifiez les relations entre classes (héritage, composition, agrégation, association)
- Pensez à la séparation des responsabilités (Single Responsibility Principle)
- Utilisez des énumérations pour les données limitées (statuts, types, etc.)
- Implémentez d'abord le modèle, puis les fonctionnalités
- Testez avec des données réelles/mock
- Refactorez régulièrement pour améliorer la conception
- Documentez avec des exemples d'utilisation
- Pensez aux cas limites et aux erreurs possibles