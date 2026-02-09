🚍 Analyse du Ridership des Transports Urbains — Chicago & Philadelphie

Power BI | Python (ETL) | Analyse de données | Aide à la décision

📌 Présentation du projet

Ce projet analyse la fréquentation (fréquentation) des réseaux de transport urbain de Chicago et Philadelphie à partir de données historiques. L'objectif est de concevoir un tableau de bord Power BI interactif et orienté décision, permettant de :

Suivre l'évolution du trafic dans le temps

Comparer les performances entre villes, modes et itinéraires

Identifier les zones d'instabilité et de sous-performance

Appuyer des recommandations stratégiques et opérationnelles

🎯 Problématique métier

Les agences de transport gèrent des réseaux complexes où la demande varie selon :

la ville,

le mode de transport (bus, train…),

les routes (lignes) individuelles.

Sans une vue analytique fiable, il est difficile de :

anticiper la fluctuation de la demande,

optimiser l'allocation des ressources,

repérer les routes sous-performantes,

benchmarker les performances entre villes.

🛠️ Technique d'empilement

Python (ETL)

pandas (préparation & qualité des données)

Power BI Desktop

Modélisation (schéma en étoile)

Mesures DAX et KPI

Tableaux de bord interactifs

🔧 ETL & préparation des données (Python)

Les sources étant hétérogènes, un pipeline de préparation a été réalisé en Python pour produire des tables propres et cohérentes avant Power BI.

Étapes principales :

Import des fichiers et consolidation (Chicago / Philadelphie)

Standardisation des champs (Année, Mois, Ville, Mode, Itinéraire, Achalandage)

Nettoyage : doublons, valeurs manquantes, types de données, formats texte

Harmonisation inter-villes pour permettre la comparaison

Exporter les tableaux « propres » prêts à charger dans Power BI (processed/*.csv)

Contrôles qualité :

validation des clés (période + itinéraire/mode + ville)

vérification de complétude par période et par ville

détection de valeurs aberrantes (zéros incohérents, négatifs)

🗂️ Modèle de données (Power BI)

Le modèle repose sur un schéma en étoile :

Faits

Fait_mode : fréquentation par mode

Fait_route : fréquentation par itinéraire

Dimensions

Dim_City, Dim_Mode, Dim_Route, Dim_Mois, Dim_Année

Tableau de mesures

Mesures DAX (centralisation des KPI)

📊 Structure du tableau de bord 🔹 Page 1 — Vue d'ensemble

Objectif : vision globale du trafic.

Nombre total de passagers

Évolution temporelle (Chicago vs Philadelphie)

Répartition par mode et par ville

Volatilité de la demande

Taux d'atteinte des objectifs

🔹 Page 2 — Qualité de service (Mode vs Itinéraire)

Objectif : comparaison performance/stabilité entre modes et itinéraires.

Mode pièces vs itinéraire

Top 10 / Bottom 10 itinéraires

Mode de volatilité vs Route

Graphique « Performance vs Volatilité » pour une lecture décisionnelle

🔹 Page 3 — Comparaison Chicago vs Philadelphie

Objectif : benchmarking inter-villes.

KPI Chicago vs Philadelphie + écart

Évolution comparative dans le temps

Répartition par mode et différence de stabilité (volatilité)

📈 KPIs clés

Nombre total de passagers (Mode / Itinéraire)

Mode de pièce % / Itinéraire de la pièce %

Évolution mensuelle (MoM)

Volatilisation (écart-type)

Itinéraires du haut/du bas

Performance vs Volatilité (Mode vs Route)

Écart Chicago vs Philadelphie (valeur et %)

💡 Informations et recommandations

Piloter la stratégie au niveau des modes (levier principal du volume)

Optimiser les itinéraires sous-performantes (fréquence, itinéraires, priorisation)

Surveiller les segments à forte utilisation (stabilité du service)

Adapter les décisions par ville (benchmark Chicago vs Philadelphie)

📁 Contenu du dépôt

notebooks/ — notebooks Python (ETL / Nettoyage)

data/processed/ — données nettoyées prêtes Power BI

PowerBI_Dashboard.pbix — rapport Power BI

README.md — documentation

📁 Planification 
[Voici le lien de Jira](https://imanelen25-1770646756973.atlassian.net/jira/software/projects/KAN/boards/1?atlOrigin=eyJpIjoiNTA1ZjA3ZTlhNDc3NDc5ZTgxYmZhYTUyNzZjZDY2YjgiLCJwIjoiaiJ9)

