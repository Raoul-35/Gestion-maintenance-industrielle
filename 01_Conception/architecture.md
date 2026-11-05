# ARCHITECTURE TECHNIQUE
## Gestion de maintenance industrielle

### 1. Architecture générale

Le classeur est organisé en cinq feuilles fonctionnelles.

### 2. Description des feuilles

| Feuille | Fonction |
|---|---|
| ACCUEIL | Navigation générale |
| LISTES | Référentiel des données |
| SAISIE | Formulaire des interventions |
| HISTORIQUE | Base des interventions enregistrées |
| TABLEAU_BORD | Analyse et visualisation |

### 3. Organisation de la feuille LISTES

Les données seront organisées en plusieurs catégories :

- Services
- Équipements
- Types de pannes
- Causes des pannes
- Types de maintenance
- Techniciens
- États des interventions

Les listes seront structurées pour permettre la création de menus déroulants dépendants.

### 4. Organisation de la feuille SAISIE

Le formulaire comportera les champs suivants :

| Champ | Type de donnée |
|---|---|
| Numéro d'intervention | Automatique |
| Date | Date |
| Service | Menu déroulant |
| Équipement | Menu dépendant |
| Type de panne | Menu dépendant |
| Cause de la panne | Menu déroulant |
| Type de maintenance | Menu déroulant |
| Technicien | Menu déroulant |
| Description | Texte |
| Durée d'intervention | Nombre |
| État | Menu déroulant |

### 5. Organisation de la feuille HISTORIQUE

Chaque ligne représentera une intervention enregistrée.

Les données seront organisées sous forme de tableau structuré avec des en-têtes fixes.

### 6. Automatisation

Le projet utilisera :

- Des formules pour les calculs et les recherches.
- La validation des données pour les menus déroulants.
- VBA pour les macros Excel.
- LibreOffice Basic pour les macros Calc.

### 7. Architecture des automatisations

Les principales opérations automatisées seront :

1. Actualisation des menus dépendants.
2. Vérification des champs obligatoires.
3. Génération des numéros d'intervention.
4. Enregistrement des interventions.
5. Réinitialisation du formulaire.
6. Actualisation des statistiques.

### 8. Compatibilité

Les deux versions du classeur seront développées et testées séparément.

Les formules seront choisies en privilégiant les fonctions communes aux deux logiciels lorsque cela est possible.

Les macros seront adaptées à chaque environnement.

### 9. Flux de données

LISTES → SAISIE → HISTORIQUE → TABLEAU_BORD

La feuille ACCUEIL permettra d'accéder aux différentes fonctionnalités.
