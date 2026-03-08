# Module 13 — Variables CSS (Custom Properties)

> **Niveau :** Avancé | **Durée estimée :** 3 heures

---

## 13.1 Qu'est-ce qu'une variable CSS ?

Une **variable CSS** (ou propriété personnalisée) est une valeur nommée que vous pouvez réutiliser partout dans votre feuille de style. Elles permettent de centraliser les valeurs importantes (couleurs, tailles, espacements) et de les modifier en un seul endroit.

### Analogie

Imaginez que la couleur principale de votre site est `#3498db`. Sans variables, si vous décidez de la changer, vous devez modifier chaque occurrence dans tous vos fichiers CSS. Avec une variable, vous la changez une seule fois.

---

## 13.2 Déclarer et utiliser des variables CSS

### Syntaxe

```css
/* Déclaration : commence par -- */
:root {
  --couleur-principale: #3498db;
}

/* Utilisation : fonction var() */
.bouton {
  background-color: var(--couleur-principale);
}
```

### Convention : déclarer dans `:root`

```css
/* :root cible l'élément <html> — portée globale */
:root {
  /* ─── Palette de couleurs ─── */
  --couleur-principale:    #3498db;
  --couleur-secondaire:    #2ecc71;
  --couleur-accent:        #e74c3c;
  --couleur-fond:          #f0f2f5;
  --couleur-fond-carte:    #ffffff;
  --couleur-texte:         #333333;
  --couleur-texte-doux:    #666666;
  --couleur-bordure:       #e0e0e0;

  /* ─── Typographie ─── */
  --police-principale:     'Inter', Arial, sans-serif;
  --police-titres:         'Playfair Display', Georgia, serif;
  --taille-base:           1rem;
  --taille-sm:             0.875rem;
  --taille-lg:             1.25rem;
  --taille-xl:             1.5rem;
  --taille-2xl:            2rem;
  --graisse-normal:        400;
  --graisse-bold:          700;
  --interligne:            1.6;

  /* ─── Espacements ─── */
  --espace-xs:   4px;
  --espace-sm:   8px;
  --espace-md:   16px;
  --espace-lg:   24px;
  --espace-xl:   32px;
  --espace-2xl:  48px;
  --espace-3xl:  64px;

  /* ─── Bordures ─── */
  --rayon-sm:    4px;
  --rayon-md:    8px;
  --rayon-lg:    12px;
  --rayon-xl:    16px;
  --rayon-pill:  9999px;

  /* ─── Ombres ─── */
  --ombre-sm:    0 1px 3px rgba(0, 0, 0, 0.1);
  --ombre-md:    0 4px 12px rgba(0, 0, 0, 0.1);
  --ombre-lg:    0 8px 30px rgba(0, 0, 0, 0.12);
  --ombre-xl:    0 20px 60px rgba(0, 0, 0, 0.15);

  /* ─── Transitions ─── */
  --transition-rapide:  all 0.15s ease;
  --transition-normal:  all 0.3s ease;
  --transition-lente:   all 0.5s ease;

  /* ─── Z-index ─── */
  --z-base:     0;
  --z-dropdown: 100;
  --z-modal:    200;
  --z-toast:    300;
}
```

---

## 13.3 Valeur de secours (fallback)

```css
/* Si --couleur-principale n'existe pas, utilise #3498db */
.element {
  color: var(--couleur-principale, #3498db);
}

/* Fallback en chaîne */
.element {
  color: var(--couleur-custom, var(--couleur-principale, #333));
}
```

---

## 13.4 La portée (scope) des variables

```css
/* Variable globale */
:root {
  --couleur: blue;
}

/* Variable locale (écrase la globale dans ce contexte) */
.composant-special {
  --couleur: red;
}

.composant-special p {
  color: var(--couleur); /* Utilise red */
}

p {
  color: var(--couleur); /* Utilise blue */
}
```

---

## 13.5 Variables CSS et JavaScript

```javascript
// Lire une variable CSS
const root = document.documentElement;
const couleur = getComputedStyle(root).getPropertyValue('--couleur-principale');

// Modifier une variable CSS dynamiquement
root.style.setProperty('--couleur-principale', '#e74c3c');
// Toute la page se met à jour instantanément !
```

---

## 13.6 Thème sombre / Thème clair

```css
/* ─── Thème clair (défaut) ─── */
:root {
  --fond:          #ffffff;
  --fond-secondaire: #f0f2f5;
  --texte:         #1a1a2e;
  --texte-doux:    #666;
  --bordure:       #e0e0e0;
  --ombre:         0 2px 10px rgba(0, 0, 0, 0.1);
}

/* ─── Thème sombre (automatique) ─── */
@media (prefers-color-scheme: dark) {
  :root {
    --fond:          #1a1a2e;
    --fond-secondaire: #16213e;
    --texte:         #e0e0e0;
    --texte-doux:    #aaa;
    --bordure:       #333;
    --ombre:         0 2px 10px rgba(0, 0, 0, 0.4);
  }
}

/* ─── Thème sombre (manuel via classe) ─── */
.theme-sombre {
  --fond:          #1a1a2e;
  --fond-secondaire: #16213e;
  --texte:         #e0e0e0;
  --texte-doux:    #aaa;
  --bordure:       #333;
}

/* Application */
body {
  background-color: var(--fond);
  color: var(--texte);
  transition: background-color 0.3s ease, color 0.3s ease;
}

.carte {
  background-color: var(--fond-secondaire);
  border: 1px solid var(--bordure);
  box-shadow: var(--ombre);
}
```

---

## 13.7 Variables calculées avec `calc()`

```css
:root {
  --espace-base: 8px;
}

.element {
  padding: calc(var(--espace-base) * 2);   /* 16px */
  margin: calc(var(--espace-base) * 3);    /* 24px */
  gap: calc(var(--espace-base) * 1.5);     /* 12px */
}
```

---

## 13.8 Exemple complet — Système de design

```css
/* design-system.css */

:root {
  /* Couleurs primaires */
  --bleu-50:  #eff6ff;
  --bleu-100: #dbeafe;
  --bleu-500: #3b82f6;
  --bleu-600: #2563eb;
  --bleu-700: #1d4ed8;

  /* Alias sémantiques */
  --couleur-action:       var(--bleu-500);
  --couleur-action-hover: var(--bleu-600);
  --couleur-action-fond:  var(--bleu-50);

  /* Système d'espacement en base 4 */
  --s1:  4px;
  --s2:  8px;
  --s3:  12px;
  --s4:  16px;
  --s5:  20px;
  --s6:  24px;
  --s8:  32px;
  --s10: 40px;
  --s12: 48px;
  --s16: 64px;
}

/* Bouton utilisant le système */
.btn-primary {
  background-color: var(--couleur-action);
  color: white;
  padding: var(--s3) var(--s6);
  border-radius: var(--rayon-md);
  border: none;
  cursor: pointer;
  font-size: var(--taille-base);
  font-weight: var(--graisse-bold);
  transition: var(--transition-rapide);
}

.btn-primary:hover {
  background-color: var(--couleur-action-hover);
  transform: translateY(-1px);
  box-shadow: var(--ombre-md);
}
```

---

## 📝 Exercices

**Exercice 13.1** — Créez un système de variables CSS complet pour un site.  
**Exercice 13.2** — Implémentez un bouton de bascule thème clair/sombre avec JavaScript.  
**Exercice 13.3** — Créez 3 variantes d'un composant carte en utilisant des variables locales.

---

## 📌 Résumé

| Concept | Syntaxe |
|---------|---------|
| Déclaration | `--ma-variable: valeur;` |
| Utilisation | `var(--ma-variable)` |
| Avec fallback | `var(--ma-variable, valeur-defaut)` |
| Portée globale | Déclarer dans `:root` |
| Portée locale | Déclarer dans un sélecteur |
| Via JS | `element.style.setProperty('--var', valeur)` |

## 🔗 Références

- [MDN — CSS Custom Properties](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)
- [web.dev — CSS Variables](https://web.dev/learn/css/color/)

---
*⬅️ [Module 12](../12-animations/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 14 — Architecture CSS](../14-architecture/README.md)*
