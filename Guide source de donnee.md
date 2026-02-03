# **Guide Pratique : Utilisation des APIs Temps Réel CTA (Chicago) et SEPTA (Philadelphie)**

Ce guide décrit comment utiliser les APIs **CTA Bus Tracker** et **SEPTA TransitView** pour récupérer des données en temps réel sur les transports urbains, et comment combiner cela avec les données historiques de ridership.

---

## 1. Sources de données historiques

| Source | Type | Contenu | Lien |
|--------|------|---------|------|
| CTA Ridership (Chicago) | RDF → CSV | Moyennes mensuelles par ligne et type de jour (depuis 2001) | [Télécharger](#) |
| SEPTA Ridership (Philadelphia) | CSV | Ridership moyen quotidien par arrêt et par mode | [Télécharger](#) |



----------



----------

## **2. APIs Temps Réel**

### **2.1 CTA Bus Tracker (Chicago)**

-   **Type** : REST API (JSON)
    
-   **Accès** : Clé API gratuite (obtenez-la [ici](https://www.transitchicago.com/developers/bustracker/))
    
-   **Fonctionnalités** :
    
    -   Liste des routes (`getroutes`)
    -   Liste des arrêts par route (`getstops`)
    -   Positions des véhicules en temps réel (`getvehicles`)
    -   Prédictions d’arrivée (`getpredictions`) – parfois indisponibles
    -   Calcul des fréquences et intervalles entre bus
-   **Limitations** :
    
    -   Certaines données peuvent être manquantes (arrêts, prédictions)
    -   La ponctualité ne peut être calculée que si `getpredictions` est disponible

#### **Exemple Python : Récupérer la liste des routes**

```python

import requests
import pandas as pd

CTA_API_KEY = "VOTRE_CLE_API"  # Remplacez par votre clé
CTA_BASE_URL = "https://www.ctabustracker.com/bustime/api/v3"

def get_cta_routes(api_key):
    params = {"key": api_key, "format": "json"}
    response = requests.get(f"{CTA_BASE_URL}/getroutes", params=params)
    data = response.json().get("bustime-response", {}).get("routes", [])
    return pd.DataFrame(data)
```
# Utilisation
df_routes = get_cta_routes(CTA_API_KEY)
print(df_routes.head())


**Résultat** : Un DataFrame contenant la liste des routes disponibles.

----------

### **2.2 SEPTA TransitView (Philadelphie)**

-   **Type** : REST API (JSON)
    
-   **Accès** : Public, pas de clé API nécessaire
    
-   **Fonctionnalités** :
    
    -   Positions GPS de tous les véhicules (`TransitViewAll`)
    -   Positions GPS par route spécifique (`TransitView`)
    -   Calcul des fréquences et intervalles entre véhicules
-   **Limitations** :
    
    -   Pas de prédictions d’arrivée
    -   Informations sur les arrêts manquantes (à compléter avec les données GTFS statiques)

#### **Exemple Python : Récupérer les positions de tous les véhicules**

```python

SEPTA_ALL_URL = "https://www3.septa.org/api/TransitViewAll/index.php"

def get_septa_vehicles():
    response = requests.get(SEPTA_ALL_URL)
    data = response.json().get("VehiclePositions", [])
    return pd.DataFrame(data)

# Utilisation
df_vehicles = get_septa_vehicles()
print(df_vehicles.head())

```
**Résultat** : Un DataFrame avec les positions en temps réel de tous les véhicules SEPTA.

----------

## **3. Exemple Complet : Analyse des Données Temps Réel**

Voici un script Python complet pour récupérer et analyser les données des deux APIs :

```python
import requests
import pandas as pd

# Configuration
CTA_API_KEY = "VOTRE_CLE_API"
CTA_BASE = "https://www.ctabustracker.com/bustime/api/v3"
SEPTA_ALL_URL = "https://www3.septa.org/api/TransitViewAll/index.php"

# Fonctions utilitaires
def call_cta(endpoint, params):
    try:
        response = requests.get(f"{CTA_BASE}/{endpoint}", params=params, timeout=10)
        response.raise_for_status()
        return response.json().get("bustime-response", {})
    except Exception as e:
        print(f"Erreur CTA : {e}")
        return None

def call_septa(url):
    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        return response.json()
    except Exception as e:
        print(f"Erreur SEPTA : {e}")
        return None

# 1. Récupérer les routes CTA
print("=== Routes CTA ===")
cta_routes = call_cta("getroutes", {"key": CTA_API_KEY, "format": "json"})
df_cta_routes = pd.DataFrame(cta_routes.get("routes", []))
print(df_cta_routes.head())

# 2. Récupérer les positions des véhicules SEPTA
print("\n=== Véhicules SEPTA ===")
septa_data = call_septa(SEPTA_ALL_URL)
df_septa_vehicles = pd.DataFrame(septa_data.get("VehiclePositions", []))
print(df_septa_vehicles.head())

# 3. Exemple d'analyse : Fréquence des véhicules par route
if not df_septa_vehicles.empty:
    freq_by_route = df_septa_vehicles["route"].value_counts()
    print("\nFréquence des véhicules par route :\n", freq_by_route)

```
----------

## **4. Conseils pour Aller Plus Loin**

-   **Combiner avec les données historiques** : Utilisez les données de fréquentation pour analyser les tendances et les retards.
-   **Automatiser la collecte** : Planifiez des appels réguliers aux APIs pour suivre l’évolution des données.
-   **Visualiser les résultats** : Utilisez des bibliothèques comme `matplotlib` ou `folium` pour cartographier les positions des véhicules.

----------

## **5. Ressources Utiles**

-   [Documentation officielle CTA](https://www.transitchicago.com/developers/bustracker/)
-   [Documentation SEPTA](https://api.septa.org/)

