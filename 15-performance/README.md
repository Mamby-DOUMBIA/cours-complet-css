# Module 15 — Performance CSS

> **Niveau :** Avancé | **Durée estimée :** 3 heures

---

## 15.1 Le chemin de rendu critique

Le navigateur suit ces étapes pour afficher une page :

```
HTML → DOM ─┐
            ├→ Render Tree → Layout → Paint → Composite
CSS → CSSOM ─┘
```

Le CSS est **bloquant** : le navigateur ne peut pas afficher la page avant d'avoir téléchargé et analysé toutes les feuilles de style liées dans le `<head>`. C'est pourquoi optimiser le CSS est crucial.

---

## 15.2 Charger le CSS efficacement

```html
<!-- ✅ CSS critique inline dans le <head> (rendu immédiat) -->
<style>
  /* Styles essentiels pour le premier écran visible */
  body { margin: 0; font-family: Arial, sans-serif; }
  header { background: #2c3e50; height: 60px; }
</style>

<!-- ✅ CSS non critique chargé en asynchrone -->
<link rel="preload" href="styles.css" as="style" onload="this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="styles.css"></noscript>

<!-- ✅ Préconnexion aux serveurs de polices -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

---

## 15.3 Sélecteurs performants

```css
/* ❌ Sélecteurs trop généraux ou trop profonds */
* { box-sizing: border-box; }           /* OK pour le reset, à éviter ailleurs */
div div div p span { color: red; }      /* Trop imbriqué */
[class^="icon-"] { display: inline; }  /* Sélecteur d'attribut lent */

/* ✅ Sélecteurs simples et directs */
.texte-rouge { color: red; }
.icone { display: inline; }
```

---

## 15.4 Propriétés qui déclenchent reflow vs. repaint

```css
/* ❌ Déclenche reflow (recalcul de tout le layout) — LENT */
/* Éviter d'animer ces propriétés */
width:    ;
height:   ;
margin:   ;
padding:  ;
top:      ;
left:     ;
font-size:;

/* ✅ Déclenche seulement repaint — MOYEN */
color:            ;
background-color: ;
border-color:     ;
outline:          ;

/* ✅ Aucun reflow ni repaint — RAPIDE (GPU) */
transform:  ;   /* translateX, scale, rotate */
opacity:    ;
filter:     ;

/* Toujours animer transform et opacity quand possible */
.box:hover {
  /* ❌ Lent */
  /* margin-top: -10px; */

  /* ✅ Rapide */
  transform: translateY(-10px);
}
```

---

## 15.5 Minification et optimisation

```css
/* Avant minification */
.bouton {
  background-color: #3498db;
  color: white;
  padding: 12px 24px;
  border-radius: 6px;
}

/* Après minification (pour la production) */
.bouton{background-color:#3498db;color:#fff;padding:12px 24px;border-radius:6px}
```

**Outils de minification :**
- [cssnano](https://cssnano.co/) — via PostCSS
- [clean-css](https://github.com/clean-css/clean-css)
- Vite / Webpack — minification automatique en production

---

## 15.6 Supprimer le CSS inutilisé (PurgeCSS)

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    require('@fullhuman/postcss-purgecss')({
      content: ['./src/**/*.html', './src/**/*.js'],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || []
    })
  ]
}
```

---

## 15.7 Bonnes pratiques de performance

```css
/* 1. Utiliser will-change avec parcimonie */
.element-anime {
  will-change: transform; /* Avertit le navigateur AVANT l'animation */
}
/* Supprimer après l'animation avec JavaScript */

/* 2. Éviter les reflows dans les animations */
@keyframes glissement {
  from { transform: translateX(-100%); } /* ✅ */
  to   { transform: translateX(0); }     /* ✅ */
}

/* 3. Contenir les éléments complexes */
.widget-lourd {
  contain: layout style; /* Isole les calculs de layout */
}

/* 4. Utiliser content-visibility pour le rendu différé */
.section-bas-de-page {
  content-visibility: auto;
  contain-intrinsic-size: 0 500px; /* Taille approximative */
}
```

---

## 📌 Résumé Performance

| Action | Impact |
|--------|--------|
| Animer `transform` et `opacity` | ⭐⭐⭐ Très élevé |
| CSS critique inline | ⭐⭐⭐ Très élevé |
| Minification | ⭐⭐ Élevé |
| PurgeCSS | ⭐⭐⭐ Très élevé |
| Préchargement des polices | ⭐⭐ Élevé |
| `content-visibility` | ⭐⭐ Élevé |

## 🔗 Références

- [web.dev — CSS Performance](https://web.dev/performance/)
- [MDN — will-change](https://developer.mozilla.org/fr/docs/Web/CSS/will-change)
- [PurgeCSS](https://purgecss.com/)

---
*⬅️ [Module 14](../14-architecture/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 16 — CSS Avancé](../16-css-avance/README.md)*
