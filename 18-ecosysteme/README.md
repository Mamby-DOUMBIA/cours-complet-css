# Module 18 — Écosystème CSS

> **Niveau :** Expert | **Durée estimée :** 6 heures

---

## 18.1 Introduction à Sass / SCSS

### Qu'est-ce que Sass ?

**Sass** (Syntactically Awesome Style Sheets) est un **préprocesseur CSS** : un outil qui ajoute des fonctionnalités supplémentaires au CSS (variables, imbrication, mixins, fonctions) et génère du CSS standard que le navigateur comprend.

**SCSS** est la syntaxe moderne de Sass — elle utilise les accolades et points-virgules comme le CSS standard, ce qui la rend facile à prendre en main.

### Installation

```bash
# Via npm
npm install -D sass

# Compiler un fichier SCSS en CSS
npx sass styles/main.scss styles/main.css

# Mode watch (recompile à chaque modification)
npx sass --watch styles/main.scss styles/main.css
```

### Les variables Sass

```scss
// Variables SCSS (différentes des variables CSS natives)
$couleur-principale: #3498db;
$couleur-secondaire: #2ecc71;
$police-base: 'Inter', sans-serif;
$taille-base: 16px;
$espace-base: 8px;

.bouton {
  background-color: $couleur-principale;
  font-family: $police-base;
  padding: $espace-base * 1.5 $espace-base * 3;
}
```

### L'imbrication (nesting)

```scss
// SCSS — avant compilation
.navigation {
  background-color: #2c3e50;
  padding: 0 20px;

  // Imbrication : .navigation ul
  ul {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  // .navigation li
  li {
    &:first-child { margin-left: 0; }
    &:last-child  { margin-right: 0; }
  }

  // .navigation a
  a {
    color: white;
    text-decoration: none;
    padding: 16px 20px;
    display: block;
    transition: background 0.2s;

    // .navigation a:hover
    &:hover {
      background-color: rgba(255,255,255,0.1);
    }

    // .navigation a.actif
    &.actif {
      font-weight: bold;
      border-bottom: 3px solid #3498db;
    }
  }
}

/* CSS généré — après compilation */
.navigation { background-color: #2c3e50; padding: 0 20px; }
.navigation ul { display: flex; list-style: none; margin: 0; padding: 0; }
.navigation li:first-child { margin-left: 0; }
.navigation li:last-child { margin-right: 0; }
.navigation a { color: white; text-decoration: none; padding: 16px 20px; display: block; transition: background 0.2s; }
.navigation a:hover { background-color: rgba(255,255,255,0.1); }
.navigation a.actif { font-weight: bold; border-bottom: 3px solid #3498db; }
```

### Les mixins

```scss
// Définition d'un mixin (comme une fonction réutilisable)
@mixin flex-center($direction: row) {
  display: flex;
  flex-direction: $direction;
  justify-content: center;
  align-items: center;
}

@mixin responsive($taille) {
  @if $taille == mobile {
    @media (max-width: 576px) { @content; }
  } @else if $taille == tablette {
    @media (max-width: 768px) { @content; }
  } @else if $taille == desktop {
    @media (min-width: 992px) { @content; }
  }
}

@mixin ombre-carte($intensite: 1) {
  box-shadow:
    0 2px 4px rgba(0, 0, 0, 0.05 * $intensite),
    0 8px 16px rgba(0, 0, 0, 0.08 * $intensite);
}

// Utilisation des mixins
.hero {
  @include flex-center(column);
  height: 100vh;
}

.carte {
  padding: 24px;
  @include ombre-carte(1.5);

  @include responsive(mobile) {
    padding: 16px;
  }
}
```

### Les extensions (`@extend`)

```scss
// Classe de base
%bouton-base {
  display: inline-flex;
  align-items: center;
  padding: 10px 20px;
  border: none;
  border-radius: 6px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

// Extensions
.btn-principal {
  @extend %bouton-base;
  background: #3498db;
  color: white;
  &:hover { background: #2980b9; }
}

.btn-secondaire {
  @extend %bouton-base;
  background: transparent;
  color: #3498db;
  border: 2px solid #3498db;
  &:hover { background: #3498db; color: white; }
}
```

### Les fonctions Sass

```scss
@use 'sass:math';
@use 'sass:color';

// Fonction personnalisée
@function rem($px) {
  @return math.div($px, 16px) * 1rem;
}

h1 { font-size: rem(32px); } // → 2rem
p  { font-size: rem(16px); } // → 1rem

// Manipulation de couleurs
$base: #3498db;
.bouton-hover {
  background: color.adjust($base, $lightness: -10%);
}
```

---

## 18.2 Introduction à Tailwind CSS

### Concept : Utility-first CSS

**Tailwind CSS** est un framework CSS **"utility-first"** : au lieu d'écrire des classes sémantiques (`.carte`, `.bouton`), vous composez votre design en appliquant directement des classes utilitaires prédéfinies sur vos éléments HTML.

```html
<!-- CSS classique -->
<button class="bouton-principal">Cliquer</button>

<!-- Tailwind CSS -->
<button class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-4 rounded-lg transition-colors duration-200">
  Cliquer
</button>
```

### Installation

```bash
npm install -D tailwindcss
npx tailwindcss init

# tailwind.config.js généré automatiquement
```

```javascript
// tailwind.config.js
module.exports = {
  content: ['./src/**/*.{html,js,jsx}'],
  theme: {
    extend: {
      colors: {
        'bleu-marque': '#3498db',
      }
    }
  },
  plugins: []
}
```

```css
/* styles/input.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Classes Tailwind essentielles

```html
<!-- Mise en page Flexbox -->
<div class="flex justify-center items-center gap-4 flex-wrap">

<!-- Mise en page Grid -->
<div class="grid grid-cols-3 gap-6">

<!-- Typographie -->
<h1 class="text-4xl font-bold text-gray-900 leading-tight">
<p class="text-base text-gray-600 leading-relaxed max-w-prose">

<!-- Espacements -->
<div class="p-6 m-4 mt-8 mb-4 px-6 py-3">

<!-- Couleurs -->
<div class="bg-white text-gray-800 border border-gray-200">
<button class="bg-blue-500 hover:bg-blue-600 text-white">

<!-- Bordures et ombres -->
<div class="rounded-lg shadow-md border border-gray-100">

<!-- Responsive -->
<div class="w-full sm:w-1/2 lg:w-1/3">
<div class="text-sm md:text-base lg:text-lg">

<!-- États -->
<button class="bg-blue-500 hover:bg-blue-600 focus:ring-2 focus:ring-blue-300 active:bg-blue-700 disabled:opacity-50">

<!-- Dark mode -->
<div class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white">
```

### Composants avec `@apply`

```css
/* Extraire des classes réutilisables */
@layer components {
  .btn {
    @apply inline-flex items-center px-4 py-2 rounded-lg font-semibold transition-colors duration-200;
  }

  .btn-primary {
    @apply btn bg-blue-500 text-white hover:bg-blue-600;
  }

  .btn-secondary {
    @apply btn border-2 border-blue-500 text-blue-500 hover:bg-blue-500 hover:text-white;
  }

  .card {
    @apply bg-white rounded-xl shadow-md p-6 border border-gray-100;
  }
}
```

---

## 18.3 Introduction à Bootstrap

### Qu'est-ce que Bootstrap ?

**Bootstrap** est un framework CSS **component-based** : il fournit des composants prêts à l'emploi (boutons, modales, navigations, grilles) avec un design cohérent.

```html
<!-- Intégration via CDN -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

### Le système de grille Bootstrap (12 colonnes)

```html
<div class="container">
  <div class="row">
    <!-- 12 colonnes sur mobile, 6 sur tablette, 4 sur desktop -->
    <div class="col-12 col-md-6 col-lg-4">Colonne 1</div>
    <div class="col-12 col-md-6 col-lg-4">Colonne 2</div>
    <div class="col-12 col-md-6 col-lg-4">Colonne 3</div>
  </div>
</div>
```

### Composants Bootstrap

```html
<!-- Boutons -->
<button class="btn btn-primary">Principal</button>
<button class="btn btn-secondary">Secondaire</button>
<button class="btn btn-danger btn-sm">Petit danger</button>

<!-- Carte -->
<div class="card shadow-sm">
  <img src="image.jpg" class="card-img-top" alt="">
  <div class="card-body">
    <h5 class="card-title">Titre</h5>
    <p class="card-text">Contenu...</p>
    <a href="#" class="btn btn-primary">Lire</a>
  </div>
</div>

<!-- Navigation -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container">
    <a class="navbar-brand" href="#">MonSite</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link active" href="#">Accueil</a></li>
        <li class="nav-item"><a class="nav-link" href="#">Contact</a></li>
      </ul>
    </div>
  </div>
</nav>

<!-- Alertes -->
<div class="alert alert-success alert-dismissible fade show" role="alert">
  Opération réussie !
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

## 18.4 Introduction à PostCSS

**PostCSS** est un outil qui transforme le CSS avec des plugins JavaScript. Il permet d'utiliser des fonctionnalités CSS futures dès aujourd'hui.

```bash
npm install -D postcss postcss-cli autoprefixer cssnano
```

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    require('autoprefixer'),  // Ajoute les préfixes navigateurs automatiquement
    require('cssnano')({      // Minifie le CSS
      preset: 'default'
    })
  ]
}
```

```css
/* CSS en entrée */
.element {
  display: flex;
  user-select: none;
}

/* CSS en sortie (avec autoprefixer) */
.element {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
}
```

---

## 18.5 Comparatif des outils

| Outil | Type | Avantages | Inconvénients |
|-------|------|-----------|---------------|
| **CSS natif** | Langage | Standard, pas de compilation | Répétitif sur grands projets |
| **Sass/SCSS** | Préprocesseur | Puissant, variables, mixins | Compilation nécessaire |
| **Tailwind CSS** | Framework utility-first | Rapide, personnalisable, petit bundle | Classes HTML longues, courbe d'apprentissage |
| **Bootstrap** | Framework component | Prêt à l'emploi, documentation riche | Design générique, bundle lourd |
| **PostCSS** | Post-processeur | Très flexible, plugins variés | Configuration nécessaire |

### Quand utiliser quoi ?

| Projet | Recommandation |
|--------|---------------|
| Apprentissage CSS | CSS natif uniquement |
| Site vitrine, blog | CSS natif + variables CSS |
| Application Web complexe | Tailwind CSS ou Sass |
| Prototype rapide | Bootstrap |
| Site institutionnel | Sass + BEM |
| Projet avec équipe | Tailwind ou Sass selon culture d'équipe |

---

## 📌 Résumé

| Outil | Commande clé | Point fort |
|-------|-------------|-----------|
| Sass | `npx sass --watch` | Variables, mixins, nesting |
| Tailwind | `npx tailwindcss -w` | Classes utilitaires, productivité |
| Bootstrap | CDN ou npm | Composants prêts |
| PostCSS | `postcss` | Autoprefixer, minification |

## 🔗 Références

- [Sass — Documentation](https://sass-lang.com/documentation/)
- [Tailwind CSS — Documentation](https://tailwindcss.com/docs)
- [Bootstrap — Documentation](https://getbootstrap.com/docs/5.3/)
- [PostCSS — Documentation](https://postcss.org/)

---
*⬅️ [Module 17](../17-accessibilite/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 19 — Projets pratiques](../19-projets/README.md)*
