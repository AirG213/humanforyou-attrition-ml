# Livrable éthique — Projet IA HumanForYou (Attrition)

## 1. Contexte et finalité du projet

HumanForYou est une entreprise pharmaceutique (environ 4 000 employés, **4 410 dans le jeu de données**) confrontée à un taux de rotation annuel d'environ 15 % (**16,12 % mesuré dans le dataset** — 711 départs sur 4 410 employés).
Le projet vise à :

- identifier les facteurs influençant l'attrition,
- proposer un modèle prédictif permettant d'anticiper les départs,
- formuler des recommandations d'amélioration (rétention, conditions de travail, organisation).

**Positionnement éthique** : le modèle est un **outil d'aide à la décision**. Il ne doit pas automatiser des décisions RH individuelles (sanctions, licenciements, promotions).

---

## 2. Données utilisées et sensibilité

Sources de données (anonymisées, **4 410 employés identifiés par EmployeeID** dans chaque fichier) :

- **general_data.csv** (4 410 × 24) : données RH générales — profil (Age, Gender, MaritalStatus, Education, EducationField), poste (Department, JobRole, JobLevel), salaire (MonthlyIncome, PercentSalaryHike, StockOptionLevel), ancienneté (YearsAtCompany, TotalWorkingYears, YearsSinceLastPromotion, YearsWithCurrManager, NumCompaniesWorked), déplacements (BusinessTravel, DistanceFromHome), formation (TrainingTimesLastYear), et la variable cible Attrition (Yes/No).
- **manager_survey_data.csv** (4 410 × 3) : évaluation manager — implication (JobInvolvement, 1-4) et performance (PerformanceRating, 1-4). **Aucune valeur manquante.**
- **employee_survey_data.csv** (4 410 × 4) : enquête QVT — satisfaction environnement (EnvironmentSatisfaction), satisfaction travail (JobSatisfaction), équilibre vie pro/perso (WorkLifeBalance), chacune notée de 1 à 4. **83 non-réponses au total** (25 + 20 + 38 NA).
- **in_time.csv / out_time.csv** (4 410 × 262) : horaires d'entrée/sortie (badgeuse), couvrant **261 jours ouvrés** du 1er janvier au 31 décembre 2015. **9,5 % de cellules NA** (absences, congés, jours non travaillés).

**Variables constantes détectées** :

- `EmployeeCount` : toujours égal à 1,
- `Over18` : toujours égal à "Y",
- `StandardHours` : toujours égal à 8.

**Valeurs manquantes dans general_data** :

- `NumCompaniesWorked` : 19 NA (0,4 %),
- `TotalWorkingYears` : 9 NA (0,2 %).

**Sensibilité** :

- données RH = données potentiellement sensibles (vie professionnelle, habitudes, satisfaction),
- certaines variables peuvent être liées à des caractéristiques personnelles : Age (18-60 ans), Gender (60 % hommes / 40 % femmes), MaritalStatus (Married/Single/Divorced), Education (1-5), EducationField (6 domaines), Department (R&D / Sales / HR),
- risque de ré-identification si croisement, même avec identifiants anonymes (EmployeeID 1 à 4 410),
- le département HR ne compte que 189 employés (4,3 % du total), ce qui augmente le risque de ré-identification dans ce sous-groupe.

---

## 3. Méthodologie d'analyse éthique

Cadre utilisé : **7 exigences d'une IA digne de confiance (Commission Européenne)**.
Application tout au long du projet :

- préparation et gouvernance des données,
- choix des variables / traitements,
- choix des modèles et des métriques,
- interprétation et recommandations,
- communication et garde-fous d'usage.

Pour chaque exigence :

- risques identifiés,
- décisions prises en équipe,
- contrôles / mesures de mitigation.

---

## 4. Exigence 1 — Respect de l'autonomie humaine

### Risques

- décision RH automatisée basée sur un score,
- pression managériale ("surveillance" / "profilage"),
- perte de contrôle humain sur les décisions.

### Décisions d'équipe

- le score d'attrition ne déclenche **aucune action automatique**,
- toute décision RH reste **humaine, documentée, contextualisée**,
- priorité à des recommandations **collectives/organisationnelles** plutôt qu'individuelles.

### Contrôles

- procédure RH écrite : "score = indicateur, pas verdict",
- revue humaine obligatoire avant toute action,
- traçabilité des décisions (raison, contexte, justification).

---

## 5. Exigence 2 — Robustesse technique et sécurité

### Risques

- sur-apprentissage (overfitting) donnant de fausses alertes,
- modèles instables selon l'échantillon,
- **données manquantes constatées** : 19 NA dans NumCompaniesWorked, 9 NA dans TotalWorkingYears, 83 non-réponses dans l'enquête QVT (EnvironmentSatisfaction : 25, JobSatisfaction : 20, WorkLifeBalance : 38), et 9,5 % de NA dans les données de badgeuse (absences),
- **3 variables constantes** (EmployeeCount, Over18, StandardHours) n'apportent aucune information discriminante,
- **déséquilibre de classes** : 83,9 % No vs 16,1 % Yes sur la variable Attrition — risque de modèle biaisé vers la classe majoritaire,
- dérive dans le temps (changement organisationnel, données de 2015 uniquement).

### Décisions d'équipe

- séparation train/test + validation croisée,
- comparaison de plusieurs modèles,
- choix final fondé sur métriques pertinentes, stabilité et interprétabilité.

### Contrôles

- suivi des performances (F1, AUC, rappel) dans le temps,
- tests de sensibilité (performance par sous-groupes),
- règles de "retraining" planifiées si dérive.

---

## 6. Exigence 3 — Confidentialité et gouvernance des données

### Risques

- accès non autorisé (données RH),
- ré-identification indirecte (croisement variables) — risque accru pour les petits sous-groupes (ex. : 189 employés HR, 81 en EducationField "Human Resources"),
- conservation trop longue ou diffusion non contrôlée,
- l'enquête QVT comporte 83 non-réponses : les employés n'ayant pas répondu pourraient présenter un profil spécifique (biais de sélection à surveiller).

### Décisions d'équipe

- traitement local dans un repo restreint,
- pas d'export de données brutes dans des rapports publics,
- minimisation : ne garder que les colonnes utiles.

### Contrôles

- accès limité aux membres du projet,
- séparation "raw" / "processed",
- suppression/masquage des sorties contenant des informations sensibles,
- documentation de provenance et transformations.

---

## 7. Exigence 4 — Transparence

### Risques

- "boîte noire" : décisions incomprises,
- mauvaise interprétation des scores,
- absence d'explication des variables importantes.

### Décisions d'équipe

- privilégier des modèles explicables (baseline logistique, arbres),
- documenter les étapes (nettoyage, encodage, choix variables),
- produire une explication claire des facteurs influents.

### Contrôles

- fiches explicatives (variables, limites, interprétation),
- rapport simplifié pour non-techniciens,
- avertissements : corrélation ≠ causalité.

---

## 8. Exigence 5 — Diversité, non-discrimination et équité

### Risques

- discrimination directe/indirecte via variables sensibles (Age, Gender, MaritalStatus, EducationField, **Department**),
- reproduction de biais historiques,
- décisions injustes pour certains groupes.

**Disparités d'attrition constatées dans les données** :

| Variable | Groupe à risque élevé | Taux d'attrition | Groupe à risque faible | Taux d'attrition |
|---|---|---|---|---|
| MaritalStatus | Single | **25,5 %** | Divorced | 10,1 % |
| Department | Human Resources | **30,2 %** | Sales | 15,0 % |
| EducationField | Human Resources | **40,7 %** | Technical Degree | 11,4 % |
| Gender | Male | 16,7 % | Female | 15,3 % |
| JobLevel | Niveau 2 | 17,8 % | Niveau 5 | 13,0 % |

> ⚠️ Les célibataires, le département HR et le domaine d'étude HR présentent des taux d'attrition nettement supérieurs. Ces écarts doivent être surveillés pour éviter toute discrimination indirecte dans les recommandations.

### Décisions d'équipe

- analyser la performance du modèle par sous-groupes (Gender, MaritalStatus, Department, EducationField),
- tester l'impact des variables sensibles (avec/sans),
- éviter toute recommandation ciblant des attributs protégés,
- vérifier que le modèle ne pénalise pas injustement les célibataires ou les employés HR.

### Contrôles

- audit fairness (écarts de rappel/FP/FN par groupe),
- possibilité de retirer/neutraliser certaines variables,
- validation par une règle métier RH : "pas d'action basée sur attribut protégé",
- comparaison systématique des taux de faux positifs/négatifs entre sous-groupes sensibles.

---

## 9. Exigence 6 — Bien-être environnemental et sociétal

### Risques

- climat de défiance (surveillance),
- stress des employés si score utilisé individuellement,
- dérives managériales (micro-management).

### Décisions d'équipe

- cadrage "amélioration des conditions de travail",
- recommandations orientées politiques RH (formation, mobilité, organisation),
- pas de scoring communiqué aux managers sans formation.

### Contrôles

- charte d'usage,
- formation des utilisateurs (RH/management),
- indicateurs de suivi QVT post-déploiement.

---

## 10. Exigence 7 — Responsabilité

### Risques

- dilution des responsabilités ("c'est le modèle qui l'a dit"),
- absence de redevabilité en cas d'erreur.

### Décisions d'équipe

- responsabilité RH sur décisions,
- responsabilité équipe data sur qualité modèle, documentation, limites,
- mécanisme de remontée d'incidents.

### Contrôles

- registre des versions (modèle, date, métriques),
- procédure de contestation / revue,
- comité de validation avant mise en production (même fictif).

---

## 11. Décisions éthiques transverses (engagements)

- Modèle = aide à la décision, jamais automatisation.
- Transparence : expliquer variables et limites.
- Minimisation des données : n'utiliser que le nécessaire.
- Surveillance des biais : contrôle par sous-groupes.
- Sécurité : accès restreint, séparation raw/processed.
- Traçabilité : documenter chaque transformation et chaque choix.

---

## 12. Points de vigilance identifiés après vérification des données

Cette section a été complétée après analyse exploratoire du dataset.

### 12.1 Taux de non-réponse à l'enquête QVT (biais de sélection)

- **83 non-réponses** sur 4 410 employés × 3 questions :
  - EnvironmentSatisfaction : 25 NA (0,6 %),
  - JobSatisfaction : 20 NA (0,5 %),
  - WorkLifeBalance : 38 NA (0,9 %).
- **Point de vigilance** : les non-répondants pourraient avoir un profil atypique (insatisfaits ou désengagés). Il faudra vérifier si le taux de non-réponse est corrélé à l'attrition, et traiter ces valeurs manquantes de manière transparente (imputation, suppression, ou indicateur de non-réponse).

### 12.2 Variables constantes / inutiles (minimisation)

- **3 variables constantes** identifiées, à supprimer avant modélisation :
  - `EmployeeCount` : toujours 1 (redondant),
  - `Over18` : toujours "Y" (aucune variance),
  - `StandardHours` : toujours 8 (aucune variance).
- Ces variables n'apportent aucune information discriminante et doivent être retirées conformément au principe de minimisation des données.

### 12.3 Valeurs manquantes dans les données RH (robustesse)

- `NumCompaniesWorked` : 19 NA (0,4 %) — parcours professionnel manquant,
- `TotalWorkingYears` : 9 NA (0,2 %) — expérience totale manquante.
- **Données badgeuse** : 9,5 % de cellules NA dans in_time/out_time (absences, congés, jours fériés) — normal mais à documenter lors du calcul de features horaires.
- **Point de vigilance** : l'évaluation manager (manager_survey_data) ne comporte **aucune valeur manquante**, ce qui contraste avec l'enquête QVT et soulève la question de la fiabilité (obligation de réponse ? données imputées ?).

### 12.4 Premiers indices de biais par groupe (équité)

- **MaritalStatus** : les célibataires (Single) ont un taux d'attrition de 25,5 %, soit 2,5× celui des divorcés (10,1 %) et 2× celui des mariés (12,5 %). Un modèle pourrait reproduire ce biais.
- **Department** : le département HR présente un taux d'attrition de 30,2 % contre 15 % pour Sales et 15,7 % pour R&D. Ce département ne compte que 189 employés (4,3 % du total), ce qui le rend à la fois statistiquement fragile et facilement identifiable.
- **EducationField** : le domaine "Human Resources" affiche 40,7 % d'attrition (81 employés seulement) contre 11,4 % pour "Technical Degree".
- **Gender** : écart modéré (Male 16,7 % vs Female 15,3 %), à surveiller dans les prédictions.
- **Déséquilibre de classes** : la variable cible Attrition est déséquilibrée (83,9 % No / 16,1 % Yes) — nécessite une stratégie adaptée (stratification, SMOTE, pondération, métrique adaptée comme F1/rappel plutôt qu'accuracy).

### 12.5 Cohérence inter-fichiers

- Les 4 fichiers contiennent exactement **4 410 EmployeeID identiques** (1 à 4 410), confirmant la cohérence du dataset.
- Aucun employé absent d'un fichier par rapport à un autre.

### 12.6 Risques de ré-identification

- Les sous-groupes de petite taille augmentent le risque de ré-identification :
  - Department HR : 189 employés,
  - EducationField HR : 81 employés,
  - JobRole "Human Resources" : 156 employés.
- Le croisement de Department + JobLevel + Gender + Age pourrait suffire à identifier un individu. Vigilance renforcée sur les sorties de modèle pour ces sous-groupes.

---

## 13. Conclusion

Le projet vise à réduire l'attrition en identifiant des facteurs d'influence et en proposant des actions d'amélioration.
L'IA doit rester **contrôlée**, **explicable**, **non-discriminante** et **au service du bien-être** des employés, avec une **responsabilité humaine** explicite.
