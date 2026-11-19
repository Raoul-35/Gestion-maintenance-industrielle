# MODULE 5 — GESTION DU PARC D'ÉQUIPEMENTS INDUSTRIELS

## LEÇON 2 — Conception et structuration d'un registre des équipements

### 1. Objectifs pédagogiques

À la fin de cette leçon, tu devras comprendre :

- Comment concevoir un registre des équipements industriels.

- Comment organiser les informations en lignes et en colonnes.

- Comment choisir les types de données adaptés.

- Pourquoi utiliser des identifiants uniques.

- Comment éviter les doublons et les incohérences.

- Comment préparer un registre exploitable pour les opérations de maintenance.


## 2. Qu'est-ce qu'un registre des équipements ?

Un registre des équipements est un document ou une base de données qui rassemble les informations relatives à l'ensemble des équipements d'une installation industrielle.

Il constitue une référence centrale pour les techniciens, les responsables de maintenance et les gestionnaires du parc.

Il permet notamment de répondre à des questions comme :

- Combien de moteurs possède l'usine ?

- Quels équipements appartiennent au service Électricité ?

- Où se trouve une pompe particulière ?

- Quelle est la puissance du moteur MOT-001 ?

- Quels équipements sont actuellement en panne ?

Un registre bien conçu doit permettre de retrouver ces informations rapidement et sans ambiguïté.

### Exemple

Imaginons une installation qui possède trois moteurs électriques.

| **CODE\_EQUIPEMENT** | **DESIGNATION** | **SERVICE** | **LOCALISATION** | **PUISSANCE\_KW** |
| :-: | :-: | :-: | :-: | :-: |
| MOT-001 | Moteur pompe transfert | Production | Salle des pompes | 7,5 |
| MOT-002 | Moteur ventilateur | Production | Atelier 1 | 11 |
| MOT-003 | Moteur compresseur | Utilités | Local compresseur | 22 |

Chaque ligne représente un équipement.

Chaque colonne représente une caractéristique de cet équipement.

C'est le principe fondamental de l'organisation d'un registre.


## 3. Comprendre la structure d'une base de données

Pour bien construire notre registre, nous devons maîtriser quatre notions.

### 3.1 Le champ

Un champ représente une information particulière concernant un équipement.

Exemples :

- Code équipement.

- Désignation.

- Marque.

- Puissance.

- Date de mise en service.

Dans Calc, un champ correspond généralement à une colonne.

### 3.2 L'enregistrement

Un enregistrement représente l'ensemble des informations relatives à un équipement.

Dans Calc, un enregistrement correspond généralement à une ligne de données.

Exemple :

| **MOT-001** | **Moteur pompe transfert** | **Production** | **Salle des pompes** | **7,5** |
| :-: | :-: | :-: | :-: | :-: |

Cette ligne constitue un enregistrement.

### 3.3 La clé primaire

Une clé primaire est un champ qui permet d'identifier de manière unique chaque enregistrement.

Dans notre registre, le champ `CODE_EQUIPEMENT` joue ce rôle.

Exemple :

- MOT-001 : moteur de transfert.

- MOT-002 : moteur de ventilation.

- MOT-003 : moteur de compresseur.

Deux équipements ne doivent jamais posséder le même code.

**Attention :** la marque, le modèle et la puissance ne constituent pas des identifiants uniques. Plusieurs équipements peuvent partager ces caractéristiques.

### 3.4 Le référentiel

Un référentiel est une liste de valeurs de référence utilisées pour uniformiser les informations saisies.

Exemples :

**Référentiel des services :**

- Production

- Électricité

- Mécanique

- Utilités

- Instrumentation

**Référentiel des états :**

- En service

- En panne

- En maintenance

- À l'arrêt

- Réformé

Pourquoi est-ce important ?

Sans référentiel, un même service pourrait être enregistré de plusieurs manières :

- Électricité

- ELECTRICITE

- Service électrique

- ELEC

Ces différences compliquent les filtres, les recherches et les statistiques.


## 4. Choisir les bons types de données

Toutes les informations ne doivent pas être enregistrées de la même manière.

C'est une notion fondamentale dans la conception d'une base de données.

| **Champ** | **Type de données** | **Exemple** |
| :-: | :-: | :-: |
| CODE\_EQUIPEMENT | Texte | MOT-001 |
| DESIGNATION | Texte | Moteur asynchrone |
| SERVICE | Texte contrôlé | Production |
| LOCALISATION | Texte | Salle des pompes |
| MARQUE | Texte | Siemens |
| MODELE | Texte | 1LE1001 |
| NUMERO\_SERIE | Texte | SN0045821 |
| PUISSANCE\_KW | Numérique | 7,5 |
| DATE\_MISE\_EN\_SERVICE | Date | 15/03/2024 |
| ETAT | Texte contrôlé | En service |
| OBSERVATIONS | Texte | Fonctionnement normal |

### Attention à une erreur fréquente : les numéros de série

Un numéro de série peut contenir des chiffres et des lettres.

Exemple : `SN0045821`.

Il faut donc le traiter comme du texte et non comme un nombre.

Pourquoi ?

Parce qu'un numéro de série est un identifiant, pas une valeur destinée à un calcul.

De même, un code comme `MOT-001` doit être enregistré comme du texte.

En revanche, la puissance nominale doit être numérique, car nous pouvons vouloir calculer la puissance totale du parc.


## 5. Gérer les informations manquantes

Dans une installation industrielle, il est fréquent de ne pas connaître toutes les caractéristiques d'un équipement.

Par exemple :

- La plaque signalétique est illisible.

- Le numéro de série n'a pas été relevé.

- La date de mise en service est inconnue.

- La documentation constructeur est indisponible.

Il ne faut jamais inventer ces informations.

Deux solutions sont possibles :

**Solution 1 : laisser la cellule vide.**

C'est généralement préférable lorsqu'une donnée est simplement inconnue.

**Solution 2 : utiliser une valeur normalisée.**

Par exemple, une colonne spécifique pourrait contenir `Non renseigné`.

Attention : cette solution doit être utilisée avec cohérence. Il ne faut pas mélanger arbitrairement cellules vides, tirets, zéros et expressions différentes.


## 6. Les règles de qualité d'un registre

Un registre professionnel doit respecter plusieurs principes.

| **Principe** | **Explication** |
| :-: | :-: |
| Unicité | Chaque équipement possède un code unique. |
| Cohérence | Les mêmes informations sont enregistrées de la même manière. |
| Exactitude | Les données correspondent à la réalité du terrain. |
| Complétude | Les informations importantes sont renseignées autant que possible. |
| Traçabilité | Les modifications importantes peuvent être retrouvées. |
| Actualisation | Les informations évoluent lorsque la situation réelle change. |

### Exemple industriel

Un moteur MOT-001 est déplacé de la salle des pompes vers l'atelier 2.

Son code équipement reste `MOT-001`.

En revanche, sa localisation doit être actualisée.

C'est pourquoi nous avons choisi de séparer l'identifiant de la localisation.


## 7. Application à notre projet GMI

Notre feuille `EQUIPEMENTS` contient déjà les champs suivants :

| **Colonne** | **Champ** | **Type attendu** |
| :-: | :-: | :-: |
| A | CODE\_EQUIPEMENT | Texte |
| B | DESIGNATION | Texte |
| C | SERVICE | Texte contrôlé |
| D | LOCALISATION | Texte |
| E | MARQUE | Texte |
| F | MODELE | Texte |
| G | NUMERO\_SERIE | Texte |
| H | PUISSANCE\_KW | Numérique |
| I | DATE\_MISE\_EN\_SERVICE | Date |
| J | ETAT | Texte contrôlé |
| K | OBSERVATIONS | Texte |

Notre registre possède donc une structure cohérente.

Nous allons maintenant chercher à améliorer progressivement sa fiabilité, notamment grâce à la validation des données, aux listes déroulantes et au contrôle des doublons.

Nous ne modifierons pas la structure actuelle sans avoir étudié les conséquences sur les autres feuilles et les formules du classeur.


## 8. Synthèse de la leçon

Les notions essentielles à retenir :

- Un registre contient les informations de référence du parc.

- Un champ représente une caractéristique.

- Un enregistrement représente un équipement.

- Une clé primaire identifie chaque équipement de manière unique.

- Un référentiel permet de normaliser les valeurs.

- Le type de données doit être adapté à la nature de l'information.

- Les données inconnues ne doivent jamais être inventées.

