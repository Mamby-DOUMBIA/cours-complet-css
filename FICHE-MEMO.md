# 📌 Fiche Mémo CSS — Référence Rapide

> Consultez cette fiche pour retrouver rapidement la syntaxe des propriétés CSS les plus utilisées.

---

## 🎨 Couleurs

```css
color: red;                        /* Couleur du texte */
color: #3498db;                    /* Hexadécimal */
color: rgb(52, 152, 219);          /* RGB */
color: rgba(52, 152, 219, 0.8);    /* RGB + transparence */
color: hsl(210, 70%, 53%);         /* HSL */
background-color: #f0f0f0;         /* Couleur de fond */
opacity: 0.5;                      /* Opacité (0 = transparent, 1 = opaque) */
```

---

## 📦 Box Model

```css
/* Contenu */
width: 300px;
height: 200px;
max-width: 100%;
min-height: 50px;

/* Padding (rembourrage interne) */
padding: 20px;                     /* Tous les côtés */
padding: 10px 20px;                /* Haut/bas, Gauche/droite */
padding: 10px 20px 15px 25px;      /* Haut, Droite, Bas, Gauche (sens horaire) */
padding-top: 10px;
padding-right: 20px;
padding-bottom: 15px;
padding-left: 25px;

/* Bordure */
border: 1px solid #000;
border-width: 2px;
border-style: solid | dashed | dotted | none;
border-color: #333;
border-radius: 8px;                /* Coins arrondis */
border-radius: 50%;                /* Cercle parfait */

/* Margin (marge externe) */
margin: 20px;
margin: 0 auto;                    /* Centrage horizontal */
margin-top: 10px;

/* Modèle de boîte */
box-sizing: border-box;            /* Recommandé : padding/border inclus dans width/height */
box-sizing: content-box;           /* Défaut : padding/border s'ajoutent à width/height */
```

---

## 🔤 Typographie

```css
font-family: 'Arial', sans-serif;
font-family: 'Georgia', serif;
font-size: 16px;                   /* Pixels */
font-size: 1rem;                   /* Relatif à la racine */
font-size: 1.2em;                  /* Relatif au parent */
font-weight: normal | bold | 400 | 700;
font-style: normal | italic;
font-variant: normal | small-caps;

line-height: 1.5;                  /* Interligne (sans unité = recommandé) */
letter-spacing: 0.05em;            /* Espacement entre les lettres */
word-spacing: 0.1em;               /* Espacement entre les mots */

text-align: left | center | right | justify;
text-decoration: none | underline | line-through | overline;
text-transform: none | uppercase | lowercase | capitalize;
text-indent: 2em;                  /* Retrait de première ligne */
text-overflow: ellipsis;           /* Troncature avec "..." */

white-space: normal | nowrap | pre | pre-wrap;
word-break: break-word;
overflow-wrap: break-word;
```

---

## 🖼️ Arrière-plans

```css
background-color: #f5f5f5;
background-image: url('image.jpg');
background-repeat: no-repeat | repeat | repeat-x | repeat-y;
background-position: center center | top left | 50% 50%;
background-size: cover | contain | 100% auto;
background-attachment: scroll | fixed | local;

/* Raccourci */
background: #f5f5f5 url('image.jpg') no-repeat center center / cover;

/* Gradients */
background: linear-gradient(to right, #3498db, #9b59b6);
background: linear-gradient(45deg, #e74c3c, #f39c12);
background: radial-gradient(circle, #3498db, #1a252f);
background: conic-gradient(from 0deg, red, blue, green, red);
```

---

## 📐 Mise en page

```css
/* Display */
display: block;
display: inline;
display: inline-block;
display: flex;
display: grid;
display: none;                     /* Cache l'élément */

/* Position */
position: static;                  /* Défaut */
position: relative;                /* Relatif à sa position normale */
position: absolute;                /* Relatif au parent positionné */
position: fixed;                   /* Relatif au viewport */
position: sticky;                  /* Mélange relative/fixed */

top: 0; right: 0; bottom: 0; left: 0;
z-index: 10;                       /* Ordre d'empilement */

/* Overflow */
overflow: visible | hidden | scroll | auto;
overflow-x: hidden;
overflow-y: auto;
```

---

## 💪 Flexbox

```css
/* Sur le conteneur */
display: flex;
flex-direction: row | row-reverse | column | column-reverse;
flex-wrap: nowrap | wrap | wrap-reverse;
justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
align-items: stretch | flex-start | flex-end | center | baseline;
align-content: flex-start | flex-end | center | space-between | space-around | stretch;
gap: 16px;
column-gap: 20px;
row-gap: 10px;

/* Sur les éléments */
flex-grow: 1;                      /* Capacité à grandir */
flex-shrink: 0;                    /* Capacité à rétrécir */
flex-basis: 200px;                 /* Taille de base */
flex: 1;                           /* Raccourci (grow shrink basis) */
flex: 1 1 auto;
align-self: auto | flex-start | flex-end | center | stretch;
order: 0;                          /* Ordre d'affichage */
```

---

## 🔲 CSS Grid

```css
/* Sur le conteneur */
display: grid;
grid-template-columns: 200px 200px 200px;
grid-template-columns: repeat(3, 1fr);
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
grid-template-rows: 100px auto;
grid-template-areas:
  "header header"
  "sidebar main"
  "footer footer";
gap: 16px;
column-gap: 20px;
row-gap: 10px;

/* Sur les éléments */
grid-column: 1 / 3;                /* De la ligne 1 à la ligne 3 */
grid-column: span 2;               /* S'étend sur 2 colonnes */
grid-row: 1 / 2;
grid-area: header;                 /* Utilise une zone nommée */
```

---

## 📱 Responsive Design

```css
/* Viewport meta tag (dans le HTML) */
/* <meta name="viewport" content="width=device-width, initial-scale=1.0"> */

/* Media queries */
@media (max-width: 768px) { }       /* Mobile */
@media (min-width: 769px) { }       /* Tablette et plus */
@media (min-width: 1024px) { }      /* Desktop */
@media (orientation: landscape) { } /* Paysage */
@media (prefers-color-scheme: dark) { } /* Thème sombre */
@media (prefers-reduced-motion: reduce) { } /* Animation réduite */

/* Unités relatives */
width: 100%;
width: 50vw;
height: 100vh;
font-size: clamp(1rem, 2.5vw, 2rem); /* Min, préféré, max */
```

---

## 🎬 Animations et transitions

```css
/* Transitions */
transition: all 0.3s ease;
transition: color 0.2s ease-in-out, background 0.3s linear;
transition-property: color;
transition-duration: 0.3s;
transition-timing-function: ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier();
transition-delay: 0.1s;

/* Transformations */
transform: translateX(10px);
transform: translateY(-20px);
transform: translate(10px, -20px);
transform: rotate(45deg);
transform: scale(1.2);
transform: scale(1.2, 0.8);
transform: skew(15deg);
transform: matrix(1, 0, 0, 1, 10, 20);
transform-origin: center center | top left | 50% 50%;

/* Animations */
@keyframes nom-animation {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes nom-animation {
  0%   { opacity: 0; }
  50%  { opacity: 0.5; }
  100% { opacity: 1; }
}

animation: nom-animation 0.5s ease-in-out;
animation-name: nom-animation;
animation-duration: 0.5s;
animation-timing-function: ease;
animation-delay: 0s;
animation-iteration-count: 1 | infinite;
animation-direction: normal | reverse | alternate | alternate-reverse;
animation-fill-mode: none | forwards | backwards | both;
animation-play-state: running | paused;
```

---

## 🔑 Variables CSS

```css
/* Déclaration (généralement dans :root) */
:root {
  --couleur-principale: #3498db;
  --couleur-secondaire: #2ecc71;
  --taille-police-base: 16px;
  --espacement-base: 8px;
  --rayon-bordure: 4px;
}

/* Utilisation */
.bouton {
  background-color: var(--couleur-principale);
  font-size: var(--taille-police-base);
  padding: calc(var(--espacement-base) * 2);
  /* Valeur de secours si la variable n'existe pas */
  color: var(--couleur-texte, #333);
}
```

---

## 🔮 Fonctions CSS avancées

```css
calc(100% - 40px)                  /* Calcul */
min(300px, 100%)                   /* Valeur minimale */
max(100px, 20%)                    /* Valeur maximale */
clamp(1rem, 2.5vw, 2rem)           /* Min, préféré, max */
var(--ma-variable, valeur-defaut)  /* Variable avec fallback */

/* Filtres */
filter: blur(4px);
filter: brightness(1.2);
filter: contrast(0.8);
filter: grayscale(100%);
filter: sepia(50%);
filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.3));
filter: blur(4px) brightness(0.8);

/* Ombres */
box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.2);
box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
```

---

## 🎯 Sélecteurs — Référence rapide

| Sélecteur | Exemple | Description |
|-----------|---------|-------------|
| Universel | `*` | Tous les éléments |
| Type | `p`, `h1`, `div` | Éléments d'un type |
| Classe | `.ma-classe` | Éléments avec cette classe |
| ID | `#mon-id` | Élément avec cet identifiant |
| Descendant | `div p` | `<p>` à l'intérieur d'un `<div>` |
| Enfant direct | `div > p` | `<p>` enfant direct d'un `<div>` |
| Frère adjacent | `h1 + p` | `<p>` immédiatement après `<h1>` |
| Frère général | `h1 ~ p` | Tous les `<p>` après `<h1>` |
| Attribut | `[type="text"]` | Éléments avec cet attribut |
| :hover | `a:hover` | Au survol |
| :focus | `input:focus` | Au focus |
| :active | `button:active` | Au clic |
| :nth-child | `li:nth-child(2n)` | Éléments pairs |
| :first-child | `p:first-child` | Premier enfant |
| :last-child | `p:last-child` | Dernier enfant |
| :not | `p:not(.special)` | Pas cette classe |
| ::before | `p::before` | Avant le contenu |
| ::after | `p::after` | Après le contenu |
| ::placeholder | `input::placeholder` | Texte indicatif |

---

## 📊 Spécificité — Tableau de calcul

| Type de sélecteur | Valeur de spécificité |
|-------------------|----------------------|
| Style inline (`style=""`) | 1-0-0-0 |
| Sélecteur d'ID (`#id`) | 0-1-0-0 |
| Classe, pseudo-classe, attribut | 0-0-1-0 |
| Élément, pseudo-élément | 0-0-0-1 |
| `!important` | Écrase tout (à éviter) |

---

*Mémo CSS — Formation CSS Complète*
