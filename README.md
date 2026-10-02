# Analyse exploratoire des performances des élèves

## Description

Ce projet consiste en une première analyse exploratoire de données (EDA — *Exploratory Data Analysis*) portant sur les performances scolaires de 1 000 élèves.
L'objectif est d'examiner la structure et la qualité des données, de produire des statistiques descriptives et d'identifier les relations entre les différents scores obtenus par les élèves.


## Objectifs

Cette analyse vise à :

* comprendre la structure du jeu de données ;
* identifier les différents types de variables ;
* vérifier la présence de valeurs manquantes et de doublons ;
* obtenir des statistiques descriptives sur les scores ;
* visualiser la distribution des scores en mathématiques ici notre variable cible ;
* étudier les corrélations entre les scores ;
* visualiser la relation entre les scores de lecture et d'écriture.


## Jeu de données

Le jeu de données utilisé est **Students Performance in Exams**.
https://www.kaggle.com/datasets/spscientist/students-performance-in-exams

Il contient :

* **1 000 observations**, correspondant aux élèves ;
* **8 variables** décrivant leurs caractéristiques et leurs résultats.

Les variables comprennent notamment :

* `gender` : genre de l'élève ;
* `race/ethnicity` : groupe ethnique ;
* `parental level of education` : niveau d'éducation des parents ;
* `lunch` : type de repas ;
* `test preparation course` : participation à un cours de préparation ;
* `math score` : score en mathématiques ;
* `reading score` : score en lecture ;
* `writing score` : score en écriture.


## Technologies utilisées

* **Python**
* **Jupyter Notebook**
* **Pandas** pour la manipulation et analyse des données
* **NumPy** pour les calculs numériques
* **Matplotlib** pour la visualisation de données
* **Seaborn** pour la visualisation statistique


## Analyse réalisée

### 1. Exploration de la structure des données

La taille du DataFrame a été vérifiée avec `df.shape`.

Le jeu de données contient :

> **1 000 lignes et 8 colonnes.**

La méthode `df.info()` a ensuite permis d'identifier :

* 5 variables textuelles (`str`) ;
* 3 variables numériques (`int64`) ;
* 1 000 valeurs non nulles dans chacune des colonnes.

### 2. Statistiques descriptives

La méthode `df.describe()` a permis d'obtenir les principales statistiques des trois variables numériques.

Les scores moyens sont :

| Variable      | Moyenne |
| ------------- | ------: |
| Mathématiques |   66,09 |
| Lecture       |   69,17 |
| Écriture      |   68,05 |

Les écarts-types des trois scores sont relativement proches, avec une dispersion légèrement plus élevée pour les scores d'écriture. (15.16308	14.600192	15.195657)

### 3. Vérification des données manquantes

La commande `df.isnull().sum()` n'a détecté **aucune valeur manquante** dans le jeu de données.

Il n'a donc pas été nécessaire d'utiliser `fillna()` ou `dropna()`.

### 4. Vérification des doublons

La commande `df.duplicated().sum()` a retourné :

```text
0
```

Aucune ligne dupliquée exacte n'a donc été détectée.

## Visualisations

### Distribution des scores en mathématiques

Un histogramme a été utilisé afin d'observer la distribution des scores en mathématiques.

Les scores sont principalement concentrés entre **60 et 80**, avec une concentration particulièrement importante autour de la tranche 60–70. Les scores très faibles et très élevés sont moins fréquents.

### Matrice de corrélation

Une heatmap a été utilisée pour étudier les corrélations entre les trois scores numériques.

Les trois variables présentent des corrélations positives. La corrélation la plus forte est observée entre les **scores de lecture et d'écriture**.

### Relation entre lecture et écriture

Un nuage de points a été réalisé pour visualiser la relation entre `reading score` et `writing score`.

Les points forment globalement une diagonale ascendante et sont relativement regroupés autour de cette tendance, ce qui confirme visuellement la présence d'une **forte corrélation positive** entre les deux variables.

Cette corrélation indique une association entre les deux scores, mais ne permet pas à elle seule d'établir une relation de causalité.

## Structure du projet

```text
student-performance/
│
├── data/
│   └── StudentsPerformance.csv
│
├── carnets/
│   └── 01_exploration_cleaning.ipynb
│
└── README.md
```

## Installation et utilisation

### 1. Installer les bibliothèques nécessaires

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 2. Lancer Jupyter Notebook

```bash
python -m jupyter notebook
```

### 3. Ouvrir le notebook

Depuis l'interface Jupyter, ouvrir :

```text
carnets/01_exploration_cleaning.ipynb
```

Le notebook contient les différentes étapes d'exploration, de vérification des données et de visualisation.


## Conclusion

Cette première analyse exploratoire a permis de comprendre la structure du jeu de données, de vérifier sa qualité et d'étudier les relations entre les performances des élèves.

L'analyse met notamment en évidence une forte association positive entre les scores de lecture et d'écriture, ainsi qu'une distribution des scores en mathématiques principalement concentrée autour des valeurs intermédiaires à élevées.