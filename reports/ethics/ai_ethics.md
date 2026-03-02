# Livrable éthique - Projet IA HumanForYou (Attrition)

| Équipe projet | Rôle |
| :--- | :--- |
| **Gouadfel Rayan** | *Project Manager* |
| **Trappier Quentin** | *Data Analyst* |
| **Arrighi Fabien** | *Data Engineer* |
| **Marcelli Enzo** | *Machine Learning Engineer* |

---

## Résumé exécutif

**Contexte** : HumanForYou (4410 employés, taux d'attrition 16,12%) souhaite développer un modèle prédictif d'aide à la décision RH. **Position éthique** : Le modèle constitue un outil d'aide à la décision, jamais un automate de décisions individuelles. **Décision retenue** : Combinaison solution B (modèle explicable) + D (communication agrégée uniquement) après application de la méthodologie CESI 7-étapes. **Garde-fous principaux** : Audit fairness systématique, transparence documentée, accès restreint, aucun scoring individuel communiqué, revue humaine obligatoire. **Conformité** : Application des 7 exigences d'IA digne de confiance (Commission Européenne) avec registre de décisions traçables.

---

## Table des matières

1. [Contexte et finalité](#1-contexte-et-finalité)
2. [Données et sensibilité](#2-données-et-sensibilité) 
3. [Méthodologie CESI appliquée](#3-méthodologie-cesi-appliquée)
4. [Exigences UE d'IA digne de confiance](#4-exigences-ue-dia-digne-de-confiance)
5. [Registre de décisions](#5-registre-de-décisions)
6. [Conclusion](#6-conclusion)

---

## 1. Contexte et finalité

HumanForYou est une entreprise pharmaceutique confrontée à un taux d'attrition de **16,12%** (711 départs sur 4410 employés). Le projet vise à identifier les facteurs d'attrition et formuler des recommandations d'amélioration par un modèle prédictif.

**Finalité éthique** : Améliorer les conditions de travail et la rétention **sans surveillance ni discrimination individuelle**.

---

## 2. Données et sensibilité

**Sources** : 4 fichiers anonymisés (EmployeeID 1-4410) couvrant profils RH, évaluations managers, enquêtes QVT et données de badgeuse 2015.

**Synthèse des points critiques** :
- Valeurs manquantes : 83 non-réponses QVT, 28 NA variables RH
- Variables constantes : 3 variables inutiles identifiées 
- Déséquilibre classes : 83,9% vs 16,1% sur variable cible
- Risque ré-identification : petits sous-groupes (HR : 189 employés)

*Détails complets : voir [annexes_ethics.md](annexes_ethics.md)*

---

## 3. Méthodologie CESI appliquée

### 3.1 Situation initiale
Dataset RH sensible, disparités observées (célibataires 25,5%, HR 30,2%), usage potentiel réel avec impact sur les employés.

### 3.2 Solutions envisagées

| Solution | Description | Performance | Éthique |
|---|---|---|---|
| **A - Complet** | Toutes variables, y compris sensibles | Maximale | Risque discrimination |
| **B - Explicable** | Variables non-sensibles, modèle interprétable | Correcte | Transparence élevée |
| **C - Descriptif** | Analyse statistique seule, pas de scoring | Nulle | Risque minimal |
| **D - Agrégé** | Modèle entraîné, résultats collectifs uniquement | Moyenne | Équilibre |

### 3.3 Parties prenantes

| Partie prenante | Intérêt principal | Risque exposition |
|---|---|---|
| **Employés** | Protection données, non-discrimination | Élevé |
| **RH** | Recommandations actionnables | Moyen |
| **Managers** | Support décisionnel | Moyen |
| **Direction** | Performance business | Faible |
| **Équipe data** | Qualité technique et éthique | Moyen |

### 3.4 Impacts par solution

| Solution | Avantages | Inconvénients | Risques |
|---|---|---|---|
| **B** | Explicabilité, confiance | Performance moindre | Sous-détection |
| **D** | Protection individuelle | Perte granularité | Non-détection situations critiques |
| **B+D** | Équilibre transparence/protection | Complexité mise en œuvre | Gestion double contrainte |

### 3.5 Filtre éthique

| Critère éthique | Évaluation solution B+D | Décision |
|---|---|---|
| **Respect des personnes** | ✅ Aucun scoring individuel communiqué | Conforme |
| **Non-malveillance** | ✅ Usage amélioration RH, pas surveillance | Conforme |  
| **Transparence** | ✅ Modèles explicables + documentation | Conforme |
| **Légalité** | ✅ Respect RGPD + non-discrimination | Conforme |
| **Valeurs collectives** | ✅ Amélioration conditions travail | Conforme |

**Décision GO** validée collectivement et individuellement (test règle d'or).

---

## 4. Exigences UE d'IA digne de confiance

### 4.1 Respect de l'autonomie humaine
- **Risques** : Automatisation décisions, scoring punitif, déresponsabilisation
- **Décisions** : Aucune action automatique, revue humaine obligatoire, traçabilité
- **Contrôles** : Procédure "score = indicateur", validation managériale, audit usage

### 4.2 Robustesse technique et sécurité  
- **Risques** : Overfitting, déséquilibre classes, données manquantes
- **Décisions** : Validation croisée, métriques adaptées (F1/AUC), comparaison multi-modèles
- **Contrôles** : Tests sensibilité, monitoring performance, stratégie retraining

### 4.3 Confidentialité et gouvernance données
- **Risques** : Ré-identification, accès non-autorisé, conservation excessive  
- **Décisions** : Traitement local, minimisation données, séparation raw/processed
- **Contrôles** : Accès restreint équipe, suppression données brutes rapports, documentation provenance

### 4.4 Transparence
- **Risques** : Boîte noire, scores mal interprétés, décisions incomprises
- **Décisions** : Modèles explicables privilégiés, documentation complète étapes
- **Contrôles** : Fiches variables non-techniciens, explication facteurs, avertissement corrélation≠causalité

### 4.5 Diversité, non-discrimination et équité
- **Risques** : Discrimination variables sensibles, reproduction biais historiques, disparités (Single 25,5% vs Divorced 10,1%)
- **Décisions** : Audit fairness systématique, tests avec/sans variables sensibles, règle métier anti-discrimination  
- **Contrôles** : Comparaison taux FP/FN sous-groupes, retrait variables discriminantes, protection petits groupes

### 4.6 Bien-être environnemental et sociétal
- **Risques** : Climat surveillance, stress employés, dérives managériales
- **Décisions** : Cadrage "amélioration conditions", pas scoring individuel communiqué, usage collectif
- **Contrôles** : Charte usage, formation utilisateurs, indicateurs QVT post-déploiement

### 4.7 Responsabilité
- **Risques** : Dilution responsabilités, absence redevabilité, "c'est l'algorithme"  
- **Décisions** : Responsabilité RH sur décisions, équipe data sur qualité modèle, traçabilité complète
- **Contrôles** : Registre versions, procédure contestation, mécanisme remontée incidents

---

## 5. Registre de décisions

| Décision | Niveau | Exigence UE | Risque mitigé | Contrôle associé |
|---|---|---|---|---|
| Modèle explicable (régression/arbres) | Modèle-métriques | Transparence | Boîte noire | Documentation variables |
| Communication agrégée uniquement | Résultats métier | Autonomie humaine | Scoring punitif | Charte usage |
| Suppression variables constantes | Données | Confidentialité | Sur-collecte | Minimisation |
| Audit fairness par sous-groupes | Modèle-métriques | Non-discrimination | Biais historiques | Tests FP/FN |
| Accès restreint équipe projet | Données | Confidentialité | Accès non-autorisé | Contrôle identité |
| Validation croisée obligatoire | Modèle-métriques | Robustesse | Overfitting | Tests sensibilité |
| Traçabilité décisions RH | Déploiement/usage | Responsabilité | Dilution responsabilité | Registre versions |
| Formation utilisateurs RH | Déploiement/usage | Bien-être sociétal | Dérive managériale | Charte + formation |

---

## 6. Conclusion

### Conditions d'usage
Le modèle est autorisé **exclusivement** comme outil d'aide à la décision stratégique RH. Toute utilisation pour scoring individuel, décisions automatisées ou surveillance est **prohibée**.

### Limites identifiées  
- Performance potentiellement réduite par contraintes éthiques
- Risque sous-détection situations critiques individuelles
- Nécessité expertise RH pour interpréter recommandations

### Responsabilité
- **Équipe data** : qualité technique, documentation, audit biais
- **Service RH** : décisions finales, formation utilisateurs, respect charte usage
- **Direction** : validation politique éthique, ressources monitoring

**Validation finale** : Ce projet respecte les 7 exigences UE et applique rigoureusement la méthodologie CESI pour garantir une IA digne de confiance.
