# Module 11 — Responsive Design

> **Niveau :** Intermédiaire  
> **Durée estimée :** 5 heures  
> **Prérequis :** Modules 01 à 10

---

## 11.1 Qu'est-ce que le responsive design ?

### Définition

Le **responsive design** (design adaptatif) est une approche de conception Web qui permet à une page de s'adapter automatiquement à la taille de l'écran sur lequel elle est affichée — que ce soit un smartphone, une tablette, un ordinateur portable ou un grand écran.

### La balise meta viewport (OBLIGATOIRE)

```html
<!-- À mettre dans le <head> de TOUTES vos pages -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Explication :**
- `width=device-width` : La largeur de la page correspond à la largeur de l'écran
- `initial-scale=1.0` : Pas de zoom initial

---

## 11.2 Les media queries

### Syntaxe de base

```css
/* S'applique UNIQUEMENT quand la largeur est inférieure ou égale à 768px */
@media (max-width: 768px) {
  body {
    font-size: 14px;
  }
}

/* S'applique quand la largeur est supérieure ou égale à 769px */
@media (min-width: 769px) {
  .sidebar {
    display: block;
  }
}

/* Intervalle : entre 600px et 900px */
@media (min-width: 600px) and (max-width: 900px) {
  .colonne {
    width: 50%;
  }
}
```

### Types de media

```css
@media screen { }        /* Écrans (défaut) */
@media print { }         /* Impression */
@media (orientation: landscape) { } /* Paysage */
@media (orientation: portrait) { }  /* Portrait */
@media (prefers-color-scheme: dark) { }   /* Mode sombre */
@media (prefers-reduced-motion: reduce) { } /* Animations réduites */
```

---

## 11.3 Les points de rupture (breakpoints)

### Breakpoints courants

```css
/* ─── Mobile-first approach (recommandée) ─── */

/* Base : mobile (< 576px) — pas de media query nécessaire */
.conteneur { width: 100%; padding: 0 16px; }

/* Petit écran / paysage mobile */
@media (min-width: 576px) {
  .conteneur { max-width: 540px; }
}

/* Tablette */
@media (min-width: 768px) {
  .conteneur { max-width: 720px; }
}

/* Desktop */
@media (min-width: 992px) {
  .conteneur { max-width: 960px; }
}

/* Grand desktop */
@media (min-width: 1200px) {
  .conteneur { max-width: 1140px; }
}

/* Très grand écran */
@media (min-width: 1400px) {
  .conteneur { max-width: 1320px; }
}
```

---

## 11.4 L'approche mobile-first

### Concept

**Mobile-first** signifie que vous écrivez d'abord les styles pour mobile, puis vous les **augmentez** pour les écrans plus grands avec des `@media (min-width: ...)`.

```css
/* ✅ Mobile-first (recommandé) */

/* Styles de base pour mobile */
.navigation {
  display: flex;
  flex-direction: column; /* Liens empilés sur mobile */
}

/* À partir de la tablette : liens en ligne */
@media (min-width: 768px) {
  .navigation {
    flex-direction: row;
  }
}

/* ❌ Desktop-first (éviter) */
.navigation {
  display: flex;
  flex-direction: row; /* Styles pour desktop par défaut */
}
@media (max-width: 768px) {
  .navigation {
    flex-direction: column; /* Annuler pour mobile */
  }
}
```

---

## 11.5 Les unités relatives pour le responsive

```css
/* Pourcentages pour les largeurs */
.colonne { width: 100%; }
@media (min-width: 768px) {
  .colonne { width: 50%; }
}

/* rem pour la typographie */
:root { font-size: 16px; } /* Base */
@media (max-width: 480px) {
  :root { font-size: 14px; } /* Plus petit sur mobile */
}

/* vw et vh pour les sections */
.hero {
  height: 100vh; /* Pleine hauteur de l'écran */
}

/* clamp() — responsive sans media query */
h1 {
  font-size: clamp(1.5rem, 4vw, 3rem);
  /* Min: 1.5rem, préféré: 4vw, max: 3rem */
}

.conteneur {
  width: clamp(320px, 90%, 1200px);
}
```

---

## 11.6 Images responsives

```css
/* Image qui s'adapte à son conteneur */
img {
  max-width: 100%;
  height: auto;
  display: block;
}

/* Image de fond responsive */
.hero {
  background-image: url('hero-mobile.jpg');
  background-size: cover;
  background-position: center;
}

@media (min-width: 768px) {
  .hero {
    background-image: url('hero-desktop.jpg');
  }
}
```

```html
<!-- Balise picture pour images responsives -->
<picture>
  <source media="(min-width: 768px)" srcset="image-desktop.jpg">
  <source media="(min-width: 480px)" srcset="image-tablette.jpg">
  <img src="image-mobile.jpg" alt="Description">
</picture>
```

---

## 11.7 Navigation responsive

```html
<nav class="navbar">
  <div class="logo">MonSite</div>
  <button class="menu-toggle" aria-label="Menu">☰</button>
  <ul class="nav-menu">
    <li><a href="#">Accueil</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
/* ─── Mobile ─── */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 16px;
  height: 60px;
  background: #2c3e50;
}

.logo { color: white; font-weight: bold; }

.menu-toggle {
  display: block; /* Visible sur mobile */
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
}

.nav-menu {
  display: none; /* Caché sur mobile */
  position: absolute;
  top: 60px;
  left: 0;
  width: 100%;
  background: #2c3e50;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-menu.ouvert {
  display: block; /* Ouvert via JavaScript */
}

.nav-menu li a {
  display: block;
  padding: 14px 20px;
  color: white;
  text-decoration: none;
  border-top: 1px solid rgba(255,255,255,0.1);
}

/* ─── Desktop ─── */
@media (min-width: 768px) {
  .menu-toggle {
    display: none; /* Caché sur desktop */
  }

  .nav-menu {
    display: flex; /* Toujours visible et en ligne */
    position: static;
    width: auto;
    background: none;
  }

  .nav-menu li a {
    border-top: none;
    padding: 8px 14px;
    border-radius: 6px;
    transition: background 0.2s;
  }

  .nav-menu li a:hover {
    background: rgba(255,255,255,0.1);
  }
}
```

---

## 11.8 CSS Container Queries (CSS Moderne)

Les Container Queries permettent d'adapter un composant selon la taille de son conteneur (et non de l'écran entier) :

```css
/* Définir un contexte de conteneur */
.carte-conteneur {
  container-type: inline-size;
  container-name: carte;
}

/* S'adapte à la taille du conteneur */
@container carte (min-width: 400px) {
  .carte {
    display: flex;
    gap: 20px;
  }

  .carte img {
    width: 150px;
    flex-shrink: 0;
  }
}
```

---

## 📝 Exercice 11.1 — Page responsive complète

Créez une page avec :
- Header responsive (hamburger sur mobile, liens sur desktop)
- Grille de cartes : 1 colonne sur mobile, 2 sur tablette, 3 sur desktop
- Footer avec colonnes qui s'empilent sur mobile

---

## ✅ Corrigé — Grille responsive

```css
.grille {
  display: grid;
  gap: 20px;
  /* Mobile : 1 colonne */
  grid-template-columns: 1fr;
}

/* Tablette */
@media (min-width: 600px) {
  .grille {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop */
@media (min-width: 992px) {
  .grille {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Ou, sans media query (avec auto-fill) : */
.grille {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}
```

---

## 📌 Résumé

| Concept | Description |
|---------|-------------|
| `<meta viewport>` | Obligatoire pour le responsive |
| `@media` | Conditions d'application des styles |
| Mobile-first | Écrire pour mobile, améliorer pour desktop |
| `min-width` | Media query mobile-first |
| `max-width` | Media query desktop-first |
| `clamp()` | Valeurs fluides sans media query |
| Container Queries | Adaptation au conteneur (moderne) |

## 🔗 Références

- [MDN — Responsive Design](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [web.dev — Responsive Web Design Basics](https://web.dev/responsive-web-design-basics/)
- [MDN — Media queries](https://developer.mozilla.org/fr/docs/Web/CSS/Media_Queries)

---
*⬅️ [Module 10](../10-grid/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 12 — Animations](../12-animations/README.md)*
