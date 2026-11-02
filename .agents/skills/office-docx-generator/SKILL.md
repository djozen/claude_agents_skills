---
name: "office-docx-generator"
description: "Crée ou modifie des documents Word (.docx) : rapport, devis, proposition, programme, cours, modèle à compléter. Use for Word/.docx generation, editing or templates."
---

# Génération de documents Word (.docx)

## Quand l'utiliser
- La personne demande un fichier Word, un .docx ou un modèle à compléter.
- Le document sera édité, relu ou commenté par d'autres (texte long, contrat, proposition, cours).
- Un fichier .docx est fourni et doit être modifié : le modifier dans son propre format, sur une copie.

Si le document demandé correspond à un gabarit du skill `training-architecture-templates` (proposition de formation, programme, cours apprenant/formateur, architecture logicielle), suivre d'abord sa structure.

Si un skill `docx` natif est disponible dans la session, le charger et suivre ses consignes en priorité.

## Démarche
1. **Cadrer** : public, objectif, langue, longueur, charte graphique (logo, couleurs, police). Sans charte : mise en page sobre.
2. **Rassembler le contenu d'abord** (texte, chiffres, structure), puis mettre en forme. Ne jamais inventer de chiffres ni de faits.
3. **Générer** avec `python-docx` (Python) ou `docx` (npm). Pour modifier un fichier existant : dézipper, modifier `word/document.xml`, rezipper, puis valider.
4. **Vérifier** (voir plus bas) puis livrer.

## Règles de construction
- Utiliser de vrais **styles** (Titre 1, Titre 2, Corps de texte, Liste) et jamais du gras ou des tailles appliqués à la main : la navigation et la table des matières en dépendent.
- Format de page : **A4** par défaut (marges 2 cm), US Letter seulement si demandé.
- Listes : vraies listes (numérotation Word), jamais de caractères `•` saisis à la main.
- Tableaux : largeur de colonnes explicite, ligne d'en-tête répétée sur chaque page, fond d'en-tête léger, bordures fines. Avec docx-js : `columnWidths` ET largeur de chaque cellule en DXA, `ShadingType.CLEAR` (jamais `SOLID`).
- Saut de page : toujours dans un paragraphe. Pas de `\n` dans un texte : un paragraphe par ligne.
- Images : préciser le type (`png`, `jpg`) et ajouter un texte alternatif.
- En-tête / pied de page : titre du document et numéro de page (« Page X sur Y »).
- Table des matières : uniquement sur les documents de plus de 5 à 6 pages, avec les titres natifs.
- Modèle à compléter : champs entre crochets et repérables (`[NOM_CLIENT]`), consignes de rédaction en italique gris, à supprimer une fois remplies.

## Vérification obligatoire
1. Convertir en PDF : `soffice --headless --convert-to pdf fichier.docx`.
2. Rasteriser les pages : `pdftoppm -jpeg -r 100 fichier.pdf page`, puis les regarder.
3. Chercher : texte qui déborde, tableaux coupés, titres orphelins en bas de page, polices de remplacement, images déformées.
4. Relire l'orthographe, les noms propres, les dates et les montants.
5. Corriger puis revérifier si un défaut est trouvé.

## Livraison
- Nom de fichier explicite, sans espaces ni accents : `proposition-formation-symfony-2026-10.docx`.
- Livrer le fichier avec une ligne de contexte : contenu, hypothèses, champs à compléter.
- Proposer au plus une suite logique (ex. version PDF pour signature).

## Cible PHP / Symfony
Si le document doit être produit par l'application elle-même : **PHPWord**, avec gabarits `.docx` séparés du code, valeurs injectées par `setValue('CHAMP', ...)`, génération dans un service dédié et injectable.