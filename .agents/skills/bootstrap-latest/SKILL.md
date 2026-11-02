---
name: "bootstrap-latest"
description: "Crée des interfaces avec Bootstrap : v5.3 stable en production, v6 alpha sur demande. Use for Bootstrap pages, grid, components, Sass theming, Symfony/Twig integration."
---

# Bootstrap : dernière version

## Étape 0 : vérifier la version avant d'écrire du code
Les versions changent. Avant de générer, vérifier l'état actuel (`npm view bootstrap version`, `npm view bootstrap dist-tags`, ou le blog officiel blog.getbootstrap.com) et annoncer la version utilisée.

État connu au 28/10/2026 (à revalider) :
- **Stable : 5.3.8** (août 2025), recommandée pour tout projet en production.
- **Pré-version : 6.0.0-alpha.1** (annoncée le 8/10/2026). C'est une alpha : la syntaxe peut encore changer avant la bêta. Bootstrap 5 reste supporté ; une 5.4.0 est annoncée avant la fin de vie de la v5.

**Règle de choix :**
- Production, client, délai ferme : **5.3.x**.
- La personne demande explicitement la v6, un prototype ou une veille technique : **6 alpha**, en prévenant que c'est une alpha.
- Ne jamais mélanger la syntaxe v5 et v6 dans le même fichier. Indiquer la version en commentaire en tête du code.

## Quand choisir Bootstrap (plutôt qu'une alternative)
Admin et outils internes, MVP, prototypes rapides, sites rendus côté serveur sans framework JS (Symfony/Twig, Laravel, Django, Rails), équipes peu à l'aise en CSS, bases de code Bootstrap existantes. Pour une identité visuelle très spécifique ou une application React/Vue, proposer plutôt le skill `tailwind-pro-ui`.

---

## A. Bootstrap 5.3 (stable)

### Installation
- **CDN** : liens CSS et `bootstrap.bundle.min.js` depuis jsDelivr, avec l'attribut `integrity` (SRI) recopié depuis la page officielle de téléchargement. Ne jamais inventer un hash.
- **npm** : `npm i bootstrap@5.3.8` (ou la dernière 5.3.x) ; importer le JS par composant pour réduire le poids.

### Squelette de page
```html
<!doctype html>
<html lang="fr" data-bs-theme="light">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>[Titre]</title>
  <!-- Bootstrap 5.3.x : CSS (avec integrity officiel) -->
</head>
<body>
  <!-- contenu -->
  <!-- Bootstrap 5.3.x : bootstrap.bundle.min.js -->
</body>
</html>
```

### Repères de syntaxe v5
- Grille : `container`, `row`, `col-md-6`, `g-3` ; breakpoints `sm md lg xl xxl`.
- Utilitaires responsives en **infixe** : `d-md-none`, `justify-content-md-end`, `col-lg-6`.
- Modes de couleur : `data-bs-theme="dark"` sur `<html>` ou sur un composant.
- Composants : `btn btn-primary`, `modal`, `offcanvas`, `dropdown`, `accordion`, `navbar`, `card`, `toast`, `form-floating`.
- Validation de formulaire : classe `needs-validation` + `novalidate`, retours `invalid-feedback`.

### Personnalisation (Sass)
- Surcharger les variables avant l'import : `$primary`, `$font-family-sans-serif`, `$border-radius`, `$spacer`, puis `@import "bootstrap/scss/bootstrap";` (la 5.3 s'appuie sur `@import`).
- Avec une Dart Sass récente, des avertissements de dépréciation peuvent apparaître ; les masquer via les options de Sass plutôt que de réécrire l'import.
- Préférer les **variables CSS** (`--bs-*`) pour les ajustements à l'exécution (thème, mode sombre).

---

## B. Bootstrap 6 alpha (sur demande uniquement)

Sources à consulter avant de coder : blog officiel (annonce du 8/10/2026), notes de version GitHub `v6.0.0-alpha.1`, guide de migration du dépôt, et les fichiers `llms.txt` / `llms-full.txt` publiés par la doc.

### Prérequis navigateur
Chrome/Edge 130+, Firefox 132+, Safari 18+. Aucun correctif de compatibilité en dessous. S'appuie sur `:has()`, container queries, `oklch()`, `color-mix()`, `light-dark()` et `<dialog>`.

### Différences principales à respecter
| Sujet | v5.3 | v6 alpha |
|---|---|---|
| JavaScript | bundle classique, global `bootstrap` | **ESM uniquement**, `<script type="module">`, plus de global ni d'UMD |
| Utilitaires responsives | infixe `d-md-none`, `col-lg-6` | **préfixe** `md:d-none`, `lg:col-6`, `hover:opacity-50` |
| Offcanvas | `offcanvas` | **Drawer** (`md:drawer`) |
| Modal | `modal` | **Dialog**, basé sur `<dialog>` |
| Dropdown | `dropdown` | **Menu** |
| Accordion | JS Collapse | basé sur `<details>` / `<summary>` |
| Sass | `@import`, `_variables.scss` | `@use` / `@forward`, **token maps** (`$root-tokens`, `$alert-tokens`), `defaults()` ; `$grid-breakpoints` devient `$breakpoints` |
| Préfixe CSS | `$prefix` Sass | réglé dans la configuration PostCSS |

- Nouveautés mentionnées : Stepper, chip input, combobox, OTP input, plugin Range, formulaires redéfinis, carrousel reconstruit.
- Le projet est écrit en TypeScript et fournit ses types : retirer `@types/bootstrap`.
- Certains noms de classes de composants (ex. boutons `btn-solid theme-primary`) sont rapportés par des sources secondaires : **les valider dans la doc officielle** avant de les utiliser.
- Installation : `npm i bootstrap@6.0.0-alpha.1`.

---

## Rendre l'interface professionnelle (v5 comme v6)
- Ne pas livrer le look par défaut : personnaliser couleur principale, police, rayon, ombres, espacements.
- Hiérarchie typographique claire, une seule couleur d'accent, gris neutres cohérents.
- Composants cohérents : mêmes hauteurs de champs et de boutons, mêmes espacements verticaux.
- États complets : survol, focus visible, désactivé, chargement, erreur, vide.
- Accessibilité : libellé sur chaque champ, `aria-*` sur les composants dynamiques, contraste ≥ 4,5:1, navigation clavier, `visually-hidden` pour les textes d'aide.
- Mobile d'abord ; tester à 375, 768 et 1280 px.

## Intégration Symfony / Twig
- Thème de formulaires : `twig: form_themes: ['bootstrap_5_layout.html.twig']` dans `config/packages/twig.yaml`.
- Assets : AssetMapper (`php bin/console importmap:require bootstrap`) ou Webpack Encore. Le JS ESM de la v6 s'intègre naturellement avec AssetMapper.
- Pagination : thème Bootstrap 5 de KnpPaginator ou Pagerfanta.
- Garder les composants réutilisables dans des partiels ou composants Twig plutôt que de dupliquer le HTML.

## Vérification avant livraison
1. Ouvrir la page dans un navigateur et contrôler les 3 largeurs.
2. Parcourir la page au clavier ; vérifier focus visible et ordre logique.
3. Contrôler la console (aucune erreur JS) et le mode sombre si proposé.
4. Vérifier que le HTML n'utilise qu'une seule version de syntaxe (v5 ou v6).