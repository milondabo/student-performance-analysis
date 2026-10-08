# Analyse exploratoire et préparation des données — Students Performance

## Description

Ce projet porte sur l'analyse et la préparation d'un jeu de données contenant les performances scolaires de 1 000 élèves.

L'objectif est de suivre une première démarche de Data Science allant de l'exploration des données jusqu'à leur préparation pour une future utilisation en Machine Learning.

Le projet est réalisé progressivement à travers plusieurs étapes :
- exploration et nettoyage des données ;
- analyse statistique et visualisation ;
- encodage des variables catégorielles ;
- standardisation des variables numériques ;
- création de nouvelles variables à partir des données existantes.

## Objectifs

Ce projet permet de :

- comprendre la structure d'un jeu de données ;
- identifier les différents types de variables ;
- réaliser une analyse statistique descriptive ;
- détecter les valeurs manquantes et les doublons ;
- visualiser la distribution des données ;
- analyser les relations entre variables ;
- transformer les variables catégorielles en variables numériques ;
- standardiser les variables numériques ;
- créer de nouvelles variables pertinentes ;
- produire un jeu de données prêt pour une future étape de Machine Learning.

## Dataset

Le dataset utilisé est **Students Performance in Exams**, disponible sur Kaggle.

Il contient **1 000 observations et 8 variables** décrivant notamment :

- le genre ;
- le groupe ethnique ;
- le niveau d'éducation des parents ;
- le type de déjeuner ;
- la participation à un cours de préparation ;
- le score en mathématiques ;
- le score en lecture ;
- le score en écriture.

### Variables numériques

- `math score`
- `reading score`
- `writing score`

### Variables catégorielles

- `gender`
- `race/ethnicity`
- `parental level of education`
- `lunch`
- `test preparation course`

# Milestone 1 — Exploration et nettoyage

Le premier notebook `01_exploration_cleaning.ipynb` est consacré à l'exploration du dataset.

### Analyses réalisées

- identification du nombre de lignes et de colonnes avec `shape` ;
- analyse de la structure du dataset avec `info()` ;
- statistiques descriptives avec `describe()` ;
- recherche de valeurs manquantes ;
- recherche de doublons ;
- analyse de la distribution des scores ;
- matrice de corrélation ;
- analyse de la relation entre les scores de lecture et d'écriture.

### Résultats principaux

Le dataset initial présente :

- **1 000 lignes** ;
- **8 colonnes** ;
- **aucune valeur manquante** ;
- **aucun doublon exact**.

Les moyennes observées sont approximativement :

Score             Moyenne
Mathématiques     66,09
Lecture           69,17
Écriture          68,05

Les trois scores présentent des dispersions relativement proches.

L'analyse de corrélation montre notamment une **forte relation positive entre les scores de lecture et d'écriture** : les élèves ayant de bons résultats en lecture ont généralement tendance à avoir également de bons résultats en écriture.

# Milestone 2 — Feature Engineering

Le deuxième notebook `02_feature_engineering.ipynb` est consacré à la transformation des données afin de les rendre exploitables par des algorithmes de Machine Learning.

## 1. Identification des variables catégorielles

Les variables catégorielles ont été identifiées automatiquement à partir de leur type :

```python
categorical_cols = df.select_dtypes(include="str").columns
````

Les variables identifiées sont :

* `gender`
* `race/ethnicity`
* `parental level of education`
* `lunch`
* `test preparation course`

## 2. Encodage des variables catégorielles

Les variables catégorielles ont été transformées à l'aide du **One-Hot Encoding** :

```python
df_encoded = pd.get_dummies(
    df,
    columns=categorical_cols,
    dtype=int
)
```

Cette transformation permet de représenter les catégories sous forme de variables numériques binaires.

Par exemple :

```text
gender_female
gender_male
```

avec des valeurs `0` ou `1`.

Le dataset passe ainsi de **8 à 20 colonnes** après l'encodage.

## 3. Standardisation des variables numériques

Les trois scores numériques ont été standardisés avec `StandardScaler` :

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

df_encoded[numeric_cols] = scaler.fit_transform(
    df_encoded[numeric_cols]
)
```

La standardisation permet de centrer les variables autour de 0 et de les ramener à une échelle comparable.

Les variables concernées sont :

* `math score`
* `reading score`
* `writing score`

## 4. Création d'une nouvelle variable

Une nouvelle variable appelée `average_score` a été créée.

Elle correspond à la moyenne des trois scores scolaires :

```python
df_encoded["average_score"] = df[
    ["math score", "reading score", "writing score"]
].mean(axis=1)
```

### Pourquoi cette variable ?

Les trois scores mesurent différentes dimensions de la performance scolaire. La variable `average_score` permet de les synthétiser en un **indicateur global de performance académique**.

Elle reste exprimée sur une échelle de 0 à 100, ce qui la rend facilement interprétable.

> Cette variable a été créée à partir des scores originaux afin de conserver leur interprétation sur l'échelle initiale.

## 5. Contrôle du dataset final

Après les transformations, le dataset final contient :

* **1 000 lignes** ;
* **21 colonnes** ;
* **0 valeur manquante** ;
* **0 doublon** ;
* uniquement des variables numériques.

Le dataset est donc prêt à être utilisé pour une future étape de Machine Learning.

## Technologies utilisées

* **Python**
* **Jupyter Notebook**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**

## Structure du projet

```text
student-performance-analysis/
│
├── data/
│   ├── StudentsPerformance.csv
│   └── engineered_data.csv
│
├── carnets/
│   ├── 01_exploration_cleaning.ipynb
│   └── 02_feature_engineering.ipynb
│
└── README.md
```

## Utilisation

### 1. Installer les dépendances

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### 2. Lancer Jupyter Notebook

```bash
python -m jupyter notebook
```

### 3. Ouvrir les notebooks

Commencer par :

```text
carnets/01_exploration_cleaning.ipynb
```

puis poursuivre avec :

```text
carnets/02_feature_engineering.ipynb
```

## Suite du projet

Le dataset `engineered_data.csv` constitue maintenant une base préparée pour les prochaines étapes du parcours Data Science, notamment :

* analyse plus approfondie des variables ;
* sélection de caractéristiques ;
* entraînement de modèles de Machine Learning ;
* évaluation des performances des modèles.

## Auteur

**Ilona Joanne Ndabo**

Projet réalisé dans le cadre d'un parcours d'apprentissage en Data Science et Machine Learning.
