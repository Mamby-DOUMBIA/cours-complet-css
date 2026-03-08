# Module 09 — Flexbox

> **Niveau :** Intermédiaire  
> **Durée estimée :** 6 heures  
> **Prérequis :** Modules 01 à 08

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Créer des mises en page avec Flexbox
- Aligner des éléments horizontalement et verticalement
- Contrôler la distribution de l'espace
- Créer des designs flexibles et adaptatifs

---

## 9.1 Introduction à Flexbox

### Qu'est-ce que Flexbox ?

**Flexbox** (Flexible Box Layout) est un module CSS de mise en page **unidimensionnel** : il organise les éléments sur un axe à la fois (ligne ou colonne).

Avant Flexbox, centrer un élément verticalement ou créer des colonnes de même hauteur était très difficile. Flexbox a révolutionné la mise en page CSS en rendant ces tâches triviales.

### Le concept fondamental

Flexbox fonctionne avec deux types d'éléments :

1. **Le conteneur flex** (`display: flex`) — l'élément parent
2. **Les éléments flex** — les enfants directs du conteneur

```html
<!-- Conteneur flex -->
<div class="conteneur-flex">
  <!-- Éléments flex -->
  <div class="element">1</div>
  <div class="element">2</div>
  <div class="element">3</div>
</div>
```

```css
.conteneur-flex {
  display: flex; /* Active Flexbox */
}
/* Les trois div enfants deviennent automatiquement des éléments flex */
```

---

## 9.2 Les axes Flexbox

Flexbox utilise deux axes perpendiculaires :

```
AXEL PRINCIPAL (main axis) — direction: row (défaut)
→ → → → → → → → → → →
┌──────────────────────────────────────────┐
│  ┌────────┐  ┌────────┐  ┌────────┐     │
│  │ Item 1 │  │ Item 2 │  │ Item 3 │  ↕  │
│  └────────┘  └────────┘  └────────┘     │ AXE TRANSVERSAL
│                                          │ (cross axis)
└──────────────────────────────────────────┘
```

Avec `flex-direction: column`, les axes sont inversés :

```
AXEL PRINCIPAL (main axis) — direction: column
  ↓
┌────────┐
│ Item 1 │
└────────┘
  ↓
┌────────┐  ← → AXE TRANSVERSAL
│ Item 2 │
└────────┘
  ↓
┌────────┐
│ Item 3 │
└────────┘
```

---

## 9.3 Propriétés du conteneur flex

### `flex-direction` — Direction des éléments

```css
.conteneur {
  display: flex;
  flex-direction: row;            /* → Défaut : gauche à droite */
  flex-direction: row-reverse;    /* ← Droite à gauche */
  flex-direction: column;         /* ↓ Haut en bas */
  flex-direction: column-reverse; /* ↑ Bas en haut */
}
```

### `flex-wrap` — Retour à la ligne

Par défaut, les éléments flex essaient tous de tenir sur une seule ligne.

```css
.conteneur {
  display: flex;
  flex-wrap: nowrap;       /* Défaut : une seule ligne (peut déborder) */
  flex-wrap: wrap;         /* Retour à la ligne si nécessaire */
  flex-wrap: wrap-reverse; /* Retour à la ligne, lignes inversées */
}
```

### `flex-flow` — Raccourci direction + wrap

```css
.conteneur {
  flex-flow: row wrap;          /* Remplace flex-direction et flex-wrap */
  flex-flow: column nowrap;
}
```

### `justify-content` — Alignement sur l'axe principal

```css
.conteneur {
  display: flex;
  justify-content: flex-start;    /* Début de l'axe (défaut) */
  justify-content: flex-end;      /* Fin de l'axe */
  justify-content: center;        /* Centré */
  justify-content: space-between; /* Espace entre les éléments */
  justify-content: space-around;  /* Espace autour des éléments */
  justify-content: space-evenly;  /* Espace égal partout */
}
```

**Visualisation :**
```
flex-start:    [1][2][3]____________
flex-end:      ____________[1][2][3]
center:        ______[1][2][3]______
space-between: [1]_____[2]_____[3]
space-around:  __[1]___[2]___[3]__
space-evenly:  ___[1]___[2]___[3]___
```

### `align-items` — Alignement sur l'axe transversal

```css
.conteneur {
  display: flex;
  height: 200px; /* Nécessaire pour voir l'effet */

  align-items: stretch;     /* Défaut : s'étire pour remplir */
  align-items: flex-start;  /* Haut du conteneur */
  align-items: flex-end;    /* Bas du conteneur */
  align-items: center;      /* Centré verticalement */
  align-items: baseline;    /* Aligné sur la ligne de base du texte */
}
```

### `align-content` — Alignement des lignes (multi-lignes)

S'applique quand il y a plusieurs lignes (avec `flex-wrap: wrap`) :

```css
.conteneur {
  display: flex;
  flex-wrap: wrap;
  height: 400px;

  align-content: flex-start;    /* Lignes groupées en haut */
  align-content: flex-end;      /* Lignes groupées en bas */
  align-content: center;        /* Lignes groupées au centre */
  align-content: space-between; /* Espace entre les lignes */
  align-content: space-around;  /* Espace autour des lignes */
  align-content: stretch;       /* Lignes s'étirent (défaut) */
}
```

### `gap` — Espacement entre les éléments

```css
.conteneur {
  display: flex;
  gap: 16px;           /* Espace horizontal et vertical identique */
  gap: 16px 24px;      /* Espace vertical | espace horizontal */
  row-gap: 16px;       /* Uniquement l'espace vertical */
  column-gap: 24px;    /* Uniquement l'espace horizontal */
}
```

---

## 9.4 Propriétés des éléments flex

### `flex-grow` — Capacité à s'agrandir

Définit la capacité d'un élément à **prendre de l'espace supplémentaire** disponible dans le conteneur.

```css
/* Valeur par défaut : 0 (ne grandit pas) */
.element { flex-grow: 0; }

/* Tous les éléments se partagent l'espace équitablement */
.element { flex-grow: 1; }

/* Cet élément prend 2x plus d'espace que les autres */
.element-large { flex-grow: 2; }
```

**Exemple pratique :**
```css
.conteneur {
  display: flex;
  width: 600px;
}

.sidebar { flex-grow: 1; }   /* Prend 1/4 de l'espace libre */
.main    { flex-grow: 3; }   /* Prend 3/4 de l'espace libre */
```

### `flex-shrink` — Capacité à rétrécir

Définit la capacité d'un élément à **rétrécir** si l'espace manque.

```css
/* Valeur par défaut : 1 (rétrécit si nécessaire) */
.element { flex-shrink: 1; }

/* Cet élément ne rétrécit jamais */
.logo { flex-shrink: 0; }

/* Cet élément rétrécit 2x plus vite */
.element-flexible { flex-shrink: 2; }
```

### `flex-basis` — Taille de base

Définit la taille initiale de l'élément **avant** que l'espace libre soit distribué.

```css
.element {
  flex-basis: auto;    /* Défaut : taille basée sur width/height */
  flex-basis: 200px;   /* Taille de base fixe */
  flex-basis: 25%;     /* Pourcentage du conteneur */
  flex-basis: 0;       /* Pas de taille de base */
}
```

### `flex` — Raccourci (flex-grow + flex-shrink + flex-basis)

```css
/* flex: grow shrink basis */
.element { flex: 1 1 auto; }   /* Peut grandir et rétrécir, taille auto */
.element { flex: 1; }          /* Équivalent à flex: 1 1 0 */
.element { flex: auto; }       /* Équivalent à flex: 1 1 auto */
.element { flex: none; }       /* Équivalent à flex: 0 0 auto — rigide */
.element { flex: 0 0 200px; }  /* Taille fixe de 200px */
```

**Patterns courants :**
```css
/* Tous les éléments ont la même taille et partagent l'espace */
.colonne { flex: 1; }

/* Élément de taille fixe + élément qui prend le reste */
.sidebar { flex: 0 0 280px; }  /* 280px fixes */
.main    { flex: 1; }           /* Prend le reste */

/* Logo qui ne rétrécit jamais */
.logo { flex: 0 0 auto; }
```

### `order` — Ordre d'affichage

```css
/* Défaut : 0. L'ordre HTML est conservé */
.premier  { order: -1; } /* Affiché en premier */
.normal   { order: 0; }  /* Affiché dans l'ordre normal */
.dernier  { order: 1; }  /* Affiché en dernier */
```

### `align-self` — Alignement individuel

```css
/* Écrase align-items pour cet élément spécifique */
.element-special {
  align-self: center;     /* Centré verticalement */
  align-self: flex-start; /* En haut */
  align-self: flex-end;   /* En bas */
  align-self: stretch;    /* S'étire */
  align-self: auto;       /* Suit align-items du conteneur */
}
```

---

## 9.5 Cas d'utilisation pratiques

### Cas 1 : Centrage parfait (horizontal ET vertical)

```css
/* La façon la plus simple de centrer un élément */
.conteneur-centrage {
  display: flex;
  justify-content: center; /* Centré horizontalement */
  align-items: center;     /* Centré verticalement */
  height: 100vh;           /* Hauteur plein écran */
}
```

### Cas 2 : Barre de navigation

```css
.navbar {
  display: flex;
  justify-content: space-between; /* Logo à gauche, liens à droite */
  align-items: center;
  padding: 0 24px;
  height: 64px;
  background-color: #2c3e50;
}

.nav-logo {
  font-size: 20px;
  font-weight: bold;
  color: white;
  flex-shrink: 0; /* Le logo ne rétrécit pas */
}

.nav-liens {
  display: flex;
  gap: 8px;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-liens a {
  color: rgba(255,255,255,0.85);
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.nav-liens a:hover {
  background-color: rgba(255,255,255,0.15);
  color: white;
}
```

### Cas 3 : Layout avec sidebar

```css
.page-layout {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  flex: 0 0 260px; /* Taille fixe, ne grandit pas, ne rétrécit pas */
  background-color: #2c3e50;
  padding: 20px;
}

.contenu-principal {
  flex: 1;           /* Prend tout l'espace restant */
  padding: 40px;
  background-color: #f5f5f5;
}
```

### Cas 4 : Grille de cartes adaptatives

```css
.grille-cartes {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
}

.carte {
  flex: 1 1 280px; /* Minimum 280px, peut grandir et rétrécir */
  /* Les cartes font au minimum 280px et se partagent l'espace disponible */
  background: white;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
```

### Cas 5 : Footer collé en bas de page

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* La page fait au moins la hauteur de l'écran */
}

main {
  flex: 1; /* Le main prend tout l'espace disponible */
}

footer {
  /* Restera toujours en bas, même si le contenu est court */
  background-color: #2c3e50;
  color: white;
  padding: 20px;
  text-align: center;
}
```

---

## 9.6 Exemple complet annoté

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flexbox — Démonstration</title>
  <link rel="stylesheet" href="flexbox-demo.css">
</head>
<body>

  <!-- Barre de navigation -->
  <nav class="navbar">
    <div class="nav-logo">MonSite</div>
    <ul class="nav-liens">
      <li><a href="#">Accueil</a></li>
      <li><a href="#">Services</a></li>
      <li><a href="#">À propos</a></li>
      <li><a href="#" class="btn-contact">Contact</a></li>
    </ul>
  </nav>

  <!-- Contenu principal avec sidebar -->
  <div class="page-layout">
    <aside class="sidebar">
      <h3>Catégories</h3>
      <ul>
        <li><a href="#">CSS</a></li>
        <li><a href="#">HTML</a></li>
        <li><a href="#">JavaScript</a></li>
      </ul>
    </aside>

    <main class="contenu">
      <h1>Articles récents</h1>
      <!-- Grille de cartes -->
      <div class="grille-cartes">
        <article class="carte">
          <h2>Titre de l'article 1</h2>
          <p>Lorem ipsum dolor sit amet...</p>
          <div class="carte-pied">
            <span class="tag">CSS</span>
            <a href="#" class="lire-plus">Lire la suite →</a>
          </div>
        </article>
        <article class="carte">
          <h2>Titre de l'article 2</h2>
          <p>Lorem ipsum dolor sit amet...</p>
          <div class="carte-pied">
            <span class="tag">Flexbox</span>
            <a href="#" class="lire-plus">Lire la suite →</a>
          </div>
        </article>
        <article class="carte">
          <h2>Titre de l'article 3</h2>
          <p>Lorem ipsum dolor sit amet...</p>
          <div class="carte-pied">
            <span class="tag">Grid</span>
            <a href="#" class="lire-plus">Lire la suite →</a>
          </div>
        </article>
      </div>
    </main>
  </div>

  <!-- Pied de page -->
  <footer class="footer">
    <p>© 2024 MonSite — Formation CSS Complète</p>
  </footer>

</body>
</html>
```

```css
/* ============================================================
   flexbox-demo.css — Démonstration Flexbox
   ============================================================ */

*, *::before, *::after { box-sizing: border-box; }

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  margin: 0;
  background-color: #f0f2f5;
  color: #333;
  /* Le body est un conteneur flex vertical */
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* ─── Navbar ─── */
.navbar {
  display: flex;
  justify-content: space-between; /* Logo à gauche, liens à droite */
  align-items: center;            /* Centrage vertical */
  padding: 0 32px;
  height: 64px;
  background-color: #1a252f;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}

.nav-logo {
  color: white;
  font-size: 20px;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.nav-liens {
  display: flex;          /* Les liens en ligne */
  align-items: center;
  gap: 4px;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-liens a {
  color: rgba(255,255,255,0.8);
  text-decoration: none;
  padding: 8px 14px;
  border-radius: 6px;
  font-size: 14px;
  transition: all 0.2s;
}

.nav-liens a:hover {
  background-color: rgba(255,255,255,0.1);
  color: white;
}

.btn-contact {
  background-color: #3498db !important;
  color: white !important;
}

/* ─── Layout principal ─── */
.page-layout {
  display: flex;    /* Sidebar + Contenu côte à côte */
  flex: 1;          /* Prend tout l'espace vertical disponible */
}

/* ─── Sidebar ─── */
.sidebar {
  flex: 0 0 240px;  /* Taille fixe, ne grandit pas, ne rétrécit pas */
  background-color: #2c3e50;
  padding: 24px;
  color: #ecf0f1;
}

.sidebar h3 {
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.5);
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
  color: rgba(255,255,255,0.8);
  text-decoration: none;
  border-radius: 6px;
  transition: background-color 0.2s;
  font-size: 14px;
}

.sidebar li a:hover {
  background-color: rgba(255,255,255,0.1);
  color: white;
}

/* ─── Contenu principal ─── */
.contenu {
  flex: 1;          /* Prend tout l'espace restant */
  padding: 32px;
  overflow: hidden;
}

.contenu h1 {
  font-size: 26px;
  color: #1a252f;
  margin: 0 0 24px 0;
}

/* ─── Grille de cartes ─── */
.grille-cartes {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.carte {
  flex: 1 1 260px;  /* Min 260px, peut grandir et rétrécir */
  background: white;
  border-radius: 10px;
  padding: 24px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
  /* Flexbox pour le pied de carte collé en bas */
  display: flex;
  flex-direction: column;
}

.carte h2 {
  font-size: 18px;
  color: #1a252f;
  margin: 0 0 12px 0;
}

.carte p {
  color: #666;
  font-size: 14px;
  line-height: 1.6;
  flex: 1; /* Pousse le pied de carte en bas */
}

.carte-pied {
  display: flex;
  justify-content: space-between; /* Tag à gauche, lien à droite */
  align-items: center;
  margin-top: 16px;
  padding-top: 16px;
  border-top: 1px solid #f0f0f0;
}

.tag {
  background-color: #eaf4fb;
  color: #3498db;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 600;
}

.lire-plus {
  color: #3498db;
  text-decoration: none;
  font-size: 13px;
  font-weight: 600;
  transition: color 0.2s;
}

.lire-plus:hover {
  color: #1a6694;
}

/* ─── Footer ─── */
.footer {
  background-color: #1a252f;
  color: rgba(255,255,255,0.5);
  text-align: center;
  padding: 20px;
  font-size: 13px;
}
```

---

## 📝 Exercices pratiques

### Exercice 9.1 — Centrage Flexbox

Créez une page avec un élément centré parfaitement au milieu de l'écran.

### Exercice 9.2 — Barre de navigation

Créez une barre de navigation avec :
- Logo à gauche
- Liens de navigation au centre
- Bouton "S'inscrire" à droite
- Alignement vertical parfait

### Exercice 9.3 — Layout 3 colonnes

Créez une mise en page avec :
- Sidebar gauche (200px fixe)
- Contenu central (s'adapte)
- Sidebar droite (200px fixe)

### Exercice 9.4 — Footer collant

Créez une page où le footer est toujours collé en bas, même si le contenu est trop court.

---

## ✅ Corrigé — Exercice 9.1

```css
body {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f2f5;
}

.carte-centree {
  background: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 8px 30px rgba(0,0,0,0.12);
  text-align: center;
  max-width: 400px;
  width: 100%;
}
```

---

## ❌ Erreurs fréquentes

### 1. Confondre `justify-content` et `align-items`
```css
/* ❌ Confusion fréquente */
.conteneur {
  display: flex;
  /* flex-direction: row par défaut → axe principal = horizontal */
  justify-content: center; /* horizontal ✅ */
  align-items: center;     /* vertical ✅ */
}

/* ⚠️ Si flex-direction: column, les axes sont inversés ! */
.conteneur {
  flex-direction: column;
  justify-content: center; /* vertical avec column */
  align-items: center;     /* horizontal avec column */
}
```

### 2. Oublier `flex-wrap` pour les grilles
```css
/* ❌ Les éléments débordent sur une seule ligne */
.grille { display: flex; }
.item { flex: 0 0 300px; }

/* ✅ Les éléments passent à la ligne suivante */
.grille { display: flex; flex-wrap: wrap; }
.item { flex: 1 1 300px; }
```

---

## 📌 Résumé du module 09

| Propriété | Sur | Description |
|-----------|-----|-------------|
| `display: flex` | Conteneur | Active Flexbox |
| `flex-direction` | Conteneur | Direction des éléments |
| `flex-wrap` | Conteneur | Retour à la ligne |
| `justify-content` | Conteneur | Alignement axe principal |
| `align-items` | Conteneur | Alignement axe transversal |
| `gap` | Conteneur | Espacement entre éléments |
| `flex-grow` | Élément | Capacité à grandir |
| `flex-shrink` | Élément | Capacité à rétrécir |
| `flex-basis` | Élément | Taille de base |
| `flex` | Élément | Raccourci grow+shrink+basis |
| `align-self` | Élément | Alignement individuel |
| `order` | Élément | Ordre d'affichage |

---

## 🔗 Références

- [MDN — Flexbox](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Flexbox)
- [CSS-Tricks — A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy — Jeu interactif](https://flexboxfroggy.com/#fr)
- [web.dev — Flexbox](https://web.dev/learn/css/flexbox/)

---

*⬅️ [Module 08](../08-mise-en-page/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 10 — CSS Grid](../10-grid/README.md)*
