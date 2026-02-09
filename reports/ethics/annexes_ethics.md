# Annexes - Livrable éthique HumanForYou

## Table des matières

- [1. Solutions envisagées - Analyse détaillée](#1-solutions-envisagées---analyse-détaillée)
  * [1.1. Tableau des solutions possibles](#11-tableau-des-solutions-possibles)
  * [1.2. Analyse des impacts par solution](#12-analyse-des-impacts-par-solution)
  * [1.3. Mesures d'atténuation identifiées](#13-mesures-datténuation-identifiées)
- [2. Parties prenantes - Analyse détaillée](#2-parties-prenantes---analyse-détaillée)
- [3. Dilemmes éthiques détaillés](#3-dilemmes-éthiques-détaillés)
- [4. Points de vigilance dataset - Détails chiffrés](#4-points-de-vigilance-dataset---détails-chiffrés)
  * [4.1. Taux de non-réponse à l'enquête QVT](#41-taux-de-non-réponse-à-lenquête-qvt-biais-de-sélection)
  * [4.2. Variables constantes / inutiles](#42-variables-constantes--inutiles-minimisation)
  * [4.3. Valeurs manquantes dans les données RH](#43-valeurs-manquantes-dans-les-données-rh-robustesse)
  * [4.4. Premiers indices de biais par groupe](#44-premiers-indices-de-biais-par-groupe-équité)
  * [4.5. Risques de ré-identification détaillés](#45-risques-de-ré-identification-détaillés)
- [5. Glossaire technique](#5-glossaire-technique)

---

## 1. Solutions envisagées - Analyse détaillée

### 1.1 Tableau des solutions possibles

| # | Solution envisagée | Description |
|---|---|---|
| A | Modèle prédictif complet | Utilisation de toutes les variables disponibles, y compris sensibles, pour maximiser la performance prédictive. |
| B | Modèle explicable simplifié | Modèle restreint à des variables non-sensibles et interprétables (régression logistique, arbre de décision). |
| C | Analyse descriptive uniquement | Pas de modèle prédictif. Identification statistique des facteurs d'attrition sans scoring individuel. |
| D | Utilisation agrégée uniquement | Modèle entraîné mais résultats communiqués uniquement sous forme de tendances collectives, sans score individuel. |

### 1.2 Analyse des impacts par solution
| Solution | Impacts positifs | Impacts négatifs | Risque éthique principal |
|---|---|---|---|
| **A - Modèle complet** | Meilleure précision. Détection fine des profils à risque. | Utilisation de variables sensibles. Risque de discrimination indirecte. Opacité possible. | Discrimination, profilage individuel, boîte noire. |
| **B - Modèle explicable** | Transparence. Explicabilité des facteurs. Confiance des parties prenantes. | Performance potentiellement réduite. Perte d'information. | Sous-détection de certains profils à risque. |
| **C - Analyse descriptive** | Aucun scoring individuel. Risque éthique minimal. | Pas de capacité prédictive. Recommandations moins ciblées. | Sous-exploitation des données, inefficacité pour le client. |
| **D - Utilisation agrégée** | Équilibre entre performance et protection. Recommandations collectives. | Pas d'alerte individuelle. Peut masquer des situations critiques. | Perte de granularité, risque de non-détection. |

### 1.3 Mesures d'atténuation identifiées

- **Pour la solution A** : audit fairness, retrait/neutralisation des variables sensibles, seuils de décision différenciés.
- **Pour la solution B** : enrichissement par SHAP/LIME pour compenser la simplicité du modèle.
- **Pour la solution D** : complément par des indicateurs QVT agrégés et des entretiens RH.

---

## 2. Parties prenantes - Analyse détaillée

| Partie prenante | Rôle / Intérêt | Exposition au risque |
|---|---|---|
| **Employés** | Sujets des données. Impactés par les décisions RH dérivées du modèle. | Élevée : profilage, discrimination, surveillance. |
| **Service RH** | Commanditaire. Utilisateur direct des résultats. | Moyenne : responsabilité décisionnelle, risque de mauvais usage. |
| **Managers** | Évaluateurs (manager_survey). Destinataires potentiels des scores. | Moyenne : pression au micro-management, biais de confirmation. |
| **Direction** | Décideur final sur les politiques de rétention. | Faible directement, mais responsabilité institutionnelle. |
| **Équipe data** | Concepteurs du modèle. Responsables de la qualité technique et éthique. | Moyenne : responsabilité sur les biais, la documentation, les limites. |
| **Clients / partenaires** | Impactés indirectement par la qualité des équipes (retard projets). | Faible. |
| **Société** | Impact sociétal de l'usage de l'IA en RH. Précédent pour d'autres entreprises. | Faible directement, mais enjeu normatif. |

---

## 3. Dilemmes éthiques détaillés

| Dilemme | Tension | Position retenue |
|---|---|---|
| **Précision vs équité** | L'inclusion de variables sensibles (MaritalStatus, Gender) améliore la précision du modèle mais introduit un risque de discrimination indirecte. | Tester les modèles avec et sans variables sensibles. Privilégier l'équité si l'écart de performance est acceptable. |
| **Variables sensibles vs perte d'information** | Retirer MaritalStatus supprime un facteur prédictif fort (25,5 % d'attrition chez les célibataires). | Conserver la variable pour l'analyse descriptive, mais auditer son impact sur les prédictions par sous-groupe. |
| **Performance business vs protection individuelle** | La direction souhaite des résultats actionnables. Les employés souhaitent ne pas être profilés. | Résultats communiqués sous forme agrégée (tendances, facteurs). Pas de liste nominative de « risques de départ ». |
| **Transparence totale vs protection du modèle** | Publier tous les détails du modèle permet la reproductibilité mais peut induire des comportements d'évitement (gaming). | Documentation complète pour l'équipe et le jury. Communication simplifiée et orientée « facteurs d'amélioration » pour l'entreprise. |
| **Exhaustivité des données vs minimisation** | Utiliser les 261 jours de badgeuse enrichit le modèle mais constitue une forme de surveillance granulaire. | Agréger les données horaires en indicateurs synthétiques (heures moyennes, régularité) plutôt que d'utiliser les pointages individuels jour par jour. |

---

## 4. Points de vigilance dataset - Détails chiffrés

### 4.1 Taux de non-réponse à l'enquête QVT (biais de sélection)

- **83 non-réponses** sur 4 410 employés × 3 questions :
  - EnvironmentSatisfaction : 25 NA (0,6 %),
  - JobSatisfaction : 20 NA (0,5 %),
  - WorkLifeBalance : 38 NA (0,9 %).
- **Point de vigilance** : les non-répondants pourraient avoir un profil atypique (insatisfaits ou désengagés). Il faudra vérifier si le taux de non-réponse est corrélé à l'attrition, et traiter ces valeurs manquantes de manière transparente (imputation, suppression, ou indicateur de non-réponse).

### 4.2 Variables constantes / inutiles (minimisation)

- **3 variables constantes** identifiées, à supprimer avant modélisation :
  - `EmployeeCount` : toujours 1 (redondant),
  - `Over18` : toujours "Y" (aucune variance),
  - `StandardHours` : toujours 8 (aucune variance).

### 4.3 Valeurs manquantes dans les données RH (robustesse)

- `NumCompaniesWorked` : 19 NA (0,4 %) - parcours professionnel manquant,
- `TotalWorkingYears` : 9 NA (0,2 %) - expérience totale manquante.
- **Données badgeuse** : 9,5 % de cellules NA dans in_time/out_time (absences, congés, jours fériés).
- **Contraste** : l'évaluation manager (manager_survey_data) ne comporte aucune valeur manquante, ce qui questionne la fiabilité (obligation de réponse ? données imputées ?).

### 4.4 Premiers indices de biais par groupe (équité)

- **MaritalStatus** : les célibataires (Single) ont un taux d'attrition de 25,5 %, soit 2,5× celui des divorcés (10,1 %) et 2× celui des mariés (12,5 %).
- **Department** : le département HR présente un taux d'attrition de 30,2 % contre 15 % pour Sales et 15,7 % pour R&D. Ce département ne compte que 189 employés (4,3 % du total).
- **EducationField** : le domaine "Human Resources" affiche 40,7 % d'attrition (81 employés seulement) contre 11,4 % pour "Technical Degree".
- **Gender** : écart modéré (Male 16,7 % vs Female 15,3 %), à surveiller dans les prédictions.
- **Déséquilibre de classes** : 83,9 % No / 16,1 % Yes sur la variable cible Attrition.

### 4.5 Risques de ré-identification détaillés

- Sous-groupes de petite taille :
  - Department HR : 189 employés,
  - EducationField HR : 81 employés,
  - JobRole "Human Resources" : 156 employés.
- Le croisement de Department + JobLevel + Gender + Age pourrait suffire à identifier un individu dans ces petits sous-groupes.

---

## 5. Glossaire technique

**Déséquilibre de classes** : Situation où la variable cible (Attrition) présente des proportions très inégales (83,9% No vs 16,1% Yes), nécessitant des techniques de rééquilibrage.

**Disparité d'impact (Disparate Impact)** : Mesure si un modèle produit des résultats différents entre groupes protégés, indépendamment de l'intention discriminatoire.

**Données de badgeuse** : Enregistrements automatiques des heures d'entrée/sortie des employés, ici utilisés pour détecter des signes de surcharge de travail.

**EmployeeID** : Identifiant technique anonymisé (1 à 4410) permettant le croisement des 4 fichiers de données sans révéler l'identité.

**JobLevel** : Niveau hiérarchique dans l'entreprise (1 = junior, 5 = senior management), variable ordinale structurante.

**Manager Survey** : Évaluation par le supérieur hiérarchique de l'implication et de la performance de l'employé (JobInvolvement, PerformanceRating).

**MaritalStatus** : État civil de l'employé (Single/Married/Divorced), variable sensible protégée nécessitant une vigilance anti-discrimination.

**Ré-identification** : Risque de pouvoir identifier un individu spécifique à partir du croisement de variables, particulièrement élevé dans les petits sous-groupes.

**Variables constantes** : Variables ayant la même valeur pour tous les individus du dataset, donc inutiles pour la modélisation prédictive.

**Variables sensibles** : Attributs protégés par la législation anti-discrimination (âge, genre, état civil, département) nécessitant un audit de biais systématique.