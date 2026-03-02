# Prosit Retour - Boucle 2

## Aide au tutorat

### Définitions

Voici l'approche du prosit, ce que les élèves doivent avoir compris au minimum :

## Problème

Je souhaite modéliser le prix médian d'une maison d'un quartier en fonction des données que j'ai concernant l'ensemble de quartiers (block group).

## Données d'entrées

Les données préparées (fin de du WS du prosit précédent).

## Hypothèse

Variation linéaire du prix en fonction des différents attributs (super important qu'ils arrivent à ces réflexions en prosit aller : plus la maison est près de l'eau, plus elle va être chère en général, plus les revenus du ménage sont important, plus ils vont acheter une maison chère. Plus la famille est grande, plus la maison achetée sera chère)

---

## Construction du modèle

Cette hypothèse nous amène à la construction d'un modèle :

$y$ (le prix médian d'une maison) = modèle linéaire : pour une simple variable $x$ :

$$y = \theta_0 + \theta_1 x$$

où $x^{(i)}$ correspond à une observation et $\theta$ correspond au poids associé à chaque attribut de l'observation permettant ainsi d'estimer le prix médian d'une maison ($y$) à partir des attributs observés dans les différentes observations du jeu de données.

---

## Comment définir les valeurs du vecteur $\theta$ à partir de l'ensemble des observations ?

On a des approches de résolution exactes mais sur de grands jeux de données avec beaucoup d'attributs et/ou beaucoup d'observation et du bruit (imprécision ou doublons dans les mesures par exemple), elles ne sont pas efficaces (en temps mais aussi si j'apprends sur un jeu de données, est ce que je peux généraliser à un autres ?).

C'est la que le principe de la **descente du gradient** entre en jeu avec un apprentissage supervisé : je connais des prix médians pour $m$ exemples de quartiers sur lesquels je vais baser mon apprentissage.

---

## Fonction objectif

On va pouvoir définir des valeurs pour mon vecteur $\theta$ et définir une fonction objectif qui va permettre d'identifier en quelle mesure ce vecteur est efficace pour estimer le prix médian d'une maison ($\hat{y}^{(i)}$) connaissant vraiment le prix médian d'une maison $y^{(i)}$ pour une observation donnée $i$.

### Fonctions objectifs possibles

On peut envisager plusieurs fonctions objectifs :

**MSE (Mean Squared Error) :**

$$MSE = \frac{1}{m} \sum_{i=1}^{m} (y^{(i)} - \hat{y}^{(i)})^2$$

où $m$ est le nombre d'observations dans mon jeu de données d'entraînement.

**RMSE (Root Mean Squared Error) :**

$$RMSE = \sqrt{\frac{1}{m} \sum_{i=1}^{m} (y^{(i)} - \hat{y}^{(i)})^2}$$

où $m$ est le nombre d'observations dans mon jeu de données d'entraînement.

Plus ces valeurs sont proches de 0, plus les $\hat{y}$, estimés grâce à $\theta$ sont proches de $y$, les valeurs connues dans l'échantillon d'entraînement.

---

## Descente du gradient

Pour explorer l'espace des valeurs que peut prendre $\theta$, la stratégie de la descente du gradient pourra être exploitée avec des paramètres importants : 
- Le **taux d'apprentissage** $\alpha$ (learning rate)
- Le **nombre d'itérations** (epochs) sur le jeu de données

La ressource "Descente de gradient" détaille les concepts mathématiques liés à cette partie et le WS son usage concret avec ScikitLearn.

Très grossièrement, cette approche va permettre d'explorer le domaine de définition du vecteur $\theta$ en le modifiant (selon le taux d'apprentissage défini) d'une itération à l'autre de manière à minimiser la fonction objectif.

### Minimum global vs minimum local

Dans le cas idéal où les distributions des différents attributs suivraient toutes une loi normale, les fonctions objectifs définies ci-dessus seront bien des fonctions convexes et on pourrait atteindre un minimum globale. 

Dans la réalité, ce n'est pas forcément le cas et il peut il y avoir des minimums locaux, l'approche de la descente du gradient ne nous garantie donc pas d'atteindre un minimum global mais **« une bonne préparation des données »** et des choix judicieux de paramètres contribuent à s'en approcher.

---

## Évaluation de la qualité du modèle

On peut chercher à mesurer la qualité du résultat obtenu au final en confrontant le modèle obtenu en sortie de la descente de gradient à un **jeu de test**, c'est à dire un jeu de données dont on connaît la sortie qui n'a pas été utilisé pour l'entraînement du modèle. 

Ainsi :
- Un **MSE sur le jeu de test > au MSE obtenu sur le jeu d'entraînement** peut être un indicateur de **sur-apprentissage** (overfitting)
- Un **MSE élevé en général** est un indicateur de **sous-apprentissage** (underfitting)
