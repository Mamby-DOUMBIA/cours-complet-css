# Cartographie du projet

Date de cartographie: 2026-03-08

## Vue d'ensemble

Ce dossier contient une formation CSS structuree comme un projet pedagogique complet.
Le coeur du contenu est organise en 19 modules numerotes, complete par des documents racine
de navigation et de reference, puis par un espace de projets pratiques.

## Perimetre observe

- Racine documentaire: `README.md`, `SOMMAIRE.md`, `GLOSSAIRE.md`, `FICHE-MEMO.md`, `LICENSE`
- Modules pedagogiques: `01-introduction` a `18-ecosysteme`
- Bloc pratique: `19-projets` avec 5 sous-projets
- Ressources annexes: `ressources/`
- Espaces prepares mais vides: `assets/css/`, `assets/images/`, `css-course/`

## Metriques rapides

- 34 fichiers au total
- 29 dossiers au total
- 25 fichiers Markdown
- 5 fichiers HTML
- 2 fichiers CSS
- 1 fichier `.gitignore`

## Structure fonctionnelle

### 1. Documentation racine

La racine joue le role de point d'entree pedagogique et de navigation:

- `README.md`: presentation generale du cours, objectifs, public vise, parcours recommande
- `SOMMAIRE.md`: table des matieres detaillee des 19 modules
- `GLOSSAIRE.md`: definitions des termes techniques
- `FICHE-MEMO.md`: aide-memoire CSS
- `LICENSE`: licence MIT

### 2. Modules de cours

Les modules `01` a `18` sont majoritairement composes d'un `README.md` chacun.
Ils couvrent la progression suivante:

- `01-introduction`: seul module avec demonstration locale (`demo.html`, `demo.css`)
- `02-environnement` a `08-mise-en-page`: fondamentaux
- `09-flexbox` a `12-animations`: mise en page moderne et responsive
- `13-variables` a `18-ecosysteme`: CSS avance, architecture, performance, accessibilite et outils

### 3. Projets pratiques

Le dossier `19-projets` contient:

- `README.md`: point d'entree du bloc projet
- `01-page-complete`: `index.html`, `styles.css`
- `02-page-responsive`: `README.md` uniquement
- `03-galerie`: `index.html`
- `04-dashboard`: `index.html`
- `05-ecommerce`: `index.html`

Lecture: les projets sont presents, mais tous ne sont pas au meme niveau de finition.
Le projet 2 semble documente sans livrable HTML/CSS dans l'etat actuel.

## Etat de structure par dossier

| Dossier | Fichiers | Markdown | HTML | CSS | Observation |
|---|---:|---:|---:|---:|---|
| `01-introduction` | 3 | 1 | 1 | 1 | module le plus concret pour demarrage rapide |
| `02-environnement` a `18-ecosysteme` | 17 | 17 | 0 | 0 | modules guides centres sur la documentation |
| `19-projets` | 7 | 2 | 4 | 1 | zone de mise en pratique heterogene |
| `ressources` | 1 | 1 | 0 | 0 | ressources complementaires |
| `assets` | 0 | 0 | 0 | 0 | structure reservee, actuellement vide |
| `css-course` | 0 | 0 | 0 | 0 | dossier vide, a confirmer ou supprimer plus tard |

## Points notables

- La numerotation des modules est propre et facilite la lecture sequentielle.
- Le projet est fortement oriente documentation Markdown.
- Les demonstrations executables sont encore limitees en volume.
- La structure `assets/` existe deja pour accueillir des ressources mutualisees.
- Le dossier `css-course/` parait etre un reliquat ou un espace de travail non utilise.

## Risques et incoherences mineures

- `README.md` mentionne une arborescence cible qui suppose un depot nomme `css-course`, alors que le travail reel est a la racine actuelle.
- Les dossiers vides peuvent creer une ambiguite sur le perimetre publie.
- Les projets pratiques n'ont pas un niveau de completude uniforme.

## Recommandations immediates

1. Versionner l'etat actuel pour figer une base propre du cours.
2. Conserver `assets/` seulement si son usage est prevu a court terme.
3. Clarifier le role de `css-course/` ou le supprimer dans une future passe de nettoyage.
4. Ajouter au fil du temps des livrables concrets supplementaires dans `19-projets`.
5. Harmoniser la documentation racine avec l'arborescence reellement publiee sur GitHub.

## Arborescence synthetique

```text
.
|-- README.md
|-- SOMMAIRE.md
|-- GLOSSAIRE.md
|-- FICHE-MEMO.md
|-- LICENSE
|-- 01-introduction/
|-- 02-environnement/
|-- 03-syntaxe/
|-- 04-selecteurs/
|-- 05-box-model/
|-- 06-couleurs/
|-- 07-typographie/
|-- 08-mise-en-page/
|-- 09-flexbox/
|-- 10-grid/
|-- 11-responsive/
|-- 12-animations/
|-- 13-variables/
|-- 14-architecture/
|-- 15-performance/
|-- 16-css-avance/
|-- 17-accessibilite/
|-- 18-ecosysteme/
|-- 19-projets/
|-- assets/
|-- css-course/
`-- ressources/
```
