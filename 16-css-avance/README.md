# Module 16 — CSS Avancé

> **Niveau :** Expert | **Durée estimée :** 5 heures

---

## 16.1 Fonctions CSS avancées

### `calc()`

```css
/* Mélange d'unités */
.conteneur {
  width: calc(100% - 40px);
  padding: calc(1rem + 10px);
  margin-top: calc(var(--espace-base) * 3);
}

/* Colonnes fluides avec gouttière */
.colonne {
  width: calc(33.333% - 20px);
  /* Ou avec CSS Grid : prefer Grid pour ce cas */
}
```

### `clamp(min, préféré, max)`

```css
/* Typographie fluide sans media query */
h1 {
  font-size: clamp(1.5rem, 4vw, 3.5rem);
  /* Sur mobile (320px) : ~1.5rem
     Sur desktop (1440px) : ~3.5rem
     Entre les deux : 4vw */
}

.conteneur {
  width: clamp(320px, 90vw, 1200px);
}

.carte {
  padding: clamp(16px, 3%, 40px);
}
```

### `min()` et `max()`

```css
.image {
  width: min(500px, 100%); /* La plus petite des deux valeurs */
}

.texte {
  font-size: max(14px, 1rem); /* La plus grande des deux valeurs */
}
```

---

## 16.2 Les filtres CSS

```css
/* Flou */
.fond-flou { filter: blur(8px); }

/* Luminosité */
.sombre { filter: brightness(0.7); }
.clair  { filter: brightness(1.3); }

/* Contraste */
.fort-contraste { filter: contrast(1.5); }

/* Niveaux de gris */
.noir-blanc { filter: grayscale(100%); }

/* Sépia */
.retro { filter: sepia(60%); }

/* Saturation */
.vivid { filter: saturate(2); }

/* Rotation des teintes */
.teinte { filter: hue-rotate(90deg); }

/* Inversion */
.negatif { filter: invert(100%); }

/* Ombre portée (préserve la forme) */
.icone-svg {
  filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.3));
}

/* Combinaisons */
.photo-retro {
  filter: sepia(50%) contrast(1.1) brightness(1.05);
}

/* Flou de fond (backdrop-filter) */
.nav-glassmorphism {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(12px) saturate(180%);
  -webkit-backdrop-filter: blur(12px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.2);
}
```

---

## 16.3 Formes et masques CSS

### `clip-path`

```css
/* Formes géométriques */
.triangle  { clip-path: polygon(50% 0%, 0% 100%, 100% 100%); }
.diamant   { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.hexagone  { clip-path: polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%); }
.cercle    { clip-path: circle(50% at 50% 50%); }
.ellipse   { clip-path: ellipse(60% 40% at 50% 50%); }

/* Rognage d'image */
.image-diagonale {
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
}

/* Animation de clip-path */
.bouton-clip {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 0.4s ease;
}

.bouton-clip:hover {
  clip-path: inset(0 0% 0 0);
}
```

### `shape-outside` (texte autour d'une forme)

```css
.image-flottante {
  float: left;
  shape-outside: circle(50%);
  clip-path: circle(50%);
  width: 200px;
  height: 200px;
  margin-right: 20px;
}
```

---

## 16.4 Effets de mélange (blend modes)

```css
/* mix-blend-mode : mélange l'élément avec son arrière-plan */
.titre-overlay {
  mix-blend-mode: multiply;   /* Multiplie les couleurs */
  mix-blend-mode: screen;     /* Inverse de multiply */
  mix-blend-mode: overlay;    /* Combine multiply et screen */
  mix-blend-mode: difference; /* Soustrait les couleurs */
  mix-blend-mode: hard-light;
  mix-blend-mode: soft-light;
  mix-blend-mode: luminosity;
}

/* background-blend-mode : mélange les couches de fond */
.hero {
  background-image: url('photo.jpg');
  background-color: #3498db;
  background-blend-mode: multiply;
}
```

---

## 16.5 CSS Scroll Snap

```css
/* Défilement par "snap" (accrochage) */
.carrousel {
  display: flex;
  overflow-x: scroll;
  scroll-snap-type: x mandatory; /* Axe X, accrochage obligatoire */
  scroll-behavior: smooth;
  gap: 20px;
}

.slide {
  flex: 0 0 100%;
  scroll-snap-align: start; /* center | end */
}

/* Scroll vertical par sections */
.sections-scroll {
  height: 100vh;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
}

.section {
  height: 100vh;
  scroll-snap-align: start;
}
```

---

## 16.6 CSS Logical Properties

```css
/* Propriétés physiques (éviter) */
margin-left:  ;
margin-right: ;
padding-top:  ;

/* Propriétés logiques (modernes, supportent RTL/LTR) */
margin-inline-start:  ; /* Gauche en LTR, droite en RTL */
margin-inline-end:    ; /* Droite en LTR, gauche en RTL */
padding-block-start:  ; /* Haut */
padding-block-end:    ; /* Bas */
margin-inline:        ; /* Gauche + Droite */
padding-block:        ; /* Haut + Bas */
border-block-end:     ; /* Bordure du bas */
inset-inline-start:   ; /* Équivalent à left en LTR */
```

---

## 16.7 Fonctionnalités CSS très modernes

### `:has()` — Le sélecteur parent

```css
/* Sélectionner un parent selon ses enfants */
/* "Sélectionne .carte qui contient une image" */
.carte:has(img) {
  padding: 0;
}

/* "Sélectionne le label dont l'input est coché" */
label:has(input:checked) {
  color: green;
  font-weight: bold;
}

/* "Sélectionne li qui a un sous-menu" */
li:has(ul) > a::after {
  content: " ▾";
}
```

### CSS Nesting (sans Sass !)

```css
/* CSS Nesting natif (navigateurs modernes) */
.carte {
  background: white;
  padding: 20px;

  /* & représente .carte */
  &:hover {
    box-shadow: 0 8px 24px rgba(0,0,0,0.15);
  }

  & .titre {
    font-size: 1.25rem;
    color: #1a1a2e;
  }

  &.vedette {
    border: 2px solid #3498db;
  }

  @media (max-width: 768px) {
    padding: 12px;
  }
}
```

### `@layer` — Couches de cascade

```css
/* Organiser la spécificité en couches */
@layer reset, base, composants, utilitaires;

@layer reset {
  * { box-sizing: border-box; margin: 0; }
}

@layer base {
  body { font-family: sans-serif; }
}

@layer composants {
  .bouton { background: #3498db; color: white; }
}

@layer utilitaires {
  .mt-4 { margin-top: 16px; }
}
/* Les utilitaires ont toujours la priorité sur les composants */
```

---

## 📝 Exercice 16.1 — Carte glassmorphism

```css
/* Créez cette carte glassmorphism */
.glass-card {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255,255,255,0.2);
  border-radius: 16px;
  padding: 30px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.1);
}
```

---

## 📌 Résumé

| Fonction/Propriété | Description |
|--------------------|-------------|
| `calc()` | Calcul avec unités mixtes |
| `clamp()` | Valeur fluide avec limites |
| `filter` | Effets visuels (flou, gris, luminosité) |
| `backdrop-filter` | Effet verre dépoli |
| `clip-path` | Découpe en formes géométriques |
| `mix-blend-mode` | Modes de mélange de couleurs |
| `scroll-snap` | Défilement par accrochage |
| `:has()` | Sélecteur parent (moderne) |
| CSS Nesting | Imbrication native |
| `@layer` | Gestion de la cascade en couches |

## 🔗 Références

- [MDN — Fonctions CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Functions)
- [MDN — filter](https://developer.mozilla.org/fr/docs/Web/CSS/filter)
- [Can I Use — :has()](https://caniuse.com/css-has)

---
*⬅️ [Module 15](../15-performance/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 17 — Accessibilité](../17-accessibilite/README.md)*
