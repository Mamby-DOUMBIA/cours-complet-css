# Module 08 — Mise en page CSS

> **Niveau :** Intermédiaire  
> **Durée estimée :** 4 heures  
> **Prérequis :** Modules 01 à 07

---

## 8.1 La propriété `display`

### Éléments block et inline

```css
/* Block : prend toute la largeur, commence sur une nouvelle ligne */
div, p, h1, section, article, header, footer { display: block; }

/* Inline : largeur du contenu, ne crée pas de saut de ligne */
span, a, strong, em, img { display: inline; }

/* inline-block : comme inline mais accepte width/height/padding vertical */
.bouton { display: inline-block; padding: 8px 16px; }

/* Cacher un élément (ne prend pas de place) */
.cache { display: none; }

/* Cacher visuellement mais garder la place */
.invisible { visibility: hidden; }
```

---

## 8.2 La propriété `position`

```css
/* static : flux normal de la page (défaut) */
.normale { position: static; }

/* relative : décalée par rapport à sa position normale */
.relative {
  position: relative;
  top: 10px;    /* Se déplace de 10px vers le bas */
  left: 20px;   /* Se déplace de 20px vers la droite */
  /* Conserve son espace dans le flux ! */
}

/* absolute : positionnée par rapport à son ancêtre positionné le plus proche */
.parent { position: relative; } /* Crée un contexte de positionnement */
.enfant-absolu {
  position: absolute;
  top: 0;
  right: 0;
  /* Ne conserve PAS son espace dans le flux */
}

/* fixed : positionnée par rapport au viewport */
.navbar-fixe {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
}

/* sticky : mélange de relative et fixed */
.titre-section {
  position: sticky;
  top: 0; /* Colle en haut quand on défile jusqu'à lui */
  background: white;
  z-index: 10;
}
```

### Le `z-index`

```css
/* Contrôle l'ordre d'empilement des éléments positionnés */
.arriere-plan { z-index: 0; }
.contenu      { z-index: 10; }
.modal        { z-index: 100; }
.notification { z-index: 1000; }
/* Un z-index fonctionne UNIQUEMENT si position n'est pas static */
```

---

## 8.3 La propriété `overflow`

```css
.boite {
  overflow: visible; /* Défaut : le contenu déborde */
  overflow: hidden;  /* Coupe le contenu qui dépasse */
  overflow: scroll;  /* Barre de défilement toujours visible */
  overflow: auto;    /* Barre de défilement si nécessaire (recommandé) */

  overflow-x: hidden; /* Uniquement horizontal */
  overflow-y: auto;   /* Uniquement vertical */
}
```

---

## 8.4 Les flottants (héritage historique)

> **Note :** Les flottants sont une ancienne technique. Aujourd'hui, utilisez Flexbox ou Grid. Connaitre les flottants reste utile pour lire du code legacy.

```css
/* Float entourer une image de texte */
.image-flottante {
  float: left;
  margin: 0 20px 10px 0;
}

/* Dégager le flottant */
.conteneur::after {
  content: "";
  display: block;
  clear: both;
}
```

---

## 📝 Exercice 8.1 — Positionnement

Créez une carte avec :
- Un badge "Nouveau" positionné en absolute dans le coin supérieur droit
- Une image avec un overlay de gradient
- Un titre sur l'overlay

## 📌 Résumé

| Valeur position | Flux | Référence |
|-----------------|------|-----------|
| `static` | Dans le flux | N/A |
| `relative` | Dans le flux (conserve la place) | Sa position normale |
| `absolute` | Hors du flux | Ancêtre positionné |
| `fixed` | Hors du flux | Viewport |
| `sticky` | Dans le flux → Fixed au scroll | Viewport au scroll |

## 🔗 Références
- [MDN — display](https://developer.mozilla.org/fr/docs/Web/CSS/display)
- [MDN — position](https://developer.mozilla.org/fr/docs/Web/CSS/position)

---
*⬅️ [Module 07](../07-typographie/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 09 — Flexbox](../09-flexbox/README.md)*
