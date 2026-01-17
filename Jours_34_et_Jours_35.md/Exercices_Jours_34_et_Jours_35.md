# 10 Exercices Linux pour la Maîtrise

## Exercice 1 - Navigation et Manipulation de Fichiers
1. Crée la structure de dossiers suivante : `~/projet/src/`, `~/projet/docs/`, `~/projet/tests/`
2. Dans `src/`, crée 3 fichiers : `main.py`, `utils.py`, `config.ini`
3. Copie `main.py` vers `tests/` sous le nom `test_main.py`
4. Liste le contenu de `projet/` de façon récursive avec une commande
5. Quelle commande utiliser pour voir la taille de chaque fichier ?

## Exercice 2 - Permissions et Propriété
```bash
# Situation initiale
-rw-r--r-- 1 alice users 1024 Jun 20 10:00 rapport.txt
```

1. Alice veut que son collègue Bob puisse lire ET modifier le fichier
2. Personne d'autre ne doit y avoir accès
3. Le fichier doit être exécutable par le propriétaire seulement
4. Change le groupe propriétaire en "finance"
5. Quelles commandes utiliser pour chaque étape ?

## Exercice 3 - Recherche et Filtrage
Dans un répertoire contenant des fichiers log :
```
error_20230620.log
access_20230620.log
debug_20230621.log
error_20230621.log
backup.tar.gz
config.yaml
```

1. Trouve tous les fichiers `.log` contenant "ERROR" (majuscules)
2. Trouve les fichiers modifiés dans les dernières 24 heures
3. Extrait les 10 dernières lignes de chaque fichier `error_*.log`
4. Compte le nombre total d'erreurs dans tous les logs
5. Quelle commande trouverait les fichiers > 100MB ?

## Exercice 4 - Processus et Ressources
1. Lance `sleep 3600 &` en arrière-plan
2. Trouve son PID
3. Tue-le proprement (SIGTERM)
4. Lance `top` et identifie :
   - Le processus utilisant le plus de CPU
   - Le processus utilisant le plus de mémoire
5. Comment limiter la consommation mémoire d'un processus ?

## Exercice 5 - Script Shell : Backup Automatique
Écris un script qui :
1. Crée un backup du répertoire `/var/www/` avec timestamp
2. Compresse le backup en `.tar.gz`
3. Garde seulement les 7 derniers backups
4. Envoie un email si le backup échoue
5. Se lance automatiquement tous les jours à 2h du matin

Quelle serait la structure du script ?

## Exercice 6 - Gestion des Utilisateurs
Un nouveau développeur arrive dans l'équipe :
1. Crée l'utilisateur "dev123" avec home directory
2. Ajoute-le au groupe "developers"
3. Donne-lui les droits sudo pour seulement certaines commandes
4. Configure son mot de passe pour expirer dans 90 jours
5. Comment vérifier qu'il ne peut pas accéder à `/root/` ?

## Exercice 7 - Surveillance Système
Le serveur est lent. Diagnostique :
1. Quelles commandes pour identifier la source du problème ?
2. Comment vérifier l'espace disque restant ?
3. Comment voir les connexions réseau actives ?
4. Quels logs consulter pour des erreurs système ?
5. Propose 3 métriques à surveiller en permanence

## Exercice 8 - Configuration Réseau
Problème : le serveur ne peut pas se connecter à internet
1. Vérifie la configuration IP de l'interface réseau
2. Teste la connectivité vers 8.8.8.8
3. Vérifie la table de routage
4. Examine les règles du firewall
5. Quels fichiers de configuration éditer pour corriger ?

## Exercice 9 - Analyse de Logs Apache
Logs Apache dans `/var/log/apache2/access.log` :
```
192.168.1.100 - - [20/Jun/2023:10:30:45] "GET /index.html HTTP/1.1" 200 1234
192.168.1.101 - - [20/Jun/2023:10:31:22] "POST /login HTTP/1.1" 401 567
192.168.1.100 - - [20/Jun/2023:10:32:11] "GET /admin.php HTTP/1.1" 403 789
```

1. Compte le nombre de requêtes par IP
2. Trouve les requêtes qui ont échoué (status 4xx ou 5xx)
3. Extrait les 5 pages les plus visitées
4. Détecte les tentatives de brute force (plus de 10 requêtes/minute)
5. Comment automatiser cette analyse quotidiennement ?

## Exercice 10 - Scénario Critique
Une application en production plante :
1. Comment récupérer rapidement les logs avant qu'ils ne tournent ?
2. Comment capturer un core dump pour analyse ?
3. Quelles commandes pour monitorer en temps réel ?
4. Comment redémarrer le service sans perdre les connexions actives ?
5. Quelle procédure mettre en place pour éviter la récidive ?

---

**Méthode d'apprentissage :**
1. **Pratique** : Utilise une VM ou Docker pour tester
2. **Comprendre** : Ne pas juste copier, saisir le "pourquoi"
3. **Documente** : Crée ton propre cheatsheet
4. **Automatise** : Scripte les tâches répétitives
5. **Partage** : Explique à quelqu'un d'autre

**Mnémoniques utiles :**
- `chmod` : u=user, g=group, o=others, a=all
- Permissions : 4=r, 2=w, 1=x (ex: 755 = rwxr-xr-x)
- Redirections : `>` écraser, `>>` ajouter, `2>&1` combiner sorties
- Processus : `ps aux` = voir tout, `kill -9` = dernier recours