---
name: "tailwind-pro-ui"
description: "Crée des interfaces professionnelles avec Tailwind CSS v4 et un design system. Use for modern custom UI, dashboards, app shells, shadcn/ui, Twig/Symfony or React front ends."
---

# Tailwind CSS v4 : interfaces de niveau professionnel

## Pourquoi ce choix
Tailwind CSS est l'alternative à Bootstrap la plus adoptée pour les nouveaux projets : CSS final très léger, personnalisation totale, bon accueil dans React, Vue, Svelte et en rendu serveur. Son compromis : pas de composants prêts à l'emploi et une bonne base CSS requise. Il n'y a pas de « meilleur » absolu ; pour un look sur mesure et une application moderne, c'est le choix par défaut de ce skill.

| Contexte | Choix recommandé |
|---|---|
| Identité visuelle propre, produit SaaS, application React/Next.js | **Tailwind v4 + shadcn/ui** |
| Vue ou Svelte | Tailwind v4 + shadcn-vue / shadcn-svelte ou Headless UI |
| Symfony/Twig, Laravel, rendu serveur | Tailwind v4 + composants Twig ou partiels (+ daisyUI ou Flowbite si besoin de composants prêts) |
| Outil interne rapide, admin, équipe peu à l'aise en CSS | Bootstrap (skill `bootstrap-latest`) |

Ne pas mélanger Tailwind et Bootstrap dans la même page en production (conflits de classes, poids).

## Étape 0 : vérifier la version
Avant de coder : `npm view tailwindcss version` et la doc officielle. État connu (à revalider) : **4.3.x**, dernière 4.3.3 en juillet 2026 ; la série 3.4 serait supportée jusqu'au 28/02/2027 selon endoflife.date (pas de politique de support officielle documentée). Cibler la v4 pour tout nouveau projet ; ne migrer un projet v3 qu'avec l'outil de mise à niveau officiel.

## Installation v4
- Une seule ligne dans le CSS d'entrée : `@import "tailwindcss";`
- **Vite** : plugin `@tailwindcss/vite`. **Autre bundler** : `@tailwindcss/postcss`. **Sans bundler** : CLI `@tailwindcss/cli`. **Prototype jetable** : script navigateur `@tailwindcss/browser` (jamais en production).
- Détection automatique des fichiers sources ; `@source` pour ajouter un dossier (ex. `templates/` Twig).
- Configuration **dans le CSS** : `@theme { ... }` pour les tokens, `@custom-variant` pour des variantes (ex. mode sombre par classe), `@utility` pour des utilitaires propres. Pas de `tailwind.config.js` par défaut (`@config` si indispensable).
- Navigateurs cibles modernes (Safari 16.4+, Chrome 111+, Firefox 128+) : vérifier la doc si le public est plus ancien.

### Pièges v3 → v4 (vérifier dans le guide de mise à niveau)
- Utilitaires renommés : `shadow-sm` → `shadow-xs`, `shadow` → `shadow-sm`, `rounded-sm` → `rounded-xs`, `rounded` → `rounded-sm`, `outline-none` → `outline-hidden`.
- `bg-opacity-*` supprimé : utiliser `bg-black/50`.
- Le modificateur important se place à la fin (`bg-red-500!`).
- Ne jamais construire un nom de classe par concaténation (`bg-${couleur}-500`) : la détection est statique. Utiliser des correspondances complètes (`{ danger: 'bg-red-600', ok: 'bg-green-600' }`).

## Design system minimal (avant la première page)
Définir dans `@theme` puis s'y tenir :
1. **Couleurs** : une couleur d'accent avec échelle 50–950, une échelle de gris neutre, 3 couleurs sémantiques (succès, avertissement, erreur). Préférer des tokens sémantiques (`--color-surface`, `--color-text-muted`, `--color-border`) pour gérer le mode sombre.
2. **Typographie** : une police de titres et une de corps (ou une seule), échelle limitée (12, 14, 16, 18, 24, 32, 48), interlignage cohérent.
3. **Espacements** : grille de 4 px, rythme vertical régulier ; sections séparées par des espaces, pas par des bordures partout.
4. **Rayon et ombres** : 2 ou 3 rayons, 3 niveaux d'élévation maximum.
5. **Mouvement** : transitions courtes (150–200 ms) ; `motion-reduce:` respecté.

## Critères de niveau professionnel
- **États complets** pour chaque composant interactif : repos, survol, `focus-visible`, actif, désactivé, chargement, erreur, vide.
- **Accessibilité** : contraste ≥ 4,5:1 (texte), anneau de focus visible, cibles tactiles confortables (≈ 44 px), libellés de champs, `aria-*` sur les éléments dynamiques, navigation clavier, HTML sémantique avant les `div`.
- **Responsive mobile d'abord** avec `sm: md: lg:` ; utiliser les **container queries** (`@container`, `@md:`) pour les composants réutilisables.
- **Mode sombre** pensé dès le début (`dark:` ou tokens sémantiques), pas ajouté à la fin.
- **Densité et hiérarchie** : une action principale par écran, textes secondaires atténués, alignements stricts.
- **Cohérence** : mêmes hauteurs de champs et de boutons, mêmes espacements ; pas de valeurs arbitraires `[13px]` sauf exception documentée.
- **Maintenabilité** : extraire les motifs répétés en composants (React, composant Twig, partiel), pas en `@apply` massifs ; fusionner proprement les classes (`tailwind-merge`, `clsx`/`cva` côté JS).

## Motifs d'interface à maîtriser
Coque d'application (barre latérale + barre supérieure), tableau de données (tri, pagination, état vide), formulaires (groupes, aide, erreurs en ligne), cartes de synthèse (KPI), boîtes de dialogue, notifications, navigation par onglets, fil d'Ariane, squelettes de chargement.

## Bibliothèques de composants
- **shadcn/ui** (React, Next.js) : composants copiés dans le projet via CLI, basés sur des primitives accessibles et Tailwind ; le code est à soi et modifiable. Respecter sa structure (`components/ui`) et ses variables de thème.
- **Headless UI** : comportements accessibles sans style (React, Vue).
- **daisyUI / Flowbite / Preline** : composants prêts à l'emploi pour le rendu serveur ; un seul kit par projet.

## Intégration Symfony / Twig
- **TailwindBundle** (`symfonycasts/tailwind-bundle`) avec AssetMapper : `composer require symfonycasts/tailwind-bundle`, `php bin/console tailwind:init`, `php bin/console tailwind:build --watch`. Vérifier la compatibilité avec Tailwind v4 dans la doc du bundle.
- Composants réutilisables : **Symfony UX Twig Components** ; fusion des classes avec une extension Twig de type `tailwind_merge`.
- Ajouter `templates/` aux sources détectées (`@source`) ; éviter les classes générées dynamiquement côté PHP.
- Formulaires Symfony : créer ou adopter un thème de formulaire Tailwind (vérifier celui fourni par la version de Symfony utilisée) pour garder des champs cohérents.

## Vérification avant livraison
1. Compiler le CSS (build de production) et contrôler le poids final.
2. Ouvrir la page dans un navigateur : 375, 768, 1280 px, mode clair et sombre.
3. Navigation clavier complète, focus visible, aucun piège au clavier.
4. Contrôle d'accessibilité (axe ou Lighthouse) et contraste des couleurs.
5. Aucune classe dynamique construite par concaténation ; aucune valeur arbitraire inutile.
6. Relire les états : vide, chargement, erreur.