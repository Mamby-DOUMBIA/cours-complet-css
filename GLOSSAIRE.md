# 📖 Glossaire des termes CSS

> Ce glossaire regroupe les définitions de tous les termes techniques utilisés dans ce cours. Consultez-le chaque fois qu'un terme vous semble obscur.

---

## A

**Attribut**
Information supplémentaire placée dans une balise HTML. Exemple : `class="mon-titre"` est un attribut dans `<h1 class="mon-titre">`.

**Axe principal (main axis)**
Dans Flexbox, l'axe le long duquel les éléments flex sont disposés. Déterminé par `flex-direction`.

**Axe transversal (cross axis)**
Dans Flexbox, l'axe perpendiculaire à l'axe principal.

---

## B

**BEM (Block Element Modifier)**
Méthodologie de nommage des classes CSS. Exemple : `.bouton`, `.bouton__icone`, `.bouton--actif`.

**Box Model (Modèle de boîte)**
Modèle qui définit comment chaque élément HTML est représenté comme une boîte rectangulaire composée de : contenu, padding, bordure et marge.

**Breakpoint (Point de rupture)**
Valeur de largeur d'écran à partir de laquelle la mise en page change. Utilisé dans les media queries.

---

## C

**Cascade**
Mécanisme par lequel le navigateur détermine quelles règles CSS s'appliquent lorsque plusieurs règles ciblent le même élément. La cascade prend en compte l'origine, la spécificité et l'ordre des règles.

**Conteneur flex**
Élément HTML sur lequel on applique `display: flex`. Ses enfants directs deviennent des éléments flex.

**Custom Property (Propriété personnalisée)**
Variable CSS déclarée avec deux tirets. Exemple : `--couleur-principale: #3498db;`.

---

## D

**Déclaration CSS**
Paire propriété/valeur. Exemple : `color: red;`.

**DevTools (Outils développeur)**
Outils intégrés au navigateur permettant d'inspecter et de déboguer le HTML, le CSS et le JavaScript d'une page Web.

---

## E

**Élément block**
Élément HTML qui occupe toute la largeur disponible et commence sur une nouvelle ligne. Exemples : `<div>`, `<p>`, `<h1>`.

**Élément inline**
Élément HTML qui n'occupe que l'espace nécessaire à son contenu et ne crée pas de nouvelle ligne. Exemples : `<span>`, `<a>`, `<strong>`.

**Em**
Unité CSS relative à la taille de police de l'élément parent. Si le parent a une taille de 16px, alors 1em = 16px.

---

## F

**Flexbox (Flexible Box Layout)**
Module CSS de mise en page unidimensionnel permettant de disposer des éléments en ligne ou en colonne avec un contrôle fin de l'espacement et de l'alignement.

**Float**
Propriété CSS ancienne permettant de faire "flotter" un élément à gauche ou à droite. Aujourd'hui remplacée par Flexbox et Grid pour la mise en page.

**fr (Fraction unit)**
Unité CSS utilisée exclusivement avec CSS Grid. Représente une fraction de l'espace disponible dans la grille.

---

## G

**Grid (CSS Grid Layout)**
Module CSS de mise en page bidimensionnel permettant de créer des grilles de colonnes et de lignes.

**Grid area**
Zone rectangulaire de la grille définie par des lignes de grille de début et de fin (colonnes et lignes).

---

## H

**Héritage**
Mécanisme par lequel certaines propriétés CSS d'un élément parent sont transmises à ses éléments enfants. Exemple : `color` et `font-family` sont héritées.

**HSL**
Format de couleur CSS basé sur la teinte (Hue), la saturation (Saturation) et la luminosité (Lightness). Exemple : `hsl(210, 100%, 50%)`.

---

## I

**ID**
Identifiant unique attribué à un seul élément HTML. En CSS, ciblé avec le sélecteur `#identifiant`.

---

## K

**Keyframe**
Image clé dans une animation CSS. Définie avec `@keyframes`, elle spécifie l'état de l'élément à un moment précis de l'animation.

---

## M

**Media Query**
Règle CSS conditionnelle permettant d'appliquer des styles différents selon les caractéristiques du périphérique (largeur d'écran, orientation, etc.).

**Minification**
Processus de suppression des espaces, commentaires et caractères inutiles dans un fichier CSS pour réduire sa taille.

**Mobile-first**
Approche de conception qui consiste à créer d'abord le design pour mobile, puis à l'adapter aux écrans plus grands avec des media queries.

---

## P

**Padding (Rembourrage)**
Espace entre le contenu d'un élément et sa bordure. Fait partie du Box Model.

**Pixel (px)**
Unité CSS absolue représentant un point sur l'écran.

**Pseudo-classe**
Sélecteur CSS ciblant un état particulier d'un élément. Exemple : `:hover` (survol), `:focus` (focus clavier).

**Pseudo-élément**
Sélecteur CSS permettant de cibler une partie spécifique d'un élément. Exemple : `::before` (avant le contenu), `::after` (après le contenu).

---

## R

**Rem**
Unité CSS relative à la taille de police de l'élément racine (`<html>`). Si la racine a une taille de 16px, alors 1rem = 16px.

**Règle CSS**
Ensemble composé d'un sélecteur et d'un bloc de déclarations.

**Responsive Design**
Approche de conception Web qui crée des interfaces s'adaptant à différentes tailles d'écran.

---

## S

**Sass / SCSS**
Préprocesseur CSS ajoutant des fonctionnalités comme les variables, l'imbrication et les mixins. SCSS est la syntaxe moderne de Sass.

**Sélecteur**
Partie d'une règle CSS qui désigne le ou les éléments HTML à styliser.

**Spécificité**
Mesure de la priorité d'un sélecteur CSS. Un sélecteur plus spécifique écrase un sélecteur moins spécifique. Calculée selon une hiérarchie : styles inline > ID > classes > éléments.

---

## T

**Transition**
Animation CSS simple permettant de modifier progressivement une propriété d'un état à un autre.

---

## U

**Unité relative**
Unité CSS dont la valeur dépend d'un autre élément ou du contexte. Exemples : `em`, `rem`, `%`, `vw`, `vh`.

**Unité absolue**
Unité CSS dont la valeur est fixe et indépendante du contexte. Exemples : `px`, `cm`, `mm`.

---

## V

**Viewport**
Zone visible de la page Web dans la fenêtre du navigateur.

**vw / vh**
Unités CSS relatives au viewport. `1vw` = 1% de la largeur du viewport, `1vh` = 1% de la hauteur du viewport.

---

## Z

**z-index**
Propriété CSS définissant l'ordre d'empilement des éléments positionnés (sur l'axe Z, c'est-à-dire la profondeur).
