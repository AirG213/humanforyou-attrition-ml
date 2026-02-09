# Annexes - Livrable éthique HumanForYou

## Table des matières

- [A1. Dictionnaire des données](#a1-dictionnaire-des-données)
- [A2. Valeurs manquantes et variables constantes](#a2-valeurs-manquantes-et-variables-constantes)
- [A3. Disparités par sous-groupes](#a3-disparités-par-sous-groupes)
- [A4. Risques de ré-identification](#a4-risques-de-ré-identification)
- [A5. Dilemmes éthiques](#a5-dilemmes-éthiques)

---

## A1. Dictionnaire des données

### Variables sensibles identifiées

| Variable | Type | Description | Justification sensibilité |
|---|---|---|---|
| **Gender** | Catégorique | Male/Female | Attribut protégé, risque discrimination de genre |
| **MaritalStatus** | Catégorique | Single/Married/Divorced | Discrimination familiale, disparité forte (Single 25,5%) |
| **Age** | Numérique | Âge employé | Discrimination âge, corrélation salaire/ancienneté |
| **Department** | Catégorique | HR/Sales/R&D | Petits groupes (HR=189), stéréotypes métiers |
| **EducationField** | Catégorique | Domain d'études | Très petits groupes (HR=81), biais formation |
| **JobRole** | Catégorique | Poste occupé | Croisement avec autres variables = ré-identification |

### Variables métier critiques

| Variable | Type | Usage éthique | Précautions |
|---|---|---|---|
| **EmployeeID** | Identifiant | Liaison fichiers uniquement | Ne jamais communiquer, anonymisation |
| **Attrition** | Binaire | Variable cible | Usage collectif, pas de scoring individuel |
| **MonthlyIncome** | Numérique | Facteur équité salariale | Audit disparités par sous-groupes |
| **PerformanceRating** | Ordinal | Évaluation manager | Risque biais évaluateur, corrélation attrition |

---

## A2. Valeurs manquantes et variables constantes

### Tableau des valeurs manquantes

| Fichier | Variable | NA count | % manquant | Impact modèle |
|---|---|---|---|---|
| general_data.csv | NumCompaniesWorked | 19 | 0,4% | Faible |
| general_data.csv | TotalWorkingYears | 9 | 0,2% | Faible |
| employee_survey_data.csv | EnvironmentSatisfaction | 25 | 0,6% | Moyen (biais sélection QVT) |
| employee_survey_data.csv | JobSatisfaction | 20 | 0,5% | Moyen (biais sélection QVT) |
| employee_survey_data.csv | WorkLifeBalance | 38 | 0,9% | Moyen (biais sélection QVT) |
| in_time.csv / out_time.csv | Badgeage | ~9,5% | 9,5% | Élevé (absences, congés) |

### Variables constantes à supprimer

| Variable | Valeur unique | Justification suppression |
|---|---|---|
| EmployeeCount | 1 | Redondant, aucune variance |
| Over18 | "Y" | Légalement obligatoire, aucune information |
| StandardHours | 8 | Politique entreprise uniforme |

---

## A3. Disparités par sous-groupes

### Taux d'attrition par variables sensibles

| Variable | Modalité | Effectif | Taux attrition | Écart vs moyenne |
|---|---|---|---|---|
| **MaritalStatus** | Single | 1196 | 25,5% | +9,4 points |
| | Married | 2541 | 12,5% | -3,6 points |
| | Divorced | 673 | 10,1% | -6,0 points |
| **Department** | HR | 189 | 30,2% | +14,1 points |
| | Sales | 1204 | 15,0% | -1,1 points |
| | R&D | 3017 | 15,7% | -0,4 points |
| **EducationField** | Human Resources | 81 | 40,7% | +24,6 points |
| | Technical Degree | 1102 | 11,4% | -4,7 points |
| | Marketing | 395 | 17,5% | +1,4 points |
| **Gender** | Male | 2135 | 16,7% | +0,6 points |
| | Female | 2275 | 15,3% | -0,8 points |

### Points d'attention équité

- **MaritalStatus** : Célibataires 2,5× plus à risque que divorcés
- **Department HR** : Taux critique (30,2%) sur petit effectif (189)  
- **EducationField HR** : Taux extrême (40,7%) sur très petit effectif (81)
- **Gender** : Écart modéré mais à surveiller systématiquement

---

## A4. Risques de ré-identification

### Sous-groupes à risque élevé

| Croisement variables | Effectif mini | Risque | Précautions |
|---|---|---|---|
| Department=HR + JobLevel | 15-40 | Très élevé | Agrégation forcée |
| EducationField=HR + Gender | 35-46 | Très élevé | Suppression résultats détaillés |
| JobRole=HR + MaritalStatus | 20-80 | Élevé | Communication anonymisée |
| Department + Age + Gender | < 10 | Critique | Interdiction publication |

### Mesures de protection

1. **Seuil minimal** : Aucun résultat communiqué sur groupes < 50 individus
2. **Agrégation forcée** : Regroupement départements/niveaux si nécessaire
3. **Anonymisation** : Suppression croisements identificatoires
4. **Audit systématique** : Vérification re-identifiabilité avant publication

---

## A5. Dilemmes éthiques

### Tensions identifiées et résolutions

| Dilemme | Tension | Résolution retenue |
|---|---|---|
| **Performance vs équité** | Variables sensibles améliorent prédiction mais discriminent | Audit fairness + tests avec/sans variables sensibles |
| **Transparence vs gaming** | Documentation complète vs risque contournement | Documentation technique complète, communication métier simplifiée |
| **Granularité vs protection** | Alertes individuelles vs surveillance | Communication agrégée uniquement, facteurs collectifs |
| **Exhaustivité vs minimisation** | Toutes données disponibles vs RGPD | Suppression variables constantes, agrégation temporelle badgeuse |

**Test de la règle d'or appliqué** : "Accepterais-je que mon employeur utilise ce modèle sur mes données dans ces conditions ?" → **OUI** avec les garde-fous B+D retenus.