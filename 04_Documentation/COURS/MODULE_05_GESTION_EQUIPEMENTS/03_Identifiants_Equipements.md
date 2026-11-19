# 03 — Identifiants des équipements industriels

## 1. Définition

Un identifiant d'équipement est un code unique permettant de distinguer un équipement de tous les autres dans un parc industriel.

Exemple : EQP-0001, EQP-0002, EQP-0003.

## 2. Identifiant dépendant de la position

Un code peut être généré à partir du numéro de ligne dans Calc.

Exemple :

`=IF(B2="";"";"EQP-"&TEXT(ROW()-1;"0000"))`

Cette méthode est simple, mais le code dépend de la position de la ligne. Il peut donc changer lors de certaines opérations sur le tableau.

## 3. Identifiant permanent

Un identifiant permanent est attribué à un équipement et conservé comme une valeur fixe.

Il ne doit pas changer lorsque l'équipement est déplacé dans le tableau, trié ou modifié.

Un code attribué à un équipement réformé ne doit pas être réutilisé pour un nouvel équipement.

## 4. Génération assistée

Une méthode sans macro consiste à :

1. Extraire la partie numérique des codes existants.
2. Rechercher le numéro le plus élevé.
3. Ajouter 1.
4. Construire le nouveau code.
5. Copier le code proposé et le coller comme valeur fixe.

Exemple de formule d'extraction :

`=IF(C2="";"";VALUE(RIGHT(C2;4)))`

Recherche du numéro maximal :

`=MAX(E2:E1000)`

Calcul du prochain numéro :

`=MAX(E2:E1000)+1`

Construction du code :

`="EQP-"&TEXT(B7;"0000")`

## 5. Contrôle des doublons

La fonction COUNTIF permet de vérifier qu'un code permanent n'est pas attribué plusieurs fois.

`=IF(C2="";"";IF(COUNTIF($C$2:$C$1000;C2)>1;"DOUBLON";"UNIQUE"))`

## 6. Limites et précautions

- Les codes doivent respecter un format homogène.
- Les cellules contenant les identifiants permanents doivent conserver des valeurs fixes.
- Le générateur doit être contrôlé pour éviter les erreurs de saisie.
- Dans un système multi-utilisateur, il faut empêcher deux personnes d'attribuer simultanément le même code.
- Les équipements réformés doivent conserver leur ancien identifiant dans l'historique.

## 7. Application au projet GMI

Une feuille de test `TEST_CODES` a été créée dans le classeur GMI pour expérimenter la génération assistée et le contrôle des doublons avant toute modification du registre principal `EQUIPEMENTS`.
