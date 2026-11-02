---
name: "training-architecture-templates"
description: "Structure des gabarits : proposition commerciale de formation, programme de formation, cours apprenant et formateur, document d'architecture logicielle PHP/Symfony. Use for training or architecture documents."
---

# Gabarits : formation et architecture logicielle

Ce skill définit le **fond** (sections, contenus attendus) de cinq documents récurrents. La **forme** (fichier) est produite avec le skill de format adapté : `office-docx-generator` (par défaut), `office-pdf-generator` (version figée), `office-xlsx-generator` (budgets, plannings), `office-pptx-generator` (support projeté).

## Règles communes
- Format par défaut : Word A4, champs à compléter entre crochets `[CHAMP]`, consignes en italique gris à supprimer.
- Ne jamais inventer d'informations propres au client, au formateur ou à l'organisme (n° de déclaration d'activité, tarifs, certifications) : laisser un champ `[À COMPLÉTER]`.
- Si le contexte (thème, client, durée, pile technique) est donné, préremplir intelligemment ; sinon laisser le gabarit générique.
- Verbes d'action mesurables pour tous les objectifs (identifier, implémenter, comparer, déboguer…), jamais « comprendre » ou « connaître » seuls.

---

## 1. Proposition commerciale de formation
Sections :
1. Page de garde : titre, client, référence, date, durée de validité, coordonnées.
2. Contexte et besoin du client.
3. Compréhension des enjeux.
4. Objectif d'évolution (ce que l'organisation ou les personnes sauront faire évoluer).
5. Notre proposition : intitulé, objectif de formation, cibles, prérequis.
6. Programme synthétique par modules.
7. Durée et modalités : dates, lieu ou distanciel, effectif, moyens pédagogiques.
8. Évaluation et suivi : positionnement, évaluations, attestation, indicateurs de satisfaction.
9. Intervenant : profil et expérience.
10. Conditions financières : tableau (poste, quantité, prix unitaire HT, total HT, TVA, TTC), modalités de paiement.
11. Conditions générales : annulation, report, propriété intellectuelle, confidentialité, données personnelles.
12. Accessibilité : référent handicap et adaptations possibles.
13. Bon pour accord : date, nom, signature et cachet du client.

## 2. Programme de formation (action de formation)
Sections :
1. Fiche d'identité : intitulé, référence, version, date de mise à jour.
2. **Objectif d'évolution** : changement attendu dans le poste ou l'organisation après la formation.
3. **Objectif de formation** : finalité globale de l'action.
4. **Cibles** : public concerné, prérequis, effectif min/max.
5. **Durée et modalités** : durée totale, répartition, dates, lieu, présentiel/distanciel/mixte, tarif, délai d'accès.
6. **Objectifs pédagogiques** : « À l'issue de la formation, le stagiaire sera capable de… », tableau (objectif, niveau de maîtrise, mode d'évaluation).
7. Contenu du programme : modules avec titre, durée, contenus.
8. **Scénario pédagogique** : tableau par séquence (horaire, durée, objectif, activité du formateur, activité de l'apprenant, méthode, support, évaluation).
9. Moyens pédagogiques et techniques.
10. Modalités d'évaluation et de suivi.
11. Accessibilité et contacts.

## 3. Cours — version apprenant
Sections : titre, module, durée ; objectifs de la séance ; prérequis ; plan ; parties de cours avec exemples et blocs de code ; encadrés « À retenir » ; exercices (énoncés sans corrigés) ; quiz de fin de partie ; synthèse ; glossaire ; ressources complémentaires ; espace de notes.

## 4. Cours — version formateur
Même trame que la version apprenant (même numérotation), plus un guide d'animation : timing par partie, consignes d'animation, questions à poser, erreurs fréquentes, points de vigilance, corrigés détaillés des exercices, réponses du quiz, variantes (public rapide / lent), matériel et préparation. Visuellement distinct (bandeau « Version formateur », encadrés de couleur).

## 5. Document d'architecture logicielle (PHP / Apache / Symfony / MySQL / GitHub / API)
Sections :
1. Page de garde, historique des versions.
2. Introduction : objet, périmètre, public, glossaire.
3. Contexte, exigences fonctionnelles et non fonctionnelles, contraintes, hypothèses.
4. Vue d'ensemble : diagramme d'architecture.
5. Pile technique : tableau (composant, technologie, version, rôle) — PHP, Apache + PHP-FPM, Symfony, MySQL, GitHub + Actions, API.
6. Architecture applicative Symfony : contrôleurs, services, entités Doctrine, repositories, DTO, voters, Messenger ; arborescence du projet.
7. Architecture des données : modèle, tableau des entités, migrations Doctrine, sauvegardes.
8. API : style (REST/JSON), versionnage, authentification (JWT/OAuth2), format des erreurs, tableau des endpoints, documentation OpenAPI.
9. **Flux de données** : tableau (id, source, destination, donnée, protocole, fréquence, format, sécurité) et diagramme du parcours d'une requête.
10. Infrastructure et déploiement : Apache (vhost, HTTPS), PHP-FPM, environnements, CI/CD GitHub Actions (lint, PHPStan, tests, build, déploiement), stratégie de branches, gestion des secrets.
11. Sécurité : authentification, autorisations, OWASP, en-têtes HTTP, données personnelles.
12. Qualité et tests : PHPUnit, analyse statique, revue de code.
13. Observabilité : logs (Monolog), supervision, alertes.
14. Performance et scalabilité : OPcache, cache HTTP, index MySQL.
15. Décisions d'architecture (ADR) et risques : tableau (décision, alternatives, justification, date).
16. Annexes.