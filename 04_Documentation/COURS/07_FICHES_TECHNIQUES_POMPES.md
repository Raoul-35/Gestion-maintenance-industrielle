# LEÇON 07 — CONCEPTION DES FICHES TECHNIQUES DES POMPES INDUSTRIELLES

## 1. Objectifs de la leçon

À la fin de cette leçon, nous devons être capables de :

- Expliquer pourquoi les fiches techniques doivent être adaptées aux familles d'équipements.
- Identifier les principales caractéristiques techniques d'une pompe industrielle.
- Distinguer les caractéristiques hydrauliques, mécaniques et électriques.
- Concevoir une feuille spécialisée dans LibreOffice Calc.
- Relier automatiquement une fiche technique au registre des équipements.
- Utiliser des listes déroulantes et des validations de données.
- Organiser les informations pour faciliter la gestion de maintenance.

## 2. Pourquoi créer des fiches techniques spécialisées ?

Les équipements industriels ne possèdent pas tous les mêmes caractéristiques.

Un moteur électrique est principalement caractérisé par sa puissance, sa tension, son courant, sa vitesse et son rendement.

Une pompe industrielle est caractérisée notamment par son débit, sa hauteur manométrique totale, sa pression et la nature du fluide transporté.

Un capteur industriel possède d'autres caractéristiques : grandeur mesurée, plage de mesure, précision et signal de sortie.

Une fiche technique unique contenant toutes les caractéristiques de toutes les familles deviendrait trop large et difficile à exploiter.

Nous adoptons donc une organisation spécialisée :

- DETAIL_MOTEURS : moteurs électriques ;
- DETAIL_POMPES : pompes industrielles ;
- DETAIL_CAPTEURS : capteurs industriels ;
- D'autres feuilles pourront être ajoutées selon les familles présentes dans le registre.

Le CODE_EQUIPEMENT constitue la clé de liaison entre le registre général et les fiches spécialisées.

## 3. Les principales caractéristiques d'une pompe industrielle

### 3.1. Débit nominal

Le débit représente le volume de fluide transporté par unité de temps.

Symbole : Q.

Unité retenue : m³/h.

Exemple pédagogique : une pompe ayant un débit de 25 m³/h transporte 25 mètres cubes de fluide par heure dans les conditions considérées.

### 3.2. Hauteur manométrique totale (HMT)

La HMT représente l'énergie totale communiquée au fluide par la pompe, exprimée sous forme d'une hauteur de liquide.

Symbole : HMT.

Unité : m.

La HMT tient compte notamment des différences de pression, de hauteur géométrique et de vitesse entre les points considérés.

Elle ne doit pas être confondue avec la hauteur géométrique seule.

### 3.3. Pression nominale

La pression est généralement exprimée en bar.

Il faut distinguer la pression de fonctionnement, la pression maximale admissible et les autres valeurs définies par le constructeur.

La signification exacte de la donnée doit être vérifiée dans la documentation technique.

### 3.4. Fluide pompé

Le fluide est la matière transportée par la pompe.

Exemples :
- Eau ;
- Huile ;
- Gasoil ;
- Essence ;
- Eau glycolée ;
- Produit chimique.

La compatibilité entre la pompe et le fluide est essentielle. Elle dépend notamment des matériaux, de la viscosité, de la température et de la compatibilité chimique.

### 3.5. Température du fluide

La température du fluide est exprimée en degrés Celsius (°C).

Elle permet de vérifier si les conditions d'utilisation respectent les limites admissibles de la pompe.

### 3.6. Densité et masse volumique

La masse volumique représente la masse d'un fluide par unité de volume.

Unité retenue : kg/m³.

Exemple : l'eau à environ 20 °C possède une masse volumique proche de 998 kg/m³.

La densité relative, au sens strict, est un rapport sans unité. Dans notre feuille, le champ M est donc nommé MASSE_VOLUMIQUE_KG_M3 plutôt que DENSITE_FLUIDE_KG_M3 afin d'éviter toute ambiguïté.

## 4. Les caractéristiques du moteur d'entraînement

Une pompe est souvent entraînée par un moteur électrique.

Nous conservons certaines caractéristiques de ce moteur :

- Puissance nominale en kW ;
- Vitesse de rotation en tr/min ;
- Tension nominale en V ;
- Courant nominal en A ;
- Fréquence en Hz.

Il faut distinguer les caractéristiques du moteur de celles de la pompe.

La puissance du moteur d'entraînement n'est pas nécessairement égale à la puissance hydraulique utile de la pompe.

## 5. Caractéristiques des raccordements

Une pompe possède généralement deux raccordements principaux :

- Aspiration : entrée du fluide dans la pompe ;
- Refoulement : sortie du fluide après son passage dans la pompe.

Les diamètres nominaux sont généralement exprimés en DN et en millimètres dans notre classeur.

Exemple pédagogique :
- Aspiration : DN 80 ;
- Refoulement : DN 65.

Le diamètre nominal ne correspond pas nécessairement au diamètre intérieur réel de la conduite.

## 6. Organisation de la feuille DETAIL_POMPES

La feuille créée contient les colonnes suivantes :

| Colonne | Champ | Signification |
|---|---|---|
| A | CODE_EQUIPEMENT | Identifiant unique de la pompe |
| B | DESIGNATION | Désignation de la pompe |
| C | MARQUE | Marque commerciale |
| D | MODELE | Référence du modèle |
| E | NUMERO_SERIE | Numéro de série |
| F | TYPE_POMPE | Catégorie de pompe |
| G | FABRICANT | Fabricant |
| H | DEBIT_NOMINAL_M3_H | Débit nominal |
| I | HMT_NOMINALE_M | Hauteur manométrique totale |
| J | PRESSION_NOMINALE_BAR | Pression nominale |
| K | TYPE_FLUIDE | Fluide transporté |
| L | TEMPERATURE_FLUIDE_C | Température du fluide |
| M | MASSE_VOLUMIQUE_FLUIDE_KG_M3 | Masse volumique du fluide |
| N | PUISSANCE_MOTEUR_KW | Puissance du moteur d'entraînement |
| O | VITESSE_ROTATION_TR_MIN | Vitesse de rotation |
| P | TENSION_MOTEUR_V | Tension du moteur |
| Q | COURANT_MOTEUR_A | Courant nominal du moteur |
| R | FREQUENCE_HZ | Fréquence nominale |
| S | DIAMETRE_ASPIRATION_MM | Diamètre nominal d'aspiration |
| T | DIAMETRE_REFOULEMENT_MM | Diamètre nominal de refoulement |
| U | TYPE_MONTAGE | Type de montage |
| V | OBSERVATIONS_TECHNIQUES | Informations complémentaires |

## 7. Liaison automatique avec le registre EQUIPEMENTS

La colonne A contient le CODE_EQUIPEMENT.

Les informations générales sont récupérées automatiquement à partir de la feuille EQUIPEMENTS.

Formule en B2 :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;2;0);"")

Formule en C2 :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;5;0);"")

Formule en D2 :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;6;0);"")

Formule en E2 :

=IFERROR(VLOOKUP(A2;$EQUIPEMENTS.$A$2:$G$21;7;0);"")

Ces formules permettent de récupérer respectivement la désignation, la marque, le modèle et le numéro de série.

La recherche exacte est imposée par le dernier argument 0.

IFERROR permet de ne pas afficher d'erreur lorsque le code est vide ou introuvable.

Le fabricant reste à renseigner séparément en G, à partir d'une source fiable, si cette information est connue et distincte de la marque.

## 8. Référentiels créés

La feuille REFERENTIEL a été enrichie avec plusieurs listes.

### 8.1. Liste des pompes

P1 : LISTE_POMPES

- P2 : EQP-0001
- P3 : EQP-0016

Ces deux codes correspondent aux pompes identifiées dans le registre actuel.

### 8.2. Types de pompes

R1 : LISTE_TYPES_POMPES

- Centrifuge ;
- Volumétrique ;
- Submersible ;
- Auto-amorçante.

Attention : ces termes ne représentent pas tous des catégories de même nature. Submersible et auto-amorçante décrivent aussi des caractéristiques de conception ou d'installation.

### 8.3. Types de fluides

T1 : LISTE_FLUIDES

- Eau ;
- Huile ;
- Gasoil ;
- Essence ;
- Eau glycolée ;
- Produit chimique ;
- Air ;
- Autre.

### 8.4. Types de montage

V1 : LISTE_MONTAGES_POMPES

- Horizontal ;
- Vertical ;
- Sur socle ;
- Immergé.

Ces listes facilitent la normalisation des informations et les recherches ultérieures.

## 9. Validations de données mises en place

Les validations réalisées sont les suivantes :

| Plage | Champ | Règle |
|---|---|---|
| A2:A21 | CODE_EQUIPEMENT | Liste des pompes |
| F2:F21 | TYPE_POMPE | Liste du référentiel |
| K2:K21 | TYPE_FLUIDE | Liste du référentiel |
| H2:H21 | DEBIT_NOMINAL_M3_H | Décimal strictement supérieur à 0 |
| I2:I21 | HMT_NOMINALE_M | Décimal strictement supérieur à 0 |
| J2:J21 | PRESSION_NOMINALE_BAR | Décimal strictement supérieur à 0 |
| L2:L21 | TEMPERATURE_FLUIDE_C | Décimal supérieur ou égal à -273,15 |
| M2:M21 | MASSE_VOLUMIQUE_FLUIDE_KG_M3 | Décimal strictement supérieur à 0 |
| N2:N21 | PUISSANCE_MOTEUR_KW | Décimal strictement supérieur à 0 |
| O2:O21 | VITESSE_ROTATION_TR_MIN | Décimal strictement supérieur à 0 |
| P2:P21 | TENSION_MOTEUR_V | Décimal strictement supérieur à 0 |
| Q2:Q21 | COURANT_MOTEUR_A | Décimal strictement supérieur à 0 |
| R2:R21 | FREQUENCE_HZ | Décimal strictement supérieur à 0 |
| S2:S21 | DIAMETRE_ASPIRATION_MM | Décimal strictement supérieur à 0 |
| T2:T21 | DIAMETRE_REFOULEMENT_MM | Décimal strictement supérieur à 0 |
| U2:U21 | TYPE_MONTAGE | Liste du référentiel |

Ces règles vérifient la cohérence élémentaire des valeurs saisies. Elles ne remplacent pas les limites et exigences propres à chaque constructeur.

## 10. Manipulations pratiques réalisées

1. Identification des deux pompes dans le registre EQUIPEMENTS.
2. Création de la liste LISTE_POMPES dans REFERENTIEL.
3. Création de la feuille DETAIL_POMPES.
4. Définition des 22 colonnes de la fiche technique.
5. Création de la liste déroulante des codes équipements.
6. Mise en place des formules de récupération automatique.
7. Vérification de la liaison pour EQP-0001 et EQP-0016.
8. Mise en place des validations numériques.
9. Création des listes de types de pompes, fluides et montages.
10. Mise en forme des en-têtes.
11. Ajustement des largeurs de colonnes.
12. Sélection des deux pompes dans la feuille.
13. Activation du filtre automatique.
14. Vérification des contrôles de saisie.
15. Enregistrement du classeur.

## 11. Précautions relatives aux données techniques

Les caractéristiques réelles doivent être obtenues à partir :
- Des plaques signalétiques ;
- Des fiches constructeurs ;
- Des notices techniques ;
- Des documents de conception de l'installation.

Il ne faut pas inventer de valeurs pour remplir les cellules.

Les champs non vérifiés doivent rester vides.

Il faut également distinguer les caractéristiques nominales du matériel des valeurs mesurées en exploitation.

## 12. Résultat attendu

Le classeur GMI possède désormais :

- Une feuille générale EQUIPEMENTS ;
- Un index FICHES_TECHNIQUES ;
- Une feuille spécialisée DETAIL_MOTEURS ;
- Une feuille spécialisée DETAIL_POMPES ;
- Un référentiel centralisé ;
- Des contrôles et listes déroulantes ;
- Des liaisons automatiques par CODE_EQUIPEMENT.

Cette architecture peut être étendue progressivement aux autres familles d'équipements.

## 13. Synthèse

La fiche technique spécialisée permet de conserver les informations propres à une catégorie d'équipements sans surcharger le registre général.

La clé de liaison reste le CODE_EQUIPEMENT.

La qualité des informations techniques dépend de leur exactitude, de leur traçabilité et de leur provenance.
