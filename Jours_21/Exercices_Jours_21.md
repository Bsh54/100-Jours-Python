# Exercices sur la lecture/écriture de fichiers et gestion des exceptions

## Exercice 1 - Compréhension des concepts
Décris avec tes propres mots la différence entre :
1. Persistance des données et stockage temporaire
2. Fichier texte et fichier binaire
3. Mode 'w' et mode 'a' lors de l'ouverture d'un fichier
4. try/except et try/finally

## Exercice 2 - Modes d'ouverture de fichiers
Pour chaque scénario, choisis le mode d'ouverture approprié et explique ton choix :
1. Lire un fichier de configuration
2. Ajouter des logs à un fichier existant
3. Créer un nouveau fichier de rapport (erreur si le fichier existe déjà)
4. Modifier un fichier existant (lecture et écriture)
5. Copier un fichier image

## Exercice 3 - Lecture de fichiers texte
Écris un programme qui :
1. Ouvre un fichier appelé "notes.txt" en lecture
2. Affiche le nombre total de lignes
3. Affiche le nombre total de caractères (espaces inclus)
4. Affiche le nombre total de mots (séparés par des espaces)
5. Gère les exceptions appropriées si le fichier n'existe pas

## Exercice 4 - Écriture avec formatage
Crée un programme qui demande à l'utilisateur :
1. Son nom
2. Son âge
3. Sa ville
Puis écrit ces informations dans un fichier "profil.txt" avec le format suivant :
```
Nom: [nom]
Âge: [âge]
Ville: [ville]
```

## Exercice 5 - Gestion d'erreurs hiérarchique
Classe les exceptions suivantes par ordre de spécificité (du plus général au plus spécifique) et explique quand elles pourraient se produire :
- Exception
- OSError
- FileNotFoundError
- UnicodeDecodeError
- LookupError

## Exercice 6 - Analyse de code
Pour chaque bloc de code ci-dessous, identifie :
- Ce qu'il fait
- Les erreurs potentielles non gérées
- Comment l'améliorer

**Bloc 1:**
```python
file = open("data.txt", "r")
content = file.read()
print(content)
file.close()
```

**Bloc 2:**
```python
try:
    file = open("data.txt", "r")
    content = file.read()
    print(content)
except:
    pass
```

**Bloc 3:**
```python
with open("data.txt", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line)
```

## Exercice 7 - Copie de fichier par morceaux
Écris une fonction `copier_fichier(source, destination, taille_bloc=1024)` qui :
1. Copie un fichier binaire par morceaux de taille spécifiée
2. Affiche la progression (pourcentage copié)
3. Gère les erreurs de fichier inexistant, permissions, etc.
4. Utilise la syntaxe `with` pour la gestion des fichiers

## Exercice 8 - Journal d'événements
Crée un système simple de journalisation qui :
1. Ouvre un fichier "journal.log" en mode ajout
2. Écrit chaque événement avec un horodatage
3. Format : "[YYYY-MM-DD HH:MM:SS] - Message"
4. Inclut différents niveaux de log (INFO, WARNING, ERROR)
5. Utilise un gestionnaire de contexte

## Exercice 9 - Exception personnalisée
Définis une exception personnalisée `FormatFichierError` qui hérite de `ValueError`.
Ensuite, écris une fonction `valider_fichier_csv(fichier)` qui :
1. Vérifie si le fichier se termine par ".csv"
2. Vérifie si la première ligne contient au moins une virgule
3. Lève ton exception personnalisée avec un message approprié si une condition échoue

## Exercice 10 - Scénario complexe
Imagine que tu développes un programme de sauvegarde. Écris le pseudocode pour :
1. Lire un fichier de configuration (JSON ou texte simple)
2. Vérifier les chemins source et destination
3. Copier les fichiers avec gestion d'erreurs détaillée
4. Créer un rapport de sauvegarde
5. Gérer les cas particuliers (fichiers verrouillés, espace insuffisant, etc.)

**Points à considérer :**
- Quelles exceptions pourraient survenir à chaque étape ?
- Comment assurer la fermeture des ressources ?
- Comment structurer ton code pour la maintenabilité ?
- Comment informer l'utilisateur des problèmes sans interrompre inutilement ?

---

**Conseils pour la réflexion :**
- Pense aux différences entre gestion d'erreurs par exceptions et par valeurs de retour
- Réfléchis à l'impact des encodages dans les applications internationales
- Considère les problèmes de performance avec les gros fichiers
- Imagine comment étendre ces concepts à d'autres types de ressources (réseau, bases de données)