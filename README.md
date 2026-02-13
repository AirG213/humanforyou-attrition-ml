# HumanForYou Attrition ML

Machine Learning project to analyze and predict employee attrition.

## Prerequisites
- Python 3 must be installed on your machine and available in your `PATH`.

## Installation
1. Create a virtual environment:
   ```powershell
   python -m venv .venv
   ```
2. Activate the virtual environment:
   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```
   If security error occurs :
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned .\.venv\Scripts\Activate.ps1
   ```  
3. Install dependencies from `requirements.txt`:
   ```powershell
   python -m pip install -r requirements.txt
   ```

## Objective
Identify key drivers of attrition and build predictive models.

## Data Sources
- HR data
- Manager evaluation
- Employee survey
- In/Out working time logs

## Pipeline

| # | Notebook | Output |
|---|---|---|
| 01 | `01_EDA.ipynb` | `data/processed/eda_summary.csv` |
| 02 | `02_Preprocessing.ipynb` | `data/processed/cleaned_attrition_base.csv` |
| 03 | `03_FeatureEngineering_Badgeuse.ipynb` | `data/processed/attrition_with_time_features.csv` |
| 04 | `04_KMeans_Exploration.ipynb` | `data/processed/kmeans_attrition_clusters.csv`, `kmeans_metrics.json` |


## Prosit 1 livrables

**Exports** (dans `data/processed/`) :
1. `eda_summary.csv` — résumé statistique EDA
2. `cleaned_attrition_base.csv` — dataset nettoyé et encodé
3. `attrition_with_time_features.csv` — features badgeuse ajoutées
4. `kmeans_attrition_clusters.csv` — dataset avec colonne cluster
5. `kmeans_metrics.json` — métriques KMeans (k sélectionné automatiquement via silhouette maximale)

**Figures** (sauvegardées dans `reports/figures/`, dpi 300) :
1. `kmeans_k_selection.png` — Choix de k (silhouette maximale + elbow)
2. `kmeans_pca.png` — Scatter PCA 2D coloré par cluster avec taux attrition
3. `kmeans_attrition.png` — Barplot taux d'attrition par cluster
4. `kmeans_top_features.png` — Top 10 features discriminantes (variance inter-cluster)

**Méthode KMeans** :
- Nombre de clusters : sélection automatique via **silhouette maximale** (argmax sur k=2→10)
- Paramètres : random_state=42
- Features : standardisées (StandardScaler)

**How to run** :
```bash
pip install -r requirements.txt
jupyter notebook
# Exécuter les notebooks dans l'ordre 01 → 04
```
