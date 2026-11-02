---
name: "office-pptx-generator"
description: "Crée ou modifie des présentations PowerPoint (.pptx) : pitch, support de formation, restitution. Use for PowerPoint/.pptx/slides file generation."
---

# Génération de présentations PowerPoint (.pptx)

## Quand l'utiliser
- La personne veut un support présenté devant un public : pitch, support de formation, restitution d'analyse, soutenance.
- Un fichier .pptx ou .potx est fourni à modifier, compléter ou utiliser comme modèle.
- Conversion d'un contenu (cours, rapport) en diaporama.

Pour un support de formation, s'appuyer sur la structure du skill `training-architecture-templates` (programme, scénario pédagogique). Si un skill `pptx` natif est disponible, le charger en priorité.

## Démarche
1. **Cadrer** : public, objectif (informer, convaincre, former), durée de la présentation, charte.
2. **Bâtir le fil narratif** avant les slides : 1 slide ≈ 1 à 2 minutes de parole.
3. **Rassembler le contenu** (chiffres, schémas, citations sourcées) ; ne jamais inventer de données.
4. **Générer** avec `python-pptx` ou `pptxgenjs`.
5. **Vérifier**, puis livrer.

## Règles de construction
- **Un message par slide** ; le titre est la conclusion (« Le temps de traitement baisse de 40 % »), pas un simple intitulé (« Résultats »).
- Peu de texte : 3 à 5 puces courtes maximum, ou un visuel, un chiffre clé, un schéma.
- Corps de texte ≥ 18 pt, titres ≥ 28 pt ; contrastes forts ; pas plus de 2 polices.
- Mise en page cohérente via le **masque de diapositives** : mêmes marges, mêmes positions de titres.
- Structure type : titre, contexte / enjeu, plan, sections, synthèse, prochaines étapes, contact.
- Graphiques natifs (modifiables) plutôt qu'images quand c'est possible ; légende et source sous chaque chiffre.
- **Notes de l'orateur** renseignées : message, transitions, timing.
- Texte alternatif sur les images ; numéros de slide.
- Pour un support de formation : alterner exposition, démonstration, exercice et synthèse, et marquer clairement les slides d'exercices.

## Vérification obligatoire
1. Convertir en PDF : `soffice --headless --convert-to pdf fichier.pptx` ; rasteriser : `pdftoppm -jpeg -r 80 fichier.pdf slide`, puis regarder chaque slide.
2. Chercher : texte qui déborde, chevauchements, images déformées, polices de remplacement, slides surchargées.
3. Vérifier la cohérence entre le nombre de slides et la durée annoncée.
4. Relire orthographe, chiffres et sources.

## Livraison
- Nom explicite : `formation-symfony-support-v1.pptx`.
- Livrer avec une ligne de contexte : nombre de slides, durée estimée, éléments à compléter.
- Proposer au plus une suite logique (ex. export PDF pour diffusion).

## Cible PHP / Symfony
Si le diaporama est produit par l'application : **PhpPresentation** (PHPOffice), avec gabarit `.pptx` préparé à la main, généré dans un service dédié. Les capacités sont plus limitées que python-pptx : prévoir des mises en page simples.