# Exercices de Développement Front-End - HTML, CSS, JavaScript et Frameworks

## Exercice 1 - Structure HTML Sémantique
Un restaurant veut créer un site web. Il a besoin des sections suivantes : en-tête avec logo et navigation, section principale avec présentation du restaurant, menu hebdomadaire, galerie photos, formulaire de réservation et pied de page.

1. Dessine la structure HTML5 sémantique de cette page en listant les balises que tu utiliserais pour chaque section.
2. Pourquoi préférer `<nav>` à une simple `<div>` pour la navigation ?
3. Quels avantages offrent les balises sémantiques pour le référencement (SEO) ?

## Exercice 2 - Tableaux Accessibles
Tu dois créer un tableau représentant l'emploi du temps d'une classe :

| Heure | Lundi | Mardi | Mercredi |
|-------|-------|-------|----------|
| 9h-10h | Mathématiques | Français | Histoire |
| 10h-11h | Sciences | EPS | Géographie |

1. Écris le code HTML pour ce tableau en le rendant accessible (avec les balises appropriées).
2. Comment ferais-tu pour fusionner deux cellules si un cours durait 2 heures ?
3. Quelles améliorations pourrais-tu apporter pour les utilisateurs de lecteurs d'écran ?

## Exercice 3 - Formulaires et Validation
Crée un formulaire d'inscription avec :
- Nom (obligatoire, 2-50 caractères)
- Email (format valide)
- Mot de passe (8+ caractères, au moins un chiffre et une majuscule)
- Date de naissance (18 ans minimum)
- Newsletter (case à cocher optionnelle)

1. Écris le code HTML avec les attributs de validation HTML5.
2. Comment validerais-tu le mot de passe côté client avec JavaScript ?
3. Pourquoi faut-il aussi valider côté serveur ?

## Exercice 4 - CSS : Modèle de Boîte Mystère
Analyse ce code CSS :
```css
div {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    margin: 10px;
    box-sizing: border-box;
}
```

1. Quelle sera la largeur totale occupée par cet élément sur la page ?
2. Que se passe-t-il si tu changes `box-sizing: border-box` en `box-sizing: content-box` ?
3. Dessine les deux boîtes (avec et sans border-box) pour visualiser la différence.

## Exercice 5 - CSS Flexbox Challenge
Tu dois créer une barre de navigation responsive avec :
- Logo à gauche
- 5 liens centrés
- Bouton de connexion à droite

Sur mobile, les éléments doivent s'empiler verticalement.

1. Écris le HTML et CSS avec Flexbox pour réaliser cette mise en page.
2. Comment gères-tu le passage du mode desktop au mode mobile ?
3. Quelle propriété Flexbox utiliserais-tu pour espacer également les liens ?

## Exercice 6 - CSS Grid Layout
Crée une galerie photo avec CSS Grid qui s'adapte automatiquement :
- 4 colonnes sur desktop
- 2 colonnes sur tablette  
- 1 colonne sur mobile
- Les images doivent garder leur ratio et remplir leur cellule

1. Écris le code CSS Grid pour cette galerie.
2. Comment fais-tu pour qu'une photo puisse occuper 2 colonnes ?
3. Quelle est la différence entre `fr` et `%` comme unité dans Grid ?

## Exercice 7 - JavaScript DOM Manipulation
Tu as une liste de tâches (todo list) avec ce HTML :
```html
<ul id="todo-list">
    <li>Acheter du pain</li>
    <li>Appeler le médecin</li>
</ul>
<input type="text" id="new-task">
<button id="add-btn">Ajouter</button>
```

1. Écris le JavaScript pour ajouter une tâche quand on clique sur le bouton.
2. Ajoute la fonctionnalité pour supprimer une tâche en cliquant dessus.
3. Comment ferais-tu pour sauvegarder les tâches dans le localStorage ?

## Exercice 8 - JavaScript : Gestion d'Événements
Crée un système de votes pour une question :
- Bouton "Pour" qui incrémente un compteur
- Bouton "Contre" qui décrémente un compteur  
- Affichage du résultat
- Limite : 1 vote par utilisateur (simulé avec une variable)

1. Écris le code HTML et JavaScript.
2. Comment empêcher l'utilisateur de voter plusieurs fois ?
3. Que se passe-t-il si deux clics arrivent presque simultanément ? Comment gérer ce cas ?

## Exercice 9 - API Fetch et Promesses
Tu dois afficher la météo d'une ville en utilisant une API publique (comme OpenWeatherMap).

1. Écris une fonction qui récupère les données météo pour une ville donnée.
2. Comment gères-tu les erreurs (ville non trouvée, problème réseau) ?
3. Affiche les données dans une carte stylée avec HTML/CSS.
4. Bonus : ajoute un champ de recherche pour changer de ville.

## Exercice 10 - Vue.js : Liste Interactive
Crée une application Vue.js pour gérer une liste de courses :
- Ajouter un article
- Cocher/décocher un article (acheté/non acheté)
- Supprimer un article
- Filtrer (tous/achetés/non achetés)
- Compter les articles restants

1. Structure les données dans l'instance Vue.
2. Implémente les méthodes nécessaires.
3. Utilise `v-for`, `v-if`, `v-model` et `@click`.

## Exercice 11 - Responsive Design Critique
Analyse ces deux approches pour un site responsive :

**Approche A :** Mobile-first, media queries avec `min-width`
**Approche B :** Desktop-first, media queries avec `max-width`

1. Quels sont les avantages de chaque approche ?
2. Pour un site avec beaucoup de contenu (blog), laquelle choisirais-tu ?
3. Comment tester efficacement le responsive design sur différents appareils ?

## Exercice 12 - Accessibilité Web
Tu développes un formulaire de commande en ligne.

1. Liste 5 bonnes pratiques d'accessibilité à implémenter.
2. Comment rendre un champ de formulaire accessible aux malvoyants ?
3. Quels outils utiliser pour tester l'accessibilité de ton site ?
4. Pourquoi l'accessibilité est-elle importante même pour les utilisateurs sans handicap ?

## Exercice 13 - Performance Web
Un site met 5 secondes à charger complètement. Analyse les problèmes possibles :

1. Quels sont les 3 principaux facteurs qui ralentissent le chargement ?
2. Comment optimiser les images pour le web ?
3. Quelle stratégie adopter pour les fichiers CSS et JavaScript ?
4. Qu'est-ce que le "Critical Rendering Path" et comment l'optimiser ?

## Exercice 14 - CSS : Héritage et Spécificité
Analyse ce code :
```css
#container .item { color: blue; }
div.item.special { color: red; }
.item { color: green; }
```

```html
<div id="container">
    <div class="item special">Texte</div>
</div>
```

1. De quelle couleur sera le texte ? Calcule la spécificité de chaque sélecteur.
2. Quelle est la différence entre `!important` et augmenter la spécificité ?
3. Pourquoi est-il déconseillé d'utiliser des sélecteurs trop spécifiques ou `!important` ?

## Exercice 15 - Projet Complet : Site Portfolio
Conçois un site portfolio pour un photographe avec :

**Exigences :**
- Page d'accueil avec présentation
- Galerie avec filtres par catégorie
- Formulaire de contact
- Page "À propos"
- Design responsive et moderne

**Questions de réflexion :**
1. Quelle architecture de fichiers proposerais-tu (structure des dossiers) ?
2. Comment organiserais-tu le CSS (méthodologie BEM, SMACSS, etc.) ?
3. Quel framework ou bibliothèque utiliserais-tu et pourquoi ?
4. Comment gérerais-tu les images (optimisation, lazy loading) ?
5. Quelles métriques de performance surveillerais-tu ?

## Exercice 16 - JavaScript : Closure et Scope
Analyse ce code :
```javascript
function createCounter() {
    let count = 0;
    return {
        increment: function() {
            count++;
            return count;
        },
        getCount: function() {
            return count;
        }
    };
}

const counter1 = createCounter();
const counter2 = createCounter();
```

1. Que retournera `counter1.getCount()` après avoir appelé `counter1.increment()` 3 fois ?
2. Que retournera `counter2.getCount()` ?
3. Pourquoi les deux compteurs sont-ils indépendants ?
4. Donne un exemple pratique d'utilisation d'une closure.

## Exercice 17 - CSS Animation
Crée une animation CSS pour :
- Un bouton qui change de couleur au survol
- Un chargement (spinner) qui tourne
- Une notification qui apparaît en glissant depuis le haut

1. Quelles propriétés CSS utiliser pour chaque animation ?
2. Quelle est la différence entre `transition` et `animation` ?
3. Comment optimiser les animations pour des performances fluides ?

## Exercice 18 - Gestion d'État avec JavaScript
Tu développes un panier d'achat pour un site e-commerce.

1. Comment stocker les articles du panier (structure de données) ?
2. Comment gérer les quantités, les promotions, les taxes ?
3. Comment synchroniser le panier entre plusieurs onglets du navigateur ?
4. Quelle approche utiliserais-tu pour une application plus complexe (Redux, Vuex, etc.) ?

## Exercice 19 - Tests Front-End
Pour l'application de liste de courses (Exercice 10) :

1. Quels types de tests écrirais-tu (unitaires, d'intégration, end-to-end) ?
2. Donne un exemple de test unitaire pour la fonction d'ajout d'article.
3. Comment tester l'interface utilisateur (clics, saisie) ?
4. Quels outils de testing utiliser (Jest, Cypress, etc.) ?

## Exercice 20 - Sécurité Front-End
Un site permet aux utilisateurs de commenter des articles.

1. Quels risques de sécurité existent ?
2. Comment empêcher les attaques XSS (Cross-Site Scripting) ?
3. Quelles précautions prendre avec les données utilisateur ?
4. Comment sécuriser la communication avec le serveur (HTTPS, tokens) ?

---

**Conseils Pédagogiques :**
- Pour chaque exercice, commence par réfléchir à la solution avant d'écrire du code
- Teste ton code dans différents navigateurs
- Utilise les outils de développement (DevTools) pour déboguer
- Documente tes décisions de conception
- Pense toujours à l'expérience utilisateur et à l'accessibilité
- Mesure les performances de tes solutions