# Prosit 2 — Prédictions immobilières par régression

## Contexte

Notre société immobilière souhaite automatiser la prédiction des prix de vente de ses biens. Les données disponibles décrivent des **block groups** (quartiers) californiens : superficie, âge médian des logements, nombre de pièces, proximité de l'océan, revenu médian des ménages, etc.

Un expert en IA a proposé d'utiliser des **modèles de régression** pour estimer le **prix médian** d'un logement à partir de l'ensemble de ces attributs. Le pipeline de traitement des données est déjà en place (issu du prosit précédent). Il reste à choisir le bon modèle, à l'entraîner et à évaluer sa pertinence.

---

## Étape 1 — Clarification des termes

Avant d'aller plus loin, assurons-nous de bien comprendre le vocabulaire utilisé.

| Terme | Définition à construire |
|---|---|
| Régression | ? |
| Régression linéaire simple | ? |
| Régression linéaire multiple | ? |
| Régression non linéaire (polynomiale, par noyau…) | ? |
| Apprentissage supervisé | ? |
| Sur-apprentissage (overfitting) | ? |
| Sous-apprentissage (underfitting) | ? |
| Validation croisée | ? |
| Jeu d'entraînement / jeu de test | ? |

> **Objectif :** être capable de définir chacun de ces termes avec ses propres mots à la fin du prosit.

---

## Étape 2 — Définition du problème

À partir de l'énoncé, formulez le problème de manière structurée :

- **Quelle est la variable cible** (ce que l'on souhaite prédire) ?
- **Quelles sont les variables d'entrée** (attributs disponibles dans le jeu de données) ?
- **Quel type de tâche** s'agit-il : classification ou régression ? Justifiez.
- **Pourquoi une approche de régression** semble-t-elle pertinente ici ?

---

## Étape 3 — Brainstorming & hypothèses de travail

### 3.1 — Intuitions sur les relations entre attributs et prix

Avant de modéliser quoi que ce soit, réfléchissez aux relations intuitives entre les attributs et le prix médian d'un logement :

- Quel impact la **proximité de l'océan** peut-elle avoir sur le prix ?
- Quel lien peut-on établir entre le **revenu médian des ménages** et le prix d'achat ?
- Une **grande famille** aura-t-elle tendance à acheter un bien plus grand, donc plus cher ?
- D'autres attributs vous semblent-ils particulièrement influents ? Lesquels et pourquoi ?

> Ces réflexions sont importantes : elles permettent de **valider ou d'invalider** les résultats obtenus par le modèle une fois entraîné.

### 3.2 — Formulation d'une hypothèse de modélisation

En supposant que les relations entre les attributs et le prix soient approximativement linéaires :

- Comment peut-on exprimer mathématiquement $\hat{y}$ (le prix estimé) en fonction des attributs $x_1, x_2, \ldots, x_n$ ?
- Quels sont les paramètres inconnus de ce modèle ?
- Comment pourrait-on **trouver les valeurs optimales** de ces paramètres ?

---

## Étape 4 — Ce que l'on sait / Ce que l'on doit apprendre

| Ce que l'on sait déjà | Ce que l'on doit approfondir |
|---|---|
| Les données sont nettoyées et préparées (prosit 1) | Comment fonctionne la descente du gradient ? |
| Il existe un lien probable entre attributs et prix | Quels paramètres influencent l'apprentissage (learning rate, epochs) ? |
| L'overfitting est un risque à anticiper | Comment mesurer la qualité d'un modèle de régression ? |
| Scikit-Learn propose des outils de régression | Quelles métriques utiliser : MSE, RMSE, R² ? |
| | Qu'est-ce que la validation croisée et pourquoi l'utiliser ? |
| | Quand préférer une régression non linéaire ? |

---

## Étape 5 — Objectifs d'apprentissage

À l'issue de ce prosit, vous devrez être capables de :

1. **Identifier** une tâche de régression à partir d'un problème réel
2. **Distinguer** régression linéaire simple, multiple, et non linéaire (polynomiale, par noyau…)
3. **Expliquer** le principe de la descente du gradient et son rôle dans l'optimisation du modèle
4. **Définir** une fonction objectif (MSE, RMSE) et justifier son usage
5. **Calculer et interpréter** les métriques de performance : MSE, RMSE, R²
6. **Détecter** des signes de sur-apprentissage ou de sous-apprentissage à partir des résultats
7. **Proposer** des pistes d'amélioration du modèle si les performances sont insuffisantes

---

## Étape 6 — Plan de travail

### Travail individuel (préparation)

- Lire les ressources fournies :
  - *Descente de gradient* (Partie 1 — concepts mathématiques)
  - *Linear Regression* (Partie 2 — mise en application)
  - Conférence Pipeline ML — M. A. Benatia
- Revoir les notions de statistiques descriptives (moyenne, variance, distribution normale)
- Se familiariser avec l'API Scikit-Learn (`LinearRegression`, `SGDRegressor`, `cross_val_score`)

### Travail en groupe (séance prosit)

1. Mettre en commun les définitions de l'étape 1
2. Formuler collectivement le problème (étape 2)
3. Débattre des hypothèses (étape 3) et aboutir à une formulation mathématique partagée
4. Compléter et valider le tableau étape 4
5. Prioriser les objectifs d'apprentissage et se répartir les recherches complémentaires
6. Planifier la réalisation du **WS_Regression.ipynb**

---

## Ressources

| Type | Titre |
|---|---|
| Conférence | Pipeline Machine Learning — M. A. Benatia (`PipelineML_BENATIA.pdf`) |
| Ressource mathématique | Partie 1 — Descente de gradient `[zip]` |
| Ressource applicative | Partie 2 — Linear Regression `[zip]` |
| Ouvrage | *Python Data Science Handbook*, Jake VanderPlas |
| Documentation | [Scikit-learn — Linear Models](https://scikit-learn.org/stable/modules/linear_model.html) |
| Workshop | `WS_Regression.ipynb` |

---

## Notes pour aller plus loin

- Pourquoi normaliser / standardiser les données avant d'entraîner un modèle linéaire ?
- Qu'est-ce que la **régularisation** (Ridge, Lasso) et dans quel cas l'utiliser ?
- La descente de gradient garantit-elle toujours de trouver le meilleur modèle possible ? Pourquoi ?
- Comment interpréter les **résidus** d'un modèle pour diagnostiquer ses faiblesses ?
