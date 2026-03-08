# Module 05 — Le Modèle de Boîte (Box Model)

> **Niveau :** Débutant  
> **Durée estimée :** 4 heures  
> **Prérequis :** Modules 01 à 04

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Comprendre et expliquer le Box Model
- Contrôler les marges, paddings, et bordures
- Calculer les dimensions réelles des éléments
- Éviter les erreurs classiques de dimensionnement

---

## 5.1 Comprendre le modèle de boîte

### Explication simple

En CSS, **chaque élément HTML est une boîte rectangulaire**. Le modèle de boîte (Box Model) décrit comment cette boîte est construite, de l'intérieur vers l'extérieur, en 4 couches concentriques.

Imaginez une lettre dans une enveloppe dans une boîte emballée avec du papier cadeau :
1. **La lettre** = le contenu (content)
2. **L'intérieur de l'enveloppe** = le rembourrage (padding)
3. **L'enveloppe** = la bordure (border)
4. **L'espace entre les boîtes** = la marge (margin)

### Schéma du Box Model

```
┌─────────────────────────────────────────────────────┐
│                      MARGIN                          │
│   ┌─────────────────────────────────────────────┐   │
│   │                  BORDER                      │   │
│   │   ┌─────────────────────────────────────┐   │   │
│   │   │              PADDING                │   │   │
│   │   │   ┌───────────────────────────┐     │   │   │
│   │   │   │                           │     │   │   │
│   │   │   │        CONTENT            │     │   │   │
│   │   │   │   (width × height)        │     │   │   │
│   │   │   │                           │     │   │   │
│   │   │   └───────────────────────────┘     │   │   │
│   │   │                                     │   │   │
│   │   └─────────────────────────────────────┘   │   │
│   │                                             │   │
│   └─────────────────────────────────────────────┘   │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 5.2 Le contenu (content)

Le contenu est la zone centrale où s'affiche le texte, les images, ou les éléments enfants.

```css
.boite {
  /* Largeur du contenu */
  width: 300px;

  /* Hauteur du contenu */
  height: 200px;

  /* Largeur maximale (utile pour le responsive) */
  max-width: 100%;

  /* Largeur minimale */
  min-width: 200px;

  /* Hauteur maximale */
  max-height: 500px;

  /* Hauteur minimale */
  min-height: 100px;
}
```

### Quand ne pas définir de hauteur fixe

**⚠️ Erreur courante des débutants :** Définir une hauteur fixe sur un élément qui contient du texte variable.

```css
/* ❌ Problématique : si le texte est long, il déborde */
.carte {
  height: 100px;
}

/* ✅ Meilleure approche : laisser la hauteur s'adapter au contenu */
.carte {
  min-height: 100px; /* Au moins 100px, mais peut grandir */
  padding: 20px;
}
```

---

## 5.3 Le rembourrage (padding)

Le padding est l'espace **entre le contenu et la bordure**. Il est à l'intérieur de l'élément — il hérite donc du fond de l'élément.

### Syntaxe

```css
/* ━━━ Syntaxe raccourcie ━━━ */

/* 1 valeur : tous les côtés identiques */
padding: 20px;
/* Résultat : haut=20px, droite=20px, bas=20px, gauche=20px */

/* 2 valeurs : haut/bas | gauche/droite */
padding: 10px 20px;
/* Résultat : haut=10px, droite=20px, bas=10px, gauche=20px */

/* 3 valeurs : haut | gauche/droite | bas */
padding: 10px 20px 15px;
/* Résultat : haut=10px, droite=20px, bas=15px, gauche=20px */

/* 4 valeurs : haut | droite | bas | gauche (sens des aiguilles d'une montre) */
padding: 10px 20px 15px 25px;
/* Résultat : haut=10px, droite=20px, bas=15px, gauche=25px */


/* ━━━ Propriétés individuelles ━━━ */
padding-top: 10px;
padding-right: 20px;
padding-bottom: 15px;
padding-left: 25px;
```

### Moyen mémo-technique pour l'ordre des valeurs

> **TR**ès **B**ien **L**u = **T**op **R**ight **B**ottom **L**eft

Ou encore : **TRBL** = **T**rouble (sens des aiguilles d'une montre à partir du haut)

### Exemples pratiques

```css
/* Bouton avec padding équilibré */
.btn {
  padding: 12px 24px; /* 12px en haut/bas, 24px à gauche/droite */
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

/* Carte avec espacement interne généreux */
.carte {
  padding: 24px; /* Espacement uniforme */
  background-color: white;
  border-radius: 8px;
}

/* Navigation avec padding asymétrique */
.nav-lien {
  padding: 16px 20px; /* Plus large horizontalement */
  color: white;
  text-decoration: none;
}
```

---

## 5.4 La bordure (border)

La bordure entoure le padding et le contenu.

### Syntaxe

```css
/* Raccourci : épaisseur | style | couleur */
border: 2px solid #333;

/* Propriétés individuelles */
border-width: 2px;
border-style: solid;
border-color: #333;

/* Par côté */
border-top: 3px solid #3498db;
border-right: 1px dashed #ccc;
border-bottom: 2px solid #2ecc71;
border-left: 4px solid #e74c3c;

/* Désactiver une bordure */
border: none;
border-bottom: none;
```

### Styles de bordure

```css
border-style: solid;    /* Ligne continue */
border-style: dashed;   /* Tirets */
border-style: dotted;   /* Points */
border-style: double;   /* Double ligne */
border-style: groove;   /* Effet 3D enfoncé */
border-style: ridge;    /* Effet 3D en relief */
border-style: inset;    /* Apparence 3D intérieure */
border-style: outset;   /* Apparence 3D extérieure */
border-style: none;     /* Pas de bordure */
border-style: hidden;   /* Invisible (pour les tableaux) */
```

### Coins arrondis (`border-radius`)

```css
/* Même rayon pour tous les coins */
border-radius: 8px;

/* Coins spécifiques : haut-gauche | haut-droite | bas-droite | bas-gauche */
border-radius: 8px 0 8px 0; /* Coins diagonaux arrondis */

/* Cercle parfait */
border-radius: 50%;

/* Forme "pilule" */
border-radius: 999px;
width: 200px;
height: 50px;

/* Ellipse */
border-radius: 50% / 30%;

/* Valeurs différentes : haut-gauche | haut-droite | bas-droite | bas-gauche */
border-radius: 10px 20px 30px 40px;
```

---

## 5.5 La marge (margin)

La marge est l'espace **extérieur** à l'élément — elle sépare l'élément de ses voisins.

### Syntaxe

```css
/* Raccourci (même logique que padding) */
margin: 20px;
margin: 10px 20px;
margin: 10px 20px 15px;
margin: 10px 20px 15px 25px;

/* Propriétés individuelles */
margin-top: 10px;
margin-right: 20px;
margin-bottom: 15px;
margin-left: 25px;
```

### `margin: auto` — Centrage

```css
/* Centrage horizontal d'un bloc */
.conteneur {
  width: 800px;
  margin: 0 auto; /* 0 pour haut/bas, auto pour gauche/droite */
}

/* Centrage avec marge haut/bas */
.conteneur {
  max-width: 800px;
  margin: 40px auto;
}
```

### Marges négatives

```css
/* Les marges peuvent être négatives ! */
.chevauchement {
  margin-top: -20px; /* L'élément remonte de 20px */
}
```

### ⚠️ La fusion des marges (Margin Collapse)

**C'est une des sources de confusion les plus courantes en CSS.**

Quand deux marges verticales (haut et bas) se rencontrent, elles ne s'additionnent pas — la plus grande des deux est retenue.

```html
<p class="premier">Premier paragraphe</p>
<p class="second">Deuxième paragraphe</p>
```

```css
.premier {
  margin-bottom: 30px; /* ← 30px */
}

.second {
  margin-top: 20px; /* ← 20px */
}

/* L'espace entre les deux paragraphes sera 30px (pas 50px !)
   Car la marge la plus grande "gagne". */
```

**Quand la fusion se produit :**
- Entre deux éléments frères (haut → bas)
- Entre un parent et son premier/dernier enfant (si pas de padding/border entre les deux)

**Comment éviter la fusion :**
```css
/* Méthode 1 : Utiliser padding au lieu de margin (si applicable) */
/* Méthode 2 : Ajouter un border ou padding au parent */
.parent {
  padding-top: 1px; /* Empêche la fusion avec l'enfant */
  /* ou */
  border-top: 1px solid transparent;
  /* ou */
  overflow: hidden;
}
/* Méthode 3 : Utiliser Flexbox ou Grid (la fusion n'existe pas avec ces layouts) */
```

---

## 5.6 `box-sizing` — La propriété la plus importante

### Le problème du `box-sizing: content-box` (défaut)

Par défaut, CSS calcule la taille totale d'un élément en **ajoutant** le padding et la bordure à la largeur définie.

```css
.boite {
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}

/* Taille réelle = 300 + 20*2 + 5*2 = 350px ! */
/* Pas 300px comme vous vous y attendiez */
```

### La solution : `box-sizing: border-box`

Avec `border-box`, le padding et la bordure sont **inclus** dans la largeur définie.

```css
.boite {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}

/* Taille réelle = 300px (exactement) */
/* Le contenu rétrécit pour accommoder le padding et la bordure */
```

### Application globale recommandée

```css
/* À placer au début de TOUS vos fichiers CSS */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### Tableau comparatif

| | `content-box` (défaut) | `border-box` (recommandé) |
|---|---|---|
| `width` inclut le padding ? | ❌ Non | ✅ Oui |
| `width` inclut la bordure ? | ❌ Non | ✅ Oui |
| Calcul de taille | Imprévisible | Intuitif |
| Usage | Héritage | Moderne |

---

## 5.7 Exemples pratiques complets

### Exemple 1 : Une carte de profil

```html
<div class="carte-profil">
  <img src="photo.jpg" alt="Photo de profil" class="photo">
  <div class="infos">
    <h2 class="nom">Marie Dupont</h2>
    <p class="role">Développeuse Front-end</p>
    <p class="bio">Passionnée par l'UI/UX et le CSS moderne.</p>
  </div>
</div>
```

```css
/* Réinitialisation Box Model */
*, *::before, *::after {
  box-sizing: border-box;
}

/* Carte principale */
.carte-profil {
  width: 320px;
  background-color: white;

  /* Bordure subtile */
  border: 1px solid #e0e0e0;

  /* Coins arrondis */
  border-radius: 12px;

  /* Ombre portée pour la profondeur */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);

  /* Pas de débordement (pour les coins arrondis sur l'image) */
  overflow: hidden;
}

/* Photo */
.photo {
  width: 100%;      /* Occupe toute la largeur de la carte */
  height: 200px;
  object-fit: cover; /* L'image remplit la zone sans se déformer */
  display: block;
}

/* Section des informations */
.infos {
  padding: 20px;    /* Espacement interne confortable */
}

/* Nom */
.nom {
  font-size: 20px;
  font-weight: 700;
  color: #1a1a2e;
  margin: 0 0 4px 0; /* Pas de marge haut, 4px bas */
}

/* Rôle */
.role {
  font-size: 14px;
  color: #3498db;
  font-weight: 500;
  margin: 0 0 12px 0;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* Biographie */
.bio {
  font-size: 14px;
  color: #666;
  line-height: 1.6;
  margin: 0;
}
```

### Exemple 2 : Calcul de dimensions

```css
/* Démonstration du calcul de taille */

/* Sans border-box (ÉVITER) */
.sans-border-box {
  /* box-sizing: content-box; ← défaut */
  width: 200px;
  padding: 20px;
  border: 5px solid blue;
  /* Taille occupée = 200 + 40 + 10 = 250px */
}

/* Avec border-box (RECOMMANDÉ) */
.avec-border-box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid green;
  /* Taille occupée = 200px exactement */
  /* Contenu interne = 200 - 40 - 10 = 150px */
}
```

---

## 📝 Exercices pratiques

### Exercice 5.1 — Comprendre le Box Model

Créez une boîte avec :
- Largeur de 300px, hauteur de 150px
- Padding de 20px
- Bordure de 3px solid
- Marge de 30px
- Activez `box-sizing: border-box`

Utilisez les DevTools pour vérifier le Box Model de votre élément.

### Exercice 5.2 — Centrage

Créez un conteneur centré de 700px de large avec :
- Fond blanc
- Padding de 40px
- Marges automatiques pour le centrage horizontal
- Marge de 40px en haut et en bas

### Exercice 5.3 — Grille de cartes

Créez 3 cartes côte à côte, chacune avec :
- Même largeur
- Même padding
- Bordures arrondies
- Ombres portées

---

## ✅ Corrigé — Exercice 5.1

```css
*, *::before, *::after {
  box-sizing: border-box; /* Appliqué globalement */
}

.ma-boite {
  width: 300px;
  height: 150px;
  padding: 20px;
  border: 3px solid #3498db;
  margin: 30px;
  background-color: #eaf4fb;
  color: #2c3e50;
}
```

**Vérification dans les DevTools :**
- Content : 254px × 104px (300 - 20*2 - 3*2 = 254px)
- Padding : 20px tous les côtés
- Border : 3px tous les côtés
- Margin : 30px tous les côtés
- **Taille totale avec marge = 300 + 30*2 = 360px**

---

## ❌ Erreurs fréquentes des débutants

### 1. Oublier `box-sizing: border-box`
```css
/* ❌ Les éléments sont plus larges que prévu */
.colonne {
  width: 50%;
  padding: 20px; /* Ajoute 40px à la largeur totale ! */
}

/* ✅ Correct */
* { box-sizing: border-box; }
.colonne {
  width: 50%;
  padding: 20px; /* Inclus dans les 50% */
}
```

### 2. Utiliser `margin: auto` sur les éléments inline
```css
/* ❌ Ne fonctionne pas : <span> est inline */
span { margin: 0 auto; }

/* ✅ Correct : convertir en block ou inline-block */
span {
  display: block; /* ou inline-block */
  margin: 0 auto;
}
```

### 3. Définir une hauteur fixe sans gérer le débordement
```css
/* ❌ Le texte déborde si trop long */
.boite { height: 100px; }

/* ✅ Gérer le débordement */
.boite {
  min-height: 100px;
  overflow: hidden; /* ou auto, scroll */
}
```

---

## 📌 Résumé du module 05

| Couche | Propriétés | Description |
|--------|-----------|-------------|
| Content | `width`, `height` | Zone du contenu |
| Padding | `padding` | Espace intérieur (hérite du fond) |
| Border | `border`, `border-radius` | Contour de l'élément |
| Margin | `margin` | Espace extérieur |
| Box-sizing | `box-sizing: border-box` | Inclut padding+border dans width/height |

---

## 🔗 Références

- [MDN — Le modèle de boîte](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/The_box_model)
- [MDN — box-sizing](https://developer.mozilla.org/fr/docs/Web/CSS/box-sizing)
- [CSS-Tricks — The CSS Box Model](https://css-tricks.com/the-css-box-model/)

---

*⬅️ [Module 04](../04-selecteurs/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 06 — Couleurs](../06-couleurs/README.md)*
