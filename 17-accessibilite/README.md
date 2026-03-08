# Module 17 — Accessibilité et UX

> **Niveau :** Avancé | **Durée estimée :** 3 heures

---

## 17.1 Pourquoi l'accessibilité est cruciale

L'accessibilité Web (abrégée **a11y**) consiste à concevoir des sites utilisables par tous, y compris les personnes handicapées (visuelles, motrices, cognitives). En Europe, la directive européenne sur l'accessibilité rend celle-ci obligatoire pour de nombreux sites. Au-delà de l'obligation légale, un site accessible est un site meilleur pour tous.

**Les WCAG** (Web Content Accessibility Guidelines) définissent les standards d'accessibilité en 3 niveaux : A, AA et AAA. Le niveau **AA est le minimum recommandé**.

---

## 17.2 Le contraste des couleurs

### Ratios de contraste WCAG

| Niveau | Texte normal | Grand texte (18pt+) |
|--------|--------------|---------------------|
| **AA** (minimum) | 4.5:1 | 3:1 |
| **AAA** (optimal) | 7:1 | 4.5:1 |

```css
/* ✅ Bon contraste (ratio : 7:1 approx.) */
.texte-principal {
  background-color: white;   /* #ffffff */
  color: #333333;            /* Ratio ≈ 12.6:1 ✅ */
}

/* ✅ Bon contraste sur fond sombre */
.texte-inverse {
  background-color: #2c3e50;
  color: #ecf0f1;            /* Ratio ≈ 8.6:1 ✅ */
}

/* ❌ Contraste insuffisant */
.mauvais-contraste {
  background-color: white;
  color: #aaaaaa;            /* Ratio ≈ 2.3:1 ❌ */
}

/* ❌ Contraste insuffisant */
.texte-gris-clair {
  background-color: #f0f0f0;
  color: #cccccc;            /* Ratio ≈ 1.6:1 ❌ */
}
```

**Outils de vérification :**
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Coolors Contrast Checker](https://coolors.co/contrast-checker/)
- Chrome DevTools → Inspect → Accessibility

---

## 17.3 Focus visible — Navigation clavier

Toute personne naviguant au clavier (tabulation) doit voir clairement quel élément est actif.

```css
/* ❌ Ne jamais supprimer le focus sans alternative */
* { outline: none; } /* Interdit ! */
:focus { outline: none; } /* Dangereux ! */

/* ✅ Personnaliser le focus de manière visible */
:focus-visible {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}

/* Personnalisation par composant */
.bouton:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.5);
}

.lien:focus-visible {
  outline: 2px dashed currentColor;
  outline-offset: 4px;
  border-radius: 2px;
}

input:focus-visible {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.25);
}

/* :focus-visible vs :focus */
/* :focus-visible = s'active UNIQUEMENT lors de la navigation clavier */
/* :focus = s'active aussi au clic de souris */
```

---

## 17.4 Typographie accessible

```css
/* ✅ Taille minimale recommandée : 16px pour le texte courant */
body {
  font-size: 1rem; /* 16px */
  line-height: 1.6; /* Interligne confortable */
}

/* ✅ Ne pas empêcher le zoom du navigateur */
/* ❌ Ne pas faire : */
/* html { font-size: 62.5%; } avec des px fixes partout */
/* Utiliser rem pour permettre le zoom */

/* ✅ Largeur de ligne optimale pour la lecture */
p, li {
  max-width: 70ch; /* 70 caractères maximum par ligne */
}

/* ✅ Espacement suffisant */
p {
  margin-bottom: 1.25em;
  letter-spacing: 0.01em;
}

/* ✅ Éviter l'alignement justifié (crée des espaces irréguliers) */
/* ❌ text-align: justify; */
p { text-align: left; }
```

---

## 17.5 Animations et préférences utilisateur

```css
/* Respecter prefers-reduced-motion */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Approche plus nuancée */
.element-anime {
  transition: transform 0.3s ease;
}

@media (prefers-reduced-motion: reduce) {
  .element-anime {
    transition: none; /* Ou une transition très courte */
  }
}
```

---

## 17.6 Mode sombre et préférences de couleur

```css
/* Adapter automatiquement au mode sombre du système */
:root {
  --fond: #ffffff;
  --texte: #1a1a2e;
  --carte: #f5f5f5;
  --bordure: #e0e0e0;
}

@media (prefers-color-scheme: dark) {
  :root {
    --fond: #1a1a2e;
    --texte: #e0e0e0;
    --carte: #16213e;
    --bordure: #2a3a4a;
  }
}

body {
  background-color: var(--fond);
  color: var(--texte);
}
```

---

## 17.7 Éléments accessibles — Patterns CSS

### Texte masqué visuellement mais accessible aux lecteurs d'écran

```css
/* Classe utilitaire "screen-reader only" */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}

/* Utilisation */
/* <button class="btn-fermer">
     <span aria-hidden="true">×</span>
     <span class="sr-only">Fermer la fenêtre</span>
   </button> */
```

### Indicateur d'erreur accessible

```css
/* Ne pas indiquer les erreurs avec la couleur seule */

/* ❌ Uniquement la couleur (problème pour les daltoniens) */
.champ-erreur { border-color: red; }

/* ✅ Couleur + icône + texte */
.champ-erreur {
  border-color: #e74c3c;
  border-width: 2px;
}

.champ-erreur::after {
  content: " ⚠";
  color: #e74c3c;
}

.message-erreur {
  color: #e74c3c;
  font-size: 0.875rem;
  margin-top: 4px;
  display: flex;
  align-items: center;
  gap: 6px;
}

.message-erreur::before {
  content: "⚠";
  font-size: 1rem;
}
```

### Lien "Aller au contenu" (skip link)

```css
/* Permet aux utilisateurs clavier de sauter la navigation */
.lien-contenu {
  position: absolute;
  top: -100%;
  left: 0;
  background: #3498db;
  color: white;
  padding: 12px 20px;
  font-weight: bold;
  text-decoration: none;
  z-index: 9999;
  border-radius: 0 0 4px 0;
  transition: top 0.2s;
}

.lien-contenu:focus {
  top: 0; /* Visible uniquement au focus clavier */
}

/* Dans le HTML :
   <a href="#contenu-principal" class="lien-contenu">Aller au contenu</a>
   ... navigation ...
   <main id="contenu-principal">...</main> */
```

---

## 17.8 Bonnes pratiques UI/UX en CSS

```css
/* 1. Zones de clic suffisamment grandes (minimum 44×44px) */
.bouton-icon {
  min-width: 44px;
  min-height: 44px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

/* 2. Curseur approprié */
button, [role="button"] { cursor: pointer; }
[disabled] { cursor: not-allowed; }
[readonly] { cursor: default; }
abbr[title] { cursor: help; }

/* 3. Sélection de texte */
/* Certains éléments ne devraient pas être sélectionnables */
button, label { user-select: none; }

/* 4. États des formulaires clairement distincts */
input:disabled { opacity: 0.5; background: #f5f5f5; }
input:read-only { background: #f9f9f9; border-style: dashed; }
input:required { border-left: 3px solid #e74c3c; }
```

---

## 📌 Résumé — Checklist Accessibilité CSS

| Élément | Standard |
|---------|----------|
| Contraste texte/fond | Minimum 4.5:1 (AA) |
| Focus visible | Toujours visible et contrasté |
| Taille du texte | Minimum 16px (corps) |
| Largeur de ligne | Maximum 70-75 caractères |
| Zones de clic | Minimum 44×44px |
| Animations | Respecter `prefers-reduced-motion` |
| Mode sombre | Respecter `prefers-color-scheme` |
| Erreurs | Ne pas indiquer UNIQUEMENT par la couleur |

## 🔗 Références

- [WebAIM — Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [MDN — Accessibilité CSS](https://developer.mozilla.org/fr/docs/Learn/Accessibility/CSS_and_JavaScript)
- [WCAG 2.1](https://www.w3.org/TR/WCAG21/)

---
*⬅️ [Module 16](../16-css-avance/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 18 — Écosystème CSS](../18-ecosysteme/README.md)*
