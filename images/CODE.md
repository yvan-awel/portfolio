# Comprendre le code de ton portfolio

Ce document explique **ce que fait chaque fichier**, **comment lire la syntaxe**,
avec des exemples tirés directement de ton projet. L'objectif : que tu puisses
modifier le site toi-même sans te sentir perdu.

---

## 1. Vue d'ensemble

| Fichier | Rôle |
|---|---|
| `index.html` | Le contenu de la page : les textes, les titres, les images, la structure |
| `css/style.css` | L'apparence : couleurs, tailles, espacements, mise en page |
| `js/script.js` | Le comportement : ce qui bouge/réagit quand on clique |

Un moyen simple de se rappeler : **HTML = le squelette**, **CSS = les vêtements**,
**JS = les muscles** (ce qui fait bouger le squelette).

---

## 2. Le HTML (`index.html`)

### 2.1 La syntaxe de base : les balises

Une balise HTML s'écrit `<nom>...</nom>`. Elle "enveloppe" un contenu.

```html
<h2>Compétences</h2>
```

- `<h2>` = balise d'ouverture
- `Compétences` = le contenu (ce qui s'affiche)
- `</h2>` = balise de fermeture (avec le `/`)

Certaines balises n'ont pas de contenu et se referment toutes seules, comme `<img>` :

```html
<img src="images/photo.jpg" alt="Photo de Yvan Awelba">
```

### 2.2 Les attributs

Un attribut donne une information supplémentaire à une balise. Il s'écrit
`nom="valeur"` à l'intérieur de la balise ouvrante.

```html
<a href="mailto:yvanawelba6@gmail.com" class="contact-card">
```

- `href` : dit vers où le lien pointe (ici, ça ouvre le logiciel mail)
- `class` : donne un "nom" à cet élément pour pouvoir le styliser en CSS (voir plus bas)

Autres attributs que tu croiseras dans le fichier :
- `id="accueil"` → identifiant unique (un seul élément peut avoir cet id sur toute la page)
- `src="..."` → source d'une image
- `alt="..."` → texte de remplacement si l'image ne charge pas (important pour l'accessibilité)

### 2.3 Les balises importantes utilisées dans ton site

```html
<section id="projets" class="section">
  <div class="container">
    <h2 class="section__title">Projets & expériences techniques</h2>
    ...
  </div>
</section>
```

- `<section>` : découpe la page en grandes parties (Accueil, Profil, Projets...).
  Chaque section a un `id` différent, ce qui permet aux liens du menu de "sauter"
  directement dessus (ex : `<a href="#projets">` va à `<section id="projets">`).
- `<div class="container">` : une simple boîte invisible, utilisée pour centrer le
  contenu et limiter sa largeur (voir `.container` en CSS).
- `<h2>`, `<h3>` : titres, du plus important (`<h1>`, utilisé une seule fois dans le
  hero) au moins important.
- `<ul>` / `<li>` : une liste (`<ul>` = la liste entière, `<li>` = chaque élément).
- `<article class="project-card">` : représente un contenu "autonome" — ici, une
  carte de projet. Sémantiquement plus précis que `<div>`.

### 2.4 Exemple concret : une carte de projet

```html
<article class="project-card">
  <div class="project-card__header">
    <h3>Système de gestion des candidats à un concours</h3>
    <span class="badge">Projet académique</span>
  </div>
  <ul>
    <li>Développement d'un système de gestion des inscriptions...</li>
  </ul>
</article>
```

Pour **ajouter un nouveau projet**, tu copies ce bloc entier (de `<article>` à
`</article>`), tu le colles juste après, et tu changes le texte.

---

## 3. Le CSS (`css/style.css`)

### 3.1 La syntaxe de base : les règles

Une règle CSS cible un élément et lui applique des propriétés.

```css
.hero__title {
  font-size: 3rem;
  font-weight: 700;
}
```

- `.hero__title` = le **sélecteur** (quel élément on cible)
- `{ ... }` = le bloc de déclarations
- `font-size: 3rem;` = une **propriété** (`font-size`) et sa **valeur** (`3rem`),
  toujours terminée par un point-virgule `;`

### 3.2 Les sélecteurs

| Sélecteur | Exemple | Cible |
|---|---|---|
| `.classe` | `.btn` | Tous les éléments avec `class="btn"` |
| `#id` | `#year` | L'unique élément avec `id="year"` |
| Combiné | `.hero__photo img` | Une balise `<img>` **à l'intérieur** de `.hero__photo` |
| Pseudo-classe | `.nav-link:hover` | `.nav-link` **quand la souris est dessus** |

Exemple tiré de ton fichier :

```css
.btn--primary:hover {
  background: var(--gold-soft);
}
```
→ Quand on survole un bouton `.btn--primary`, son fond devient `--gold-soft`.

### 3.3 Les variables CSS (`:root`)

Tout en haut du fichier :

```css
:root {
  --gold: #c9a227;
  --bg-dark: #262523;
}
```

`--gold` est une **variable** : une couleur qu'on définit une seule fois puis
qu'on réutilise partout avec `var(--gold)`. C'est le gros avantage : si tu veux
changer le doré du site, tu modifies **une seule ligne** ici, et toute la page
suit automatiquement (boutons, titres, bordures...).

```css
.hero__eyebrow {
  color: var(--gold); /* utilise la variable définie plus haut */
}
```

### 3.4 La mise en page : Flexbox et Grid

Ton site utilise deux systèmes de mise en page modernes (pas de vieux `float`) :

**Flexbox** — pour aligner des éléments en ligne ou en colonne :
```css
.hero__inner {
  display: flex;              /* active flexbox */
  align-items: center;        /* centre verticalement */
  justify-content: space-between; /* écarte les éléments aux extrémités */
  gap: 48px;                  /* espace entre les éléments */
}
```

**Grid** — pour des grilles à plusieurs colonnes qui s'adaptent toutes seules :
```css
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 24px;
}
```
→ Ça crée autant de colonnes de 220px minimum que la largeur de l'écran le permet.
C'est ce qui fait que les cartes de compétences se réorganisent automatiquement
selon la taille de l'écran, sans code supplémentaire.

### 3.5 Le responsive (`@media`)

```css
@media (max-width: 768px) {
  .hero__inner {
    flex-direction: column-reverse;
  }
}
```

Un `@media` dit : "applique ces règles **seulement si** l'écran fait moins de
768px de large (mobile/tablette)". Tout ce qui est dans ce bloc **écrase** les
règles normales, uniquement sur petit écran.

---

## 4. Le JavaScript (`js/script.js`)

### 4.1 La syntaxe de base : sélectionner un élément

```js
const burger = document.getElementById("burger");
```

- `document` = toute la page HTML
- `.getElementById("burger")` = va chercher l'élément qui a `id="burger"`
- `const burger = ...` = on stocke le résultat dans une variable nommée `burger`
  pour pouvoir la réutiliser

### 4.2 Réagir à un clic

```js
burger.addEventListener("click", () => {
  navMenu.classList.toggle("is-open");
});
```

- `.addEventListener("click", ...)` = "écoute les clics sur cet élément"
- `() => { ... }` = une fonction qui s'exécute à chaque clic
- `.classList.toggle("is-open")` = ajoute la classe `is-open` si elle n'est pas
  là, ou la retire si elle y est déjà — c'est exactement ce mécanisme qui ouvre
  et ferme le menu mobile (le CSS a une règle `.navbar__menu.is-open { ... }`
  qui rend le menu visible)

### 4.3 Modifier du texte automatiquement

```js
document.getElementById("year").textContent = new Date().getFullYear();
```

- `new Date().getFullYear()` = demande à JavaScript l'année en cours
- `.textContent = ...` = remplace le texte de l'élément par cette valeur

C'est pour ça que le footer affiche toujours l'année correcte sans que tu aies
à la changer à la main chaque 1er janvier.

### 4.4 Parcourir plusieurs éléments

```js
document.querySelectorAll(".nav-link").forEach((link) => {
  link.addEventListener("click", () => {
    navMenu.classList.remove("is-open");
  });
});
```

- `.querySelectorAll(".nav-link")` = récupère **tous** les liens du menu (une liste)
- `.forEach((link) => { ... })` = répète l'action pour chaque lien de la liste
- Résultat : quel que soit le lien cliqué, le menu mobile se referme

---

## 5. Autre — d'autres façons de faire (pour plus tard)

Ce que tu as est volontairement simple (HTML/CSS/JS "bruts"), pour bien
comprendre les fondations. Voici comment on pourrait faire évoluer le projet
plus tard, si tu veux aller plus loin :

- **Frameworks CSS (Tailwind, Bootstrap)** : au lieu d'écrire tes propres classes
  (`.btn--primary`), tu utilises des classes toutes faites directement dans le
  HTML (`class="bg-yellow-500 px-4 py-2 rounded"`). Plus rapide à écrire, mais
  moins facile à comprendre au début et le HTML devient plus chargé.

- **Préprocesseur CSS (Sass/SCSS)** : une version "améliorée" du CSS qui permet
  des variables plus puissantes, l'imbrication de règles, etc. Le fichier `.scss`
  est ensuite "compilé" en `.css` classique — ça demande un petit outil de build.

- **Framework JavaScript (React, Vue)** : utile quand un site devient une vraie
  application interactive (formulaires complexes, données qui changent souvent,
  état à synchroniser). Pour un portfolio comme le tien, ce n'est pas nécessaire :
  ça ajoute de la complexité (build, dépendances) sans vrai bénéfice ici.

- **Générateur de site statique (Astro, Eleventy, Jekyll)** : pratique si un
  jour tu veux écrire un blog avec plein d'articles similaires — tu écris un
  "modèle" une fois, et le contenu (articles en Markdown) vient le remplir
  automatiquement.

- **Formulaire de contact fonctionnel** : actuellement, les liens "Contact"
  ouvrent juste ton mail (`mailto:`) ou ton téléphone (`tel:`). Pour un vrai
  formulaire qui envoie un message sans quitter le site, il faudrait soit un
  service comme Formspree/EmailJS (aucun serveur à gérer), soit une petite
  API que tu codes toi-même (par exemple en Python/Flask, en lien avec tes
  compétences déjà en cours d'acquisition).

- **Organisation du CSS en plusieurs fichiers** : sur un plus gros projet, on
  sépare souvent `base.css` (reset, variables), `layout.css` (structure),
  `components.css` (boutons, cartes...) au lieu d'un seul `style.css`. Pour la
  taille actuelle du site, un seul fichier reste plus simple à suivre.

N'hésite pas à essayer une de ces pistes plus tard, une fois à l'aise avec les
bases — mais rien de tout ça n'est nécessaire pour que ton portfolio actuel
fonctionne très bien.
