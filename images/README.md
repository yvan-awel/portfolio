# Portfolio — Yvan Awelba

Site simple en **HTML / CSS / JavaScript pur** (aucun framework, aucune étape de build).

## Structure du projet

```
portfolio/
├── index.html          → toute la page (une seule page, avec des sections)
├── css/
│   └── style.css       → toutes les couleurs, la mise en page, le responsive
├── js/
│   └── script.js       → menu mobile + année automatique dans le footer
└── images/
    ├── photo.jpg        → À AJOUTER par toi (ta vraie photo)
    └── placeholder.svg  → avatar de secours, utilisé tant que photo.jpg n'existe pas
```

## Étape 1 — Ajouter ta photo

Le site cherche un fichier `images/photo.jpg`. Ce fichier n'existe pas encore
(je n'ai pas pu extraire l'image depuis le CV que tu as envoyé). Ajoute une
photo carrée (idéalement 500x500px ou plus) dans le dossier `images/` et
nomme-la `photo.jpg`. En attendant, un avatar avec tes initiales "YA"
s'affiche automatiquement à la place.

## Étape 2 — Tester en local

Pas besoin de serveur particulier : ouvre simplement `index.html` dans ton
navigateur (double-clic dessus), ou utilise l'extension "Live Server" de
VS Code pour un rechargement automatique pendant que tu modifies le code.

## Étape 3 — Déployer sur Vercel

**Option A — Sans ligne de commande (le plus simple) :**
1. Crée un dépôt GitHub et mets-y ce dossier (`index.html`, `css/`, `js/`, `images/`).
2. Va sur https://vercel.com, connecte-toi avec GitHub.
3. Clique "Add New... > Project", choisis ton dépôt.
4. Comme c'est du HTML/CSS/JS pur (pas de framework), laisse "Framework Preset"
   sur "Other" et clique "Deploy". C'est tout — pas de build command à configurer.

**Option B — Avec la CLI Vercel :**
```bash
npm install -g vercel
cd portfolio
vercel
```
Suis les instructions à l'écran (connexion, nom du projet), puis `vercel --prod`
pour la mise en ligne définitive.

## Pour modifier le contenu plus tard

- **Textes** : tout est directement dans `index.html`, section par section
  (commentaires `<!-- ... -->` pour t'aider à te repérer).
- **Couleurs** : tout est centralisé en haut de `css/style.css`, dans le bloc
  `:root { ... }`. Change `--gold` ou `--bg-dark` et toute la page suit.
- **Ajouter un projet** : copie un bloc `<article class="project-card">...</article>`
  dans la section Projets et modifie le texte.
