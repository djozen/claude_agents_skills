---
name: "office-xlsx-generator"
description: "Crée ou corrige des classeurs Excel (.xlsx) avec formules, mise en forme et graphiques : budget, suivi, devis, tableau de bord. Use for Excel/.xlsx/.csv generation or cleanup."
---

# Génération de classeurs Excel (.xlsx)

## Quand l'utiliser
- La personne veut un tableau avec calculs, tri, filtres ou graphiques : budget, suivi, planning, devis, inventaire, tableau de bord.
- Un fichier .xlsx, .xlsm ou .csv est fourni à corriger, enrichir ou nettoyer (colonnes mal placées, doublons, formats).
- Conversion entre formats tabulaires.

Si un skill `xlsx` natif est disponible, le charger en priorité.

## Démarche
1. **Cadrer** : que doit permettre le classeur (saisir, calculer, analyser) et pour qui.
2. **Préparer les données** avec `pandas` si elles viennent d'une source ; ne jamais inventer de chiffres.
3. **Construire** avec `openpyxl` : données, formules, mise en forme, graphiques.
4. **Recalculer et vérifier**, puis livrer.

## Structure d'un bon classeur
- Une feuille par rôle : `Saisie` (entrées), `Calculs` (si nécessaire), `Synthèse` (résultats, graphiques), `Lisez-moi` (but, hypothèses, mode d'emploi).
- Les hypothèses (taux de TVA, tarifs, dates) dans des cellules dédiées et référencées, jamais recopiées dans les formules.
- Données en **tableau structuré** (une ligne d'en-tête, une ligne par enregistrement, pas de cellules fusionnées au milieu des données).

## Règles de construction
- Écrire des **formules** (`=SOMME(B2:B20)` côté Excel FR, `=SUM(...)` dans openpyxl qui attend la syntaxe anglaise) et non des résultats calculés en dur.
- Formats de cellule explicites : nombres, pourcentages, dates, devises (`# ##0,00 €`).
- Ligne d'en-tête figée, filtres automatiques, largeurs de colonnes ajustées, mise en forme conditionnelle pour les alertes.
- Listes déroulantes et validation de données sur les champs de saisie.
- Couleurs sobres : cellules de saisie d'une teinte (ex. bleu pâle), cellules calculées neutres.
- Graphiques : titre, axes nommés, un message par graphique.
- Protéger les cellules de formules si le classeur est destiné à des tiers.

## Vérification obligatoire
1. **Recalculer** avec LibreOffice (`soffice --headless --convert-to xlsx --outdir sortie fichier.xlsx`) puis relire les valeurs.
2. Chercher les erreurs : `#REF!`, `#DIV/0!`, `#NAME?`, `#VALUE!`.
3. Contrôler que les totaux correspondent aux données sources (recalcul indépendant avec pandas).
4. Ouvrir le rendu (conversion PDF puis image) pour vérifier la lisibilité.

## Livraison
- Nom explicite : `budget-formation-2026.xlsx`.
- Une ligne de contexte : contenu des feuilles, hypothèses, cellules à renseigner.
- Ne jamais écraser le fichier d'origine : écrire une copie.

## Cible PHP / Symfony
Si l'export est produit par l'application : **PhpSpreadsheet** (ou `box/spout`/OpenSpout pour de gros volumes en flux), généré dans un service dédié ; pour de très gros exports, écrire en flux ou en CSV plutôt qu'en mémoire.