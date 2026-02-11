# 🚍 Analyse du Ridership des Transports Urbains — Chicago & Philadelphie

 ### Power BI | Python | Analyse de données | Aide à la décision

# Présentation du projet

Ce projet analyse la fréquentation des réseaux de transport urbain de Chicago et Philadelphie à partir de données historiques. 
L'objectif est de concevoir un tableau de bord Power BI interactif et orienté décision, permettant de :
- Suivre l'évolution du trafic dans le temps
- Comparer les performances entre villes, modes et itinéraires
- Identifier les zones d'instabilité et de sous-performance
- Appuyer des recommandations stratégiques et opérationnelles

# Problématique métier

Les agences de transport gèrent des réseaux complexes où la demande varie selon :

- la ville,
- le mode de transport (bus, train…),
-les routes (lignes) individuelles.

# Technique d'empilement

- Python (EDA & Préparation & qualité des données)
- Power BI Desktop
- Modélisation (schéma en étoile)
- Mesures DAX et KPI
- Tableaux de bord interactifs

# EDA & préparation des données (Python)

Les sources étant hétérogènes, un pipeline de préparation a été réalisé en Python pour produire des tables propres et cohérentes avant Power BI.

## Étapes principales :

- Import des fichiers et consolidation (Chicago / Philadelphie)

- Standardisation des champs (Année, Mois, Ville, Mode, Itinéraire, Achalandage)

- Nettoyage : doublons, valeurs manquantes, types de données, formats texte

- Harmonisation inter-villes pour permettre la comparaison

- Export les tableaux « propres » prêts à charger dans Power BI (processed/*.csv)

## Contrôles qualité :

- validation des clés (période + itinéraire/mode + ville)

- vérification de complétude par période et par ville

- détection de valeurs aberrantes (zéros incohérents, négatifs)

# Modèle de données (Power BI)

Le modèle repose sur un schéma en étoile :

### Faits

- Fait_mode : fréquentation par mode

- Fait_route : fréquentation par itinéraire

### Dimensions

Dim_city, Dim_mode, Dim_route, Dim_month, Dim_year


# Structure du tableau de bord

##  Page 1 — Analyse par Mode de Transport

**Objectif :**  

Fournir une vue d’ensemble du comportement du ridership par mode et par ville.

**Contenu :**

- KPIs principaux :
  - Moyenne du ridership
  - Somme totale du ridership
  - Écart-type (mesure de la volatilité)
- Répartition du ridership par mode (Bus vs Rail)
- Comparaison des modes entre Chicago et Philadelphie
- Évolution mensuelle du ridership
- Évolution annuelle du ridership

Cette page permet de comprendre la structure globale du réseau et les tendances principales.

##  Page 2 — Analyse par Routes

**Objectif :**

Analyser la distribution du trafic à un niveau plus détaillé.

**Contenu :**

- KPIs liés aux routes :
  - Nombre total de routes
  - Volume total de ridership
- Classement des routes par niveau de fréquentation
- Comparaison des routes entre les deux villes
- Évolution mensuelle par ville
- Évolution annuelle agrégée

Cette page met en évidence la concentration du trafic et la structure interne des réseaux urbains.



### 📈 KPIs clés

| Indicateur | Description |
|------------|------------|
| Moyenne du ridership | Niveau moyen de fréquentation |
| Somme du ridership | Volume total de fréquentation |
| Écart-type | Mesure de la variabilité |
| Nombre de routes | Couverture du réseau |
| Ridership par mode | Contribution Bus vs Rail |
| Ridership par route | Répartition du trafic |

# Informations et recommandations

Piloter la stratégie au niveau des modes (levier principal du volume)

Optimiser les itinéraires sous-performantes (fréquence, itinéraires, priorisation)

Surveiller les segments à forte utilisation (stabilité du service)

Adapter les décisions par ville (benchmark Chicago vs Philadelphie)

# Contenu du dépôt

- notebook Python (EDA / Nettoyage)

- data_cleaned — données nettoyées prêtes Power BI

- temp Dashboard.pbix — rapport Power BI

- README.md — documentation

# Planification 

[Voici le lien de Jira](https://imanelen25-1770646756973.atlassian.net/jira/software/projects/KAN/boards/1?atlOrigin=eyJpIjoiNTA1ZjA3ZTlhNDc3NDc5ZTgxYmZhYTUyNzZjZDY2YjgiLCJwIjoiaiJ9)

