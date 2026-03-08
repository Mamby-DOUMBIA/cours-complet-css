# Module 07 — Typographie Web

> **Niveau :** Débutant  
> **Durée estimée :** 3 heures  
> **Prérequis :** Modules 01 à 06

---

## 7.1 La propriété `font-family`

### Piles de polices (font stacks)

```css
/* Toujours fournir des polices de secours */
body {
  font-family: 'Arial', Helvetica, sans-serif;
}

h1, h2, h3 {
  font-family: 'Georgia', 'Times New Roman', serif;
}

code, pre {
  font-family: 'Courier New', Courier, monospace;
}
```

### Catégories de polices

| Catégorie | Description | Exemples |
|-----------|-------------|----------|
| `serif` | Avec empattements | Georgia, Times New Roman |
| `sans-serif` | Sans empattements | Arial, Helvetica, Verdana |
| `monospace` | Largeur fixe | Courier New, Consolas |
| `cursive` | Manuscrite | Comic Sans, Dancing Script |
| `fantasy` | Décorative | Impact |

---

## 7.2 La propriété `font-size`

```css
/* Unités absolues */
p { font-size: 16px; }   /* Pixels — standard */
p { font-size: 12pt; }   /* Points — pour l'impression */

/* Unités relatives */
p { font-size: 1rem; }   /* Relatif à <html> (recommandé) */
p { font-size: 1.2em; }  /* Relatif au parent */
p { font-size: 100%; }   /* Identique à 1em */

/* Mots-clés */
p { font-size: small; }
p { font-size: medium; }  /* Défaut navigateur ≈ 16px */
p { font-size: large; }

/* Échelle typographique classique */
h1 { font-size: 2.5rem; }   /* 40px */
h2 { font-size: 2rem; }     /* 32px */
h3 { font-size: 1.5rem; }   /* 24px */
h4 { font-size: 1.25rem; }  /* 20px */
h5 { font-size: 1rem; }     /* 16px */
h6 { font-size: 0.875rem; } /* 14px */
body { font-size: 1rem; }   /* 16px */
small { font-size: 0.75rem; } /* 12px */
```

---

## 7.3 La propriété `font-weight`

```css
p { font-weight: normal; }   /* Équivalent à 400 */
p { font-weight: bold; }     /* Équivalent à 700 */

/* Valeurs numériques (100 à 900, par 100) */
p { font-weight: 100; } /* Thin */
p { font-weight: 300; } /* Light */
p { font-weight: 400; } /* Regular */
p { font-weight: 500; } /* Medium */
p { font-weight: 600; } /* SemiBold */
p { font-weight: 700; } /* Bold */
p { font-weight: 900; } /* Black */
```

---

## 7.4 `line-height` — Interligne

```css
/* ❌ Avec unité — se comporte mal à l'héritage */
p { line-height: 24px; }

/* ✅ Sans unité — recommandé (multiplicateur) */
p { line-height: 1.6; } /* 1.6 × la taille de police */

/* Pour les titres : interligne plus resserré */
h1 { line-height: 1.2; }
h2 { line-height: 1.3; }

/* Pour les corps de texte : interligne plus ouvert */
p  { line-height: 1.6; }
```

---

## 7.5 Propriétés de texte

```css
/* Alignement */
text-align: left;      /* Défaut */
text-align: center;
text-align: right;
text-align: justify;   /* Justifié (attention à la lisibilité) */

/* Décoration */
text-decoration: none;           /* Supprime le soulignement */
text-decoration: underline;
text-decoration: line-through;   /* Barré */
text-decoration: overline;

/* Transformation */
text-transform: none;
text-transform: uppercase;   /* TOUT EN MAJUSCULES */
text-transform: lowercase;   /* tout en minuscules */
text-transform: capitalize;  /* Première Lettre En Majuscule */

/* Espacement */
letter-spacing: 0.05em;  /* Entre les lettres */
word-spacing: 0.1em;     /* Entre les mots */

/* Retrait */
text-indent: 2em;        /* Retrait première ligne */

/* Troncature avec ellipsis */
.nom {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 200px;
}
```

---

## 7.6 Google Fonts — Polices personnalisées

### Méthode 1 : Via le `<link>` dans le HTML

```html
<head>
  <!-- Charger depuis Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
</head>
```

```css
body {
  font-family: 'Inter', sans-serif;
}

h1, h2, h3 {
  font-family: 'Playfair Display', serif;
}
```

### Méthode 2 : Via `@import` dans le CSS

```css
/* Au début du fichier CSS */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');

body {
  font-family: 'Inter', sans-serif;
}
```

### Méthode 3 : `@font-face` (polices locales)

```css
@font-face {
  font-family: 'MaPolice';
  src: url('fonts/ma-police.woff2') format('woff2'),
       url('fonts/ma-police.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap; /* Affiche le texte pendant le chargement */
}

body {
  font-family: 'MaPolice', sans-serif;
}
```

---

## 7.7 Exemple : Typographie complète

```css
/* ─── Typographie système professionnelle ─── */

:root {
  /* Polices */
  --police-principale: 'Inter', 'Segoe UI', Arial, sans-serif;
  --police-titres: 'Playfair Display', Georgia, serif;
  --police-code: 'Fira Code', 'Courier New', monospace;

  /* Échelle typographique */
  --taille-base: 1rem;          /* 16px */
  --taille-sm: 0.875rem;        /* 14px */
  --taille-lg: 1.125rem;        /* 18px */
  --taille-xl: 1.25rem;         /* 20px */
  --taille-2xl: 1.5rem;         /* 24px */
  --taille-3xl: 1.875rem;       /* 30px */
  --taille-4xl: 2.25rem;        /* 36px */

  /* Graisses */
  --graisse-normal: 400;
  --graisse-medium: 500;
  --graisse-semibold: 600;
  --graisse-bold: 700;

  /* Interlignes */
  --interligne-serre: 1.2;
  --interligne-normal: 1.6;
  --interligne-ouvert: 1.8;
}

/* Application */
body {
  font-family: var(--police-principale);
  font-size: var(--taille-base);
  line-height: var(--interligne-normal);
  color: #333;
}

h1, h2, h3, h4 {
  font-family: var(--police-titres);
  line-height: var(--interligne-serre);
  font-weight: var(--graisse-bold);
  color: #1a1a2e;
}

h1 { font-size: var(--taille-4xl); }
h2 { font-size: var(--taille-3xl); }
h3 { font-size: var(--taille-2xl); }
h4 { font-size: var(--taille-xl); }

p {
  font-size: var(--taille-base);
  line-height: var(--interligne-normal);
  margin-bottom: 1.25em;
}

code, pre {
  font-family: var(--police-code);
  font-size: var(--taille-sm);
}
```

---

## 📝 Exercice 7.1 — Page typographique

Créez une page article avec :
- Titre en serif (Google Font "Playfair Display")
- Corps de texte en sans-serif (Google Font "Inter")
- Différentes tailles et graisses

## 📌 Résumé

| Propriété | Valeurs courantes |
|-----------|------------------|
| `font-family` | Pile de polices avec fallback |
| `font-size` | `rem` pour les tailles (accessibilité) |
| `font-weight` | 400 (normal), 600 (semi-bold), 700 (bold) |
| `line-height` | 1.2-1.4 (titres), 1.5-1.8 (texte) |
| `text-align` | left, center, right, justify |

## 🔗 Références
- [Google Fonts](https://fonts.google.com/)
- [MDN — Typographie Web](https://developer.mozilla.org/fr/docs/Learn/CSS/Styling_text)
- [web.dev — Web Typography](https://web.dev/learn/css/typography/)

---
*⬅️ [Module 06](../06-couleurs/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 08 — Mise en page](../08-mise-en-page/README.md)*
