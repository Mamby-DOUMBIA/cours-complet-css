# Module 02 — Environnement de développement

> **Niveau :** Débutant absolu  
> **Durée estimée :** 1 heure  
> **Prérequis :** Module 01

---

## 📚 Objectifs de ce module

À la fin de ce module, vous serez capable de :
- Installer et configurer VS Code pour le développement CSS
- Utiliser les extensions essentielles
- Prévisualiser vos pages en temps réel
- Inspecter et déboguer le CSS avec les DevTools du navigateur
- Organiser correctement les fichiers d'un projet Web

---

## 2.1 Installer et configurer VS Code

### Qu'est-ce que VS Code ?

**Visual Studio Code** (ou VS Code) est un éditeur de code gratuit, léger et très populaire, développé par Microsoft. C'est l'outil numéro 1 des développeurs Web dans le monde. Il offre :
- La coloration syntaxique (le code est coloré selon sa signification)
- L'autocomplétion (suggestions de code en cours de frappe)
- Un terminal intégré
- Des milliers d'extensions pour améliorer la productivité

### Installation

1. Rendez-vous sur [code.visualstudio.com](https://code.visualstudio.com/)
2. Cliquez sur le bouton de téléchargement correspondant à votre système d'exploitation (Windows, macOS, Linux)
3. Installez le logiciel en suivant les instructions

### Premier lancement

Lors du premier lancement, VS Code vous accueille avec un écran de bienvenue. Vous pouvez choisir un thème de couleur selon vos préférences (clair ou sombre).

---

## 2.2 Extensions VS Code essentielles

Les extensions ajoutent des fonctionnalités à VS Code. Voici les indispensables pour le développement CSS :

### Comment installer une extension

1. Cliquez sur l'icône des extensions dans la barre latérale gauche (ou `Ctrl+Shift+X`)
2. Tapez le nom de l'extension dans la barre de recherche
3. Cliquez sur "Installer"

### Extensions recommandées

| Extension | Auteur | Utilité |
|-----------|--------|---------|
| **Live Server** | Ritwick Dey | Prévisualisation en temps réel |
| **Prettier** | Prettier | Formatage automatique du code |
| **CSS Peek** | Pranay Prakash | Voir les styles CSS depuis le HTML |
| **IntelliSense for CSS** | Zignd | Autocomplétion CSS améliorée |
| **Color Highlight** | Naumovs | Colore les codes couleur CSS |
| **Auto Rename Tag** | Jun Han | Renomme automatiquement les balises HTML |

### Extension Live Server — Configuration

Live Server est l'extension la plus importante : elle crée un serveur local et recharge automatiquement votre page quand vous sauvegardez un fichier.

**Pour lancer Live Server :**
1. Ouvrez un fichier HTML
2. Clic droit dans l'éditeur → "Open with Live Server"
3. Ou cliquez sur "Go Live" en bas à droite de VS Code

Votre page s'ouvre automatiquement dans le navigateur à l'adresse `http://127.0.0.1:5500/index.html`.

---

## 2.3 Les outils développeur du navigateur (DevTools)

### Accéder aux DevTools

Tous les navigateurs modernes incluent des outils de débogage puissants :
- **Chrome / Edge** : `F12` ou `Ctrl+Shift+I` (Windows/Linux) ou `Cmd+Option+I` (Mac)
- **Firefox** : `F12` ou `Ctrl+Shift+I`
- **Safari** : `Cmd+Option+I` (activer d'abord dans les préférences)

### L'onglet "Elements" (Éléments)

C'est l'outil le plus utile pour le CSS. Il vous permet de :

1. **Inspecter un élément** : Clic droit sur n'importe quel élément de la page → "Inspecter"
2. **Voir le HTML** : Dans le panneau de gauche
3. **Voir et modifier le CSS** : Dans le panneau de droite
4. **Ajouter/modifier des propriétés CSS en temps réel** : Cliquez sur une valeur CSS pour la modifier
5. **Voir le Box Model** : Un diagramme visuel montre le contenu, padding, border et margin de l'élément sélectionné

### Astuce : tester le CSS en direct

Dans les DevTools, vous pouvez :
- Cliquer sur n'importe quelle valeur CSS et la modifier
- Cocher/décocher des propriétés CSS pour les activer/désactiver
- Ajouter de nouvelles propriétés CSS
- Ces modifications sont temporaires : elles disparaissent si vous rechargez la page

### L'onglet "Styles"

Le panneau Styles montre :
- Toutes les règles CSS appliquées à l'élément sélectionné
- Les règles sont classées par ordre de spécificité (les plus spécifiques en haut)
- Les règles écrasées sont barrées

```
/* Exemple d'affichage DevTools */

element.style {
  /* Styles inline */
}

h1.titre-principal {  /* styles.css:15 */
  color: #2c3e50;    ← Appliqué
  font-size: 32px;   ← Appliqué
}

h1 {                  /* styles.css:8 */
  ~~color: black;~~  ← Barré (écrasé par la règle ci-dessus)
}
```

---

## 2.4 Organisation des fichiers d'un projet Web

### Structure recommandée pour un projet simple

```
mon-projet/
│
├── index.html          ← Page principale
├── about.html          ← Autre page (optionnel)
│
├── css/
│   ├── styles.css      ← CSS principal
│   └── reset.css       ← Réinitialisation CSS (optionnel)
│
├── images/
│   ├── logo.png
│   ├── photo-hero.jpg
│   └── icone.svg
│
└── js/
    └── script.js       ← JavaScript (optionnel)
```

### Structure pour un projet plus grand

```
mon-projet/
│
├── index.html
│
├── css/
│   ├── main.css        ← Fichier CSS principal (importe les autres)
│   ├── base/
│   │   ├── reset.css
│   │   └── typography.css
│   ├── components/
│   │   ├── header.css
│   │   ├── navigation.css
│   │   ├── cards.css
│   │   └── footer.css
│   └── pages/
│       ├── home.css
│       └── about.css
│
├── images/
├── fonts/
└── js/
```

### Conventions de nommage des fichiers

- Utilisez des **minuscules** : `styles.css` et non `Styles.CSS`
- Utilisez des **tirets** pour séparer les mots : `mon-fichier.css` et non `monFichier.css`
- Évitez les **espaces** et les **caractères spéciaux** dans les noms de fichiers
- Utilisez des **noms descriptifs** : `navigation.css` est meilleur que `nav2.css`

### Exemple : lier plusieurs fichiers CSS

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon projet</title>

  <!-- Réinitialisation CSS en premier -->
  <link rel="stylesheet" href="css/reset.css">

  <!-- Styles de base -->
  <link rel="stylesheet" href="css/base.css">

  <!-- Composants -->
  <link rel="stylesheet" href="css/components.css">

  <!-- Styles de la page spécifique -->
  <link rel="stylesheet" href="css/home.css">
</head>
<body>
  <!-- contenu -->
</body>
</html>
```

---

## 2.5 Le fichier reset.css

Chaque navigateur applique ses propres styles par défaut aux éléments HTML. Un **reset CSS** supprime ou normalise ces styles pour que votre design parte d'une base cohérente entre tous les navigateurs.

### Reset minimal recommandé

```css
/* reset.css — Réinitialisation minimale */

/* Applique box-sizing: border-box à tous les éléments */
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Suppression des marges et paddings par défaut */
* {
  margin: 0;
  padding: 0;
}

/* Amélioration du comportement des images */
img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

/* Amélioration du comportement des inputs */
input,
button,
textarea,
select {
  font: inherit;
}

/* Empêche le dépassement de texte */
p,
h1,
h2,
h3,
h4,
h5,
h6 {
  overflow-wrap: break-word;
}

/* Hauteur racine pour les calculs vh */
html,
body {
  height: 100%;
}
```

---

## 📝 Exercice pratique

### Exercice 2.1 — Configurer votre environnement

1. Installez VS Code
2. Installez les extensions Live Server et Color Highlight
3. Créez la structure de dossiers suivante :
   ```
   exercice-02/
   ├── index.html
   ├── css/
   │   └── styles.css
   └── images/
   ```
4. Créez un fichier `index.html` basique lié au fichier `styles.css`
5. Lancez Live Server et vérifiez que la page se recharge automatiquement quand vous modifiez le CSS

---

## 📌 Résumé du module 02

| Outil | Utilité |
|-------|---------|
| **VS Code** | Éditeur de code principal |
| **Live Server** | Prévisualisation en temps réel |
| **DevTools** | Inspection et débogage CSS |
| **reset.css** | Normalisation entre navigateurs |
| **Organisation des fichiers** | `css/`, `images/`, `js/` séparés |

---

## 🔗 Références

- [VS Code — Téléchargement](https://code.visualstudio.com/)
- [Chrome DevTools — Documentation](https://developer.chrome.com/docs/devtools/)
- [MDN — Firefox Developer Tools](https://firefox-source-docs.mozilla.org/devtools-user/)

---

*⬅️ [Module 01](../01-introduction/README.md) | [Retour au sommaire](../SOMMAIRE.md) | Module suivant ➡️ [Module 03 — Syntaxe CSS](../03-syntaxe/README.md)*
