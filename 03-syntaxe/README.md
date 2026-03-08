# Module 03 — Syntaxe et Structure CSS

> **Niveau :** Débutant  
> **Durée estimée :** 3 heures  
> **Prérequis :** Module 01 et 02

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Écrire des règles CSS correctement formatées
- Comprendre la cascade CSS et la spécificité
- Utiliser l'héritage CSS à votre avantage
- Éviter les erreurs de syntaxe courantes

---

## 3.1 La règle CSS — Anatomie complète

### Explication simple

Une règle CSS, c'est comme une instruction que vous donnez au navigateur : "Tous les éléments de ce type doivent avoir cet aspect". Chaque instruction est composée d'une cible (le sélecteur) et d'une liste de propriétés à appliquer.

### Anatomie d'une règle CSS

```
sélecteur {
  propriété: valeur;
  propriété: valeur;
  propriété: valeur;
}
```

Voici un exemple concret annoté :

```css
/*
 ┌── SÉLECTEUR : cible tous les éléments <h1>
 │
 h1 {
 │   ┌── PROPRIÉTÉ : quelle caractéristique modifier
 │   │       ┌── VALEUR : quelle valeur appliquer
 │   │       │
     color:  blue;
 │              └── POINT-VIRGULE : termine chaque déclaration (obligatoire)
 │
     font-size: 32px;
 │
 }  └── ACCOLADE FERMANTE : fin du bloc de déclarations
*/

h1 {
  color: blue;
  font-size: 32px;
}
```

### Les termes à connaître

| Terme | Définition | Exemple |
|-------|-----------|---------|
| **Règle CSS** | L'ensemble sélecteur + bloc de déclarations | `h1 { color: blue; }` |
| **Sélecteur** | Ce qui désigne les éléments HTML ciblés | `h1`, `.ma-classe`, `#mon-id` |
| **Bloc de déclarations** | Les accolades `{ }` et leur contenu | `{ color: blue; }` |
| **Déclaration** | Une paire propriété + valeur | `color: blue;` |
| **Propriété** | La caractéristique à modifier | `color`, `font-size`, `margin` |
| **Valeur** | La valeur de la propriété | `blue`, `32px`, `auto` |

---

## 3.2 Les sélecteurs CSS

Les sélecteurs sont le cœur du CSS. Ils permettent de cibler précisément les éléments HTML à styliser. Nous les étudierons en détail dans le Module 04, mais voici les bases :

### Sélecteur de type (balise)

```css
/* Cible TOUS les éléments <p> */
p {
  color: #555;
  line-height: 1.6;
}

/* Cible TOUS les éléments <h1> */
h1 {
  font-size: 32px;
  color: #2c3e50;
}

/* Cible TOUTES les images */
img {
  max-width: 100%;
  height: auto;
}
```

### Sélecteur de classe

```css
/* Cible tous les éléments ayant la classe "alerte" */
.alerte {
  background-color: #fff3cd;
  border: 1px solid #ffc107;
  padding: 12px;
  border-radius: 4px;
}

/* Dans le HTML : <div class="alerte">...</div> */
```

### Sélecteur d'ID

```css
/* Cible l'élément unique ayant l'ID "header-principal" */
#header-principal {
  background-color: #2c3e50;
  color: white;
  padding: 20px;
}

/* Dans le HTML : <header id="header-principal">...</header> */
```

### Groupement de sélecteurs

Vous pouvez appliquer les mêmes styles à plusieurs sélecteurs en les séparant par des virgules :

```css
/* Avant : code répétitif */
h1 { color: #2c3e50; }
h2 { color: #2c3e50; }
h3 { color: #2c3e50; }

/* Après : code groupé */
h1, h2, h3 {
  color: #2c3e50;
}
```

---

## 3.3 Les propriétés et valeurs CSS

### Les types de valeurs CSS

Les valeurs CSS peuvent prendre différentes formes selon la propriété :

**1. Mots-clés**
```css
display: block;
visibility: hidden;
text-align: center;
font-weight: bold;
position: relative;
```

**2. Valeurs numériques avec unités**
```css
font-size: 16px;       /* Pixels */
width: 50%;            /* Pourcentage */
margin: 1rem;          /* Rem */
padding: 1.5em;        /* Em */
height: 100vh;         /* Viewport height */
```

**3. Couleurs**
```css
color: red;                     /* Nom de couleur */
color: #3498db;                 /* Hexadécimal */
color: rgb(52, 152, 219);       /* RGB */
color: rgba(52, 152, 219, 0.8); /* RGBA */
color: hsl(210, 70%, 53%);      /* HSL */
```

**4. Fonctions**
```css
width: calc(100% - 40px);
font-size: clamp(1rem, 2vw, 1.5rem);
background: linear-gradient(to right, #3498db, #9b59b6);
transform: rotate(45deg);
```

**5. Chaînes de caractères**
```css
font-family: 'Arial', sans-serif;
content: 'Bonjour';
```

**6. URLs**
```css
background-image: url('images/fond.jpg');
```

---

## 3.4 Les commentaires CSS

### Syntaxe

```css
/* Ceci est un commentaire CSS sur une ligne */

/*
  Ceci est un commentaire
  sur plusieurs lignes.
  Très utile pour décrire des sections.
*/
```

### Bonne pratique : commenter son CSS

```css
/* ========================================
   SECTION : EN-TÊTE (HEADER)
   ======================================== */

header {
  background-color: #2c3e50;
  padding: 20px;
}

/* Titre principal dans l'en-tête */
header h1 {
  color: white;
  font-size: 32px; /* Taille pour les grands écrans */
}


/* ========================================
   SECTION : CONTENU PRINCIPAL
   ======================================== */

main {
  max-width: 1200px;
  margin: 0 auto;
}
```

**⚠️ Attention :** Il n'existe pas de commentaire sur une seule ligne avec `//` en CSS (contrairement à JavaScript). Seule la syntaxe `/* */` est valide.

```css
/* ✅ Correct */
color: red; /* Couleur du texte */

/* ❌ Incorrect (syntaxe JavaScript, pas CSS) */
// color: red;
```

---

## 3.5 La cascade CSS

### Qu'est-ce que la cascade ?

La **cascade** est le mécanisme par lequel le navigateur détermine **quelle règle CSS s'applique** lorsque plusieurs règles ciblent le même élément avec la même propriété.

Le terme "Cascading" dans CSS vient justement de ce mécanisme : les règles se "cascadent" (s'accumulent) les unes sur les autres.

### Les sources CSS par ordre de priorité

1. **Styles du navigateur** (user agent stylesheet) — priorité la plus basse
2. **Styles de l'utilisateur** (préférences du navigateur de l'utilisateur)
3. **Styles de l'auteur** (votre CSS) — priorité haute
4. **Styles inline** (`style=""` directement sur l'élément) — priorité très haute
5. **`!important`** — écrase tout (à utiliser avec parcimonie)

### Exemple de cascade

```css
/* Règle 1 : styles du navigateur (implicites) */
/* h1 { font-size: 2em; font-weight: bold; } */

/* Règle 2 : votre CSS */
h1 {
  color: blue;    /* ← sera appliqué */
  font-size: 24px; /* ← sera appliqué */
}

/* Règle 3 : plus loin dans le même fichier CSS */
h1 {
  color: red;     /* ← écrase color: blue (même propriété, vient après) */
}
```

Dans cet exemple, le titre `<h1>` sera en **rouge** car la deuxième règle vient après dans le fichier et écrase la première.

### L'ordre compte !

```css
/* Ordre 1 : le titre sera VERT */
h1 { color: red; }
h1 { color: blue; }
h1 { color: green; } /* ← Cette règle "gagne" car elle est la dernière */
```

---

## 3.6 La spécificité CSS

### Qu'est-ce que la spécificité ?

La spécificité détermine quelle règle **a la priorité** quand deux règles ciblent le même élément mais avec des sélecteurs différents.

**Règle générale :** Plus le sélecteur est précis, plus sa spécificité est élevée.

### Calcul de la spécificité

La spécificité est calculée comme un score en 4 niveaux :

```
Style inline    ID      Classe/Pseudo-classe/Attribut    Élément
    │            │              │                            │
   (A)          (B)            (C)                          (D)
    │            │              │                            │
   1000         100            10                            1
```

**Exemples de calcul :**

| Sélecteur | A | B | C | D | Score |
|-----------|---|---|---|---|-------|
| `p` | 0 | 0 | 0 | 1 | 0001 |
| `.classe` | 0 | 0 | 1 | 0 | 0010 |
| `#id` | 0 | 1 | 0 | 0 | 0100 |
| `style=""` | 1 | 0 | 0 | 0 | 1000 |
| `div p` | 0 | 0 | 0 | 2 | 0002 |
| `.nav a` | 0 | 0 | 1 | 1 | 0011 |
| `#nav .lien` | 0 | 1 | 1 | 0 | 0110 |
| `h1.titre` | 0 | 0 | 1 | 1 | 0011 |

### Exemple pratique

```html
<p id="intro" class="texte-principal">Bonjour !</p>
```

```css
p {
  color: black;     /* Spécificité : 0001 */
}

.texte-principal {
  color: blue;      /* Spécificité : 0010 — gagne sur p */
}

#intro {
  color: red;       /* Spécificité : 0100 — gagne sur .texte-principal */
}
```

**Résultat :** Le paragraphe sera en **rouge** car `#intro` a la spécificité la plus élevée.

### `!important` — À utiliser avec parcimonie

```css
p {
  color: black !important; /* Écrase TOUT, même les styles inline */
}
```

**⚠️ Attention :** L'utilisation de `!important` est considérée comme une mauvaise pratique car elle rend le débogage très difficile. Ne l'utilisez qu'en dernier recours.

---

## 3.7 L'héritage CSS

### Qu'est-ce que l'héritage ?

L'héritage est le mécanisme par lequel certaines propriétés CSS d'un élément **parent** sont automatiquement transmises à ses **éléments enfants**.

### Propriétés héritées par défaut

Les propriétés liées au texte sont généralement héritées :
- `color`
- `font-family`
- `font-size`
- `font-weight`
- `font-style`
- `line-height`
- `letter-spacing`
- `text-align`
- `visibility`

### Propriétés NON héritées par défaut

Les propriétés liées à la mise en page ne sont généralement PAS héritées :
- `margin`, `padding`
- `border`
- `width`, `height`
- `background`
- `display`
- `position`

### Exemple concret

```html
<div class="conteneur">
  <p>Ce texte hérite des styles du parent.</p>
  <span>Ce texte aussi !</span>
</div>
```

```css
.conteneur {
  /* Ces styles seront hérités par p et span */
  color: #333;
  font-family: Arial, sans-serif;
  font-size: 16px;
  line-height: 1.6;

  /* Ces styles NE seront PAS hérités */
  background-color: white;
  padding: 20px;
  border: 1px solid #ddd;
}

/* On n'a pas besoin de répéter color, font-family etc. sur p et span */
/* Ils les ont déjà hérités ! */
```

### Forcer l'héritage avec `inherit`

```css
/* Par défaut, border n'est pas hérité */
.parent {
  border: 2px solid blue;
}

.enfant {
  /* On force l'héritage de la bordure */
  border: inherit;
}
```

### Annuler l'héritage avec `initial`

```css
/* initial remet la propriété à sa valeur initiale (par défaut du navigateur) */
.special {
  font-family: initial; /* Remet la police par défaut du navigateur */
  color: initial;       /* Remet la couleur noire par défaut */
}
```

---

## 3.8 Les unités CSS

### Unités absolues

| Unité | Nom | Description |
|-------|-----|-------------|
| `px` | Pixel | Unité la plus courante, correspond à un point d'écran |
| `pt` | Point | 1pt = 1/72 pouce. Surtout pour l'impression |
| `cm` | Centimètre | Pour l'impression principalement |
| `mm` | Millimètre | Pour l'impression principalement |

### Unités relatives

| Unité | Basée sur | Exemple |
|-------|-----------|---------|
| `%` | L'élément parent | `width: 50%` = moitié du parent |
| `em` | Taille de police du parent | `2em` = 2× la taille du parent |
| `rem` | Taille de police du `<html>` | `1.5rem` = 1.5× la taille de la racine |
| `vw` | Largeur du viewport | `50vw` = 50% de la largeur de l'écran |
| `vh` | Hauteur du viewport | `100vh` = hauteur totale de l'écran |
| `vmin` | Le plus petit entre vw et vh | |
| `vmax` | Le plus grand entre vw et vh | |

### Quand utiliser quelle unité ?

```css
/* px : tailles fixes (bordures, ombres) */
border: 1px solid #ccc;
border-radius: 4px;

/* rem : tailles de texte */
font-size: 1rem;    /* 16px si la racine est à 16px */
font-size: 1.25rem; /* 20px */
font-size: 0.875rem; /* 14px */

/* em : marges et paddings relatifs à la taille du texte */
padding: 0.5em 1em; /* Proportionnel à la taille du texte de l'élément */

/* % : largeurs fluides */
width: 100%;
max-width: 80%;

/* vh/vw : sections plein écran */
height: 100vh; /* Section occupant toute la hauteur de l'écran */
width: 100vw;
```

---

## 📝 Exercices pratiques

### Exercice 3.1 — Analyser des règles CSS

Pour chaque règle CSS suivante, identifiez : le sélecteur, les propriétés et les valeurs.

```css
/* Règle A */
.bouton-principal {
  background-color: #3498db;
  color: white;
  padding: 12px 24px;
  border-radius: 6px;
  font-size: 16px;
}

/* Règle B */
#navigation ul li a {
  text-decoration: none;
  color: #333;
}

/* Règle C */
article > h2:first-child {
  font-size: 28px;
  margin-bottom: 16px;
}
```

### Exercice 3.2 — Spécificité

Quelle couleur aura le texte de cet élément ?

```html
<p id="special" class="texte">Quelle est ma couleur ?</p>
```

```css
p { color: black; }
.texte { color: blue; }
p.texte { color: green; }
#special { color: red; }
p#special.texte { color: orange; }
```

### Exercice 3.3 — Héritage

Créez une page HTML avec un `<div>` parent et plusieurs éléments enfants. Appliquez des styles sur le parent et observez quels styles sont hérités.

---

## ✅ Corrigé — Exercice 3.2

La couleur sera **orange** car :
- `p` → spécificité 0001
- `.texte` → spécificité 0010
- `p.texte` → spécificité 0011
- `#special` → spécificité 0100
- `p#special.texte` → spécificité 0111 ← **Le plus élevé !**

---

## 📌 Résumé du module 03

| Concept | Points clés |
|---------|-------------|
| **Règle CSS** | sélecteur { propriété: valeur; } |
| **Cascade** | En cas de conflit, l'ordre dans le fichier compte |
| **Spécificité** | ID (100) > Classe (10) > Élément (1) > Universel (0) |
| **Héritage** | Les propriétés textuelles sont héritées par défaut |
| **Commentaires** | `/* ... */` uniquement (pas de `//`) |

---

## 🔗 Références

- [MDN — Cascade et héritage](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)
- [MDN — Spécificité](https://developer.mozilla.org/fr/docs/Web/CSS/Specificity)
- [Specificity Calculator](https://specificity.keegan.st/)
- [MDN — Valeurs et unités CSS](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Values_and_units)

---

*⬅️ [Module 02](../02-environnement/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 04 — Sélecteurs CSS](../04-selecteurs/README.md)*
