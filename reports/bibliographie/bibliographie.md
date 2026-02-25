# Bibliographie — Projet IA HumanForYou

> **Projet** : Analyse et prédiction de l'attrition des employés de HumanForYou (4 410 employés, taux d'attrition 16,12 %)
> **Pipeline** : EDA → Preprocessing → Feature Engineering → KMeans Clustering → Régression logistique → Comparaison de modèles → Éthique IA
> **Format** : APA 7e édition
> **Date** : Février 2026

---

## A. Machine Learning — Fondements théoriques

### A1.

**Référence APA :**
Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning: Data Mining, Inference, and Prediction* (2e éd.). Springer. https://doi.org/10.1007/978-0-387-84858-7

**Type :** Livre de référence académique (ouvrage de recherche)

**Critère de fiabilité :** Ouvrage publié chez Springer, l'un des plus grands éditeurs scientifiques mondiaux. Plus de 40 000 citations (Google Scholar). Les trois auteurs sont professeurs à Stanford University et figures fondatrices du machine learning statistique moderne.

**Lien avec notre projet :** Couvre l'ensemble des fondements théoriques mobilisés dans notre pipeline : régression logistique (chapitre 4), validation croisée (chapitre 7), surapprentissage et régularisation (chapitre 3), méthodes de classification supervisée, et critères de sélection de modèles utilisés dans nos notebooks 06 et 07.

---

### A2.

**Référence APA :**
Bishop, C. M. (2006). *Pattern Recognition and Machine Learning*. Springer. https://doi.org/10.1007/978-0-387-45528-0

**Type :** Livre de référence académique (ouvrage de recherche)

**Critère de fiabilité :** Publié chez Springer, plus de 65 000 citations (Google Scholar). Christopher Bishop est Fellow de la Royal Society et directeur de Microsoft Research AI4Science. Ouvrage considéré comme l'un des textes fondateurs du machine learning moderne.

**Lien avec notre projet :** Fournit le cadre probabiliste de la régression logistique et de la classification bayésienne. Les chapitres sur les modèles linéaires de classification (chapitre 4) et les méthodes à noyau (chapitre 6) éclairent directement nos choix de modèles dans le notebook de comparaison (07). Le traitement des mélanges gaussiens (chapitre 9) fonde notre approche de clustering.

---

### A3.

**Référence APA :**
James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). *An Introduction to Statistical Learning: with Applications in R*. Springer. https://doi.org/10.1007/978-1-4614-7138-7

**Type :** Livre de référence académique (manuel universitaire)

**Critère de fiabilité :** Publié chez Springer, plus de 25 000 citations. Version accessible et pédagogique de l'ouvrage A1, utilisée comme manuel de référence dans des centaines de programmes universitaires de data science à travers le monde. Accès libre (open access).

**Lien avec notre projet :** Référence pédagogique directe pour la validation croisée k-fold (chapitre 5), la régression logistique (chapitre 4), le compromis biais-variance et le surapprentissage (chapitre 2), et les méthodes non-supervisées incluant K-Means et PCA (chapitre 12). Correspond parfaitement au niveau d'application de notre pipeline.

---

### A4.

**Référence APA :**
Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O., Blondel, M., Prettenhofer, P., Weiss, R., Dubourg, V., Vanderplas, J., Passos, A., Cournapeau, D., Brucher, M., Perrot, M., & Duchesnay, É. (2011). Scikit-learn: Machine learning in Python. *Journal of Machine Learning Research*, *12*(85), 2825–2830.

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans le *Journal of Machine Learning Research* (JMLR), revue majeure du domaine (impact factor élevé, comité éditorial international). Plus de 60 000 citations, l'un des articles les plus cités en informatique. Scikit-learn est la bibliothèque de référence de l'écosystème Python ML.

**Lien avec notre projet :** Scikit-learn est l'outil central de notre pipeline technique. Nous utilisons directement ses implémentations de `LogisticRegression`, `KMeans`, `StandardScaler`, `cross_val_score`, `silhouette_score`, `confusion_matrix`, `roc_auc_score`, `f1_score` et `PCA` dans l'ensemble de nos notebooks (01 à 07). Citer cet article est indispensable pour la traçabilité méthodologique.

---

## B. Évaluation des modèles

### B1.

**Référence APA :**
Fawcett, T. (2006). An introduction to ROC analysis. *Pattern Recognition Letters*, *27*(8), 861–874. https://doi.org/10.1016/j.patrec.2005.10.010

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans *Pattern Recognition Letters* (Elsevier), revue indexée Scopus/WoS avec comité de lecture. Plus de 20 000 citations. Article de référence unanimement reconnu pour l'introduction à l'analyse ROC en machine learning.

**Lien avec notre projet :** Fonde directement notre utilisation de la courbe ROC et de l'AUC comme métriques de comparaison des modèles dans le notebook 07. Essentiel dans un contexte de classes déséquilibrées (83,9 % vs 16,1 %) où l'accuracy seule est trompeuse, exactement le cas de notre dataset HumanForYou.

---

### B2.

**Référence APA :**
Sokolova, M., & Lapalme, G. (2009). A systematic analysis of performance measures for classification tasks. *Information Processing & Management*, *45*(4), 427–437. https://doi.org/10.1016/j.ipm.2009.03.002

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans *Information Processing & Management* (Elsevier), revue indexée Scopus/WoS avec comité de lecture international. Plus de 4 500 citations. Analyse systématique et rigoureuse des métriques de classification.

**Lien avec notre projet :** Justifie notre choix de métriques multiples (Precision, Recall, F1-score) plutôt qu'une seule métrique. L'article démontre les limites de chaque mesure prise isolément, ce qui valide notre approche de comparaison multi-critères dans le notebook 07 et le choix du F1-score comme compromis pour notre problème à classes déséquilibrées.

---

### B3.

**Référence APA :**
Hosmer, D. W., Jr., Lemeshow, S., & Sturdivant, R. X. (2013). *Applied Logistic Regression* (3e éd.). Wiley. https://doi.org/10.1002/9781118548387

**Type :** Livre de référence académique (ouvrage spécialisé)

**Critère de fiabilité :** Publié chez Wiley (éditeur académique de premier plan), plus de 45 000 citations toutes éditions confondues. Texte de référence mondiale sur la régression logistique, utilisé dans les cursus de biostatistique, d'épidémiologie et de data science.

**Lien avec notre projet :** Référence directe pour notre modèle principal de classification (régression logistique, notebook 06). Couvre la sélection de variables, l'interprétation des coefficients (odds ratios), les diagnostics de modèle et les stratégies de validation — autant d'éléments mobilisés pour interpréter les facteurs d'attrition chez HumanForYou.

---

## C. Clustering

### C1.

**Référence APA :**
Lloyd, S. P. (1982). Least squares quantization in PCM. *IEEE Transactions on Information Theory*, *28*(2), 129–137. https://doi.org/10.1109/TIT.1982.1056489

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans *IEEE Transactions on Information Theory*, revue de premier rang de l'IEEE (Institute of Electrical and Electronics Engineers). Plus de 18 000 citations. Article fondateur de l'algorithme K-Means, initialement rédigé en 1957 chez Bell Labs et publié en 1982.

**Lien avec notre projet :** Fonde théoriquement l'algorithme K-Means que nous utilisons dans le notebook 04 pour segmenter les employés de HumanForYou en clusters homogènes. La compréhension de la minimisation par moindres carrés intra-cluster permet d'interpréter correctement les groupes identifiés et les facteurs discriminants de l'attrition.

---

### C2.

**Référence APA :**
Rousseeuw, P. J. (1987). Silhouettes: A graphical aid to the interpretation and validation of cluster analysis. *Journal of Computational and Applied Mathematics*, *20*, 53–65. https://doi.org/10.1016/0377-0427(87)90125-7

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans *Journal of Computational and Applied Mathematics* (Elsevier), revue indexée Scopus/WoS. Plus de 14 000 citations. Article fondateur du silhouette score, devenu la métrique standard de validation de clustering.

**Lien avec notre projet :** Le silhouette score est notre critère principal de sélection automatique du nombre de clusters k (argmax sur k=2 à 10) dans le notebook 04. Cette référence justifie notre méthode de sélection du k optimal et l'interprétation de la qualité de séparation des groupes d'employés.

---

### C3.

**Référence APA :**
Davies, D. L., & Bouldin, D. W. (1979). A cluster separation measure. *IEEE Transactions on Pattern Analysis and Machine Intelligence*, *PAMI-1*(2), 224–227. https://doi.org/10.1109/TPAMI.1979.4766909

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans *IEEE Transactions on Pattern Analysis and Machine Intelligence* (IEEE TPAMI), l'une des revues les plus prestigieuses en intelligence artificielle et reconnaissance de formes (impact factor > 20). Plus de 7 000 citations.

**Lien avec notre projet :** L'indice de Davies-Bouldin complète le silhouette score comme métrique de validation interne du clustering. Il mesure le ratio de dispersion intra-cluster sur la séparation inter-cluster. Utilisé dans notre notebook 04 pour évaluer la qualité de la segmentation des employés en complément du silhouette score.

---

### C4.

**Référence APA :**
Jolliffe, I. T. (2002). *Principal Component Analysis* (2e éd.). Springer. https://doi.org/10.1007/b98835

**Type :** Livre de référence académique (ouvrage spécialisé)

**Critère de fiabilité :** Publié chez Springer, plus de 28 000 citations. Texte de référence mondiale sur l'Analyse en Composantes Principales. Ian Jolliffe est professeur émérite à l'University of Aberdeen, autorité reconnue sur les méthodes de réduction de dimension.

**Lien avec notre projet :** La PCA est utilisée dans notre notebook 04 pour la visualisation 2D des clusters K-Means (scatter PCA coloré par cluster avec taux d'attrition). Cette référence fonde notre usage de la réduction de dimension pour interpréter visuellement la segmentation des employés et valider la séparation des groupes.

---

## D. Éthique de l'IA

### D1.

**Référence APA :**
High-Level Expert Group on Artificial Intelligence. (2019). *Ethics guidelines for trustworthy AI*. European Commission. https://digital-strategy.ec.europa.eu/en/library/ethics-guidelines-trustworthy-ai

**Type :** Document institutionnel officiel (Commission Européenne)

**Critère de fiabilité :** Produit par le groupe d'experts de haut niveau mandaté par la Commission Européenne, composé de 52 experts (académiques, industriels, société civile). Document fondateur de la politique européenne en matière d'IA éthique, cité dans l'AI Act (2024). Source institutionnelle de premier rang.

**Lien avec notre projet :** Cadre structurant direct de notre livrable éthique. Les 7 exigences d'IA digne de confiance (autonomie humaine, robustesse technique, confidentialité, transparence, non-discrimination, bien-être sociétal, responsabilité) sont systématiquement appliquées dans notre analyse éthique du modèle d'attrition et dans notre registre de décisions (cf. `ai_ethics.md`, section 4).

---

### D2.

**Référence APA :**
Parlement européen & Conseil de l'Union européenne. (2016). Règlement (UE) 2016/679 du Parlement européen et du Conseil du 27 avril 2016 relatif à la protection des personnes physiques à l'égard du traitement des données à caractère personnel et à la libre circulation de ces données (Règlement Général sur la Protection des Données). *Journal officiel de l'Union européenne*, L 119, 1–88. https://eur-lex.europa.eu/eli/reg/2016/679/oj

**Type :** Texte réglementaire officiel (législation européenne)

**Critère de fiabilité :** Règlement européen d'application directe dans les 27 États membres. Source juridique primaire publiée au Journal officiel de l'Union européenne. Cadre légal incontournable pour tout traitement de données personnelles en Europe.

**Lien avec notre projet :** Notre dataset contient des données RH personnelles (âge, genre, état civil, salaire, évaluations). Le RGPD impose les principes de minimisation des données, de limitation des finalités et de protection des droits des personnes concernées. Ces principes sont directement appliqués dans notre livrable éthique : traitement local, suppression des variables constantes, seuil minimal pour la communication de résultats sur petits groupes, interdiction du scoring individuel.

---

### D3.

**Référence APA :**
Barocas, S., & Selbst, A. D. (2016). Big data's disparate impact. *California Law Review*, *104*(3), 671–732. https://doi.org/10.15779/Z38BG31

**Type :** Article peer-reviewed (revue juridique académique)

**Critère de fiabilité :** Publié dans la *California Law Review*, l'une des revues juridiques les plus prestigieuses aux États-Unis (fondée en 1912, UC Berkeley). Plus de 3 500 citations. Article fondateur du champ « algorithmic fairness », à l'intersection du droit et de l'informatique.

**Lien avec notre projet :** Démontre comment les algorithmes de machine learning peuvent reproduire et amplifier les biais historiques présents dans les données d'entraînement. Directement pertinent pour notre contexte : les disparités observées dans nos données (célibataires 25,5 % d'attrition vs divorcés 10,1 %, département HR 30,2 %) pourraient être intégrées par le modèle comme des « règles » discriminatoires. Justifie notre audit fairness par sous-groupes et notre stratégie de retrait des variables sensibles.

---

### D4.

**Référence APA :**
Mehrabi, N., Morstatter, F., Saxena, N., Lerman, K., & Galstyan, A. (2021). A survey on bias and fairness in machine learning. *ACM Computing Surveys*, *54*(6), Article 115, 1–35. https://doi.org/10.1145/3457607

**Type :** Article peer-reviewed (revue scientifique — survey)

**Critère de fiabilité :** Publié dans *ACM Computing Surveys*, revue de référence pour les états de l'art en informatique (impact factor > 16, l'un des plus élevés du domaine). Association for Computing Machinery (ACM), société savante de premier plan. Plus de 5 000 citations depuis sa publication.

**Lien avec notre projet :** Fournit une taxonomie complète des types de biais en ML (biais de sélection, biais de mesure, biais historique, biais d'agrégation) et des métriques de fairness (demographic parity, equalized odds, predictive parity). Éclaire directement notre démarche d'audit fairness : comparaison des taux de faux positifs/faux négatifs par sous-groupes (genre, état civil, département) documentée dans notre livrable éthique.

---

### D5.

**Référence APA :**
Jobin, A., Ienca, M., & Vayena, E. (2019). The global landscape of AI ethics guidelines. *Nature Machine Intelligence*, *1*(9), 389–399. https://doi.org/10.1038/s42256-019-0088-2

**Type :** Article peer-reviewed (revue scientifique)

**Critère de fiabilité :** Publié dans *Nature Machine Intelligence* (Springer Nature), revue de haut niveau du groupe Nature (impact factor > 18). Les auteurs sont affiliés à l'ETH Zürich (Health Ethics and Policy Lab). Plus de 3 800 citations. Analyse systématique de 84 documents d'éthique de l'IA à l'échelle mondiale.

**Lien avec notre projet :** Identifie les 11 principes éthiques convergents à l'échelle mondiale (transparence, justice/équité, non-malveillance, responsabilité, vie privée). Valide le cadre de référence européen que nous avons adopté (guidelines UE) en montrant qu'il est cohérent avec le consensus international. Renforce la légitimité de notre démarche éthique et de notre registre de décisions.

---

## E. Outils techniques

Cette section crédite les bibliothèques open source qui constituent l'infrastructure technique de notre pipeline d'analyse et de prédiction.

### E1.

**Référence APA :**
McKinney, W. (2010). Data structures for statistical computing in Python. In S. van der Walt & J. Millman (Eds.), *Proceedings of the 9th Python in Science Conference* (pp. 51–56). https://doi.org/10.25080/Majora-92bf1922-00a

**Type :** Article peer-reviewed (actes de conférence scientifique)

**Licence :** Bibliothèque Pandas sous licence Open Source BSD 3-Clause. Autorise l'utilisation, la modification et la distribution dans des projets académiques et commerciaux.

**Lien avec notre projet :** Pandas est l'outil central de notre traitement de données. Utilisé dans tous les notebooks (01 à 07) pour la lecture des fichiers CSV, la fusion des jeux de données via la clé `EmployeeID`, le nettoyage (suppression de variables constantes, imputation des valeurs manquantes), l'encodage des variables catégorielles et l'export des résultats intermédiaires dans `data/processed/`.

---

### E2.

**Référence APA :**
Harris, C. R., Millman, K. J., van der Walt, S. J., Gommers, R., Virtanen, P., Cournapeau, D., Wieser, E., Taylor, J., Berg, S., Smith, N. J., Kern, R., Picus, M., Hoyer, S., van Krevelen, M. H., Brett, M., Haldane, A., del Río, J. F., Wiebe, M., Peterson, P., … Oliphant, T. E. (2020). Array programming with NumPy. *Nature*, *585*(7825), 357–362. https://doi.org/10.1038/s41586-020-2649-2

**Type :** Article peer-reviewed (revue scientifique)

**Licence :** Bibliothèque NumPy sous licence Open Source BSD 3-Clause. Utilisation libre dans tout cadre académique ou commercial.

**Lien avec notre projet :** NumPy fournit les structures de calcul matriciel sous-jacentes à l'ensemble de notre pipeline. Utilisé directement dans les notebooks pour les opérations numériques (moyennes, calculs horaires dans le feature engineering badgeuse, manipulation de tableaux) et indirectement via Pandas et Scikit-learn qui s'appuient sur NumPy.

---

### E3.

**Référence APA :**
Hunter, J. D. (2007). Matplotlib: A 2D graphics environment. *Computing in Science & Engineering*, *9*(3), 90–95. https://doi.org/10.1109/MCSE.2007.55

**Type :** Article peer-reviewed (revue scientifique)

**Licence :** Bibliothèque Matplotlib sous licence PSF (compatible BSD). Utilisation libre, y compris pour la reproduction de figures dans des rapports académiques.

**Lien avec notre projet :** Matplotlib est utilisé dans les notebooks 01 (EDA) et 04 (KMeans) pour la génération de toutes les figures exportées dans `reports/figures/` : graphiques de sélection de k (elbow + silhouette), scatter PCA 2D, barplots de taux d'attrition par cluster, et top features discriminantes.

---

### E4.

**Référence APA :**
Waskom, M. L. (2021). seaborn: Statistical data visualization. *Journal of Open Source Software*, *6*(60), 3021. https://doi.org/10.21105/joss.03021

**Type :** Article peer-reviewed (revue scientifique — open source)

**Licence :** Bibliothèque Seaborn sous licence Open Source BSD 3-Clause. Utilisation et redistribution libres.

**Lien avec notre projet :** Seaborn complète Matplotlib pour les visualisations statistiques avancées dans les notebooks 01 (EDA : heatmaps de corrélation, distributions, countplots) et 04 (KMeans : visualisations de clusters). Son intégration native avec Pandas simplifie la création de graphiques à partir de nos DataFrames.

---

## F. Critères de fiabilité des sources

Cette section explicite les critères méthodologiques appliqués pour évaluer la qualité et la pertinence de chaque source retenue dans cette bibliographie.

### F1. Peer review (évaluation par les pairs)

L'évaluation par les pairs est le standard de qualité de la recherche scientifique. Chaque article soumis à une revue est examiné de manière anonyme par des experts du domaine avant publication. Ce processus garantit la rigueur méthodologique, la validité des résultats et l'originalité de la contribution. **Toutes nos sources d'articles** (Fawcett, Sokolova & Lapalme, Pedregosa et al., Lloyd, Rousseeuw, Davies & Bouldin, Barocas & Selbst, Mehrabi et al., Jobin et al., McKinney, Harris et al., Hunter, Waskom) sont publiées dans des revues à comité de lecture.

### F2. Impact factor et prestige de la revue

L'impact factor mesure le nombre moyen de citations des articles d'une revue sur une période donnée. Il constitue un indicateur de l'influence et de la visibilité d'une revue dans son domaine. Nos sources sont issues de revues à très haut impact factor :

| Revue | Impact factor approx. | Domaine |
|---|---|---|
| *Nature Machine Intelligence* | > 18 | IA / ML |
| *ACM Computing Surveys* | > 16 | Informatique (surveys) |
| *IEEE TPAMI* | > 20 | Reconnaissance de formes / IA |
| *IEEE Trans. Information Theory* | > 2 | Théorie de l'information |
| *JMLR* | > 6 | Machine learning |
| *Pattern Recognition Letters* | > 3 | Reconnaissance de formes |
| *Information Processing & Mgmt* | > 7 | Sciences de l'information |
| *California Law Review* | — | Droit (top 10 US) |
| *Nature* | > 60 | Sciences générales |
| *Computing in Science & Eng.* | > 2 | Calcul scientifique |
| *JOSS* | — | Logiciels open source (peer-reviewed) |
| *SciPy Proceedings* | — | Python scientifique (peer-reviewed) |

### F3. Éditeur académique reconnu

Les ouvrages de référence cités sont publiés chez des éditeurs académiques de premier plan :

- **Springer** (Hastie et al., Bishop, James et al., Jolliffe) : plus grand éditeur scientifique mondial, processus éditorial rigoureux avec relecture par les pairs.
- **Wiley** (Hosmer et al.) : éditeur académique fondé en 1807, catalogue de référence en statistique et biostatistique.

Ces éditeurs garantissent un processus de sélection et de relecture conforme aux standards académiques internationaux.

### F4. Institution publique et source officielle

Deux de nos sources émanent directement d'institutions européennes :

- **Commission Européenne** (Ethics Guidelines for Trustworthy AI) : institution exécutive de l'Union Européenne, mandatant un groupe de 52 experts de haut niveau.
- **Parlement européen & Conseil de l'UE** (RGPD) : co-législateurs de l'Union Européenne, source juridique primaire.

Ces sources institutionnelles sont incontestables en termes de légitimité et de fiabilité.

### F5. Nombre de citations

Le nombre de citations d'une source est un indicateur de son impact et de sa reconnaissance par la communauté scientifique. Toutes nos sources présentent un nombre de citations élevé à très élevé :

| Source | Citations approx. (Google Scholar) |
|---|---|
| Bishop (2006) | > 65 000 |
| Pedregosa et al. (2011) | > 60 000 |
| Hosmer et al. (toutes éd.) | > 45 000 |
| Harris et al. (2020) — NumPy | > 40 000 |
| Hastie et al. (2009) | > 40 000 |
| Hunter (2007) — Matplotlib | > 35 000 |
| Jolliffe (2002) | > 28 000 |
| James et al. (2013) | > 25 000 |
| Fawcett (2006) | > 20 000 |
| Lloyd (1982) | > 18 000 |
| Rousseeuw (1987) | > 14 000 |
| McKinney (2010) — Pandas | > 12 000 |
| Davies & Bouldin (1979) | > 7 000 |
| Mehrabi et al. (2021) | > 5 000 |
| Sokolova & Lapalme (2009) | > 4 500 |
| Jobin et al. (2019) | > 3 800 |
| Barocas & Selbst (2016) | > 3 500 |
| Waskom (2021) — Seaborn | > 2 500 |

### F6. Synthèse des critères appliqués

| Critère | Description | Application |
|---|---|---|
| **Peer review** | Évaluation par les pairs avant publication | Tous les articles cités (sections A–E) |
| **Impact factor** | Influence de la revue dans son domaine | Revues IF > 2, plusieurs IF > 16 |
| **Éditeur académique** | Maison d'édition reconnue (Springer, Wiley) | Tous les ouvrages cités |
| **Institution officielle** | Organisme public légitime | Commission Européenne, Parlement UE |
| **Nombre de citations** | Reconnaissance par la communauté scientifique | Toutes sources > 2 500 citations |
| **Licence open source** | Bibliothèques sous licence libre (BSD, PSF, MIT) | Toutes les bibliothèques techniques (section E) |
| **Pertinence projet** | Lien direct avec nos méthodes et données | Justifié pour chaque source |

> **Conclusion** : L'ensemble des 20 sources retenues satisfait au minimum trois des six critères de fiabilité ci-dessus. Aucune source provenant de blogs, forums, ou plateformes non académiques n'a été incluse. Cette bibliographie repose exclusivement sur des ouvrages de référence, des articles publiés dans des revues à comité de lecture, des documents institutionnels officiels européens, et des bibliothèques open source publiées dans des revues scientifiques.

---

*Bibliographie dans le cadre du projet IA HumanForYou — CESI 2025-2026*
