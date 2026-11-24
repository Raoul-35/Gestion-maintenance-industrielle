import pypandoc

markdown = r"""# Module 6 — Gestion des interventions
## Formation Excel — Système GMI (Gestion de Maintenance Industrielle)

**Classeur de travail :** `GMI_Interventions_Version_0.3.xlsm`  
**Périmètre :** demandes d’intervention (DI), ordres de travail (OT), comptes rendus d’intervention (CRI), consultation et indicateurs.

---

## 1. Objectifs pédagogiques

À la fin de ce module, l'apprenant doit être capable de :

- enregistrer et suivre une demande d'intervention ;
- appliquer un circuit de traitement cohérent à une DI ;
- transformer une DI validée en ordre de travail ;
- planifier, démarrer et clôturer un OT ;
- produire un compte rendu d'intervention ;
- assurer la numérotation des documents ;
- consulter l'historique d'une intervention ;
- suivre l'activité au moyen d'indicateurs et d'un tableau de bord.

## 2. Architecture des données

### 2.1 Feuille `DEMANDES_INTERVENTION`

| Colonne | Champ |
|---|---|
| A | NUMERO_DI |
| B | DATE_DEMANDE |
| C | HEURE_DEMANDE |
| D | DEMANDEUR |
| E | SERVICE_DEMANDEUR |
| F | CODE_EQUIPEMENT |
| G | DESIGNATION |
| H | LOCALISATION |
| I | TYPE_DEMANDE |
| J | DESCRIPTION_PROBLEME |
| K | DATE_CONSTAT |
| L | PRIORITE |
| M | STATUT_DI |
| N | ANALYSE_MAINTENANCE |
| O | DATE_VALIDATION |
| P | MOTIF_REJET_REPORT |

La DI formalise le besoin. Elle ne constitue pas encore une autorisation d'exécuter les travaux.

### 2.2 Feuille `ORDRES_TRAVAIL`

| Colonne | Champ |
|---|---|
| A | NUMERO_OT |
| B | NUMERO_DI |
| C | DATE_CREATION_OT |
| D | TYPE_TRAVAUX |
| E | PRIORITE |
| F | CODE_EQUIPEMENT |
| G | DESIGNATION |
| H | LOCALISATION |
| I | DESCRIPTION_TRAVAUX |
| J | RESPONSABLE |
| K | DATE_PREVUE_DEBUT |
| L | DATE_PREVUE_FIN |
| M | STATUT_OT |
| N | DATE_DEBUT_REELLE |
| O | DATE_FIN_REELLE |
| P | OBSERVATIONS |

L'OT est le document de préparation et de suivi de l'exécution des travaux.

### 2.3 Feuille `COMPTES_RENDU_INTERVENTION`

| Colonne | Champ |
|---|---|
| A | NUMERO_CRI |
| B | NUMERO_OT |
| C | DATE_CRI |
| D | TECHNICIEN |
| E | DESCRIPTION_TRAVAUX_REALISES |
| F | CAUSE_PANNE |
| G | DIAGNOSTIC |
| H | ACTIONS_CORRECTIVES |
| I | PIECES_UTILISEES |
| J | DUREE_ARRET |
| K | RESULTAT_ESSAIS |
| L | RECOMMANDATIONS |
| M | OBSERVATIONS |

Le CRI conserve les informations relatives aux travaux réellement exécutés et à leurs résultats.

### 2.4 Feuilles complémentaires

- `COMPTEUR_DI` : attribution des numéros de DI.
- `COMPTEURS_GMI` : compteurs indépendants pour les OT et les CRI.
- `EQUIPEMENTS` : référentiel des équipements.
- `TABLEAU_DE_BORD_INTERVENTIONS` : indicateurs filtrés par année et graphiques.
- `CONSULTATION_INTERVENTIONS` : recherche à partir d'un numéro de DI ou d'OT.
- `MENU_GMI` : interface centralisée pour accéder aux commandes.

## 3. Circuit de traitement d'une demande

### 3.1 Cycle de vie des DI

Le circuit travaillé est le suivant :

`Nouvelle → En analyse → Validée → OT créé`

Deux issues alternatives sont prévues pendant l'analyse :

- `En analyse → Rejetée`
- `En analyse → En attente`

Une DI en attente peut revenir en analyse :

`En attente → En analyse`

La validation est réservée aux DI dont le statut est **En analyse**. Une DI ne doit pas être validée directement depuis un statut vide ou Nouvelle.

### 3.2 Cycle de vie des OT

Le processus implémenté est :

`À planifier → Planifié → En cours → Terminé`

- À la création, l'OT est associé à une DI validée.
- La planification renseigne le responsable et les dates prévisionnelles.
- Le démarrage renseigne la date réelle de début.
- La clôture renseigne la date réelle de fin et déclenche la création du CRI.

## 4. Automatisations VBA réalisées

| Macro | Rôle |
|---|---|
| `Creer_DI` | Créer une DI et attribuer un numéro unique |
| `Changer_Statut_DI` | Contrôler et modifier le statut selon les transitions autorisées |
| `Valider_DI` | Valider une DI en analyse |
| `Rejeter_DI` | Rejeter une DI en analyse et enregistrer le motif |
| `Mettre_DI_En_Attente` | Mettre une DI en attente et enregistrer le motif |
| `Creer_OT` | Générer un OT depuis une DI validée |
| `Planifier_OT` | Renseigner responsable et dates prévisionnelles |
| `Demarrer_OT` | Passer l'OT à En cours et enregistrer le début réel |
| `Terminer_OT` | Clôturer l'OT et générer le CRI |
| `Rechercher_Intervention` | Rechercher une DI ou un OT et afficher les informations liées |
| `Ouvrir_Tableau_De_Bord` | Ouvrir le tableau de bord |
| `Retour_Menu_GMI` | Revenir à l'interface principale |

Les macros de traitement qui s'appuient sur la ligne active nécessitent de sélectionner d'abord la ligne de l'enregistrement concerné dans la feuille de données correspondante. Les commandes sont centralisées dans `MENU_GMI`.

### 4.1 Numérotation

- Les DI utilisent la feuille `COMPTEUR_DI`.
- Les OT et les CRI utilisent `COMPTEURS_GMI`.
- Le compteur est indépendant pour chaque type de document et chaque année.
- La numérotation est enregistrée dans une feuille de compteur plutôt que calculée uniquement à partir du dernier enregistrement visible. Cela évite de réutiliser un numéro simplement parce qu'une ligne a été supprimée.

### 4.2 Durée d'intervention

La durée est calculée à partir des dates réelles de début et de fin de l'OT :

`Durée en heures = (Date/heure de fin − Date/heure de début) × 24`

La valeur est arrondie à deux décimales et enregistrée dans `COMPTES_RENDU_INTERVENTION`, colonne J. Cette durée représente le temps écoulé entre le démarrage et la clôture ; elle ne représente pas nécessairement le temps de main-d'œuvre cumulé si plusieurs techniciens interviennent ou si l'équipement reste en attente.

## 5. Tableau de bord et consultation

Le tableau de bord présente notamment :

- le nombre total de DI ;
- les DI par statut ;
- les OT par statut ;
- la durée moyenne et la durée totale des interventions ;
- le taux de transformation des DI en OT ;
- le taux de réalisation des OT.

Le filtre d'année permet de recalculer les indicateurs pour l'année sélectionnée.

**Limite à connaître :** les indicateurs de statut reposent sur le statut actuel des enregistrements. Ils ne reconstituent pas l'état historique des statuts à une date passée, car aucun journal horodaté des changements de statut n'a encore été construit.

La feuille `CONSULTATION_INTERVENTIONS` permet une recherche par numéro de DI ou d'OT. Elle affiche les informations de la DI, de l'OT associé et, lorsqu'il existe, du CRI associé.

## 6. Procédure d'utilisation du GMI — Gestion des interventions

### A. Enregistrer une demande

1. Ouvrir `MENU_GMI`.
2. Aller dans `DEMANDES_INTERVENTION`.
3. Renseigner les champs de demande : date, heure, demandeur, service, équipement, type de demande, description, date du constat et priorité.
4. Lancer `Creer_DI` depuis le menu.
5. Vérifier que le numéro de DI a été attribué et que l'enregistrement est présent.

Ne pas saisir manuellement le numéro de DI.

### B. Analyser et décider

1. Sélectionner la ligne de la DI dans `DEMANDES_INTERVENTION`.
2. Depuis `MENU_GMI`, lancer `Changer_Statut_DI`.
3. Si le statut est vide, choisir d'abord **Nouvelle**.
4. Faire évoluer ensuite la demande vers **En analyse**.
5. Compléter l'analyse de maintenance dans la colonne N.
6. Selon la décision :
   - lancer `Valider_DI` pour une demande acceptée ;
   - lancer `Rejeter_DI` et renseigner le motif pour une demande rejetée ;
   - lancer `Mettre_DI_En_Attente` et renseigner le motif si la décision est différée.

Seule une DI en analyse peut être validée, rejetée ou mise en attente.

### C. Créer un ordre de travail

1. Sélectionner la DI validée dans `DEMANDES_INTERVENTION`.
2. Depuis `MENU_GMI`, lancer `Creer_OT`.
3. Vérifier la création de l'OT dans `ORDRES_TRAVAIL`.
4. Vérifier le lien entre le numéro d'OT et le numéro de DI.
5. Vérifier que la DI passe au statut **OT créé**.

Ne pas créer manuellement un OT pour une DI déjà traitée par la macro.

### D. Planifier l'OT

1. Dans `ORDRES_TRAVAIL`, sélectionner la ligne de l'OT à planifier.
2. Depuis `MENU_GMI`, lancer `Planifier_OT`.
3. Renseigner le responsable, la date prévue de début et la date prévue de fin.
4. Vérifier que la date de fin n'est pas antérieure à la date de début.
5. Vérifier le statut **Planifié** et les informations enregistrées.

### E. Démarrer les travaux

1. Sélectionner l'OT concerné dans `ORDRES_TRAVAIL`.
2. Depuis `MENU_GMI`, lancer `Demarrer_OT`.
3. Vérifier le passage au statut **En cours**.
4. Vérifier l'enregistrement de la date réelle de début.

### F. Terminer les travaux et établir le CRI

1. Sélectionner l'OT en cours dans `ORDRES_TRAVAIL`.
2. Depuis `MENU_GMI`, lancer `Terminer_OT`.
3. Renseigner les informations demandées : technicien, travaux réalisés, cause, diagnostic, actions correctives, pièces, essais, recommandations et observations.
4. Confirmer la clôture.
5. Vérifier le statut **Terminé**, la date réelle de fin et la création du CRI.
6. Vérifier la liaison entre le CRI et l'OT.
7. Contrôler la durée enregistrée dans le CRI.

### G. Consulter une intervention

1. Depuis `MENU_GMI`, ouvrir `CONSULTATION_INTERVENTIONS`.
2. Saisir un numéro de DI ou d'OT dans la zone de recherche.
3. Cliquer sur `RECHERCHER`.
4. Contrôler les informations de la DI, de l'OT et du CRI éventuel.
5. Utiliser `RETOUR AU MENU` pour revenir à l'accueil.

### H. Suivre l'activité

1. Depuis `MENU_GMI`, ouvrir le tableau de bord.
2. Choisir l'année d'analyse.
3. Lire les volumes par statut, les durées et les taux.
4. Interpréter les résultats en tenant compte du fait que les statuts présentés sont les statuts actuels.

## 7. Tests fonctionnels effectués pendant la formation

Les scénarios de test documentés comprennent :

- création de DI numérotées ;
- progression des statuts et validation d'une DI en analyse ;
- génération d'un OT à partir d'une DI validée ;
- planification et démarrage d'un OT ;
- clôture d'un OT et génération d'un CRI ;
- consultation par numéro de DI et par numéro d'OT ;
- consultation d'une DI sans OT ;
- navigation depuis le menu et retour au menu ;
- contrôle des compteurs et des liens DI–OT–CRI.

Les enregistrements de démonstration mentionnés dans les tests sont notamment `DI-2026-0004`, `DI-2026-0005`, `OT-2026-0001`, `OT-2026-0002` et `CRI-2026-0001`. Ils doivent être conservés comme données de test ou clairement identifiés comme tels.

**À refaire avant archivage final :** exécuter un test complet sur un nouvel enregistrement après les dernières modifications VBA, notamment pour confirmer le calcul de durée dans un CRI nouvellement généré. Le premier CRI de test ayant été créé avant l'ajout du calcul de durée, sa durée peut être vide.

## 8. Points à compléter avant de considérer le module 6 comme stabilisé

### Priorité 1 — Fiabilité du cycle de travail

1. Ajouter une gestion explicite des OT suspendus, annulés ou reportés, avec motif et règles de transition.
2. Renforcer les contrôles de clôture : présence des champs essentiels, date de début réelle valide, cohérence des dates et absence de CRI en double.
3. Fiabiliser les recherches VBA en précisant les paramètres de `Range.Find` (`LookIn`, `LookAt`, `SearchOrder`, `SearchDirection` et `MatchCase`).
4. Tester les macros en cas d'annulation d'une saisie, de champ vide, de numéro inexistant et de double clic sur une commande.

### Priorité 2 — Traçabilité et exploitation

5. Ajouter un historique horodaté des changements de statut DI et OT, avec l'utilisateur ou le responsable du changement si cette information est disponible.
6. Enrichir la consultation pour afficher aussi les dates prévues, les dates réelles, la localisation, la priorité et les motifs de rejet ou d'attente.
7. Définir clairement la règle métier sur le nombre de CRI autorisés par OT : un CRI unique à la clôture ou plusieurs comptes rendus successifs.
8. Ajouter le suivi des coûts : pièces, quantités, prix unitaires, main-d'œuvre et coût total. Cette partie pourra être développée avec le module consacré aux pièces et aux coûts si le périmètre pédagogique le prévoit.

### Priorité 3 — Ergonomie et indicateurs

9. Vérifier les formules du tableau de bord avec plusieurs scénarios et années.
10. Clarifier les définitions des taux et durées : le temps d'arrêt équipement, le temps d'intervention et le temps de main-d'œuvre ne sont pas toujours identiques.
11. Ajouter des contrôles de saisie et des listes de validation pour les champs normalisés.
12. Préparer une sauvegarde et une version de référence du classeur avant d'ajouter de nouvelles fonctionnalités.

## 9. Critères de clôture du module 6

Le module 6 pourra être considéré comme stabilisé lorsque :

- une DI peut être créée, analysée et orientée sans transition de statut incohérente ;
- une DI validée peut générer un seul OT lié ;
- l'OT peut être planifié, démarré et clôturé selon des règles contrôlées ;
- le CRI est créé et lié à l'OT sans doublon ;
- les dates et durées sont cohérentes ;
- les compteurs ne réattribuent pas les numéros existants ;
- la consultation restitue correctement les informations liées ;
- les indicateurs sont vérifiés sur des cas de test ;
- une procédure d'utilisation est disponible et le classeur est sauvegardé.

---

**Fin du support — Module 6 : Gestion des interventions**  
**Étape suivante après stabilisation : Module 7 — Gestion de la maintenance préventive.**
"""

output_path = "/mnt/data/Module_06_Gestion_des_interventions_GMI.md"
pypandoc.convert_text(markdown, "md", format="md", outputfile=output_path, extra_args=["--standalone"])
print(output_path)
