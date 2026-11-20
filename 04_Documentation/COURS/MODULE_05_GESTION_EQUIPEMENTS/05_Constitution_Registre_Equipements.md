# MODULE 05 — GESTION DES ÉQUIPEMENTS INDUSTRIELS

## Leçon 05 — Constitution et renseignement du registre des équipements

### 1. Objectifs pédagogiques

À la fin de cette leçon, l'apprenant doit être capable de :

- Constituer un registre d'équipements industriels.
- Identifier chaque équipement de manière unique.
- Renseigner correctement les informations d'un équipement.
- Distinguer les données d'identification, de localisation et de classification.
- Utiliser des listes déroulantes pour normaliser les données.
- Contrôler les doublons et la cohérence des enregistrements.

### 2. Définition du registre des équipements

Le registre des équipements est une base de données qui regroupe les informations essentielles relatives aux équipements d'une installation industrielle.

Il constitue l'une des structures fondamentales d'une GMAO (Gestion de Maintenance Assistée par Ordinateur).

Chaque ligne du registre représente un équipement physique unique.

Exemple : deux pompes identiques installées dans une même usine doivent posséder deux codes d'identification différents si elles représentent deux équipements physiques distincts.

### 3. Structure d'un enregistrement

Un enregistrement est l'ensemble des informations relatives à un équipement donné.

Dans notre classeur GMI, les informations sont organisées en plusieurs catégories :

| Catégorie | Informations |
|---|---|
| Identification | Code, désignation |
| Organisation | Service |
| Localisation | Emplacement physique |
| Caractéristiques techniques | Marque, modèle, numéro de série, puissance |
| Gestion | Date de mise en service, état, observations |
| Classification | Famille, sous-famille et leurs codes |

### 4. Règles de renseignement

- Chaque équipement doit posséder un code unique.
- Le code d'identification doit rester stable pendant toute la durée de vie de l'équipement.
- La désignation doit être claire et compréhensible.
- Le service correspond au rattachement organisationnel.
- La localisation indique l'emplacement physique.
- La famille et la sous-famille doivent être cohérentes.
- Les informations inconnues doivent rester vides plutôt que d'être inventées.
- Les équipements distincts ne doivent jamais partager le même code.
### 5. Contrôles automatiques du registre

#### 5.1. Contrôle des doublons de codes

Dans la colonne `CONTROLE_CODE` de la feuille `EQUIPEMENTS`, nous utilisons une formule basée sur `COUNTIF`.

Exemple :

```calc
=IF(A2="";"";IF(COUNTIF($A$2:$A$1000;A2)>1;"DOUBLON";"UNIQUE"))
```

Explication :

- `IF(A2="";"";...)` : laisse la cellule vide si aucun code n'est renseigné.
- `COUNTIF($A$2:$A$1000;A2)` : compte le nombre d'occurrences du code de la cellule A2 dans la plage.
- `>1` : vérifie si le code apparaît plusieurs fois.
- `"DOUBLON"` : signale un code utilisé plusieurs fois.
- `"UNIQUE"` : confirme que le code apparaît une seule fois.

Résultats attendus :

| Situation | Résultat |
|---|---|
| Code EQP-0001 présent une seule fois | UNIQUE |
| Code EQP-0001 présent deux fois | DOUBLON |
| Cellule du code vide | Cellule de contrôle vide |

#### 5.2. Génération automatique du code famille

Dans la colonne O (`CODE_FAMILLE`), la formule utilisée est :

```calc
=IF(M2="";"";IFERROR(VLOOKUP(M2;$REFERENTIEL.$G$2:$H$5;2;0);""))
```

Explication :

- `M2` contient la famille sélectionnée.
- `VLOOKUP` recherche cette famille dans le référentiel.
- `$REFERENTIEL.$G$2:$H$5` représente la plage de recherche.
- `2` indique que le résultat doit provenir de la deuxième colonne.
- `0` impose une correspondance exacte.
- `IFERROR` évite d'afficher une erreur si la recherche échoue.
- `IF` laisse la cellule vide lorsqu'aucune famille n'est sélectionnée.

Exemples :

| Famille | Code obtenu |
|---|---|
| Machines tournantes | MEC |
| Équipements électriques | ELE |
| Instrumentation | INS |
| Automatisme et commande | AUT |

#### 5.3. Génération automatique du code sous-famille

Dans la colonne P (`CODE_SOUS_FAMILLE`), la formule utilisée est :

```calc
=IF(N2="";"";IFERROR(INDEX($REFERENTIEL.$C$2:$C$13;MATCH(N2;$REFERENTIEL.$D$2:$D$13;0));""))
```

Explication :

- `N2` contient la sous-famille sélectionnée.
- `MATCH` recherche sa position dans la liste des sous-familles.
- `INDEX` récupère le code correspondant dans la colonne C.
- `IFERROR` évite l'affichage d'une erreur.
- `IF` laisse la cellule vide si aucune sous-famille n'est sélectionnée.

Exemples :

| Sous-famille | Code obtenu |
|---|---|
| Pompes | PMP |
| Transformateurs | TRF |
| Capteurs | CAP |
| Automates programmables | API |

### 6. Utilisation des listes déroulantes

Les listes déroulantes permettent de normaliser les informations saisies.

Dans notre classeur :

- La colonne SERVICE utilise la plage nommée `SERVICES`.
- La colonne FAMILLE utilise la liste des familles du référentiel.
- La colonne SOUS_FAMILLE utilise une liste dépendante de la famille sélectionnée.

La plage nommée `SERVICES` a été étendue de :

```calc
$LISTES.$A$2:$A$5
```

à :

```calc
$LISTES.$A$2:$A$6
```

Cette modification a permis d'ajouter le service Énergie sans supprimer les services déjà présents.

### 7. Contrôle des résultats

Après le renseignement du registre, les vérifications suivantes doivent être réalisées :

1. Vérifier que chaque équipement possède un code unique.
2. Vérifier que les familles et sous-familles sont cohérentes.
3. Vérifier la génération automatique des codes.
4. Vérifier que les listes déroulantes fonctionnent.
5. Tester volontairement un doublon pour confirmer son signalement.
6. Restaurer ensuite le code initial.
### 8. Travaux pratiques réalisés dans LibreOffice Calc

Le travail pratique a été effectué dans le classeur `GMI_Version_0.1.ods`, principalement dans la feuille `EQUIPEMENTS`.

#### 8.1. Préparation du registre

Les colonnes suivantes ont été utilisées :

| Colonne | Champ |
|---|---|
| A | CODE_EQUIPEMENT |
| B | DESIGNATION |
| C | SERVICE |
| D | LOCALISATION |
| E | MARQUE |
| F | MODELE |
| G | NUMERO_SERIE |
| H | PUISSANCE_KW |
| I | DATE_MISE_EN_SERVICE |
| J | ETAT |
| K | OBSERVATIONS |
| L | CONTROLE_CODE |
| M | FAMILLE |
| N | SOUS_FAMILLE |
| O | CODE_FAMILLE |
| P | CODE_SOUS_FAMILLE |

#### 8.2. Mise à jour de la liste des services

La liste initiale contenait quatre services :

- Électricité
- Automatisme
- Instrumentation
- Mécanique

Le service Énergie a été ajouté dans la feuille `LISTES`.

La plage nommée `SERVICES` a ensuite été étendue afin d'intégrer cette nouvelle valeur.

#### 8.3. Renseignement des équipements

Vingt équipements industriels ont été enregistrés, de `EQP-0001` à `EQP-0020`.

Les équipements représentaient différentes familles :

- Machines tournantes
- Équipements électriques
- Instrumentation
- Automatisme et commande

Pour chaque équipement, les informations disponibles ont été renseignées. Les données inconnues, comme certains numéros de série ou modèles, ont été laissées vides.

#### 8.4. Vérification des classifications

Les listes déroulantes ont permis de sélectionner les familles et sous-familles.

Les codes correspondants ont été générés automatiquement dans les colonnes O et P.

Exemples vérifiés :

| Équipement | Famille | Sous-famille | Code famille | Code sous-famille |
|---|---|---|---|---|
| Pompe alimentation chaudière | Machines tournantes | Pompes | MEC | PMP |
| Transformateur auxiliaire | Équipements électriques | Transformateurs | ELE | TRF |
| Capteur de température chaudière | Instrumentation | Capteurs | INS | CAP |
| Automate de commande chaudière | Automatisme et commande | Automates programmables | AUT | API |

#### 8.5. Test de détection des doublons

Un test volontaire a été réalisé en remplaçant temporairement le code `EQP-0002` par `EQP-0001`.

Le résultat attendu a été obtenu :

- La première occurrence affichait `DOUBLON`.
- La deuxième occurrence affichait également `DOUBLON`.

Le code initial `EQP-0002` a ensuite été restauré et les deux lignes ont retrouvé le statut `UNIQUE`.

### 9. Résultat final du travail pratique

À la fin de la manipulation, le registre contenait :

- 20 équipements industriels renseignés.
- 20 codes d'identification distincts.
- Des familles et sous-familles cohérentes.
- Des codes de classification générés automatiquement.
- Des listes déroulantes fonctionnelles.
- Un contrôle automatique des doublons opérationnel.

### 10. Points essentiels à retenir

1. Le registre des équipements constitue une base fondamentale de la GMAO.
2. Chaque équipement physique doit posséder un identifiant unique.
3. La désignation ne remplace pas le code d'identification.
4. La famille et la sous-famille servent à organiser les équipements.
5. Les listes déroulantes limitent les erreurs de saisie.
6. Les formules permettent d'automatiser certains contrôles et traitements.
7. La qualité des données conditionne la fiabilité des analyses de maintenance.

### 11. Lien avec les prochaines leçons

Le registre des équipements servira de référence pour les prochaines fonctionnalités du système GMI :

- Gestion des fiches techniques.
- Gestion des interventions.
- Gestion préventive.
- Gestion corrective.
- Gestion des pièces de rechange.
- Calcul des indicateurs de maintenance.

**Fin de la leçon 05 — Constitution et renseignement du registre des équipements.**
