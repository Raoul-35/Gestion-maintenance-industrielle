# MODULE 5 — GESTION DU PARC D'ÉQUIPEMENTS INDUSTRIELS

## Leçon 1 — Principes fondamentaux de la gestion d'un parc d'équipements

### 1. Objectifs pédagogiques

À la fin de cette leçon, l'apprenant doit être capable de :

- Définir un parc d'équipements industriels.

- Expliquer l'importance de l'identification des équipements.

- Distinguer le code équipement de la désignation.

- Différencier le service de la localisation.

- Identifier les informations nécessaires à une fiche équipement.

- Expliquer le rôle de la base de données des équipements dans la gestion de la maintenance.

### 2. Définition d'un parc d'équipements industriels

Un parc d'équipements industriels désigne l'ensemble des machines, installations et dispositifs techniques utilisés par une entreprise pour assurer ses activités.

Il peut comprendre :

- Les moteurs électriques ;

- Les pompes industrielles ;

- Les compresseurs ;

- Les ventilateurs ;

- Les chaudières ;

- Les convoyeurs ;

- Les groupes électrogènes ;

- Les transformateurs ;

- Les équipements d'instrumentation.

La gestion du parc consiste à identifier, répertorier, caractériser et suivre ces équipements tout au long de leur cycle de vie.

### 3. Identification des équipements

Chaque équipement doit posséder un identifiant unique afin d'éviter toute confusion dans le système de gestion.

Exemple :

| **Code équipement** | **Désignation** |
| :-: | :-: |
| MOT-001 | Moteur asynchrone |
| MOT-002 | Moteur asynchrone |
| PMP-001 | Pompe centrifuge |
| CMP-001 | Compresseur |

Deux moteurs peuvent avoir la même marque, le même modèle et la même puissance, mais doivent posséder des codes équipements différents.

Un bon code équipement doit être unique, stable, lisible et durable.

**À retenir :** le code identifie individuellement l'équipement ; la désignation indique sa nature.

### 4. Les informations d'une fiche équipement

Une fiche équipement rassemble les données nécessaires à l'identification, à la connaissance technique et au suivi d'une machine.

#### 4.1 Identification technique

- Code équipement ;

- Désignation ;

- Marque ;

- Modèle ;

- Numéro de série.

#### 4.2 Informations organisationnelles

- Service ;

- Localisation ;

- Installation concernée.

Le service représente l'entité organisationnelle responsable ou utilisatrice de l'équipement.

La localisation représente son emplacement physique.

#### 4.3 Caractéristiques techniques

Exemples :

- Puissance nominale ;

- Tension nominale ;

- Courant nominal ;

- Vitesse nominale ;

- Pression nominale ;

- Débit nominal.

Les caractéristiques à enregistrer dépendent de la nature de l'équipement.

#### 4.4 Informations de gestion

- Date de mise en service ;

- État de l'équipement ;

- Observations.

### 5. Les états d'un équipement

Les états possibles peuvent notamment être :

| **État** | **Signification** |
| :-: | :-: |
| En service | Équipement disponible pour son utilisation |
| En panne | Équipement présentant une défaillance |
| En maintenance | Équipement pris en charge pour une intervention |
| À l'arrêt | Équipement arrêté, sans nécessairement être en panne |
| Réformé | Équipement retiré définitivement du parc |

Un équipement à l'arrêt n'est donc pas nécessairement en panne.

Cette distinction est importante pour produire des indicateurs de maintenance fiables.

### 6. Structuration des données

Une base de données d'équipements doit être organisée de manière cohérente.

Chaque équipement doit être représenté par un enregistrement distinct.

Chaque caractéristique doit être placée dans une colonne appropriée.

Il faut éviter :

- Les codes équipements en double ;

- Les désignations incohérentes ;

- Les informations mélangées dans une même colonne ;

- Les unités de mesure non précisées ;

- Les valeurs inventées lorsque les informations sont inconnues.

Une information inconnue doit rester vide ou être représentée par une valeur normalisée, selon les règles définies pour l'application.

### 7. Importance pour la maintenance industrielle

Une base de données correctement structurée permet notamment de :

- Identifier rapidement les équipements ;

- Préparer les interventions ;

- Consulter les caractéristiques techniques ;

- Suivre les pannes ;

- Constituer l'historique des interventions ;

- Organiser la maintenance préventive ;

- Suivre les coûts de maintenance ;

- Calculer les indicateurs de performance.

Elle constitue donc l'une des bases d'un système de gestion de maintenance assistée par ordinateur (GMAO).

### 8. Application au projet GMI

Dans notre classeur de gestion de maintenance industrielle, la feuille `EQUIPEMENTS` contient actuellement les champs suivants :

| **Colonne** | **Champ** |
| :-: | :-: |
| A | CODE\_EQUIPEMENT |
| B | DESIGNATION |
| C | SERVICE |
| D | LOCALISATION |
| E | MARQUE |
| F | MODELE |
| G | NUMERO\_SERIE |
| H | PUISSANCE\_KW |
| I | DATE\_MISE\_EN\_SERVICE |
| J | ETAT |
| K | OBSERVATIONS |

Cette structure constitue la base de notre registre des équipements.

Elle sera progressivement exploitée pour construire des fonctionnalités de consultation, de suivi et de gestion de la maintenance.

### 9. Synthèse

La gestion du parc d'équipements commence par une identification rigoureuse et une structuration cohérente des informations.

Une fiche équipement bien conçue permet de retrouver rapidement les caractéristiques d'une machine et facilite toutes les opérations ultérieures de maintenance.

**Notion essentielle :** la qualité des informations enregistrées dans le parc conditionne la fiabilité des analyses et des décisions de maintenance.

