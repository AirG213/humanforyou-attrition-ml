# HumanForYou Attrition ML

Analyse et prédiction de l'attrition des employés par Machine Learning.

## Installation

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

## Lancer le projet

Exécuter les notebooks dans l'ordre `01` → `08`, ou lancer `run_all_notebooks.ipynb` pour tout exécuter d'un coup.

```powershell
jupyter notebook
```

## Architecture

```
data/
├── raw/                        # Données brutes (CSV source)
│   └── in_out_time/            # Fichiers badgeuse
└── processed/                  # Sorties générées par les notebooks
notebooks/
├── 01_EDA.ipynb                # Analyse exploratoire
├── 02_Preprocessing.ipynb      # Nettoyage, fusion, encodage
├── 03_FeatureEngineering_Badgeuse.ipynb  # Feature avg_work_hours
├── 04_KMeans_Exploration.ipynb # Clustering (KMeans + PCA)
├── 05_Regression_Preparation.ipynb      # Train/test split + scaling
├── 06_Regression_Lineaire.ipynb         # Régression logistique
├── 07_Regression_Comparaison_Modeles.ipynb  # Benchmark multi-modèles
├── 08_Conclusion.ipynb         # Synthèse et recommandations
└── run_all_notebooks.ipynb     # Exécution séquentielle complète
reports/
├── bibliographie/              # Bibliographie APA
├── ethics/                     # Livrable éthique (RGPD, guidelines UE)
├── presentation/               # Slides de présentation 
└── figures/                    # Graphiques exportés (PNG, 300 dpi)
workshops/                      # Workshops (EDA, régression, classification)
```

## Pipeline

| # | Notebook | Entrée | Sortie |
|---|---|---|---|
| 01 | EDA | `data/raw/*` | `eda_summary.csv` |
| 02 | Preprocessing | `data/raw/*` | `attrition_merged_base.csv` |
| 03 | Feature Engineering | `attrition_merged_base.csv` + badgeuse | `attrition_with_avg_hours.csv` |
| 04 | KMeans | `attrition_with_avg_hours.csv` | `kmeans_clusters.csv` |
| 05 | Préparation régression | `kmeans_clusters.csv` | `attrition_train_prepared.csv`, `attrition_test_prepared.csv` |
| 06 | Régression logistique | train/test prepared | métriques, coefficients, prédictions |
| 07 | Comparaison modèles | train/test prepared | comparaison, CV scores, prédictions |
| 08 | Conclusion | `data/processed/*` | — |

Chaque notebook lit la sortie du précédent dans `data/processed/`.
