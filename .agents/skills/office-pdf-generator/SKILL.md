---
name: "office-pdf-generator"
description: "Produit des PDF mis en page (rapport, facture, programme, fiche) depuis HTML/CSS ou code, ou manipule des PDF existants. Use for creating, merging or exporting PDF files."
---

# Génération de documents PDF

## Quand l'utiliser
- Document final, non modifiable, à imprimer, signer ou archiver.
- Export d'un Word, d'un contenu HTML ou de données en rapport ou facture.
- Manipulation d'un PDF existant : fusion, découpe, rotation, filigrane, remplissage de formulaire, extraction de texte ou de tableaux.

Si le document correspond à un gabarit du skill `training-architecture-templates`, suivre sa structure. Si un skill `pdf` natif est disponible, le charger en priorité.

## Choisir la méthode
| Besoin | Outil |
|---|---|
| Document mis en page riche (rapport, programme, devis) | HTML + CSS, converti avec **WeasyPrint** |
| Document très structuré, positionnement précis (facture, étiquette) | **ReportLab** |
| Export d'un Word / Excel / PowerPoint | LibreOffice : `soffice --headless --convert-to pdf` |
| Fusion, découpe, rotation, filigrane | **pypdf** |
| PDF scanné à rendre cherchable | OCR (`ocrmypdf`) |

## Démarche
1. Cadrer : public, objectif, langue, longueur, charte.
2. Rassembler le contenu avant la mise en forme ; ne jamais inventer de chiffres.
3. Générer le fichier avec l'outil adapté.
4. Vérifier, puis livrer.

## Règles de construction
- Format **A4** par défaut, marges de 2 cm (`@page { size: A4; margin: 2cm; }` en CSS).
- Polices incorporées ; une police pour les titres, une pour le corps ; corps entre 10 et 11 pt.
- Numéros de page et titre courant en pied ou en tête de page.
- Titres hiérarchisés, `page-break-inside: avoid` sur les tableaux courts et les blocs de code, `break-after: avoid` sur les titres.
- Tableaux : en-tête répété (`thead`), largeur 100 %, alignement des montants à droite.
- Marque-pages (signets) pour les documents de plus de 5 pages ; métadonnées (titre, auteur) renseignées, sans donnée sensible superflue.
- Accessibilité : contrastes suffisants, texte réel (pas de texte en image), texte alternatif sur les images.
- Ne jamais modifier l'original d'un PDF fourni : travailler sur une copie.

## Vérification obligatoire
1. Rasteriser quelques pages : `pdftoppm -jpeg -r 100 fichier.pdf page`, puis les regarder.
2. Chercher : débordements, tableaux coupés, titres orphelins, caractères manquants (accents), images déformées.
3. Vérifier que le texte est sélectionnable (`pdftotext`) et que le nombre de pages est celui attendu.
4. Relire montants, dates et noms propres.

## Livraison
- Nom explicite : `programme-formation-symfony-v1.pdf`.
- Une ligne de contexte avec le fichier ; au plus une suite logique proposée.

## Cible PHP / Symfony
Si le PDF est produit par l'application : **Dompdf** ou **mPDF** depuis un template Twig, ou **KnpSnappy** (wkhtmltopdf). Garder le gabarit Twig séparé du code, générer dans un service dédié, prévoir polices et images en chemins locaux.