# Module 06 — Couleurs et Arrière-plans

> **Niveau :** Débutant  
> **Durée estimée :** 3 heures  
> **Prérequis :** Modules 01 à 05

---

## 6.1 Les formats de couleur CSS

### Noms de couleur
```css
color: red;
color: blue;
color: coral;
color: darkslategray;
/* 140+ noms disponibles */
```

### Hexadécimal (le plus courant)
```css
color: #ff0000;    /* Rouge pur */
color: #3498db;    /* Bleu */
color: #2c3e50;    /* Bleu foncé */
color: #fff;       /* Blanc (raccourci #ffffff) */
color: #000;       /* Noir (raccourci #000000) */
/* Format : #RRGGBB — RR=rouge, GG=vert, BB=bleu, valeurs 00-ff */
```

### RGB et RGBA
```css
color: rgb(52, 152, 219);            /* Rouge, Vert, Bleu (0-255) */
color: rgba(52, 152, 219, 0.8);      /* + Alpha (0=transparent, 1=opaque) */
background-color: rgba(0, 0, 0, 0.5); /* Noir semi-transparent */
```

### HSL et HSLA (très lisible)
```css
/* hsl(teinte, saturation, luminosité) */
color: hsl(210, 70%, 53%);           /* Bleu */
color: hsl(0, 100%, 50%);            /* Rouge pur */
color: hsl(120, 100%, 25%);          /* Vert foncé */
color: hsla(210, 70%, 53%, 0.8);     /* Avec transparence */
/* Teinte : 0-360° (rouge=0, vert=120, bleu=240) */
```

### oklch (CSS moderne — recommandé)
```css
/* Perceptuellement uniforme — luminosité cohérente */
color: oklch(0.65 0.15 220);  /* Bleu perceptuellement équilibré */
```

---

## 6.2 La propriété `color`

```css
p { color: #333; }
a { color: #3498db; }
a:hover { color: #1a6694; }
.texte-erreur { color: #e74c3c; }
.texte-succes { color: #27ae60; }
```

---

## 6.3 La propriété `background-color`

```css
body { background-color: #f5f5f5; }
.carte { background-color: white; }
.alerte { background-color: rgba(231, 76, 60, 0.1); }
header { background-color: #2c3e50; }
```

---

## 6.4 La propriété `background-image`

```css
.hero {
  background-image: url('images/photo-hero.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
}
```

---

## 6.5 Les gradients

### linear-gradient
```css
/* De gauche à droite */
background: linear-gradient(to right, #3498db, #9b59b6);

/* Angle */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Plusieurs couleurs */
background: linear-gradient(to right, #e74c3c, #f39c12, #2ecc71);

/* Avec arrêts précis */
background: linear-gradient(to bottom, #fff 0%, #fff 50%, #3498db 50%, #3498db 100%);
```

### radial-gradient
```css
background: radial-gradient(circle, #3498db, #1a252f);
background: radial-gradient(ellipse at top, #3498db, transparent);
```

### conic-gradient
```css
/* Graphique en secteurs */
background: conic-gradient(#e74c3c 0% 30%, #3498db 30% 60%, #2ecc71 60% 100%);
```

---

## 6.6 Propriétés background avancées

```css
.section {
  background-image: url('pattern.png');
  background-repeat: repeat;            /* tile */
  background-repeat: no-repeat;
  background-repeat: repeat-x;          /* Uniquement horizontalement */
  background-position: top left;
  background-position: center center;
  background-position: 50% 50%;
  background-size: auto;
  background-size: cover;               /* Couvre toute la zone */
  background-size: contain;             /* Entier visible */
  background-size: 100px 50px;
  background-attachment: fixed;         /* Effet parallaxe */
}

/* Raccourci */
.hero {
  background: url('hero.jpg') no-repeat center center / cover;
}

/* Superposition : gradient sur image */
.hero-avec-overlay {
  background-image:
    linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
    url('hero.jpg');
  background-size: cover;
  background-position: center;
}
```

---

## 6.7 Opacité et transparence

```css
/* Opacité de l'élément entier (contenu inclus) */
.element { opacity: 0.5; }

/* Transparence uniquement sur la couleur */
.fond-transparent { background-color: rgba(52, 152, 219, 0.3); }
```

---

## 📝 Exercice 6.1 — Palette de couleurs

Créez une page affichant une palette de 6 couleurs avec gradients.

## 📌 Résumé

| Format | Exemple | Usage |
|--------|---------|-------|
| Nom | `red` | Débogage rapide |
| Hex | `#3498db` | Standard courant |
| RGB/RGBA | `rgba(52,152,219,0.8)` | Transparence |
| HSL | `hsl(210,70%,53%)` | Variantes faciles |

## 🔗 Références
- [MDN — Couleurs CSS](https://developer.mozilla.org/fr/docs/Web/CSS/color_value)
- [Coolors — Générateur de palettes](https://coolors.co/)

---
*⬅️ [Module 05](../05-box-model/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 07 — Typographie](../07-typographie/README.md)*
