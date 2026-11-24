from pathlib import Path

content = r"""# GMI — Module 07 : Gestion de la maintenance préventive

**Version du document :** 1.0  
**Statut :** Cadrage initial — avant réalisation  
**Classeur de travail :** `GMI_Interventions_Version_0.3.xlsm`  
**Projet :** Gestion de Maintenance Industrielle (GMI)

---

## 1. Finalité du module

Concevoir et intégrer au GMI un module professionnel de gestion de la maintenance préventive industrielle. Il devra permettre de définir les opérations préventives, construire les plans de maintenance par équipement, calculer les échéances, planifier et suivre les interventions, générer les ordres de travail associés, conserver leur historique et piloter l'activité au moyen d'un tableau de bord.

Le module doit s'intégrer aux fonctionnalités déjà développées dans le module 6 (gestion des interventions), sans créer un système parallèle ni dégrader les fonctions existantes.

## 2. Objectif général

Mettre en place dans Excel un système structuré permettant de planifier, suivre, contrôler et analyser les opérations de maintenance préventive des équipements industriels afin de réduire les défaillances, maîtriser les échéances et améliorer la disponibilité des installations.

## 3. Objectifs spécifiques et critères de validation

| Réf. | Objectif | Résultat / critère de validation | Statut |
|---|---|---|---|
| OP01 | Comprendre les formes de maintenance préventive | Distinguer maintenance systématique, conditionnelle et prévisionnelle, et comprendre leur usage | Validé en cours |
| OP02 | Définir les plans de maintenance | Associer plusieurs opérations à un équipement avec des paramètres indépendants | À réaliser |
| OP03 | Créer le référentiel des opérations | Disposer d'une bibliothèque structurée, réutilisable et sans doublons de codes | À réaliser |
| OP04 | Définir les périodicités et déclencheurs | Gérer les périodicités calendaires et, lorsque les données existent, les heures de fonctionnement ou cycles | À réaliser |
| OP05 | Construire le planning préventif | Calculer et afficher les prochaines échéances à partir des plans actifs | À réaliser |
| OP06 | Suivre les échéances | Identifier les interventions à venir, dues, en retard, suspendues ou reportées | À réaliser |
| OP07 | Gérer l'exécution | Créer et suivre des OT préventifs, puis enregistrer les comptes rendus | À réaliser |
| OP08 | Gérer les reports et annulations | Exiger un motif et conserver une trace des changements | À réaliser |
| OP09 | Conserver l'historique | Retrouver les opérations réalisées et leur historique par équipement et par plan | À réaliser |
| OP10 | Calculer les indicateurs | Produire des indicateurs fiables de réalisation, ponctualité, retard et charge | À réaliser |
| OP11 | Automatiser et sécuriser le fonctionnement | Développer les macros, contrôles de saisie et traitements d'erreurs nécessaires | À réaliser |
| OP12 | Tester, documenter et archiver | Réaliser les tests fonctionnels, rédiger la procédure et archiver la version validée | À réaliser |

**Règle de suivi :** un objectif ne sera déclaré terminé qu'après réalisation pratique et vérification du résultat attendu. Le statut « Validé en cours » d'OP01 correspond aux trois questions de compréhension réussies ; les autres éléments pédagogiques de cet objectif pourront être approfondis si nécessaire.

## 4. Architecture fonctionnelle prévisionnelle

Les feuilles suivantes sont proposées. Leur structure détaillée (colonnes, tables Excel, validations, formules et relations) sera définie au moment de leur création.

| N° | Feuille proposée | Rôle principal |
|---|---|---|
| 1 | `OPERATIONS_PREVENTIVES` | Bibliothèque des opérations : code, désignation, description, type, durée estimée, compétence, outils et observations |
| 2 | `PLANS_PREVENTIFS` | Association entre équipements et opérations ; paramètres de périodicité, déclenchement, dates de référence, responsable, statut et consignes |
| 3 | `PLANNING_PREVENTIF` | Programmation des échéances et visualisation des interventions planifiées |
| 4 | `ECHEANCES_PREVENTIVES` | Suivi opérationnel des échéances à venir, dues, en retard et reportées |
| 5 | `HISTORIQUE_PREVENTIF` | Traçabilité des échéances, exécutions, reports, annulations et changements de programmation |
| 6 | `RESSOURCES_PREVENTIVES` | Référentiel ou suivi des ressources utiles : compétences, techniciens, outils et moyens nécessaires |
| 7 | `TABLEAU_DE_BORD_PREVENTIF` | Indicateurs, graphiques et filtres de pilotage de la maintenance préventive |

Cette architecture est un cadrage initial. Les feuilles pourront être regroupées ou ajustées si la conception détaillée révèle un meilleur modèle de données. Il faudra éviter de stocker plusieurs fois la même information lorsqu'une feuille de référence peut être utilisée.

## 5. Intégration au GMI existant

Le module préventif devra réutiliser les feuilles et mécanismes existants lorsque cela est pertinent :

- `EQUIPEMENTS` : référentiel des équipements.
- `ORDRES_TRAVAIL` : traitement des OT préventifs et correctifs.
- `COMPTES_RENDU_INTERVENTION` : comptes rendus d'exécution.
- `COMPTEURS_GMI` : numérotation des documents, selon les règles retenues.
- `HISTORIQUE_OT` : historique des changements de statut des OT.
- `MENU_GMI` : accès centralisé aux fonctions.
- `TABLEAU_DE_BORD_INTERVENTIONS` : pilotage des interventions existantes.

### Principe de circulation des données

**Plan préventif → Échéance → Ordre de travail préventif → Exécution → Compte rendu → Historique et indicateurs.**

Un OT devra être clairement identifiable par son origine (préventive ou corrective). La méthode exacte d'identification sera arrêtée avant la modification de la feuille `ORDRES_TRAVAIL` et des macros du module 6.

Les macros existantes devront être examinées avant toute modification. Les fonctionnalités validées du module 6 devront rester opérationnelles.

## 6. Fonctions prévues dans le menu `MENU_GMI`

Une rubrique « MAINTENANCE PRÉVENTIVE » sera ajoutée au menu central. Les commandes envisagées sont :

1. Créer une opération préventive.
2. Modifier ou consulter une opération.
3. Créer un plan préventif.
4. Modifier, activer ou désactiver un plan.
5. Générer ou actualiser le planning.
6. Consulter les échéances.
7. Générer un OT préventif.
8. Reporter une échéance avec motif.
9. Annuler une programmation avec motif.
10. Consulter l'historique préventif.
11. Ouvrir le tableau de bord préventif.

Les commandes définitives seront retenues en fonction des fonctionnalités réellement développées et testées.

## 7. Tableau de bord prévisionnel

Le tableau de bord devra notamment présenter :

- Nombre de plans préventifs actifs.
- Nombre d'interventions prévues sur la période.
- Nombre d'interventions réalisées.
- Nombre d'interventions à venir.
- Nombre d'interventions dues et en retard.
- Nombre d'interventions reportées ou annulées.
- Taux de réalisation du programme préventif.
- Taux de respect des dates planifiées.
- Charge préventive prévue et durée réellement consommée, si les données sont disponibles.

Filtres envisagés : année, mois/période, équipement, famille ou service, type d'opération et statut.

Les définitions mathématiques des indicateurs seront documentées avant leur implémentation afin d'éviter les taux ambigus. Les interventions annulées ou reportées devront être traitées explicitement dans les dénominateurs.

## 8. Cheminement pédagogique et technique provisoire

Le parcours ci-dessous constitue la feuille de route de réalisation. L'ordre pourra être ajusté selon les dépendances découvertes pendant les tests.

### Phase A — Fondamentaux et conception
1. Étudier les formes de maintenance préventive : systématique, conditionnelle et prévisionnelle.
2. Définir les données nécessaires à un plan préventif.
3. Arrêter le modèle de données et les relations entre équipements, opérations, plans et échéances.

### Phase B — Référentiels et plans
4. Créer `OPERATIONS_PREVENTIVES`.
5. Créer `PLANS_PREVENTIFS`.
6. Ajouter les validations de données, listes déroulantes, contrôles de cohérence et règles contre les doublons.
7. Définir les périodicités calendaires et les paramètres de déclenchement par compteur lorsque disponibles.

### Phase C — Calcul et planification
8. Créer le mécanisme de calcul des prochaines dates d'échéance.
9. Construire `PLANNING_PREVENTIF`.
10. Construire `ECHEANCES_PREVENTIVES`.
11. Gérer les changements de périodicité, les dates de référence, les reports et les échéances manquées sans perdre la traçabilité.

### Phase D — Exécution et intégration au module 6
12. Définir comment distinguer les OT préventifs des OT correctifs.
13. Adapter avec prudence `ORDRES_TRAVAIL` et les macros nécessaires.
14. Générer un OT préventif à partir d'une échéance, sans créer de doublon.
15. Réutiliser le processus de réalisation et de compte rendu existant.
16. Enregistrer les événements dans l'historique préventif et, lorsque pertinent, dans `HISTORIQUE_OT`.

### Phase E — Pilotage
17. Définir précisément les formules des indicateurs.
18. Créer `TABLEAU_DE_BORD_PREVENTIF`, ses graphiques et ses filtres.
19. Intégrer les accès au menu `MENU_GMI`.

### Phase F — Tests, documentation et archivage
20. Tester les échéances mensuelles, trimestrielles et annuelles.
21. Tester les changements de périodicité, les reports, les annulations et les retards.
22. Tester la génération d'OT et empêcher les doublons.
23. Vérifier les comptes rendus, historiques et indicateurs.
24. Vérifier que les fonctions du module 6 continuent de fonctionner.
25. Rédiger la procédure d'utilisation et le support de cours.
26. Archiver le classeur et la documentation dans Git/GitHub.

### Phase G — Protections
27. Après validation fonctionnelle et apprentissage, protéger les feuilles et cellules adaptées.
28. Protéger le projet VBA et tester les droits d'utilisation.
29. Documenter les protections et les modalités de maintenance du classeur.

**Important :** les protections ne seront pas mises en place au début. Elles seront étudiées et appliquées à la fin, conformément à notre progression pédagogique.

## 9. Principes de conception à respecter

- Une opération préventive doit avoir un identifiant unique et stable.
- Un équipement peut être associé à plusieurs opérations.
- Une même opération peut être réutilisée dans plusieurs plans si cela est pertinent.
- La périodicité appartient à l'association équipement-opération (le plan), et non uniquement à la bibliothèque des opérations.
- Une échéance doit être identifiable et ne doit pas générer plusieurs OT par inadvertance.
- Les reports et annulations doivent être justifiés et traçables.
- Une intervention réalisée doit être reliée à son OT et à son compte rendu.
- Les dates prévues, dates réelles et dates de prochaine échéance doivent rester distinctes.
- Les calculs doivent être contrôlables et les macros doivent gérer les erreurs.
- Les fonctions existantes du GMI doivent être préservées.
- Le système doit rester utilisable dans Excel sans dépendre d'un service cloud ou d'un abonnement externe.

## 10. État d'avancement au démarrage

| Élément | État |
|---|---|
| Cadrage du module et objectif général | Défini |
| Objectifs spécifiques OP01 à OP12 | Définis |
| Distinction systématique / conditionnelle / prévisionnelle | Exercée et réponses correctes |
| Architecture fonctionnelle prévisionnelle | Définie |
| Intégration au module 6 | Principe défini, conception détaillée à faire |
| Cheminement provisoire | Défini |
| Création des feuilles du module 7 | Pas encore commencée |
| Automatisations et tableau de bord | À développer |
| Tests, procédure et archivage final du module | À réaliser |
| Protections | Reportées à la phase finale |

## 11. Prochaine étape de travail

Commencer la Phase B par la création de la feuille `OPERATIONS_PREVENTIVES` avec les colonnes suivantes :

| Colonne | Intitulé |
|---|---|
| A | CODE_OPERATION |
| B | DESIGNATION_OPERATION |
| C | DESCRIPTION |
| D | TYPE_OPERATION |
| E | DUREE_ESTIMEE_MIN |
| F | COMPETENCE_REQUISE |
| G | OUTILS_NECESSAIRES |
| H | OBSERVATIONS |

Cette feuille sera le référentiel des opérations. La périodicité ne sera pas stockée comme une propriété générale de l'opération : elle sera définie dans `PLANS_PREVENTIFS`, car une même opération peut avoir des fréquences différentes selon l'équipement et les conditions d'exploitation.

---

**Fin du document de cadrage initial — Module 07.**
"""
path = Path("/mnt/data/Cadrage_Module_07_GMI_Maintenance_Preventive.md")
path.write_text(content, encoding="utf-8")
print(f"Document créé : {path}")
