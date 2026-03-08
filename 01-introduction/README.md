# Module 01 — Introduction au CSS

> **Niveau :** Débutant absolu  
> **Durée estimée :** 2 heures  
> **Prérequis :** Notions de base en HTML (balises, attributs)

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Expliquer ce qu'est le CSS et à quoi il sert
- Comprendre la relation entre HTML, CSS et JavaScript
- Connaître l'histoire et l'évolution du CSS
- Intégrer du CSS dans une page HTML de trois manières différentes

---

## 1.1 Qu'est-ce que le CSS ?

### Explication simple

Imaginez que vous construisez une maison. Le **HTML** représente la structure de la maison : les murs, les portes, les fenêtres. Le **CSS**, lui, représente la décoration intérieure : la couleur des murs, le type de sol, l'emplacement des meubles.

Sans CSS, toutes les pages Web auraient l'apparence d'un document Word brut : du texte noir sur fond blanc, avec quelques titres plus gros. Le CSS est ce qui rend les sites Web beaux, lisibles et agréables à utiliser.

### Définition technique

**CSS** signifie **Cascading Style Sheets**, ce qui se traduit par **Feuilles de style en cascade**.

- **Feuilles de style** : Ce sont des fichiers (ou des blocs de texte) contenant des instructions qui définissent l'apparence visuelle des éléments HTML.
- **En cascade** : Les règles CSS peuvent se superposer et s'hériter entre elles, selon un ordre de priorité précis que nous étudierons dans les modules suivants.

Le CSS est un **langage de description de présentation**, pas un langage de programmation. Il ne calcule pas, ne prend pas de décisions logiques — il décrit simplement comment les éléments HTML doivent être affichés à l'écran.

### Ce que CSS peut faire

Voici ce que vous pouvez contrôler avec le CSS :

| Catégorie | Exemples |
|-----------|----------|
| **Couleurs** | Couleur du texte, couleur de fond, couleur des bordures |
| **Typographie** | Police de caractère, taille du texte, espacement |
| **Mise en page** | Disposition des éléments, colonnes, espacement |
| **Taille et espace** | Largeur, hauteur, marges, rembourrage |
| **Animations** | Transitions, animations au survol |
| **Responsive** | Adaptation à différentes tailles d'écran |
| **Effets visuels** | Ombres, dégradés, filtres |

---

## 1.2 La relation entre HTML, CSS et JavaScript

Ces trois technologies forment le trio fondamental du développement Web front-end.

```
┌─────────────────────────────────────────────────────────┐
│                    Page Web complète                      │
│                                                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │     HTML     │  │     CSS      │  │  JavaScript  │  │
│  │              │  │              │  │              │  │
│  │  Structure   │  │ Présentation │  │ Comportement │  │
│  │  & Contenu   │  │  & Style     │  │ & Dynamisme  │  │
│  │              │  │              │  │              │  │
│  │  <h1>, <p>   │  │  couleurs,   │  │  clic, form, │  │
│  │  <img>, etc. │  │  mise en     │  │  animation   │  │
│  │              │  │  page, etc.  │  │  dynamique   │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### HTML — La structure

Le HTML (HyperText Markup Language) définit **ce qui est** sur la page : le contenu et sa signification sémantique.

```html
<!-- HTML : la structure -->
<article>
  <h1>Mon premier article</h1>
  <p>Voici un paragraphe de texte.</p>
  <button>Lire la suite</button>
</article>
```

### CSS — La présentation

Le CSS définit **comment ça a l'air** : couleurs, tailles, disposition.

```css
/* CSS : la présentation */
article {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #2c3e50;
  font-size: 24px;
}

button {
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
}
```

### JavaScript — Le comportement

JavaScript définit **ce qu'il se passe** quand l'utilisateur interagit avec la page.

```javascript
// JavaScript : le comportement
button.addEventListener('click', function() {
  alert('Vous avez cliqué sur le bouton !');
});
```

### 💡 Analogie mémorable

Pensez à un **être humain** :
- **HTML** = Le squelette (la structure, les os)
- **CSS** = La peau, les vêtements, l'apparence
- **JavaScript** = Le cerveau et les muscles (les actions)

---

## 1.3 L'évolution du CSS

### CSS1 (1996)

Le CSS1 est la première version officielle du CSS, publiée par le W3C (World Wide Web Consortium). Elle offrait des fonctionnalités très basiques : couleurs, polices, alignement du texte.

```css
/* Exemple de CSS1 */
body {
  color: black;
  background: white;
  font-family: Arial;
}
```

### CSS2 (1998) et CSS2.1 (2004)

CSS2 a introduit des concepts importants :
- Le positionnement avancé (`position: absolute`, `position: fixed`)
- Les types de médias (`@media print`, etc.)
- Les pseudo-éléments (`::before`, `::after`)

### CSS3 (2010 et après)

CSS3 n'est pas une version unique mais un ensemble de **modules indépendants** développés et publiés séparément. C'est cette version qui a révolutionné le CSS avec :

- Les **arrondis** (`border-radius`)
- Les **ombres** (`box-shadow`, `text-shadow`)
- Les **dégradés** (`linear-gradient`)
- Les **transitions** et **animations** (`transition`, `@keyframes`)
- Les **flexbox** et **grid** pour la mise en page
- Les **variables CSS** (`--ma-variable`)
- Les **filtres** (`filter: blur()`)

### CSS Moderne (2020 et après)

Le CSS continue d'évoluer rapidement avec des fonctionnalités comme :
- **CSS Container Queries** : adapter le style selon la taille du conteneur parent
- **CSS Cascade Layers** : contrôle fin de la cascade
- **`:has()` selector** : sélectionner un parent selon ses enfants
- **CSS Nesting** : imbriquer les règles CSS (comme en Sass)
- **`color-mix()`** : mélanger des couleurs en CSS
- **Scroll-driven animations** : animations liées au défilement

---

## 1.4 Comment le navigateur interprète le CSS

Comprendre ce processus vous aidera à déboguer vos styles plus efficacement.

### Étape 1 : Téléchargement

Quand un navigateur visite une page Web, il télécharge le fichier HTML, puis lit les liens vers les feuilles de style CSS et les télécharge également.

### Étape 2 : Parsing (analyse)

Le navigateur analyse le HTML pour construire le **DOM** (Document Object Model), une représentation en mémoire de la structure de la page. Simultanément, il analyse le CSS pour construire le **CSSOM** (CSS Object Model).

### Étape 3 : Application des règles

Le navigateur combine le DOM et le CSSOM pour déterminer quels styles s'appliquent à chaque élément, en tenant compte de :
1. **La cascade** (l'ordre des règles)
2. **La spécificité** (la précision du sélecteur)
3. **L'héritage** (transmission des styles parent → enfant)

### Étape 4 : Rendu

Le navigateur calcule la position et la taille de chaque élément (**layout**), puis le dessine à l'écran (**paint**).

---

## 1.5 Les trois façons d'intégrer du CSS

Il existe trois méthodes pour appliquer du CSS à une page HTML. Connaître les différences est fondamental.

### Méthode 1 : CSS externe (recommandée ✅)

On crée un fichier `.css` séparé et on le lie dans le `<head>` du HTML avec la balise `<link>`.

**Fichier : index.html**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ma page</title>

  <!-- 🔗 On lie le fichier CSS externe ici -->
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Bonjour le monde !</h1>
  <p>Ceci est mon premier paragraphe stylisé.</p>
</body>
</html>
```

**Fichier : styles.css**
```css
/* Ce fichier contient tous les styles de la page */
h1 {
  color: #2c3e50;
  font-size: 32px;
}

p {
  color: #555;
  line-height: 1.6;
}
```

**Avantages :**
- ✅ Le même fichier CSS peut être partagé par plusieurs pages HTML
- ✅ Le navigateur met le fichier CSS en cache (chargement plus rapide)
- ✅ Séparation claire entre HTML (contenu) et CSS (présentation)
- ✅ Facilite la maintenance : modifier un style une fois = modifie toutes les pages

**Inconvénients :**
- ❌ Une requête HTTP supplémentaire pour charger le fichier CSS

### Méthode 2 : CSS interne (balise `<style>`)

On écrit les règles CSS directement dans le `<head>` du HTML, à l'intérieur d'une balise `<style>`.

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Ma page</title>

  <!-- 🎨 CSS interne, directement dans le <head> -->
  <style>
    h1 {
      color: #2c3e50;
      font-size: 32px;
    }

    p {
      color: #555;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <h1>Bonjour le monde !</h1>
  <p>Ceci est mon premier paragraphe stylisé.</p>
</body>
</html>
```

**Quand l'utiliser :**
- Pour des pages uniques qui n'ont pas de fichier CSS dédié
- Pour des emails HTML
- Pour du CSS critique (rendu rapide)

**Inconvénients :**
- ❌ Les styles ne sont pas réutilisables sur d'autres pages
- ❌ Mélange HTML et CSS dans le même fichier

### Méthode 3 : CSS inline (attribut `style`)

On applique les styles directement sur un élément HTML avec l'attribut `style=""`.

```html
<h1 style="color: #2c3e50; font-size: 32px;">Bonjour le monde !</h1>
<p style="color: #555; line-height: 1.6;">Ceci est mon premier paragraphe.</p>
```

**Quand l'utiliser :**
- Pour des styles très spécifiques à un seul élément
- Pour les modifications dynamiques en JavaScript

**Inconvénients :**
- ❌ Impossible à réutiliser
- ❌ Très difficile à maintenir sur un grand projet
- ❌ A la priorité la plus haute (écrase tous les autres styles) — peut créer de la confusion
- ❌ Mélange présentation et contenu

### Tableau comparatif

| Méthode | Réutilisable | Performance | Maintenabilité | Utilisation recommandée |
|---------|-------------|-------------|----------------|------------------------|
| CSS externe | ✅ Oui | ✅ Bonne (cache) | ✅ Excellente | **La grande majorité des projets** |
| CSS interne | ❌ Non | ⚠️ Moyenne | ⚠️ Moyenne | Pages uniques, emails HTML |
| CSS inline | ❌ Non | ❌ Mauvaise | ❌ Mauvaise | Styles dynamiques via JS, cas rares |

---

## 1.6 Votre premier fichier CSS — Exemple complet

Créons ensemble une page HTML simple avec un fichier CSS externe.

### Fichier : `01-premier-css/index.html`

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon premier CSS</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- En-tête de la page -->
  <header>
    <h1>Bienvenue sur ma première page CSS !</h1>
    <p>Je commence à apprendre le CSS aujourd'hui.</p>
  </header>

  <!-- Section principale -->
  <main>
    <h2>Pourquoi apprendre le CSS ?</h2>
    <p>
      Le CSS me permet de rendre mes pages Web belles et agréables à utiliser.
      Sans CSS, toutes les pages auraient le même aspect ennuyeux.
    </p>
    <ul>
      <li>Contrôler les couleurs</li>
      <li>Choisir les polices de caractères</li>
      <li>Organiser la mise en page</li>
      <li>Créer des animations</li>
    </ul>
  </main>

  <!-- Pied de page -->
  <footer>
    <p>© 2024 — Formation CSS Complète</p>
  </footer>

</body>
</html>
```

### Fichier : `01-premier-css/styles.css`

```css
/* ===================================
   STYLES DE BASE
   Fichier : styles.css
   Description : Premier fichier CSS
   =================================== */

/* --- Réinitialisation simple --- */
/* On applique box-sizing: border-box à tous les éléments
   pour que les dimensions soient plus prévisibles */
* {
  box-sizing: border-box;
}

/* --- Corps de la page --- */
body {
  /* Famille de polices : Arial en premier, puis sans-serif comme fallback */
  font-family: Arial, Helvetica, sans-serif;

  /* Couleur du texte principal */
  color: #333333;

  /* Couleur de fond de la page */
  background-color: #f4f4f4;

  /* Marge et rembourrage à zéro */
  margin: 0;
  padding: 0;

  /* Hauteur de ligne agréable pour la lecture */
  line-height: 1.6;
}

/* --- En-tête --- */
header {
  /* Fond bleu foncé */
  background-color: #2c3e50;

  /* Texte en blanc */
  color: white;

  /* Rembourrage interne : 40px en haut/bas, 20px à gauche/droite */
  padding: 40px 20px;

  /* Texte centré */
  text-align: center;
}

/* Le titre principal dans l'en-tête */
header h1 {
  /* Suppression de la marge par défaut */
  margin: 0 0 10px 0;

  /* Grande taille de police */
  font-size: 36px;
}

/* Le paragraphe dans l'en-tête */
header p {
  /* Légèrement transparent pour un effet visuel doux */
  opacity: 0.85;

  /* Taille légèrement plus grande que la normale */
  font-size: 18px;

  /* Suppression de la marge par défaut */
  margin: 0;
}

/* --- Section principale --- */
main {
  /* Largeur maximale pour que le texte ne soit pas trop large sur grand écran */
  max-width: 800px;

  /* Centrage horizontal : auto à gauche et à droite */
  margin: 40px auto;

  /* Rembourrage interne */
  padding: 30px;

  /* Fond blanc */
  background-color: white;

  /* Coins légèrement arrondis */
  border-radius: 8px;

  /* Ombre subtile */
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Titre de niveau 2 dans le main */
main h2 {
  color: #2c3e50;
  font-size: 24px;

  /* Bordure inférieure décorative */
  border-bottom: 3px solid #3498db;
  padding-bottom: 10px;
}

/* Paragraphes dans le main */
main p {
  color: #555;
}

/* Liste non ordonnée */
main ul {
  /* Rembourrage à gauche pour laisser de la place aux puces */
  padding-left: 20px;
}

/* Chaque élément de la liste */
main li {
  /* Marge en bas pour espacer les éléments */
  margin-bottom: 8px;
  color: #555;
}

/* --- Pied de page --- */
footer {
  background-color: #2c3e50;
  color: white;
  text-align: center;
  padding: 20px;
  margin-top: 40px;

  /* Taille de police plus petite */
  font-size: 14px;
}
```

### Analyse ligne par ligne

**`* { box-sizing: border-box; }`**
> L'étoile `*` est le sélecteur universel : il cible TOUS les éléments HTML. `box-sizing: border-box` est une règle de bonne pratique qui change la façon dont les dimensions sont calculées. Nous y reviendrons en détail dans le module 05.

**`font-family: Arial, Helvetica, sans-serif;`**
> On indique une liste de polices prioritaires : d'abord Arial, puis Helvetica si Arial n'est pas disponible, puis n'importe quelle police sans empattement. C'est la technique de la "pile de polices" (font stack).

**`margin: 40px auto;`**
> `40px` s'applique aux marges haut et bas. `auto` s'applique aux marges gauche et droite — ce qui centre l'élément horizontalement dans son parent.

**`box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);`**
> Crée une ombre portée. Les valeurs sont : décalage horizontal (0), décalage vertical (2px), rayon de flou (10px), couleur avec transparence (noir à 10% d'opacité).

---

## 📝 Exercices pratiques

### Exercice 1.1 — Votre première page stylisée

**Objectif :** Créer une page HTML simple et lui appliquer des styles CSS de base.

**Instructions :**
1. Créez un dossier `exercice-01-01/`
2. Créez un fichier `index.html` avec la structure HTML de base
3. Créez un fichier `styles.css` lié au HTML
4. Appliquez les styles suivants :
   - Fond de page : gris clair (`#f0f0f0`)
   - Texte : gris foncé (`#333`)
   - Police : `Georgia, serif`
   - En-tête avec fond coloré au choix
   - Contenu principal centré avec fond blanc

**Résultat attendu :** Une page avec un en-tête coloré, un contenu centré sur fond blanc, un pied de page.

### Exercice 1.2 — Comparer les méthodes d'intégration

**Objectif :** Expérimenter les trois méthodes d'intégration CSS.

**Instructions :**
1. Créez une page HTML simple
2. Appliquez des styles avec la méthode **inline** (`style=""`)
3. Appliquez des styles avec la méthode **interne** (`<style>`)
4. Appliquez des styles avec la méthode **externe** (fichier `.css`)
5. Observez les conflits : quel style prend la priorité ?

---

## ✅ Corrigé Exercice 1.1

### `exercice-01-01/index.html`

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exercice 1.1 — Ma première page stylisée</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <header>
    <h1>Ma première page stylisée</h1>
    <p>Exercice 1.1 — Formation CSS Complète</p>
  </header>

  <main>
    <h2>À propos de moi</h2>
    <p>
      Je m'appelle [Votre prénom] et j'apprends le CSS avec la formation
      "CSS Complet — Du Débutant à l'Expert".
    </p>

    <h2>Mes objectifs</h2>
    <ul>
      <li>Maîtriser les bases du CSS</li>
      <li>Créer des pages Web modernes</li>
      <li>Apprendre Flexbox et Grid</li>
      <li>Réaliser des projets concrets</li>
    </ul>
  </main>

  <footer>
    <p>Formation CSS — Module 01 — Exercice 1.1</p>
  </footer>

</body>
</html>
```

### `exercice-01-01/styles.css`

```css
/* Corrigé - Exercice 1.1 */

* {
  box-sizing: border-box;
}

body {
  font-family: Georgia, serif;
  color: #333333;
  background-color: #f0f0f0;
  margin: 0;
  padding: 0;
  line-height: 1.7;
}

header {
  background-color: #8e44ad; /* Violet */
  color: white;
  padding: 50px 20px;
  text-align: center;
}

header h1 {
  margin: 0 0 10px 0;
  font-size: 32px;
}

header p {
  margin: 0;
  opacity: 0.9;
  font-size: 16px;
  font-style: italic;
}

main {
  max-width: 750px;
  margin: 40px auto;
  padding: 30px 40px;
  background-color: white;
  border-radius: 6px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

main h2 {
  color: #8e44ad;
  font-size: 22px;
  margin-top: 30px;
}

main h2:first-child {
  margin-top: 0;
}

main p {
  color: #555;
}

main ul {
  padding-left: 22px;
}

main li {
  margin-bottom: 6px;
  color: #555;
}

footer {
  background-color: #2c3e50;
  color: #aaa;
  text-align: center;
  padding: 20px;
  font-size: 13px;
}
```

---

## 📌 Résumé du module 01

| Concept | Points clés |
|---------|-------------|
| **CSS** | Cascading Style Sheets — définit l'apparence visuelle des pages Web |
| **HTML vs CSS** | HTML = structure, CSS = présentation, JS = comportement |
| **3 méthodes** | Externe (recommandée), Interne (`<style>`), Inline (`style=""`) |
| **CSS externe** | Fichier `.css` lié avec `<link rel="stylesheet" href="...">` |
| **CSS moderne** | Variables, Grid, Flexbox, animations, container queries |

---

## 🔗 Références

- [MDN — Introduction au CSS](https://developer.mozilla.org/fr/docs/Learn/CSS/First_steps/What_is_CSS)
- [MDN — Comment CSS est structuré](https://developer.mozilla.org/fr/docs/Learn/CSS/First_steps/How_CSS_is_structured)
- [W3C CSS Specifications](https://www.w3.org/Style/CSS/specs.en.html)
- [CSS-Tricks — What is CSS?](https://css-tricks.com/css/)

---

*⬅️ [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 02 — Environnement de développement](../02-environnement/README.md)*
