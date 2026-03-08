# Module 04 — Sélecteurs CSS

> **Niveau :** Débutant → Intermédiaire  
> **Durée estimée :** 4 heures  
> **Prérequis :** Modules 01, 02, 03

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Utiliser tous les types de sélecteurs CSS
- Combiner les sélecteurs pour cibler des éléments précis
- Comprendre et calculer la spécificité
- Utiliser les pseudo-classes et pseudo-éléments

---

## 4.1 Sélecteur universel (`*`)

### Explication

Le sélecteur `*` (étoile) cible **absolument tous les éléments** de la page. Il est rarement utilisé seul pour des styles visuels, mais très souvent pour des règles de base comme `box-sizing`.

```css
/* Cible TOUS les éléments sans exception */
* {
  box-sizing: border-box; /* Bonne pratique universelle */
  margin: 0;
  padding: 0;
}

/* Exemple moins courant */
* {
  outline: 1px solid red; /* Utile pour déboguer la mise en page */
}
```

**Avertissement de performance :** Utiliser `*` avec de nombreuses propriétés peut ralentir le navigateur car il doit appliquer ces styles à chaque élément. Limitez son usage à `box-sizing` et la réinitialisation.

---

## 4.2 Sélecteur de type (balise HTML)

### Explication

Il cible tous les éléments d'un type de balise spécifique.

```css
/* Tous les paragraphes */
p {
  color: #555;
  line-height: 1.7;
  margin-bottom: 16px;
}

/* Tous les titres h1 */
h1 {
  font-size: 32px;
  font-weight: bold;
  color: #1a1a2e;
}

/* Tous les liens */
a {
  color: #3498db;
  text-decoration: underline;
}

/* Toutes les images */
img {
  max-width: 100%;
  height: auto;
  display: block;
}

/* Tous les boutons */
button {
  cursor: pointer;
  font-family: inherit;
}
```

### Sélecteurs de type groupés

```css
/* Styles appliqués à tous les niveaux de titres */
h1, h2, h3, h4, h5, h6 {
  font-family: 'Georgia', serif;
  line-height: 1.3;
  margin-bottom: 0.75em;
  color: #2c3e50;
}

/* Éléments de formulaire */
input, textarea, select, button {
  font-family: inherit;
  font-size: 1rem;
}
```

---

## 4.3 Sélecteur de classe (`.classe`)

### Explication

Le sélecteur de classe cible tous les éléments ayant un attribut `class` contenant le nom spécifié. C'est le sélecteur **le plus utilisé** en CSS.

### Règles importantes

- Un élément peut avoir **plusieurs classes** (séparées par des espaces)
- Plusieurs éléments peuvent partager la **même classe**
- Les classes commencent par un **point** (`.`) en CSS

### Exemple de base

```html
<!-- HTML -->
<p class="introduction">Premier paragraphe d'introduction.</p>
<p>Paragraphe normal.</p>
<p class="introduction important">Introduction importante.</p>
```

```css
/* CSS */

/* Cible les éléments ayant la classe "introduction" */
.introduction {
  font-size: 1.1rem;
  font-weight: 500;
  color: #2c3e50;
}

/* Cible les éléments ayant la classe "important" */
.important {
  border-left: 4px solid #e74c3c;
  padding-left: 12px;
  background-color: #fff5f5;
}
```

### Classes multiples — Combinaisons puissantes

```html
<!-- Éléments avec des combinaisons de classes -->
<div class="carte">Carte simple</div>
<div class="carte actif">Carte active</div>
<div class="carte premium actif">Carte premium active</div>
<div class="carte desactive">Carte désactivée</div>
```

```css
/* Style de base pour toutes les cartes */
.carte {
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  margin-bottom: 12px;
  background-color: white;
}

/* Variation : carte active */
.actif {
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
}

/* Variation : carte premium */
.premium {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border-color: transparent;
}

/* Variation : carte désactivée */
.desactive {
  opacity: 0.5;
  cursor: not-allowed;
  filter: grayscale(100%);
}
```

### Cibler un type avec une classe spécifique

```css
/* TOUS les éléments avec la classe "rouge" */
.rouge { color: red; }

/* Uniquement les <p> avec la classe "rouge" */
p.rouge { color: red; }

/* Uniquement les <a> avec la classe "rouge" */
a.rouge { color: red; }
```

---

## 4.4 Sélecteur d'ID (`#id`)

### Explication

L'ID est un **identifiant unique** : un seul élément de la page peut avoir un ID donné.

```html
<header id="en-tete-principal">...</header>
<main id="contenu-principal">...</main>
<footer id="pied-de-page">...</footer>
```

```css
#en-tete-principal {
  background-color: #2c3e50;
  color: white;
  padding: 20px 40px;
}

#contenu-principal {
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 20px;
}

#pied-de-page {
  background-color: #1a252f;
  color: #aaa;
  padding: 30px;
}
```

### ID vs Classes — Quand utiliser quoi ?

| Critère | ID (`#`) | Classe (`.`) |
|---------|---------|--------------|
| **Unicité** | Unique sur la page | Réutilisable |
| **Spécificité** | Haute (100) | Moyenne (10) |
| **Usage recommandé** | Ancres de navigation, JavaScript | Styles réutilisables |
| **Best practice CSS** | Éviter pour les styles | Préférer |

**Conseil professionnel :** En CSS, privilégiez toujours les classes. Les IDs sont à réserver pour JavaScript ou les ancres de navigation (`<a href="#section-id">`). Les IDs ont une spécificité très élevée qui complique la maintenance.

---

## 4.5 Sélecteurs combinés

### Sélecteur descendant (espace)

Cible un élément qui se trouve **à l'intérieur** d'un autre, à n'importe quel niveau de profondeur.

```css
/* Tous les <a> qui se trouvent n'importe où dans un <nav> */
nav a {
  text-decoration: none;
  color: white;
}

/* Tous les <p> qui se trouvent dans un <article> */
article p {
  color: #555;
  line-height: 1.8;
}

/* Tous les <li> qui se trouvent dans un <ul> qui est dans un <nav> */
nav ul li {
  display: inline-block;
  margin-right: 10px;
}
```

```html
<nav>
  <ul>
    <li><a href="#">Accueil</a></li>  <!-- ← Ciblé par nav a -->
    <li><a href="#">À propos</a></li>  <!-- ← Ciblé par nav a -->
  </ul>
  <a href="#">Logo</a>  <!-- ← Aussi ciblé par nav a -->
</nav>
```

### Sélecteur enfant direct (`>`)

Cible uniquement les éléments **enfants directs** (premier niveau).

```css
/* Uniquement les <li> enfants directs d'un <ul> */
ul > li {
  list-style: square;
}

/* Uniquement les <p> enfants directs d'un <article> */
article > p {
  font-size: 1.1rem;
}
```

```html
<ul>
  <li>Élément direct ← ciblé par ul > li</li>
  <li>Élément direct ← ciblé par ul > li
    <ul>
      <li>Élément imbriqué ← NON ciblé par ul > li</li>
    </ul>
  </li>
</ul>
```

### Sélecteur de frère adjacent (`+`)

Cible l'élément **immédiatement suivant** un autre élément au même niveau.

```css
/* Le <p> qui vient IMMÉDIATEMENT après un <h2> */
h2 + p {
  font-size: 1.1rem;
  color: #666;
  font-style: italic;
}

/* La <div> qui vient immédiatement après un <input> */
input + div.erreur {
  color: red;
  font-size: 0.85rem;
}
```

```html
<h2>Mon titre</h2>
<p>Ce paragraphe est ciblé (juste après h2).</p>
<p>Ce paragraphe n'est PAS ciblé.</p>
```

### Sélecteur de frères généraux (`~`)

Cible **tous les éléments** qui suivent un élément (pas seulement le suivant immédiat).

```css
/* Tous les <p> qui viennent APRÈS un <h2>, au même niveau */
h2 ~ p {
  color: #555;
}
```

```html
<h2>Mon titre</h2>
<p>Ciblé par h2 ~ p.</p>
<p>Aussi ciblé par h2 ~ p.</p>
<p>Aussi ciblé par h2 ~ p.</p>
```

---

## 4.6 Sélecteurs d'attributs

Très puissants, ils permettent de cibler des éléments selon leurs attributs HTML.

```css
/* Éléments ayant un attribut "href" */
a[href] {
  color: blue;
}

/* Éléments avec un attribut "type" égal à "text" */
input[type="text"] {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Éléments avec un attribut "href" qui COMMENCE par "https" */
a[href^="https"] {
  color: green; /* Liens sécurisés en vert */
}

/* Éléments avec un attribut "href" qui FINIT par ".pdf" */
a[href$=".pdf"] {
  /* Afficher une icône PDF */
  padding-right: 20px;
  background-image: url('icone-pdf.png');
  background-repeat: no-repeat;
  background-position: right center;
}

/* Éléments avec un attribut "class" qui CONTIENT "btn" */
[class*="btn"] {
  cursor: pointer;
  border-radius: 4px;
}

/* Éléments avec un attribut "lang" qui vaut exactement "fr" ou commence par "fr-" */
[lang|="fr"] {
  font-family: 'Marianne', Arial, sans-serif;
}
```

---

## 4.7 Pseudo-classes

Une pseudo-classe est un mot-clé ajouté à un sélecteur pour cibler un **état particulier** de l'élément.

### Pseudo-classes d'interaction

```css
/* Au survol de la souris */
a:hover {
  color: #e74c3c;
  text-decoration: none;
}

button:hover {
  background-color: #2980b9;
  transform: translateY(-1px);
}

/* Au clic */
button:active {
  transform: translateY(0);
  background-color: #1a6694;
}

/* Au focus (navigation clavier ou clic) */
input:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
}

/* Lien déjà visité */
a:visited {
  color: #9b59b6;
}

/* Lien non encore visité */
a:link {
  color: #3498db;
}
```

### Pseudo-classes de structure

```css
/* Premier enfant */
li:first-child {
  border-top: none;
}

/* Dernier enfant */
li:last-child {
  border-bottom: none;
}

/* N-ième enfant */
li:nth-child(2) { /* Le 2e enfant */
  background-color: #f0f0f0;
}

li:nth-child(2n) { /* Les enfants pairs (2, 4, 6…) */
  background-color: #f5f5f5;
}

li:nth-child(2n+1) { /* Les enfants impairs (1, 3, 5…) */
  background-color: white;
}

li:nth-child(3n+1) { /* Tous les 3, en commençant par 1 */
  color: #3498db;
}

/* Équivalents pratiques */
tr:nth-child(even) { background-color: #f9f9f9; } /* Pairs */
tr:nth-child(odd)  { background-color: white; }     /* Impairs */

/* Dernier de son type */
p:last-of-type {
  margin-bottom: 0;
}

/* Unique enfant */
p:only-child {
  text-align: center;
}

/* Négation */
li:not(:last-child) {
  border-bottom: 1px solid #eee;
}

input:not([type="submit"]):not([type="reset"]) {
  border: 1px solid #ccc;
}
```

### Pseudo-classes de formulaire

```css
/* Input désactivé */
input:disabled {
  background-color: #f0f0f0;
  cursor: not-allowed;
  opacity: 0.6;
}

/* Input activé */
input:enabled {
  background-color: white;
}

/* Checkbox cochée */
input[type="checkbox"]:checked + label {
  font-weight: bold;
  color: #27ae60;
}

/* Input invalide (validation HTML5) */
input:invalid {
  border-color: #e74c3c;
}

/* Input valide */
input:valid {
  border-color: #27ae60;
}

/* Input requis */
input:required {
  border-left: 3px solid #e74c3c;
}

/* Placeholder */
input::placeholder {
  color: #aaa;
  font-style: italic;
}
```

---

## 4.8 Pseudo-éléments

Les pseudo-éléments permettent de cibler une **partie spécifique** d'un élément ou d'en créer de nouveaux visuellement. On les distingue des pseudo-classes par leur double deux-points `::`.

### `::before` et `::after`

Ces deux pseudo-éléments créent un élément enfant **virtuel** respectivement avant et après le contenu de l'élément. Ils nécessitent la propriété `content`.

```css
/* Ajouter une icône avant chaque lien externe */
a[href^="http"]::before {
  content: "🔗 ";
}

/* Ajouter une numérotation automatique */
.etapes li::before {
  counter-increment: etape;
  content: counter(etape) ". ";
  font-weight: bold;
  color: #3498db;
}

/* Ligne décorative après un titre */
h2::after {
  content: "";           /* Obligatoire mais vide */
  display: block;        /* Le rend visible */
  width: 50px;
  height: 3px;
  background-color: #3498db;
  margin-top: 8px;
}

/* Citation stylisée */
blockquote::before {
  content: "\201C";      /* Guillemet ouvrant " */
  font-size: 4em;
  color: #3498db;
  line-height: 0;
  vertical-align: -0.4em;
  margin-right: 0.1em;
}

/* Tooltip avec ::after */
.infobull {
  position: relative;
  cursor: help;
}

.infobull::after {
  content: attr(data-info); /* Lit l'attribut data-info */
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background-color: #333;
  color: white;
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 0.85rem;
  white-space: nowrap;
  opacity: 0;
  transition: opacity 0.3s;
  pointer-events: none;
}

.infobull:hover::after {
  opacity: 1;
}
```

```html
<!-- Utilisation du tooltip -->
<span class="infobull" data-info="Information contextuelle">
  Survolez-moi !
</span>
```

### `::first-line` et `::first-letter`

```css
/* Style de la première ligne d'un paragraphe */
p::first-line {
  font-weight: bold;
  font-size: 1.05rem;
}

/* Lettrine (grande première lettre) */
article > p:first-of-type::first-letter {
  float: left;
  font-size: 4rem;
  line-height: 0.8;
  margin-right: 10px;
  color: #3498db;
  font-family: Georgia, serif;
}
```

### `::selection`

```css
/* Style du texte sélectionné par l'utilisateur */
::selection {
  background-color: #3498db;
  color: white;
}
```

---

## 4.9 Tableau récapitulatif des sélecteurs

| Sélecteur | Exemple | Cible |
|-----------|---------|-------|
| `*` | `*` | Tous les éléments |
| Type | `p` | Tous les `<p>` |
| Classe | `.ma-classe` | Éléments avec `class="ma-classe"` |
| ID | `#mon-id` | Élément avec `id="mon-id"` |
| Descendant | `div p` | Tous les `<p>` dans un `<div>` |
| Enfant direct | `div > p` | `<p>` enfant direct d'un `<div>` |
| Frère adjacent | `h2 + p` | `<p>` immédiatement après un `<h2>` |
| Frères généraux | `h2 ~ p` | Tous les `<p>` après un `<h2>` |
| Attribut | `[type="text"]` | Éléments avec cet attribut |
| `:hover` | `a:hover` | Lors du survol |
| `:focus` | `input:focus` | Lors du focus |
| `:nth-child(n)` | `li:nth-child(2)` | 2e enfant |
| `:not()` | `p:not(.special)` | `<p>` sans la classe "special" |
| `::before` | `p::before` | Avant le contenu de `<p>` |
| `::after` | `p::after` | Après le contenu de `<p>` |
| `::first-letter` | `p::first-letter` | Première lettre de `<p>` |
| `::placeholder` | `input::placeholder` | Texte de l'espace réservé |

---

## 📝 Exercices pratiques

### Exercice 4.1 — Navigation stylisée

Créez une barre de navigation avec les styles suivants :
- Liens en blanc sur fond sombre
- Changement de couleur au survol
- Lien actif souligné
- Utilisez les sélecteurs appropriés

### Exercice 4.2 — Tableau avec lignes alternées

```html
<table>
  <tr><td>Ligne 1</td><td>Données</td></tr>
  <tr><td>Ligne 2</td><td>Données</td></tr>
  <tr><td>Ligne 3</td><td>Données</td></tr>
  <tr><td>Ligne 4</td><td>Données</td></tr>
</table>
```
Alternez les couleurs de fond des lignes avec `:nth-child`.

### Exercice 4.3 — Formulaire stylisé

Stylisez un formulaire avec :
- Bordures normales, bleues au focus
- Bordures rouges si invalide
- Champs désactivés en gris

---

## ✅ Corrigé Exercice 4.1

```css
nav {
  background-color: #2c3e50;
  padding: 0 20px;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

nav ul li a {
  display: block;
  padding: 16px 20px;
  color: white;
  text-decoration: none;
  transition: background-color 0.2s ease;
}

nav ul li a:hover {
  background-color: #3498db;
  color: white;
}

nav ul li a.actif {
  border-bottom: 3px solid #3498db;
  font-weight: bold;
}
```

---

## 📌 Résumé du module 04

- Les sélecteurs de **type** ciblent des balises HTML (ex. `p`, `h1`)
- Les sélecteurs de **classe** `.classe` sont réutilisables et les plus courants
- Les sélecteurs d'**ID** `#id` sont uniques — à éviter pour les styles CSS
- Les **combinateurs** permettent des ciblages précis (descendant, enfant direct…)
- Les **pseudo-classes** ciblent des états (`:hover`, `:focus`, `:nth-child`)
- Les **pseudo-éléments** ciblent des parties ou créent du contenu (`::before`, `::after`)

---

## 🔗 Références

- [MDN — Sélecteurs CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Selectors)
- [MDN — Pseudo-classes](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-classes)
- [MDN — Pseudo-éléments](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-elements)
- [CSS-Tricks — Almanac des sélecteurs](https://css-tricks.com/almanac/selectors/)

---

*⬅️ [Module 03](../03-syntaxe/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 05 — Box Model](../05-box-model/README.md)*
