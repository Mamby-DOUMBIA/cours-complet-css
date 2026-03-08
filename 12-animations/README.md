# Module 12 — Animations et Transitions

> **Niveau :** Intermédiaire → Avancé | **Durée estimée :** 4 heures

---

## 12.1 Les transitions CSS

Une **transition** anime le passage d'un état à un autre progressivement.

```css
/* Raccourci : propriété | durée | easing | délai */
.bouton {
  background-color: #3498db;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.bouton:hover {
  background-color: #2980b9;
  transform: translateY(-2px);
}

/* Propriétés individuelles */
.element {
  transition-property: all;
  transition-duration: 0.3s;
  transition-timing-function: ease-in-out;
  transition-delay: 0s;
}
```

### Fonctions de temporisation

```css
transition-timing-function: linear;
transition-timing-function: ease;         /* Défaut */
transition-timing-function: ease-in;
transition-timing-function: ease-out;
transition-timing-function: ease-in-out;
transition-timing-function: cubic-bezier(0.25, 0.46, 0.45, 0.94);
```

---

## 12.2 Les transformations CSS (`transform`)

```css
/* Translation */
transform: translateX(20px);
transform: translateY(-10px);
transform: translate(20px, -10px);

/* Rotation */
transform: rotate(45deg);

/* Échelle */
transform: scale(1.2);
transform: scale(1.2, 0.8);

/* Inclinaison */
transform: skewX(15deg);

/* Combinaison (l'ordre est important !) */
transform: translateY(-4px) scale(1.02) rotate(2deg);

/* Point d'origine */
transform-origin: center center;
transform-origin: top left;

/* 3D */
transform: rotateY(45deg);
transform: perspective(600px) rotateY(30deg);
```

---

## 12.3 Les animations CSS (`@keyframes`)

```css
/* ─── Définition ─── */
@keyframes apparition {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulsation {
  0%   { transform: scale(1); box-shadow: 0 0 0 0 rgba(52,152,219,0.4); }
  70%  { transform: scale(1.05); box-shadow: 0 0 0 10px rgba(52,152,219,0); }
  100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(52,152,219,0); }
}

@keyframes rotation {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

@keyframes glissement-gauche {
  from { opacity: 0; transform: translateX(-30px); }
  to   { opacity: 1; transform: translateX(0); }
}

/* ─── Application ─── */
.carte {
  animation: apparition 0.5s ease-out forwards;
}

.icone-chargement {
  animation: rotation 1s linear infinite;
}

.bouton-pulse {
  animation: pulsation 2s ease-out infinite;
}

/* ─── Propriétés d'animation ─── */
.element {
  animation-name: apparition;
  animation-duration: 0.5s;
  animation-timing-function: ease-out;
  animation-delay: 0.2s;
  animation-iteration-count: 1;      /* ou : infinite */
  animation-direction: normal;        /* reverse | alternate */
  animation-fill-mode: forwards;      /* none | forwards | backwards | both */
  animation-play-state: running;      /* paused */
}

/* Raccourci */
.element {
  animation: apparition 0.5s ease-out 0.2s 1 normal forwards;
}
```

---

## 12.4 Animations en cascade (délais)

```css
/* Faire apparaître des éléments un par un */
.liste-item { animation: apparition 0.4s ease-out forwards; opacity: 0; }
.liste-item:nth-child(1) { animation-delay: 0.0s; }
.liste-item:nth-child(2) { animation-delay: 0.1s; }
.liste-item:nth-child(3) { animation-delay: 0.2s; }
.liste-item:nth-child(4) { animation-delay: 0.3s; }
```

---

## 12.5 Performance des animations

```css
/* Propriétés qui ne déclenchent PAS de reflow (performances optimales) */
/* ✅ Utiliser de préférence : */
transform: translateX();  /* Translation */
transform: scale();       /* Mise à l'échelle */
transform: rotate();      /* Rotation */
opacity: ;                /* Opacité */

/* ❌ Éviter d'animer (déclenche reflow) : */
width: ;
height: ;
margin: ;
padding: ;
top: ; left: ;

/* Indication au navigateur de préparer le GPU */
.element-anime {
  will-change: transform, opacity;
  /* ⚠️ Utiliser avec parcimonie ! */
}

/* Respecter les préférences de l'utilisateur */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 12.6 Exemple complet — Page animée

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Animations CSS</title>
  <link rel="stylesheet" href="animations-demo.css">
</head>
<body>
  <section class="hero">
    <h1 class="hero-titre">Bienvenue !</h1>
    <p class="hero-sous-titre">Découvrez la puissance des animations CSS</p>
    <a href="#" class="hero-bouton">Commencer →</a>
  </section>

  <section class="cartes-section">
    <div class="carte animer">🎨 Design</div>
    <div class="carte animer">⚡ Performance</div>
    <div class="carte animer">📱 Responsive</div>
  </section>
</body>
</html>
```

```css
/* animations-demo.css */
@keyframes apparition-haut {
  from { opacity: 0; transform: translateY(-20px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes apparition-bas {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body { font-family: 'Segoe UI', Arial, sans-serif; }

.hero {
  background: linear-gradient(135deg, #1a252f, #2c3e50);
  color: white;
  text-align: center;
  padding: 80px 20px;
}

.hero-titre {
  font-size: 3rem;
  animation: apparition-haut 0.7s ease-out forwards;
}

.hero-sous-titre {
  font-size: 1.2rem;
  opacity: 0.8;
  margin: 16px 0 32px;
  animation: apparition-haut 0.7s ease-out 0.15s forwards;
  opacity: 0;
}

.hero-bouton {
  display: inline-block;
  background: #3498db;
  color: white;
  padding: 14px 32px;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 600;
  animation: apparition-bas 0.7s ease-out 0.3s forwards;
  opacity: 0;
  transition: transform 0.2s ease, box-shadow 0.2s ease, background-color 0.2s;
}

.hero-bouton:hover {
  background: #2980b9;
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(52,152,219,0.4);
}

.cartes-section {
  display: flex;
  gap: 20px;
  padding: 40px;
  justify-content: center;
  flex-wrap: wrap;
}

.carte {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  font-size: 1.2rem;
  font-weight: 600;
  opacity: 0;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.carte.animer { animation: apparition-bas 0.5s ease-out forwards; }
.carte:nth-child(1) { animation-delay: 0.4s; }
.carte:nth-child(2) { animation-delay: 0.55s; }
.carte:nth-child(3) { animation-delay: 0.7s; }

.carte:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 30px rgba(0,0,0,0.15);
}
```

---

## 📝 Exercices

**Exercice 12.1** — Créez un bouton qui pulse à l'infini au survol.  
**Exercice 12.2** — Créez un menu hamburger avec une transition d'ouverture fluide.  
**Exercice 12.3** — Créez une page de chargement (spinner animé).

---

## 📌 Résumé

| Technique | Usage | Propriété clé |
|-----------|-------|---------------|
| Transition | Changement d'état | `transition` |
| Transform | Déplacement/rotation/échelle | `transform` |
| Animation | Séquence complexe | `@keyframes` + `animation` |

## 🔗 Références

- [MDN — Transitions CSS](https://developer.mozilla.org/fr/docs/Web/CSS/transition)
- [MDN — Animations CSS](https://developer.mozilla.org/fr/docs/Web/CSS/animation)
- [Easing Functions](https://easings.net/fr)

---
*⬅️ [Module 11](../11-responsive/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 13 — Variables CSS](../13-variables/README.md)*
