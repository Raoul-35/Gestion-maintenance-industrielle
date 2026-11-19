from pathlib import Path

content = r"""# Module 5 — Gestion du parc d’équipements industriels
## Leçon pratique : classification des équipements par familles et sous-familles

**Projet :** Gestion de maintenance industrielle (GMI)  
**Logiciel :** LibreOffice Calc  
**Classeur associé :** `02_Classeur/LibreOffice/GMI_Version_0.1.ods`  
**Feuille principale :** `EQUIPEMENTS`  
**Feuille de référence :** `REFERENTIEL`

---

## 1. Objectifs pédagogiques

À la fin de cette leçon, l’apprenant doit être capable de :

- expliquer l’intérêt de classer les équipements d’une installation industrielle ;
- distinguer une famille d’équipements d’une sous-famille ;
- construire un référentiel de familles et de sous-familles ;
- créer une liste déroulante de familles ;
- créer une liste déroulante de sous-familles dépendante de la famille choisie ;
- générer automatiquement les codes de famille et de sous-famille ;
- effacer automatiquement une ancienne sous-famille lorsqu’une famille change ;
- vérifier et archiver le travail réalisé.

## 2. Notions théoriques

### 2.1. Pourquoi classer les équipements ?

Dans une installation industrielle, le parc peut comprendre des moteurs, des pompes, des transformateurs, des capteurs, des automates, etc.

La classification permet notamment de :

- regrouper les équipements de même nature ;
- faciliter les recherches et les filtres ;
- préparer des plans de maintenance adaptés aux catégories d’équipements ;
- analyser les pannes et les coûts par famille ;
- structurer progressivement une base de données de GMAO.

Une classification cohérente doit être stable, compréhensible et appliquée de la même manière à tous les équipements.

### 2.2. Famille et sous-famille

- **Famille :** catégorie générale à laquelle appartient un équipement.
- **Sous-famille :** catégorie plus précise à l’intérieur d’une famille.

Exemple : « Machines tournantes » est une famille ; « Pompes » est une sous-famille.

La famille ne doit pas être confondue avec le service responsable, la localisation physique ou la fonction de l’équipement dans le procédé.

### 2.3. Référentiel

Un référentiel est une table centrale qui contient les valeurs autorisées. Ici, la feuille `REFERENTIEL` contient les familles, leurs codes, les sous-familles et les codes de sous-famille.

L’utilisation d’un référentiel évite les saisies libres incohérentes, par exemple « Pompe », « pompes » et « POMPE » pour désigner la même catégorie.

## 3. Classification retenue dans le classeur GMI

La première version pratique utilise quatre familles et douze sous-familles.

| Code famille | Famille | Code sous-famille | Sous-famille |
|---|---|---|---|
| MEC | Machines tournantes | MOT | Moteurs électriques |
| MEC | Machines tournantes | PMP | Pompes |
| MEC | Machines tournantes | CMP | Compresseurs |
| MEC | Machines tournantes | VEN | Ventilateurs |
| ELE | Équipements électriques | TRF | Transformateurs |
| ELE | Équipements électriques | VAR | Variateurs de fréquence |
| ELE | Équipements électriques | TBT | Tableaux électriques |
| INS | Instrumentation | CAP | Capteurs |
| INS | Instrumentation | TRM | Transmetteurs |
| INS | Instrumentation | IND | Indicateurs |
| AUT | Automatisme et commande | API | Automates programmables |
| AUT | Automatisme et commande | IHM | Interfaces homme-machine |

Cette liste constitue le référentiel de départ du projet. Elle pourra être enrichie lorsque le besoin sera étudié, sans ajouter des catégories arbitrairement.

## 4. Organisation des feuilles

### 4.1. Feuille `REFERENTIEL`

La table principale utilise les colonnes suivantes :

| Colonne | Intitulé | Rôle |
|---|---|---|
| A | CODE_FAMILLE | Code court de la famille |
| B | FAMILLE | Libellé de la famille |
| C | CODE_SOUS_FAMILLE | Code court de la sous-famille |
| D | SOUS_FAMILLE | Libellé de la sous-famille |
| E | CONTROLE_DOUBLON | Contrôle d’unicité du code de sous-famille |

La feuille contient également des plages auxiliaires pour les listes déroulantes :
- `G2:G5` : liste des quatre familles ;
- `H2:H5` : codes correspondants ;
- `I2:I5` : sous-familles MEC ;
- `J2:J4` : sous-familles ELE ;
- `K2:K4` : sous-familles INS ;
- `L2:L3` : sous-familles AUT.

Les en-têtes des colonnes I à L indiquent les codes MEC, ELE, INS et AUT.

### 4.2. Contrôle des doublons

Dans `E2`, la formule utilisée est :

```calc
=IF(C2="";"";IF(COUNTIF($C$2:$C$1000;C2)>1;"DOUBLON";"UNIQUE"))
```

Explication :
- `C2=""` : si aucun code de sous-famille n’est saisi, le résultat reste vide ;
- `COUNTIF($C$2:$C$1000;C2)` compte combien de fois le code apparaît dans la plage ;
- si le nombre est supérieur à 1, la cellule affiche `DOUBLON` ;
- sinon, elle affiche `UNIQUE`.

La formule a été recopiée vers le bas dans la colonne E.

## 5. Préparation de la feuille `EQUIPEMENTS`

Les colonnes de classification ajoutées au registre sont :

| Colonne | Intitulé | Fonction |
|---|---|---|
| M | FAMILLE | Choix de la famille |
| N | SOUS_FAMILLE | Choix de la sous-famille |
| O | CODE_FAMILLE | Code généré automatiquement |
| P | CODE_SOUS_FAMILLE | Code généré automatiquement |

La mise en pratique est limitée aux lignes 2 à 21, soit vingt équipements.

## 6. Manipulations pratiques réalisées

### 6.1. Créer la liste déroulante des familles

1. Dans `EQUIPEMENTS`, sélectionner `M2:M21`.
2. Ouvrir **Données → Validité**.
3. Dans l’onglet **Critères**, choisir **Plage de cellules** comme type d’autorisation.
4. Indiquer comme source :

```calc
$REFERENTIEL.$G$2:$G$5
```

5. Activer l’affichage de la liste de sélection.
6. Valider.

Résultat attendu : chaque cellule de M2 à M21 propose les quatre familles du référentiel.

### 6.2. Générer automatiquement le code de famille

Dans `O2`, saisir :

```calc
=IF(M2="";"";IFERROR(VLOOKUP(M2;$REFERENTIEL.$G$2:$H$5;2;0);""))
```

Explication :
- si M2 est vide, O2 reste vide ;
- `VLOOKUP` recherche le nom de famille choisi en M2 dans la première colonne de la plage G2:H5 ;
- l’argument `2` demande de renvoyer la valeur de la deuxième colonne, c’est-à-dire le code ;
- `0` demande une correspondance exacte ;
- `IFERROR` évite d’afficher une erreur si aucune correspondance n’est trouvée.

Recopier la formule de O2 jusqu’à O21 en copiant O2, puis en collant dans O3:O21.

Résultats attendus :
- Machines tournantes → `MEC` ;
- Équipements électriques → `ELE` ;
- Instrumentation → `INS` ;
- Automatisme et commande → `AUT`.

### 6.3. Créer la liste déroulante dépendante des sous-familles

Sélectionner `N2:N21`, puis ouvrir **Données → Validité**. Dans **Critères**, choisir **Plage de cellules** et saisir la formule de source suivante :

```calc
INDIRECT(IF($O2="MEC";"$REFERENTIEL.$I$2:$I$5";IF($O2="ELE";"$REFERENTIEL.$J$2:$J$4";IF($O2="INS";"$REFERENTIEL.$K$2:$K$4";"$REFERENTIEL.$L$2:$L$3"))))
```

Activer l’affichage de la liste de sélection et valider.

Explication :
- `O2` contient le code de famille généré automatiquement ;
- `IF` choisit la plage correspondant à ce code ;
- `INDIRECT` transforme le texte représentant l’adresse de plage en référence utilisable par la liste déroulante ;
- les références de ligne sont relatives afin que chaque ligne utilise son propre code en O.

Correspondances :
- `MEC` → `REFERENTIEL.I2:I5` ;
- `ELE` → `REFERENTIEL.J2:J4` ;
- `INS` → `REFERENTIEL.K2:K4` ;
- `AUT` → `REFERENTIEL.L2:L3`.

**Important :** la liste dépendante propose les sous-familles autorisées, mais l’utilisateur choisit manuellement celle qui correspond réellement à l’équipement. Calc ne peut pas déduire si une machine tournante est une pompe, un moteur, un compresseur ou un ventilateur à partir de la seule famille.

### 6.4. Générer automatiquement le code de sous-famille

Dans `P2`, saisir :

```calc
=IF(N2="";"";IFERROR(INDEX($REFERENTIEL.$C$2:$C$13;MATCH(N2;$REFERENTIEL.$D$2:$D$13;0));""))
```

Explication :
- si N2 est vide, P2 reste vide ;
- `MATCH` recherche le libellé de la sous-famille dans `REFERENTIEL.D2:D13` et renvoie sa position ;
- `INDEX` utilise cette position pour récupérer le code correspondant dans `REFERENTIEL.C2:C13` ;
- `IFERROR` évite l’affichage d’une erreur en cas d’absence de correspondance.

Recopier P2 jusqu’à P21.

Exemples :
- Pompes → `PMP` ;
- Transformateurs → `TRF` ;
- Capteurs → `CAP` ;
- Automates programmables → `API`.

### 6.5. Effacer l’ancienne sous-famille lorsqu’on change de famille

**Besoin fonctionnel :** si une sous-famille a été choisie, puis que l’utilisateur change la famille sur la même ligne, l’ancienne sous-famille ne doit pas rester affichée. Elle pourrait ne pas appartenir à la nouvelle famille.

Une macro LibreOffice Basic a été ajoutée dans le module existant `ModuleMaintenance`. Elle est associée à l’événement **Contenu modifié** de la feuille `EQUIPEMENTS`.

Code utilisé et testé dans le classeur :

```basic
Sub EffacerAncienneSousFamille(oEvent)

    Dim oSheet As Object
    Dim oSelection As Object
    Dim oSubFamille As Object
    Dim nRow As Long
    Dim nCol As Long

    oSheet = ThisComponent.CurrentController.ActiveSheet

    If oSheet.Name <> "EQUIPEMENTS" Then Exit Sub

    oSelection = ThisComponent.CurrentSelection

    If Not oSelection.supportsService("com.sun.star.sheet.SheetCell") Then Exit Sub

    nRow = oSelection.CellAddress.Row
    nCol = oSelection.CellAddress.Column

    If nCol <> 12 Then Exit Sub
    If nRow < 1 Or nRow > 20 Then Exit Sub

    oSubFamille = oSheet.getCellByPosition(13, nRow)

    ' Effacer seulement si une ancienne sous-famille existe
    If oSubFamille.String <> "" Then
        oSubFamille.clearContents(23)
    End If

End Sub
```

Repères d’indexation utilisés par l’API Calc :
- la colonne M correspond à l’index `12` ;
- la colonne N correspond à l’index `13` ;
- la ligne 2 correspond à l’index `1` ;
- la ligne 21 correspond à l’index `20`.

La macro :
1. vérifie que la feuille active est `EQUIPEMENTS` ;
2. vérifie que la sélection est une cellule ;
3. vérifie que la cellule modifiée se trouve en colonne M et entre les lignes 2 et 21 ;
4. efface uniquement la cellule correspondante en colonne N si elle contient une ancienne valeur.

L’événement **Contenu modifié** a été associé à `EffacerAncienneSousFamille` dans les événements de la feuille `EQUIPEMENTS`.

**Résultat testé :** après avoir choisi une sous-famille, changer la famille sur la même ligne efface l’ancienne sous-famille. Le code de famille se met à jour et la liste de sous-familles reste disponible, avec les choix de la nouvelle famille.

## 7. Tests de validation

Les quatre cas suivants ont été testés :

| Famille choisie | Code famille | Sous-famille choisie | Code sous-famille |
|---|---|---|---|
| Machines tournantes | MEC | Pompes | PMP |
| Équipements électriques | ELE | Transformateurs | TRF |
| Instrumentation | INS | Capteurs | CAP |
| Automatisme et commande | AUT | Automates programmables | API |

Un changement de famille a également été testé sur plusieurs lignes : l’ancienne sous-famille est effacée et la nouvelle liste dépendante est proposée.

## 8. Points essentiels à retenir

- Une famille regroupe plusieurs sous-familles.
- Le référentiel centralise les valeurs autorisées.
- La validation des données contrôle les choix proposés dans une cellule.
- `VLOOKUP` permet de récupérer le code de famille à partir du nom de famille.
- `INDIRECT` permet de rendre la liste de sous-familles dépendante du code de famille.
- `INDEX` et `MATCH` permettent de retrouver le code de sous-famille à partir de son libellé.
- Une macro permet d’automatiser l’effacement d’une ancienne valeur lorsqu’une autre cellule est modifiée.
- Une sous-famille doit être choisie en fonction de l’équipement réel ; elle ne doit pas être attribuée arbitrairement.

## 9. Révision autonome

Pour réviser cette leçon, refaire les opérations suivantes dans une copie du classeur :

1. Ajouter une famille et ses sous-familles au référentiel en respectant la structure existante.
2. Vérifier que le code de famille est correctement renvoyé.
3. Vérifier la plage de sous-familles correspondante.
4. Tester la liste déroulante dépendante.
5. Choisir une sous-famille et vérifier le code généré.
6. Changer la famille et vérifier que l’ancienne sous-famille est effacée.
7. Vérifier que les autres lignes ne sont pas modifiées.

Avant toute modification du référentiel ou de la macro, conserver une copie de sauvegarde du classeur.

---

**Fin de la leçon pratique — Classification des équipements par familles et sous-familles.**
"""
path = Path("/mnt/data/04_Classification_familles_sous_familles.md")
path.write_text(content, encoding="utf-8")
print(f"Fichier créé : {path}")
