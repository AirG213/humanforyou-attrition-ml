# Livrable éthique - Projet IA HumanForYou 

## Gestion du Turnover des employés avec une IA responsable

| Membres | Role |
| :--- | :--- |
| **Gouadfel Rayan** | *Project Manager* |
| **Trappier Quentin** | *Data Analyst* |
| **Arrighi Fabien** | *Data Engineer* |
| **Marcelli Enzo** | *Machine Learning Engineer* |

---

## Table des matières

1. [Contexte et finalité du projet](#1-contexte-et-finalité-du-projet)
2. [Données utilisées et sensibilité](#2-données-utilisées-et-sensibilité)
3. [Méthodologie d'analyse éthique](#3-méthodologie-danalyse-éthique)
   * [3.1. Démarche de décision éthique (atelier CESI)](#31-démarche-de-décision-éthique-atelier-cesi---gono-go)
4. [Exigence 1 - Respect de l'autonomie humaine](#4-exigence-1---respect-de-lautonomie-humaine)
5. [Exigence 2 - Robustesse technique et sécurité](#5-exigence-2---robustesse-technique-et-sécurité)
6. [Exigence 3 - Confidentialité et gouvernance des données](#6-exigence-3---confidentialité-et-gouvernance-des-données)
7. [Exigence 4 - Transparence](#7-exigence-4---transparence)
8. [Exigence 5 - Diversité, non-discrimination et équité](#8-exigence-5---diversité-non-discrimination-et-équité)
9. [Exigence 6 - Bien-être environnemental et sociétal](#9-exigence-6---bien-être-environnemental-et-sociétal)
10. [Exigence 7 - Responsabilité](#10-exigence-7---responsabilité)
11. [Décisions éthiques transverses](#11-décisions-éthiques-transverses)
12. [Points de vigilance identifiés](#12-points-de-vigilance-identifiés)
13. [Synthèse et engagements](#13-synthèse-et-engagements)
14. [Checklist de contrôles éthiques](#14-checklist-de-contrôles-éthiques)
15. [Glossaire](#15-glossaire)
16. [Références et sources](#16-références-et-sources)

---

## 1. Contexte et finalité du projet

HumanForYou est une entreprise pharmaceutique (4 410 employés dans le dataset) confrontée à un taux d'attrition de 16,12 % (711 départs sur 4 410). Le projet vise à identifier les facteurs d'attrition, proposer un modèle prédictif et formuler des recommandations d'amélioration.

**Positionnement éthique** : le modèle est un **outil d'aide à la décision**, non un automate de décisions RH individuelles.

---

## 2. Données utilisées et sensibilité

Sources anonymisées (4 410 EmployeeID) :

- **general_data.csv** (4 410 × 24) : profil, poste, salaire, ancienneté, déplacements, formation, et variable cible Attrition.
- **manager_survey_data.csv** (4 410 × 3) : implication et performance évaluées par managers. Aucune valeur manquante.
- **employee_survey_data.csv** (4 410 × 4) : enquête QVT (satisfaction environnement, travail, équilibre). 83 non-réponses au total.
- **in_time.csv / out_time.csv** (4 410 × 262) : horaires de badgeuse 2015 (261 jours ouvrés), 9,5 % de cellules NA.

**Variables constantes détectées** : `EmployeeCount`, `Over18`, `StandardHours` (inutiles pour modélisation).  
**Valeurs manquantes** : 19 NA dans `NumCompaniesWorked`, 9 NA dans `TotalWorkingYears`.  
**Risque de ré-identification** : petits sous-groupes (189 employés HR, 81 en EducationField HR).

---

## 3. Méthodologie d'analyse éthique

Cadre : **7 exigences d'une IA digne de confiance (Commission Européenne)** appliquées aux choix techniques et organisationnels du projet.

### 3.1 Démarche de décision éthique (atelier CESI - go/no-go)

1. **Situation** : Dataset RH sensible, disparités d'attrition observées (célibataires 25,5 %, HR 30,2 %), usage potentiel réel.
2. **Objectif** : Améliorer rétention sans surveillance ni discrimination individuelle.
3. **Options** : Modèle complet (A), explicable (B), descriptif seul (C), agrégé (D).
4. **Parties prenantes** : Employés, RH, managers, direction, équipe data, société.
5. **Impacts** : Performance vs équité, transparence vs protection, business vs individus.
6. **Filtre éthique** : Respect personnes, non-malveillance, transparence, légalité, valeurs collectives.
7. **Go/No-go** : Validation collective + personnelle (test de la règle d'or).

**Décision retenue** : combinaison B + D (modèle explicable + communication agrégée).

---

## 4. Exigence 1 - Respect de l'autonomie humaine

**Risque** : Automatisation des décisions RH basée sur scores algorithmiques.  
**Décision** : Le modèle ne déclenche aucune action automatique, toute décision reste humaine et contextualisée.  
**Contrôles** :
- Procédure écrite : "score = indicateur, pas verdict"
- Revue humaine obligatoire avant action
- Traçabilité des décisions RH

---

## 5. Exigence 2 - Robustesse technique et sécurité

**Risque** : Overfitting, données manquantes (83 non-réponses QVT, 28 NA variables RH), déséquilibre classes (83,9 % / 16,1 %).  
**Décision** : Validation croisée, comparaison multi-modèles, métriques adaptées au déséquilibre (F1, AUC).  
**Contrôles** :
- Tests de sensibilité par sous-groupes
- Monitoring performance dans le temps
- Stratégie de retraining planifiée

---

## 6. Exigence 3 - Confidentialité et gouvernance des données

**Risque** : Ré-identification (petits sous-groupes), accès non autorisé, conservation excessive.  
**Décision** : Traitement local, minimisation données, séparation raw/processed.  
**Contrôles** :
- Accès restreint aux membres projet
- Suppression données brutes des rapports
- Documentation transformations et provenance

---

## 7. Exigence 4 - Transparence

**Risque** : Décisions incomprises, scores mal interprétés, boîte noire.  
**Décision** : Modèles explicables privilégiés (régression logistique, arbres), documentation complète des étapes.  
**Contrôles** :
- Fiches variables et limites pour non-techniciens
- Explication facteurs influents
- Avertissement corrélation ≠ causalité

---

## 8. Exigence 5 - Diversité, non-discrimination et équité

**Risque** : Discrimination via variables sensibles (Gender, MaritalStatus, Department, EducationField), reproduction biais historiques.

**Disparités observées** :
- MaritalStatus : Single 25,5 % vs Divorced 10,1 %
- Department : HR 30,2 % vs Sales 15,0 %
- EducationField : HR 40,7 % vs Technical 11,4 %

**Décision** : Audit fairness systématique, test avec/sans variables sensibles.  
**Contrôles** :
- Comparaison taux FP/FN par sous-groupes
- Possibilité retrait variables discriminantes
- Règle métier : pas d'action basée sur attribut protégé

---

## 9. Exigence 6 - Bien-être environnemental et sociétal

**Risque** : Climat de surveillance, stress employés, dérives managériales.  
**Décision** : Cadrage "amélioration conditions travail", pas de scoring individuel communiqué.  
**Contrôles** :
- Charte d'usage, formation utilisateurs
- Recommandations collectives/organisationnelles uniquement
- Indicateurs QVT post-déploiement

---

## 10. Exigence 7 - Responsabilité

**Risque** : Dilution responsabilités ("c'est l'algorithme"), absence redevabilité.  
**Décision** : Responsabilité RH sur décisions, équipe data sur qualité modèle.  
**Contrôles** :
- Registre versions (modèle, date, métriques)
- Procédure contestation/revue
- Mécanisme remontée incidents

---

## 11. Décisions éthiques transverses

- Modèle = aide décision, jamais automatisation
- Transparence : variables et limites documentées
- Minimisation : variables constantes supprimées
- Fairness : audit par sous-groupes systématique
- Sécurité : accès restreint, séparation raw/processed
- Traçabilité : documentation choix et transformations

---

## 12. Points de vigilance identifiés

L'analyse du dataset révèle :

- **Non-réponses QVT** : 83 employés (risque biais sélection)
- **Variables constantes** : 3 variables inutiles à supprimer
- **NA données RH** : 28 valeurs manquantes à traiter
- **Déséquilibre classes** : stratégie métrique adaptée nécessaire
- **Petits sous-groupes** : risque ré-identification HR (189 employés)

*Détails chiffrés : voir annexes_ethics.md*

---

## 13. Synthèse et engagements

**Appropriation** : Le projet applique les 7 exigences IA européennes et la méthode décisionnelle CESI (7 étapes structurées) pour garantir choix éthiques documentés et assumables.

**Engagements** :
- Aide à la décision stratégique RH uniquement
- Transparence : modèles explicables et documentation
- Minimisation : suppression variables inutiles/constantes
- Fairness : audit discrimination par sous-groupes
- Sécurité : protection données et accès restreint
- Traçabilité : documentation complète des choix

**Pérennité** : Monitoring continu des biais et dérive si mise en production, formation utilisateurs, mise à jour modèle planifiée.

---

## 14. Checklist de contrôles éthiques

**Avant communication des résultats** :

- [ ] Vérifier fairness par sous-groupes (Gender, MaritalStatus, Department, EducationField)
- [ ] Comparer taux FP/FN entre groupes sensibles  
- [ ] Supprimer variables constantes (EmployeeCount, Over18, StandardHours)
- [ ] Documenter stratégie traitement NA (28 valeurs)
- [ ] Éviter résultats nominatifs/scoring individuel
- [ ] Protéger petits sous-groupes (< 200 employés)
- [ ] Valider métriques adaptées au déséquilibre classes
- [ ] Documenter limites et biais du modèle
- [ ] Préparer communication non-techniciens
- [ ] Tracer décisions et justifications éthiques

---

## 15. Glossaire

**AUC (Area Under the Curve)** : Métrique d'évaluation de la performance d'un modèle de classification, mesure la capacité à distinguer les classes (ici : employés partants vs restants).

**Attrition** : Taux de départ volontaire des employés d'une entreprise (démissions, fins de contrat non renouvelées).

**Cross-validation (Validation croisée)** : Technique de validation de modèle qui divise les données en plusieurs plis pour tester la robustesse et éviter l'overfitting.

**Dataset** : Jeu de données structuré utilisé pour l'entraînement et l'évaluation du modèle IA.

**EmployeeID** : Identifiant unique anonymisé de chaque employé dans le dataset (de 1 à 4410).

**F1-score** : Moyenne harmonique entre précision et rappel, particulièrement utile pour les classes déséquilibrées comme l'attrition.

**Fairness (Équité)** : Principe garantissant que le modèle ne discrimine pas certains groupes d'employés basés sur des caractéristiques sensibles.

**FN (Faux Négatifs)** : Employés prédits comme "restants" mais qui partent réellement. Risque : ne pas identifier des signaux d'attrition.

**FP (Faux Positifs)** : Employés prédits comme "partants" mais qui restent finalement. Risque : alarmes infondées et stress managérial.

**NA (Not Available)** : Valeurs manquantes dans le dataset (ex: 83 non-réponses dans l'enquête QVT, 28 NA dans les variables RH).

**Overfitting** : Phénomène où un modèle apprend "par cœur" les données d'entraînement au détriment de sa capacité de généralisation.

**QVT (Qualité de Vie au Travail)** : Ensemble d'indicateurs mesurant la satisfaction, l'équilibre vie professionnelle/personnelle et l'environnement de travail.

**Variables constantes** : Variables qui ont la même valeur pour tous les employés (ex: EmployeeCount=1, Over18="Y"), inutiles pour la modélisation.

**Variables sensibles** : Attributs protégés par la loi anti-discrimination (Genre, État civil, Âge, Département) nécessitant une vigilance particulière.

---

## 16. Références et sources

**Commission Européenne** : *Lignes directrices en matière d'éthique pour une IA digne de confiance* (Groupe d'experts de haut niveau sur l'IA - HLEG). Définit les 7 exigences d'une IA responsable appliquées dans ce projet.

**CESI École d'Ingénieurs** : *Méthodologie de prise de décision éthique en 7 étapes*. Cadre décisionnel structuré pour les choix techniques et organisationnels du projet.

**Dataset HumanForYou** : Données anonymisées de 4410 employés (2015) incluant profils RH, enquêtes satisfaction, évaluations managers et données de badgeuse.

*Détails techniques et tableaux complémentaires : voir [annexes_ethics.md](annexes_ethics.md)*
