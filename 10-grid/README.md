# Module 10 — CSS Grid

> **Niveau :** Intermédiaire  
> **Durée estimée :** 6 heures  
> **Prérequis :** Modules 01 à 09

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Créer des mises en page complexes avec CSS Grid
- Définir des lignes et colonnes
- Placer des éléments précisément sur la grille
- Créer des layouts responsives avec auto-fit/auto-fill

---

## 10.1 Introduction à CSS Grid

### Flexbox vs Grid

| Flexbox | Grid |
|---------|------|
| **Unidimensionnel** (une ligne OU une colonne) | **Bidimensionnel** (lignes ET colonnes) |
| Idéal pour des composants | Idéal pour les layouts de page |
| Contrôle basé sur le contenu | Contrôle basé sur la grille |

**Règle générale :**
- Utilisez **Flexbox** pour les composants (navbar, liste de cartes, boutons)
- Utilisez **Grid** pour les mises en page globales (header/sidebar/main/footer)

### Activer Grid

```css
.conteneur {
  display: grid;
}
/* Les enfants directs deviennent des éléments de grille */
```

---

## 10.2 Définir les colonnes et lignes

### `grid-template-columns`

```css
/* 3 colonnes de 200px */
.grille { grid-template-columns: 200px 200px 200px; }

/* Unité fr (fraction) */
.grille { grid-template-columns: 1fr 1fr 1fr; } /* 3 colonnes égales */
.grille { grid-template-columns: 1fr 2fr 1fr; } /* Centrale = 2x plus large */

/* Fonction repeat() */
.grille { grid-template-columns: repeat(3, 1fr); }         /* 3 colonnes égales */
.grille { grid-template-columns: repeat(4, 200px); }        /* 4 colonnes de 200px */
.grille { grid-template-columns: repeat(3, 1fr) 200px; }    /* 3 + 1 colonne fixe */

/* Colonnes mixtes */
.grille { grid-template-columns: 250px 1fr; }  /* Sidebar fixe + contenu flexible */
```

### `grid-template-rows`

```css
.grille {
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px auto 60px; /* Header, Contenu, Footer */
}
```

### L'unité `fr` (fraction)

```css
/* fr = fraction de l'espace DISPONIBLE après les éléments fixes */
.grille {
  grid-template-columns: 200px 1fr 1fr;
  /* 200px pour la 1ère colonne, espace restant divisé en 2 */
}
```

### `minmax()` — Taille flexible avec limites

```css
.grille {
  grid-template-columns: repeat(3, minmax(200px, 1fr));
  /* Chaque colonne : au moins 200px, au plus 1/3 de l'espace */
}
```

---

## 10.3 Les espaces (`gap`)

```css
.grille {
  display: grid;
  gap: 20px;              /* 20px entre colonnes ET lignes */
  gap: 16px 24px;         /* 16px entre lignes, 24px entre colonnes */
  row-gap: 16px;          /* Uniquement entre les lignes */
  column-gap: 24px;       /* Uniquement entre les colonnes */
}
```

---

## 10.4 Placer les éléments sur la grille

### `grid-column` et `grid-row`

```css
/* Les lignes de grille sont numérotées à partir de 1 */
/*
   1    2    3    4
   |    |    |    |
   ┌────┬────┬────┐
 1─│    │    │    │
   ├────┼────┼────┤
 2─│    │    │    │
   ├────┼────┼────┤
 3─│    │    │    │
   └────┴────┴────┘
*/

.element {
  grid-column: 1 / 3;   /* De la ligne 1 à la ligne 3 (occupe 2 colonnes) */
  grid-column: 2 / -1;  /* De la ligne 2 à la dernière ligne */
  grid-column: span 2;  /* S'étend sur 2 colonnes */

  grid-row: 1 / 2;      /* De la ligne 1 à la ligne 2 */
  grid-row: span 2;     /* S'étend sur 2 lignes */
}
```

### `grid-area` — Raccourci

```css
/* grid-area: ligne-debut / colonne-debut / ligne-fin / colonne-fin */
.element {
  grid-area: 1 / 1 / 3 / 3; /* Lignes 1-3, colonnes 1-3 */
}
```

---

## 10.5 Zones nommées (`grid-template-areas`)

C'est l'une des fonctionnalités les plus puissantes et lisibles de Grid :

```css
.page {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 64px 1fr 60px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

**Visualisation :**
```
┌──────────────────────────┐
│         HEADER           │
├──────────┬───────────────┤
│          │               │
│ SIDEBAR  │     MAIN      │
│          │               │
├──────────┴───────────────┤
│         FOOTER           │
└──────────────────────────┘
```

Pour laisser une cellule vide, utilisez `.` :
```css
grid-template-areas:
  "header  header"
  ".       main"
  "footer  footer";
```

---

## 10.6 `auto-fill` et `auto-fit`

Ces mots-clés permettent de créer des grilles responsives sans media queries !

```css
/* auto-fill : crée autant de colonnes que possible */
.grille {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}
/* Sur un écran de 900px : ~4 colonnes de 200px
   Sur un écran de 600px : ~3 colonnes
   Sur mobile : 1 ou 2 colonnes */

/* auto-fit : comme auto-fill mais les colonnes vides s'effacent */
.grille {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}
```

**Différence auto-fill vs auto-fit :**
- `auto-fill` : Conserve les colonnes vides (utile pour l'alignement)
- `auto-fit` : Les colonnes vides s'effacent — les éléments s'étendent davantage

---

## 10.7 Exemple complet — Layout de page

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Layout CSS Grid</title>
  <link rel="stylesheet" href="grid-demo.css">
</head>
<body>

  <div class="page-grid">

    <header class="header">
      <div class="logo">MonSite</div>
      <nav class="nav">
        <a href="#">Accueil</a>
        <a href="#">Articles</a>
        <a href="#">Contact</a>
      </nav>
    </header>

    <aside class="sidebar">
      <h3>Navigation</h3>
      <ul>
        <li><a href="#">CSS Basics</a></li>
        <li><a href="#">Flexbox</a></li>
        <li><a href="#">Grid</a></li>
      </ul>
    </aside>

    <main class="main">
      <h1>Titre de l'article</h1>

      <!-- Grille de cartes responsive -->
      <div class="grille-articles">
        <article class="article-carte">
          <h2>Article 1</h2>
          <p>Contenu de l'article...</p>
        </article>
        <article class="article-carte">
          <h2>Article 2</h2>
          <p>Contenu de l'article...</p>
        </article>
        <article class="article-carte">
          <h2>Article 3</h2>
          <p>Contenu de l'article...</p>
        </article>
        <article class="article-carte article-vedette">
          <h2>Article Vedette</h2>
          <p>Cet article occupe 2 colonnes...</p>
        </article>
      </div>
    </main>

    <footer class="footer">
      <p>© 2024 MonSite — Formation CSS Grid</p>
    </footer>

  </div>

</body>
</html>
```

```css
/* grid-demo.css */

*, *::before, *::after { box-sizing: border-box; }

body {
  margin: 0;
  font-family: 'Segoe UI', Arial, sans-serif;
  background: #f0f2f5;
  color: #333;
}

/* ─── Layout principal ─── */
.page-grid {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-rows: 64px 1fr 60px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
}

/* ─── Header ─── */
.header {
  grid-area: header;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 32px;
  background: #1a252f;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}

.logo {
  color: white;
  font-size: 20px;
  font-weight: 700;
}

.nav {
  display: flex;
  gap: 4px;
}

.nav a {
  color: rgba(255,255,255,0.8);
  text-decoration: none;
  padding: 8px 14px;
  border-radius: 6px;
  font-size: 14px;
  transition: background 0.2s;
}

.nav a:hover {
  background: rgba(255,255,255,0.1);
  color: white;
}

/* ─── Sidebar ─── */
.sidebar {
  grid-area: sidebar;
  background: #2c3e50;
  padding: 24px;
  color: white;
}

.sidebar h3 {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.4);
  margin: 0 0 16px 0;
}

.sidebar ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.sidebar li a {
  display: block;
  padding: 10px 12px;
  color: rgba(255,255,255,0.75);
  text-decoration: none;
  border-radius: 6px;
  font-size: 14px;
  transition: background 0.2s;
}

.sidebar li a:hover {
  background: rgba(255,255,255,0.1);
  color: white;
}

/* ─── Contenu principal ─── */
.main {
  grid-area: main;
  padding: 32px;
  overflow: auto;
}

.main h1 {
  font-size: 26px;
  color: #1a252f;
  margin: 0 0 24px 0;
}

/* ─── Grille d'articles ─── */
.grille-articles {
  display: grid;
  /* Grille responsive sans media query ! */
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.article-carte {
  background: white;
  padding: 24px;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

/* Article vedette : s'étend sur 2 colonnes */
.article-vedette {
  grid-column: span 2;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
}

.article-carte h2 {
  font-size: 18px;
  margin: 0 0 12px 0;
}

.article-carte p {
  font-size: 14px;
  color: #666;
  line-height: 1.6;
  margin: 0;
}

.article-vedette p {
  color: rgba(255,255,255,0.85);
}

/* ─── Footer ─── */
.footer {
  grid-area: footer;
  background: #1a252f;
  color: rgba(255,255,255,0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
}
```

---

## 📝 Exercices pratiques

### Exercice 10.1 — Layout 3 zones

Créez un layout avec header, contenu et footer en utilisant `grid-template-areas`.

### Exercice 10.2 — Galerie responsive

Créez une galerie de photos responsive avec `auto-fill` et `minmax()`.

### Exercice 10.3 — Dashboard

Créez un tableau de bord avec des widgets de différentes tailles sur une grille.

---

## ✅ Corrigé — Exercice 10.1

```css
.app {
  display: grid;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header"
    "main"
    "footer";
  min-height: 100vh;
}

.header { grid-area: header; background: #2c3e50; }
.main   { grid-area: main;   background: #f5f5f5; padding: 20px; }
.footer { grid-area: footer; background: #1a252f; }
```

---

## 📌 Résumé

| Propriété | Rôle |
|-----------|------|
| `display: grid` | Active CSS Grid |
| `grid-template-columns` | Définit les colonnes |
| `grid-template-rows` | Définit les lignes |
| `grid-template-areas` | Zones nommées |
| `gap` | Espacement |
| `grid-column / grid-row` | Placement des éléments |
| `grid-area` | Zone nommée pour un élément |
| `repeat()` | Répétition de colonnes/lignes |
| `minmax()` | Taille avec limites |
| `auto-fill / auto-fit` | Colonnes adaptatives |

## 🔗 Références

- [MDN — CSS Grid](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Grid_Layout)
- [CSS-Tricks — Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid Garden — Jeu interactif](https://cssgridgarden.com/#fr)

---
*⬅️ [Module 09](../09-flexbox/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 11 — Responsive Design](../11-responsive/README.md)*
