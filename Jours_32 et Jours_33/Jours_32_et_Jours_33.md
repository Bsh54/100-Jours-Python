## Vue d'ensemble du développement front-end

> **Note :** Certaines illustrations utilisées dans ce document sont tirées du livre *[HTML and CSS: Design and Build Websites](https://www.amazon.cn/dp/1118008189/ref=sr_1_5?__mk_zh_CN=%E4%BA%9A%E9%A9%AC%E9%80%8A%E7%BD%91%E7%AB%99&keywords=html+%26+css&qid=1554609325&s=gateway&sr=8-5)* de *Jon Duckett*, un excellent ouvrage d'introduction au développement front-end. Les lecteurs intéressés peuvent trouver ce livre sur Amazon ou d'autres sites de vente en ligne.

HTML est un langage utilisé pour décrire les pages web. Son acronyme signifie Hyper-Text Markup Language, soit langage de balisage hypertexte. Les textes, boutons, images, vidéos, etc., que nous voyons lors de la navigation sur le web sont tous décrits via HTML et restitués par le navigateur.

### Brève histoire du HTML

1. **Octobre 1991** : Un document informel du CERN ([Organisation européenne pour la recherche nucléaire](https://fr.wikipedia.org/wiki/Organisation_europ%C3%A9enne_pour_la_recherche_nucl%C3%A9aire)) présente pour la première fois 18 balises HTML publiques. L'auteur de ce document est le physicien [Tim Berners-Lee](https://fr.wikipedia.org/wiki/Tim_Berners-Lee), inventeur du [World Wide Web](https://fr.wikipedia.org/wiki/World_Wide_Web) et président du [World Wide Web Consortium (W3C)](https://fr.wikipedia.org/wiki/World_Wide_Web_Consortium).
2. **Novembre 1995** : Publication de la norme HTML 2.0 (RFC 1866).
3. **Janvier 1997** : HTML 3.2 est publié en tant que recommandation du W3C.
4. **Décembre 1997** : HTML 4.0 est publié en tant que recommandation du W3C.
5. **Décembre 1999** : HTML 4.01 est publié en tant que recommandation du W3C.
6. **Janvier 2008** : HTML5 est publié par le W3C en tant qu'ébauche de travail (Working Draft).
7. **Mai 2011** : Le W3C fait passer HTML5 au stade de "Last Call" (dernière consultation).
8. **Décembre 2012** : Le W3C désigne HTML5 comme "Candidate Recommendation" (recommandation candidate).
9. **Octobre 2014** : HTML5 est publié en tant que recommandation stable du W3C, marquant l'achèvement de sa standardisation.

#### Nouvelles fonctionnalités de HTML5

1. Prise en charge native du multimédia (balises `audio` et `video`).
2. Contenu programmable (balise `canvas`).
3. Web sémantique (balises `article`, `aside`, `details`, `figure`, `footer`, `header`, `nav`, `section`, `summary`, etc.).
4. Nouveaux contrôles de formulaire (calendrier, email, recherche, curseur, etc.).
5. Meilleure prise en charge du stockage hors ligne (`localStorage` et `sessionStorage`).
6. Prise en charge de la géolocalisation, du glisser-déposer (drag and drop), des WebSockets, des tâches en arrière-plan, etc.

### Structurer le contenu avec des balises

#### Structure de base

- `html`
  - `head`
    - `title`
    - `meta`
  - `body`

#### Texte

- **Titres (heading) et paragraphes (paragraph)**
  - `h1` à `h6`
  - `p`
- **Exposant (superscript) et indice (subscript)**
  - `sup`
  - `sub`
- **Espaces blancs (white space folding)**
- **Saut de ligne (break) et ligne horizontale (horizontal ruler)**
  - `br`
  - `hr`
- **Balises sémantiques**
  - Mise en gras et emphase - `strong`
  - Citation longue - `blockquote`
  - Abréviation et acronyme - `abbr` / `acronym`
  - Citation - `cite`
  - Informations de contact - `address`
  - Modifications du contenu - `ins` / `del`

#### Listes (list)

- **Liste ordonnée (ordered list)** - `ol` / `li`
- **Liste non ordonnée (unordered list)** - `ul` / `li`
- **Liste de définitions (definition list)** - `dl` / `dt` / `dd`

#### Liens (anchor)

- Lien vers une page
- Lien d'ancrage (anchor link)
- Lien fonctionnel (mailto, tel, etc.)

#### Images (image)

- **Emplacement de stockage des images** (chemins relatifs/absolus)
- **Image et ses dimensions** (attributs `width` et `height`)
- **Choisir le bon format d'image**
  - JPEG
  - GIF
  - PNG
- **Image vectorielle** (SVG)
- **Balises sémantiques** - `figure` / `figcaption`

#### Tableaux (table)

- **Structure de base d'un tableau** - `table` / `tr` / `td` / `th`
- **Titre du tableau** - `caption`
- **Fusion de cellules** - attributs `rowspan` et `colspan`
- **Tableaux longs** - `thead` / `tbody` / `tfoot`

#### Formulaires (form)

- **Attributs importants** - `action` / `method` / `enctype`
- **Contrôles de formulaire (input)** - attribut `type`
  - Champ texte - `text` / Mot de passe - `password` / Nombre - `number`
  - Email - `email` / Téléphone - `tel` / Date - `date` / Curseur - `range` / URL - `url` / Recherche - `search`
  - Bouton radio - `radio` / Case à cocher - `checkbox`
  - Téléchargement de fichier - `file` / Champ caché - `hidden`
  - Bouton d'envoi - `submit` / Bouton image - `image` / Bouton de réinitialisation - `reset`
- **Liste déroulante** - `select` / `option`
- **Zone de texte multiligne** - `textarea`
- **Regrouper des éléments de formulaire** - `fieldset` / `legend`

#### Audio et vidéo (audio / video)

- Formats vidéo et lecteurs
- Hébergement vidéo
- Préparatifs pour ajouter une vidéo
- Balise `video` et ses attributs - `autoplay` / `controls` / `loop` / `muted` / `preload` / `src`
- Balise `audio` et ses attributs - `autoplay` / `controls` / `loop` / `muted` / `preload` / `src` / `width` / `height` / `poster`

#### Cadres (frame)

- **Jeu de cadres (obsolète, déconseillé)** - `frameset` / `frame`
- **Cadre intégré (iframe)** - `iframe`

#### Divers

- **Type de document (doctype)**

  ```HTML
  <!doctype html>
  ```
  Ou les anciennes déclarations strictes ou transitionnelles de HTML 4.

- **Commentaires**

  ```HTML
  <!-- Ceci est un commentaire. Les commentaires ne peuvent pas être imbriqués. -->
  ```

- **Attributs**
  - `id` : Identifiant unique
  - `class` : Classe de l'élément, pour le style ou la sélection
  - `title` : Information supplémentaire (infobulle au survol)
  - `tabindex` : Ordre de tabulation
  - `contenteditable` : Indique si l'élément est éditable
  - `draggable` : Indique si l'élément peut être glissé-déposé

- **Élément de bloc (block-level) / Élément en ligne (inline-level)**
- **Entités de caractères (character entities)**

  Exemples : `&lt;` pour `<`, `&gt;` pour `>`, `&amp;` pour `&`, `&nbsp;` pour un espace insécable.

### Styliser la page avec CSS

#### Introduction

- Rôle du CSS
- Fonctionnement du CSS
- Règles, propriétés et valeurs

  ```
  sélecteur {
      propriété: valeur;
  }
  ```
- **Sélecteurs courants** : sélecteur de type, sélecteur de classe, sélecteur d'ID, sélecteur universel, sélecteur d'attribut, etc.

#### Couleurs (color)

- Comment spécifier une couleur (noms, hexadécimal, rgb, rgba, hsl, hsla)
- Terminologie des couleurs et contraste
- Couleur d'arrière-plan (`background-color`)

#### Texte (text / font)

- **Taille et famille de police** (`font-size` / `font-family`)
  - Unités : px, em, rem, %, etc.
  - Familles : polices à empattements (serif), sans empattements (sans-serif), à chasse fixe (monospace).

- **Graisse, style, étirement et décoration** (`font-weight` / `font-style` / `font-stretch` / `text-decoration`)

- **Interligne, espacement des lettres et des mots** (`line-height` / `letter-spacing` / `word-spacing`)

- **Alignement et retrait** (`text-align` / `text-indent`)

- **Style des liens** (`:link` / `:visited` / `:active` / `:hover`)

- **Nouvelles propriétés CSS3**
  - Ombre portée - `text-shadow`
  - Première lettre et première ligne - `::first-letter` / `::first-line`
  - Réaction à l'interaction utilisateur

#### Modèle de boîte (box model)

- **Contrôle de la taille de la boîte** (`width` / `height`)
- **Bordure, marge externe et marge interne** (`border` / `margin` / `padding`)
- **Affichage et masquage de la boîte** (`display` / `visibility`)
- **Nouvelles propriétés CSS3**
  - Image de bordure - `border-image`
  - Ombre portée - `box-shadow`
  - Coins arrondis - `border-radius`

#### Listes, tableaux et formulaires

- **Puces des listes** (`list-style`)
- **Bordure et arrière-plan des tableaux** (`border-collapse`)
- **Apparence des contrôles de formulaire**
- **Alignement des contrôles de formulaire**
- **Outils de développement des navigateurs** (pour inspecter et déboguer)

#### Images

- **Contrôle de la taille des images** (`display: inline-block`)
- **Alignement des images**
- **Image d'arrière-plan** (`background` / `background-image` / `background-repeat` / `background-position`)

#### Mise en page (layout)

- **Contrôle de la position des éléments** (`position` / `z-index`)
  - Flux normal (normal flow)
  - Positionnement relatif (relative)
  - Positionnement absolu (absolute)
  - Positionnement fixe (fixed)
  - Éléments flottants (`float` / `clear`)
- **Mise en page de site web**
  - Mise en page HTML5 (utilisation des balises sémantiques pour la structure)
- **Adaptation aux différentes tailles d'écran**
  - Mise en page à largeur fixe
  - Mise en page fluide (fluid layout)
  - Grilles de mise en page (layout grids)

### Contrôler le comportement avec JavaScript

#### Syntaxe de base de JavaScript

- Instructions et commentaires
- Variables et types de données
  - Déclaration et assignation
  - Types de données primitifs et objets
  - Règles de nommage des variables
- Expressions et opérateurs
  - Opérateurs d'assignation
  - Opérateurs arithmétiques
  - Opérateurs de comparaison
  - Opérateurs logiques : `&&` (ET), `||` (OU), `!` (NON)
- Structures conditionnelles
  - `if...else...`
  - `switch...case...default...`
- Boucles
  - Boucle `for`
  - Boucle `while`
  - Boucle `do...while`
- Tableaux (arrays)
  - Créer un tableau
  - Manipuler les éléments d'un tableau
- Fonctions
  - Déclarer une fonction
  - Appeler une fonction
  - Paramètres et valeur de retour
  - Fonction anonyme
  - Fonction immédiatement invoquée (IIFE)

#### Programmation orientée objet

- Concept d'objet
- Syntaxe littérale pour créer un objet
- Opérateur d'accès aux membres (`.` ou `[]`)
- Syntaxe du constructeur pour créer un objet
  - Mot-clé `this`
- Ajouter et supprimer des propriétés
  - Mot-clé `delete`
- Objets natifs standard
  - `Number` / `String` / `Boolean` / `Symbol` / `Array` / `Function`
  - `Date` / `Error` / `Math` / `RegExp` / `Object` / `Map` / `Set`
  - `JSON` / `Promise` / `Generator` / `Reflect` / `Proxy`

#### BOM (Browser Object Model)

- Propriétés et méthodes de l'objet `window`
- Objet `history`
  - `forward()` / `back()` / `go()`
- Objet `location`
- Objet `navigator`
- Objet `screen`

#### DOM (Document Object Model)

- Arborescence DOM (DOM tree)
- Accéder aux éléments
  - `getElementById()` / `querySelector()`
  - `getElementsByClassName()` / `getElementsByTagName()` / `querySelectorAll()`
  - `parentNode` / `previousSibling` / `nextSibling` / `children` / `firstChild` / `lastChild`
- Manipuler les éléments
  - `nodeValue`
  - `innerHTML` / `textContent` / `createElement()` / `createTextNode()` / `appendChild()` / `insertBefore()` / `removeChild()`
  - `className` / `id` / `hasAttribute()` / `getAttribute()` / `setAttribute()` / `removeAttribute()`
- Gestion des événements (event handling)
  - Types d'événements
    - Événements d'interface utilisateur (UI) : `load` / `unload` / `error` / `resize` / `scroll`
    - Événements clavier : `keydown` / `keyup` / `keypress`
    - Événements souris : `click` / `dblclick` / `mousedown` / `mouseup` / `mousemove` / `mouseover` / `mouseout`
    - Événements de focus : `focus` / `blur`
    - Événements de formulaire : `input` / `change` / `submit` / `reset` / `cut` / `copy` / `paste` / `select`
  - Associer un gestionnaire d'événements
    - Gestionnaire d'événements HTML (obsolète, à éviter pour séparer structure et comportement)
    - Gestionnaire d'événements DOM traditionnel (un seul gestionnaire par élément)
    - Écouteur d'événements (`addEventListener`) - méthode recommandée
  - Flux des événements (event flow) : capture puis bouillonnement (bubbling)
  - Objet événement (`event`)
    - `target` (ou `srcElement` dans les anciens IE)
    - `type`
    - `cancelable`
    - `preventDefault()` (empêcher l'action par défaut)
    - `stopPropagation()` (arrêter la propagation, `cancelBubble` dans les anciens IE)
  - Événements souris - position de l'événement
    - Position à l'écran : `screenX` et `screenY`
    - Position dans la page : `pageX` et `pageY`
    - Position dans le viewport : `clientX` et `clientY`
  - Événements clavier - quelle touche a été pressée
    - Propriété `keyCode` (ou `which` dans certains navigateurs)
    - Convertir en caractère : `String.fromCharCode(event.keyCode)`
  - Événements HTML5
    - `DOMContentLoaded` (DOM chargé, sans attendre les ressources)
    - `hashchange` (changement du fragment d'URL, #...)
    - `beforeunload` (avant de quitter la page)

#### API JavaScript modernes

- **Stockage côté client** - `localStorage` et `sessionStorage`
  ```JavaScript
  localStorage.colorSetting = '#a4509b';
  localStorage['colorSetting'] = '#a4509b';
  localStorage.setItem('colorSetting', '#a4509b');
  ```
- **Géolocalisation** - API `geolocation`
  ```JavaScript
  navigator.geolocation.getCurrentPosition(function(pos) {
      console.log(pos.coords.latitude);
      console.log(pos.coords.longitude);
  });
  ```
- **Récupérer des données d'un serveur** - API Fetch
- **Dessiner des graphiques** - API `<canvas>`
- **Audio et vidéo** - API `<audio>` et `<video>`

### Frameworks front-end

#### Framework progressif - [Vue.js](https://vuejs.org/)

Framework essentiel pour le développement en mode "front-end rendu" (single-page application).

##### Premiers pas

1. Inclure le fichier JavaScript de Vue (depuis un CDN par exemple).
   ```HTML
   <script src="https://cdn.jsdelivr.net/npm/vue"></script>
   ```
2. Liaison de données (rendu déclaratif).
   ```HTML
   <div id="app">
       <h1>{{ product }} - Informations sur le stock</h1>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue"></script>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               product: 'iPhone X'
           }
       });
   </script>
   ```
3. Conditions et boucles.
   ```HTML
   <div id="app">
       <h1>Informations sur le stock</h1>
       <hr>
       <ul>
           <li v-for="product in products">
               {{ product.name }} - {{ product.quantity }}
               <span v-if="product.quantity === 0">
                   Épuisé
               </span>
           </li>
       </ul>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue"></script>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               products: [
                   {"id": 1, "name": "iPhone X", "quantity": 20},
                   {"id": 2, "name": "Huawei Mate20", "quantity": 0},
                   {"id": 3, "name": "Xiaomi Mix3", "quantity": 50}
               ]
           }
       });
   </script>
   ```
4. Propriétés calculées (computed properties).
   ```HTML
   <!-- Ajouter dans le template du précédent exemple : -->
   <h2>Stock total : {{ totalQuantity }} unités</h2>
   <!-- Et dans la configuration Vue : -->
   <script>
       const app = new Vue({
           // ... el et data comme avant ...
           computed: {
               totalQuantity() {
                   return this.products.reduce((sum, product) => sum + product.quantity, 0);
               }
           }
       });
   </script>
   ```
5. Gestion des événements.
   ```HTML
   <!-- Ajouter un bouton dans la boucle : -->
   <button @click="product.quantity += 1">Augmenter le stock</button>
   ```
6. Saisie utilisateur (liaison bidirectionnelle avec `v-model`).
   ```HTML
   <!-- Remplacer l'affichage de la quantité par un champ input : -->
   <input type="number" v-model.number="product.quantity" min="0">
   ```
7. Charger des données JSON depuis le réseau (avec `fetch` dans le hook `created`).

##### Utiliser l'outil en ligne de commande (CLI) - vue-cli

Vue fournit un outil de génération de projet (scaffolding) très pratique pour les projets professionnels : vue-cli. Il permet d'automatiser la configuration des environnements de développement, test et production, laissant le développeur se concentrer sur le code métier.

1. Installer vue-cli globalement via npm.
2. Créer un nouveau projet avec `vue create nom-du-projet`.
3. Installer les dépendances (si ce n'est pas fait automatiquement).
4. Lancer le serveur de développement avec `npm run serve`.

#### Framework d'interface utilisateur - [Element UI](http://element.eleme.io/)

Bibliothèque de composants pour le bureau, basée sur Vue 2.0, permettant de construire des interfaces utilisateur avec support du responsive design.

1. Inclure les fichiers CSS et JavaScript d'Element.
   ```HTML
   <!-- Style -->
   <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
   <!-- Bibliothèque JavaScript -->
   <script src="https://unpkg.com/element-ui/lib/index.js"></script>
   ```
2. Un exemple simple (bouton ouvrant une boîte de dialogue).
3. Utiliser des composants (comme un tableau `el-table` avec des données).

#### Framework de visualisation de données - [ECharts](https://echarts.apache.org/)

Bibliothèque open source de visualisation de données, souvent utilisée pour générer divers types de graphiques et tableaux de bord.

#### Framework CSS basé sur Flexbox - [Bulma](https://bulma.io/)

Bulma est un framework CSS moderne basé sur Flexbox, conçu "mobile first" et modulaire. Il permet de réaliser facilement des mises en page simples ou complexes, même sans grande expertise en CSS.

```HTML
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Bulma</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
    <style>
        .column { background-color: #063; color: white; margin: 10px; padding: 10px; text-align: center; }
    </style>
</head>
<body>
    <div class="columns">
        <div class="column">Colonne 1</div>
        <div class="column">Colonne 2</div>
        <div class="column">Colonne 3</div>
    </div>
    <!-- Boutons avec différentes couleurs -->
    <button class="button is-primary">Primaire</button>
    <button class="button is-link">Lien</button>
    <button class="button is-success">Succès</button>
    <!-- Barre de progression -->
    <progress class="progress is-danger is-medium" value="60" max="100">60%</progress>
    <!-- Tableau -->
    <table class="table is-hoverable">
        <!-- Contenu du tableau -->
    </table>
</body>
</html>
```

#### Framework de mise en page responsive - [Bootstrap](https://getbootstrap.com/)

Framework front-end pour le développement rapide d'applications web, avec un système de grille et des composants prêts à l'emploi, supportant le responsive design.

1. **Caractéristiques**
   - Compatibilité avec les principaux navigateurs et appareils mobiles
   - Courbe d'apprentissage douce
   - Conception responsive

2. **Contenu**
   - Système de grille (grid system)
   - Classes CSS utilitaires
   - Composants pré-construits (boutons, formulaires, navigation, etc.)
   - Plugins JavaScript (modales, carrousels, etc.)

3. **Outils visuels** comme LayoutIt! pour construire des interfaces Bootstrap de manière visuelle.