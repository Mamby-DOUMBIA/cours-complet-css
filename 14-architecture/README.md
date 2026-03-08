# Module 14 — Architecture CSS

> **Niveau :** Avancé | **Durée estimée :** 4 heures

---

## 14.1 Pourquoi l'architecture CSS est-elle importante ?

Sur un petit projet (une page ou deux), l'organisation du CSS importe peu. Mais dès qu'un projet grandit — plusieurs pages, plusieurs développeurs, des mois de maintenance — un CSS sans architecture devient rapidement incontrôlable : conflits de styles, règles dupliquées, `!important` partout, et personne n'ose toucher au code de peur de tout casser.

Une bonne architecture CSS garantit :
- **Maintenabilité** : modifier un composant sans effets secondaires
- **Scalabilité** : le code reste organisé même en grossissant
- **Lisibilité** : n'importe quel développeur comprend la structure
- **Performance** : moins de CSS inutile, moins de conflits

---

## 14.2 Organisation des fichiers CSS

### Structure recommandée (Architecture 7-1)

L'architecture **7-1** organise le CSS en 7 dossiers thématiques et 1 fichier principal :

```
styles/
│
├── base/
│   ├── _reset.css          ← Réinitialisation CSS
│   ├── _typographie.css    ← Styles typographiques globaux
│   └── _variables.css      ← Variables CSS (custom properties)
│
├── composants/
│   ├── _boutons.css        ← Styles des boutons
│   ├── _cartes.css         ← Styles des cartes
│   ├── _formulaires.css    ← Styles des formulaires
│   ├── _navigation.css     ← Styles de la navigation
│   └── _modal.css          ← Styles des modales
│
├── disposition/
│   ├── _grille.css         ← Système de grille
│   ├── _header.css
│   ├── _footer.css
│   └── _sidebar.css
│
├── pages/
│   ├── _accueil.css
│   ├── _blog.css
│   └── _contact.css
│
├── themes/
│   ├── _theme-clair.css
│   └── _theme-sombre.css
│
├── abstracts/
│   ├── _mixins.css         ← (Si SCSS)
│   └── _fonctions.css
│
├── vendors/                ← CSS de bibliothèques tierces
│
└── main.css                ← Fichier principal (importe tout)
```

### Fichier `main.css`

```css
/* main.css — Point d'entrée unique */

/* 1. Base */
@import './base/_variables.css';
@import './base/_reset.css';
@import './base/_typographie.css';

/* 2. Disposition */
@import './disposition/_grille.css';
@import './disposition/_header.css';
@import './disposition/_footer.css';

/* 3. Composants */
@import './composants/_boutons.css';
@import './composants/_cartes.css';
@import './composants/_formulaires.css';
@import './composants/_navigation.css';

/* 4. Pages */
@import './pages/_accueil.css';
@import './pages/_blog.css';
```

---

## 14.3 La méthodologie BEM

**BEM** signifie **Block Element Modifier** (Bloc Élément Modificateur). C'est la convention de nommage CSS la plus utilisée dans le monde professionnel.

### Les trois concepts de BEM

**Block (Bloc)** : Un composant indépendant et réutilisable.
```
.carte
.bouton
.navigation
.formulaire
```

**Element (Élément)** : Une partie du bloc, qui n'a pas de sens sans lui. Séparé par `__` (double underscore).
```
.carte__image
.carte__titre
.carte__description
.carte__pied
.bouton__icone
.navigation__liste
.navigation__element
.navigation__lien
```

**Modifier (Modificateur)** : Une variation ou un état du bloc ou élément. Séparé par `--` (double tiret).
```
.carte--vedette
.carte--horizontale
.bouton--principal
.bouton--petit
.bouton--desactive
.navigation__lien--actif
```

### Exemple BEM complet

```html
<!-- HTML avec nommage BEM -->
<div class="carte carte--vedette">
  <img class="carte__image" src="photo.jpg" alt="">
  <div class="carte__corps">
    <span class="carte__categorie">CSS</span>
    <h2 class="carte__titre">Apprendre Flexbox</h2>
    <p class="carte__description">Un guide complet pour maîtriser Flexbox.</p>
  </div>
  <div class="carte__pied">
    <span class="carte__auteur">Marie Dupont</span>
    <a class="bouton bouton--petit" href="#">Lire →</a>
  </div>
</div>
```

```css
/* CSS avec BEM */

/* ─── Block ─── */
.carte {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

/* ─── Modifier du Block ─── */
.carte--vedette {
  border: 2px solid #3498db;
  box-shadow: 0 4px 20px rgba(52,152,219,0.2);
}

.carte--horizontale {
  display: flex;
  flex-direction: row;
}

/* ─── Elements ─── */
.carte__image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  display: block;
}

.carte--horizontale .carte__image {
  width: 200px;
  height: auto;
  flex-shrink: 0;
}

.carte__corps {
  padding: 20px;
  flex: 1;
}

.carte__categorie {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #3498db;
}

.carte__titre {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1a1a2e;
  margin: 8px 0;
  line-height: 1.3;
}

.carte__description {
  font-size: 0.875rem;
  color: #666;
  line-height: 1.6;
  margin: 0;
}

.carte__pied {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 20px;
  border-top: 1px solid #f0f0f0;
}

.carte__auteur {
  font-size: 0.8rem;
  color: #999;
}

/* ─── Block : Bouton ─── */
.bouton {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 0.875rem;
  font-weight: 600;
  cursor: pointer;
  text-decoration: none;
  transition: background-color 0.2s, transform 0.1s;
}

.bouton:hover { background-color: #2980b9; transform: translateY(-1px); }
.bouton:active { transform: translateY(0); }

.bouton--petit { padding: 6px 14px; font-size: 0.8rem; }
.bouton--grand { padding: 14px 28px; font-size: 1rem; }
.bouton--secondaire { background-color: transparent; color: #3498db; border: 2px solid #3498db; }
.bouton--secondaire:hover { background-color: #3498db; color: white; }
.bouton--danger { background-color: #e74c3c; }
.bouton--danger:hover { background-color: #c0392b; }
.bouton--desactive { opacity: 0.5; cursor: not-allowed; pointer-events: none; }
```

---

## 14.4 Les règles d'or de l'architecture CSS

```css
/* ✅ 1. Une classe = un rôle */
.carte { /* Styles de la carte */ }
.carte__titre { /* Styles du titre dans la carte */ }

/* ✅ 2. Éviter le nesting profond */
/* ❌ Trop profond : fragile et spécifique */
.header .nav ul li a:hover span { color: red; }

/* ✅ Utiliser BEM à la place */
.nav__sous-lien:hover { color: red; }

/* ✅ 3. Éviter les IDs en CSS */
/* ❌ Spécificité trop haute */
#bouton-principal { background: blue; }

/* ✅ Utiliser les classes */
.btn-principal { background: blue; }

/* ✅ 4. Éviter !important */
/* ❌ Indique un problème d'architecture */
.texte { color: red !important; }

/* ✅ Revoir la spécificité */
.composant .texte { color: red; }

/* ✅ 5. Écrire du CSS orienté composant */
/* Chaque composant est indépendant de son contexte */
.carte { /* Fonctionne où qu'elle soit placée */ }
```

---

## 📝 Exercice 14.1 — Refactorisation BEM

Prenez ce CSS non organisé et réécrivez-le avec BEM :

```css
/* Avant */
.header .menu li a { color: white; }
.header .menu li a:hover { color: #3498db; }
.header .logo img { height: 40px; }
.header .bouton-connexion { background: #3498db; }

/* Après — à vous de jouer ! */
```

---

## 📌 Résumé

| Concept | Description |
|---------|-------------|
| **BEM** | Block__Element--Modifier |
| **7-1** | 7 dossiers + 1 fichier main |
| **Composant** | Unité indépendante et réutilisable |
| **Bon nommage** | Classes descriptives et sans ambiiguïté |

## 🔗 Références

- [BEM — Documentation officielle](https://getbem.com/)
- [CSS-Tricks — BEM 101](https://css-tricks.com/bem-101/)
- [SMACSS](https://smacss.com/)

---
*⬅️ [Module 13](../13-variables/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 15 — Performance](../15-performance/README.md)*
