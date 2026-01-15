# Exercices sur l'envoi d'emails et SMS avec Python

## Exercice 1 - Compréhension des protocoles
Explique avec tes propres mots :
1. Comment fonctionne SMTP ? Quel est son rôle dans l'envoi d'emails ?
2. Quelle est la différence entre SMTP, POP3 et IMAP ?
3. Pourquoi utilise-t-on souvent SSL/TLS avec SMTP ?
4. Comment le format MIME permet-il d'envoyer des pièces jointes ?

## Exercice 2 - Configuration et sécurité
Réponds aux questions suivantes :
1. Pourquoi ne pas mettre les identifiants SMTP directement dans le code ?
2. Comment gérer les erreurs SMTP courantes (refus de connexion, authentification échouée) ?
3. Qu'est-ce qu'un "code d'autorisation" et en quoi diffère-t-il d'un mot de passe ?
4. Comment limiter l'envoi d'emails non sollicités (spam) depuis ton application ?

## Exercice 3 - Envoi d'emails basique
Écris un programme qui :
1. Envoie un email texte simple à plusieurs destinataires
2. Gère correctement les accents et caractères spéciaux
3. Ajoute un en-tête "Reply-To" différent de l'expéditeur
4. Utilise une connexion sécurisée (SSL/TLS)
5. Logge le succès ou l'échec de chaque envoi

## Exercice 4 - Emails HTML avec pièces jointes
Crée un système d'envoi d'emails avec template HTML :
1. Template HTML avec variables (nom, date, montant, etc.)
2. Images intégrées (pas en pièces jointes)
3. Pièces jointes multiples avec noms de fichiers corrects
4. Version texte brut alternative
5. Suivi d'ouverture (pixel tracking simple)

## Exercice 5 - Newsletter automatisée
Développe un système de newsletter qui :
1. Lit une liste d'abonnés depuis un fichier CSV/Excel
2. Personnalise chaque email (cher [Nom], ...)
3. Gère les désinscriptions (liste noire)
4. Planifie l'envoi à des heures spécifiques
5. Génère un rapport d'envoi (emails livrés, rebonds)

## Exercice 6 - Services SMS tiers
Compare 3 services SMS (Twilio, Vonage, ou services français) :
1. Processus d'inscription et configuration
2. Tarification et limites
3. Fonctionnalités offertes (SMS, MMS, vérification)
4. Qualité de la documentation et des API
5. Support client et fiabilité

## Exercice 7 - Système de vérification
Implémente un système de vérification par SMS/email :
1. Génère un code à 6 chiffres avec expiration (5 minutes)
2. Envoie le code par SMS ou email au choix
3. Valide le code saisi par l'utilisateur
4. Limite les tentatives (3 essais max)
5. Bloque temporairement après trop de demandes

## Exercice 8 - Notifications d'alerte
Crée un système de notifications pour une application :
1. Niveaux de priorité (info, warning, error, critical)
2. Canaux multiples (email, SMS, webhook)
3. Escalade (si pas d'acknowledgement en X minutes)
4. Groupes de destinataires par type d'alerte
5. Templates de message selon le type d'alerte

## Exercice 9 - Gestion des rebonds et erreurs
Écris un gestionnaire robuste qui :
1. Détecte les emails rebonds (bounce) et les supprime de la liste
2. Gère les quotas dépassés (attente avant nouvel envoi)
3. Retente l'envoi en cas d'erreur temporaire
4. Archive les emails envoyés avec statut
5. Génère des alertes pour problèmes récurrents

## Exercice 10 - Projet : Système de communication
Conçois un système complet de communication :
1. **Base de données** : Contacts avec préférences (email, SMS, les deux)
2. **Templates** : Messages types avec variables
3. **Planification** : Envoi différé, répétition
4. **Suivi** : Ouvertures, clics, réponses
5. **API REST** : Endpoints pour envoyer/recevoir
6. **Interface web** : Dashboard de gestion

**Questions de réflexion :**
- Comment assurer la confidentialité des données (RGPD en Europe) ?
- Quelle stratégie pour gérer les très gros volumes d'envois ?
- Comment prévenir l'utilisation abusive du système ?
- Comment mesurer la délivrabilité et améliorer les taux d'ouverture ?

---

**Scénarios complexes :**
1. Envoi à 100 000 destinataires avec personnalisation
2. Emails transactionnels en temps réel (commandes, factures)
3. Campagnes marketing A/B testing
4. Intégration avec un CRM existant

**Optimisation :**
- Comment paralléliser l'envoi d'emails sans dépasser les limites ?
- Comment minimiser le temps d'envoi pour de grandes listes ?
- Quelle stratégie de cache pour les templates ?

**Bonnes pratiques :**
- Ne jamais exposer les clés API/identifiants dans le code
- Utiliser des variables d'environnement ou un vault de secrets
- Implémenter des retry avec exponential backoff
- Tester avec des adresses de test avant l'envoi réel

**Défis techniques :**
1. Implémente un système de file d'attente (queue) pour les envois massifs
2. Crée un générateur d'emails responsive qui s'affiche bien sur mobile
3. Développe un analyseur d'emails rebonds pour classifier les erreurs
4. Implémente l'envoi d'emails via plusieurs fournisseurs (fallback)

**Sécurité :**
- Comment valider que l'expéditeur est autorisé ?
- Comment prévenir l'injection de contenu malveillant dans les templates ?
- Comment chiffrer les données sensibles dans les emails ?

**Tests :**
- Comment simuler l'envoi d'emails en environnement de test ?
- Comment tester les différents scénarios d'erreur ?
- Comment mesurer les performances du système ?

**Intégration :**
- Comment intégrer avec un système d'authentification existant ?
- Comment exposer les fonctionnalités via une API GraphQL ?
- Comment créer des webhooks pour les événements (livré, ouvert, cliqué) ?