# LEÇON 06 — CONCEPTION DES FICHES TECHNIQUES DÉTAILLÉES DES MOTEURS

## 1. Objectifs de la leçon

À la fin de cette leçon, nous devons être capables de :

- Distinguer le registre des équipements d'une fiche technique détaillée.
- Identifier les caractéristiques propres aux moteurs électriques.
- Organiser les caractéristiques techniques dans une feuille dédiée.
- Relier automatiquement une fiche technique à son équipement.
- Utiliser des listes déroulantes pour contrôler la saisie.
- Appliquer des formats adaptés aux différentes données techniques.
- Préparer une structure exploitable pour la gestion de maintenance.

## 2. Rappel : registre et fiche technique

Le registre des équipements contient les informations générales nécessaires à l'identification et à la gestion du parc industriel.

Exemples :
- Code équipement ;
- Désignation ;
- Service ;
- Localisation ;
- Marque ;
- Modèle ;
- Numéro de série ;
- Puissance ;
- État.

La fiche technique détaillée complète ces informations avec des caractéristiques propres à une catégorie d'équipements.

Pour un moteur électrique, on peut notamment retrouver :
- La tension nominale ;
- Le courant nominal ;
- La fréquence ;
- La vitesse nominale ;
- Le facteur de puissance ;
- Le rendement ;
- Le nombre de pôles ;
- Le type de montage ;
- La classe d'isolation ;
- L'indice de protection ;
- Le type de service.

**Principe important :** le registre répond à la question « Quel est cet équipement et où se trouve-t-il ? ». La fiche technique répond à la question « Quelles sont ses caractéristiques techniques détaillées ? ».

## 3. Organisation des feuilles du classeur GMI

Deux feuilles ont des rôles complémentaires.

### 3.1. FICHES_TECHNIQUES

Cette feuille constitue un index général des fiches techniques.

Elle contient :
- CODE_EQUIPEMENT ;
- DESIGNATION ;
- FAMILLE ;
- SOUS_FAMILLE ;
- MARQUE ;
- MODELE ;
- NUMERO_SERIE ;
- DATE_FICHE.

Elle permet de retrouver rapidement les informations principales d'un équipement.

### 3.2. DETAIL_MOTEURS

Cette feuille est réservée aux caractéristiques détaillées des moteurs électriques.

Sa structure est la suivante :

| Colonne | Champ | Signification |
|---|---|---|
| A | CODE_EQUIPEMENT | Identifiant de l'équipement |
| B | DESIGNATION | Désignation du moteur |
| C | MARQUE | Marque commerciale |
| D | MODELE | Référence du modèle |
| E | NUMERO_SERIE | Numéro de série |
| F | PUISSANCE_NOMINALE_KW | Puissance nominale en kW |
| G | TENSION_NOMINALE_V | Tension nominale |
| H | COURANT_NOMINAL_A | Courant nominal |
| I | FREQUENCE_HZ | Fréquence nominale |
| J | VITESSE_NOMINALE_TR_MIN | Vitesse nominale en tr/min |
| K | FACTEUR_PUISSANCE | Facteur de puissance cos φ |
| L | RENDEMENT_POURCENT | Rendement en pourcentage |
| M | NOMBRE_POLES | Nombre de pôles |
| N | TYPE_MONTAGE | Type de montage mécanique |
| O | CLASSE_ISOLATION | Classe thermique d'isolation |
| P | INDICE_PROTECTION_IP | Protection contre les corps solides et l'eau |
| Q | TYPE_SERVICE | Régime de fonctionnement |
| R | FABRICANT | Fabricant du moteur |
| S | OBSERVATIONS_TECHNIQUES | Informations complémentaires |

## 4. Comprendre quelques caractéristiques essentielles

### 4.1. Puissance nominale

La puissance nominale d'un moteur correspond à la puissance mécanique utile indiquée sur sa plaque signalétique.

Elle est généralement exprimée en kilowatts (kW).

### 4.2. Tension nominale

La tension nominale indique les tensions d'alimentation prévues par le constructeur.

Un moteur triphasé peut, par exemple, porter l'indication 230/400 V. Cette indication doit être interprétée en tenant compte du couplage étoile ou triangle indiqué sur la plaque.

### 4.3. Courant nominal

Le courant nominal est le courant absorbé dans les conditions nominales de fonctionnement.

Il dépend notamment de la tension, de la puissance, du rendement et du facteur de puissance.

### 4.4. Fréquence

La fréquence nominale est généralement exprimée en hertz (Hz).

Les indications 50 Hz et 60 Hz peuvent apparaître sur certaines plaques signalétiques.

### 4.5. Vitesse nominale

La vitesse nominale correspond à la vitesse de rotation du moteur dans ses conditions nominales de fonctionnement.

Elle s'exprime en tours par minute (tr/min).

### 4.6. Facteur de puissance

Le facteur de puissance, généralement noté cos φ, représente le déphasage entre la tension et le courant dans les conditions considérées.

Dans notre classeur, il est enregistré sous forme de nombre décimal compris entre 0 et 1.

### 4.7. Rendement

Le rendement représente le rapport entre la puissance utile fournie et la puissance absorbée.

Il est exprimé en pourcentage.

Dans notre classeur, nous avons choisi d'enregistrer une valeur numérique comprise entre 0 et 100. Par exemple, 90 signifie 90 %.

### 4.8. Nombre de pôles

Le nombre de pôles est une caractéristique électromagnétique du moteur.

Les valeurs courantes étudiées dans notre liste sont 2, 4, 6 et 8 pôles.

### 4.9. Type de montage

Le type de montage décrit la disposition mécanique du moteur : fixation par pattes, fixation par bride ou combinaison des deux.

### 4.10. Classe d'isolation

La classe d'isolation caractérise la tenue thermique du système isolant des enroulements.

### 4.11. Indice de protection IP

L'indice IP caractérise le degré de protection de l'enveloppe contre la pénétration de corps solides et d'eau.

### 4.12. Type de service

Le type de service décrit les conditions de fonctionnement prévues pour le moteur.

Exemple : S1 correspond à un service continu.

## 5. Liaison automatique avec le registre

Le champ CODE_EQUIPEMENT constitue la clé de liaison entre DETAIL_MOTEURS et EQUIPEMENTS.

Lorsqu'un code est sélectionné dans la colonne A, les informations générales correspondantes sont récupérées automatiquement.

Formule utilisée en B2 :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;2;0);"")

Explication :
- A2 : code sélectionné ;
- EQUIPEMENTS.$A$2:$G$21 : plage de recherche ;
- 2 : numéro de la colonne contenant la désignation ;
- 0 : recherche exacte ;
- IFERROR : évite l'affichage d'une erreur lorsque le code n'est pas renseigné ou introuvable.

Les autres formules utilisées sont :

En C2, pour la marque :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;5;0);"")

En D2, pour le modèle :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;6;0);"")

En E2, pour le numéro de série :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;7;0);"")

Les formules de B2 à E2 ont ensuite été recopiées jusqu'à la ligne 21.

## 6. Contrôle de la saisie

Les listes déroulantes et validations limitent les erreurs de saisie.

Les contrôles mis en place sont les suivants :

| Champ | Contrôle |
|---|---|
| CODE_EQUIPEMENT | Liste des moteurs identifiés |
| NOMBRE_POLES | 2, 4, 6 ou 8 |
| TYPE_MONTAGE | B3, B5, B14, B35 ou B34 |
| CLASSE_ISOLATION | A, E, B, F ou H |
| INDICE_PROTECTION_IP | Liste de valeurs IP prédéfinies |
| TYPE_SERVICE | S1 à S10 |
| PUISSANCE_NOMINALE_KW | Valeur décimale strictement positive |
| VITESSE_NOMINALE_TR_MIN | Valeur décimale strictement positive |
| FACTEUR_PUISSANCE | Valeur comprise entre 0 et 1 |
| RENDEMENT_POURCENT | Valeur comprise entre 0 et 100 |

Les champs de tension, courant et fréquence sont formatés en texte afin de conserver les indications composées, par exemple 230/400 V ou 13,2/7,6 A.

Les champs numériques ont reçu des formats adaptés :
- Puissance : deux décimales ;
- Facteur de puissance : deux décimales ;
- Rendement : deux décimales ;
- Vitesse : nombre entier.

## 7. Mise en place pratique dans Calc

Les manipulations réalisées ont été :

1. Création de la feuille DETAIL_MOTEURS.
2. Saisie des en-têtes de colonnes A à S.
3. Création d'une liste de codes moteurs dans REFERENTIEL.
4. Mise en place de la liste déroulante des codes moteurs.
5. Création des formules de récupération automatique des informations générales.
6. Recopie des formules sur les lignes suivantes.
7. Mise en place des validations de données.
8. Application des formats numériques et textuels.
9. Mise en forme des en-têtes.
10. Ajustement automatique de la largeur des colonnes.
11. Activation du filtre automatique sur A1:S21.
12. Sélection des trois moteurs actuellement identifiés dans le registre.

Les codes moteurs actuellement recensés sont :
- EQP-0002 ;
- EQP-0013 ;
- EQP-0017.

Cette liste devra être actualisée si de nouveaux moteurs sont ajoutés au registre.

## 8. Précaution concernant les données techniques

Les caractéristiques techniques ne doivent jamais être inventées pour compléter une fiche.

Les sources à privilégier sont :
- La plaque signalétique du moteur ;
- La documentation technique du fabricant ;
- La fiche constructeur ;
- Les documents techniques fiables associés à l'équipement.

Lorsqu'une information n'est pas disponible ou n'a pas été vérifiée, il faut laisser le champ vide et rechercher ultérieurement la donnée correcte.

Il faut également distinguer les caractéristiques nominales du moteur des valeurs réellement mesurées pendant son fonctionnement.

## 9. Résultat attendu

À la fin de cette leçon, le classeur GMI dispose :
- D'un index général des fiches techniques ;
- D'une feuille dédiée aux caractéristiques détaillées des moteurs ;
- D'une liaison automatique entre les codes équipements et les informations générales ;
- De listes déroulantes et de contrôles de saisie ;
- D'une structure pouvant être étendue à d'autres familles d'équipements.

Cette organisation évite de placer toutes les caractéristiques techniques de toutes les familles dans une seule feuille trop large et difficile à maintenir.

## 10. Synthèse

Une fiche technique détaillée permet de conserver les caractéristiques propres à un équipement et de faciliter les opérations de maintenance, de diagnostic et de remplacement.

La clé de liaison entre le registre et les fiches détaillées est le CODE_EQUIPEMENT.

La qualité de la GMAO dépend de la cohérence des données, de leur traçabilité et de leur exactitude.
