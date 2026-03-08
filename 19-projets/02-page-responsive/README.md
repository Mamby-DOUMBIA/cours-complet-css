# Projet 02 — Page Responsive Mobile-First

> **Niveau :** Intermédiaire | Techniques : Media queries, CSS Grid, Mobile-first

## Objectifs

Ce projet est un blog responsive conçu en approche mobile-first.
Ouvrez `index.html` dans votre navigateur et redimensionnez la fenêtre pour voir l'adaptation.

## Fichiers
- `index.html` — Structure du blog
- `styles.css` — CSS mobile-first avec media queries

## Instructions de réalisation

Créez une page de blog avec :
1. Navigation responsive (hamburger mobile → liens desktop)
2. Hero section avec image de fond
3. Grille d'articles : 1 col (mobile) → 2 col (tablette) → 3 col (desktop)
4. Sidebar qui s'affiche en colonne sur mobile, à droite sur desktop
5. Footer avec colonnes empilées sur mobile

## Corrigé

Voici le CSS mobile-first essentiel :

```css
/* ─── MOBILE (base) ─── */
.grille-articles {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
}

.mise-en-page {
  display: grid;
  grid-template-columns: 1fr; /* Colonne unique sur mobile */
}

.sidebar {
  order: 2; /* Sidebar après le contenu sur mobile */
}

/* ─── TABLETTE ─── */
@media (min-width: 640px) {
  .grille-articles {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* ─── DESKTOP ─── */
@media (min-width: 1024px) {
  .grille-articles {
    grid-template-columns: repeat(3, 1fr);
  }

  .mise-en-page {
    grid-template-columns: 1fr 300px; /* Contenu + Sidebar */
  }

  .sidebar {
    order: 0; /* Ordre normal sur desktop */
  }
}
```

---
*[Retour aux projets](../README.md)*
