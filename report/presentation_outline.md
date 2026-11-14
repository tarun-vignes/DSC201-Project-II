# Presentation outline: Glioma Grade Classification

**DSC 201 Project 2 - Tarun Vigneswaran**

Eight slides, about six minutes. Use the saved figures at a readable size.
All scores below are from the completed experiments, not another study.

## Slide 1 - Title: Comparing Machine Learning Models for Glioma Classification (20 seconds)

- Tarun Vigneswaran
- DSC 201 Project 2, Data Science II, University of Tampa
- Using clinical and gene-mutation features

**Speaker notes:** My project compares four machine learning models for glioma grade classification. I used the approved UCI dataset and kept the code close to the methods we covered in class. I will explain the data, the fair testing process, and the actual results.

## Slide 2 - Introduction: the project question (30 seconds)

- Predict the dataset's LGG or GBM label from clinical and mutation features
- Compare four course models under the same testing conditions
- Use 30 shared splits to see how much scores change
- Educational comparison, not a medical diagnosis tool

**Speaker notes:** The main question is whether clinical information and mutation features can help predict the LGG or GBM label in this dataset. I compare four standard classifiers under the same conditions. Each model gets the same people in training and testing within a repetition. Repeating that process 30 times shows how much the scores change with the split. This is a classroom comparison, not a tool for diagnosing people.

## Slide 3 - What are the two classes? (35 seconds)

- The dataset contains records of people with glioma, a type of brain tumor
- Class 0: Lower-Grade Glioma, or LGG
- Class 1: Glioblastoma, or GBM
- Finding GBM cases matters to our evaluation, so GBM is the positive class

**Speaker notes:** There are two labels in this dataset. We are distinguishing
between those labels, rather than deciding whether someone has a brain tumor.
For precision, recall, and F1, I treated GBM as the class the models are trying
to identify. This makes it clear what those scores mean.

## Slide 4 - Dataset overview (40 seconds)

- UCI Glioma Grading Clinical and Mutation Features, dataset 759
- 839 original records; 20 mutation features plus age, gender, and race
- 487 LGG records and 352 GBM records
- Source: Tasci and colleagues, 2022; DOI: 10.24432/C5R62J

**Visual:** [Class counts](../results/figures/class_distribution.png)

**Speaker notes:** The approved dataset has 23 input features. Most are yes/no
gene-mutation indicators. There are more LGG than GBM cases, so I did not rely
on accuracy alone. The original file and variable dictionary are saved with
the project so the source can be checked.

## Slide 5 - Exploration and preparation (55 seconds)

- No missing values; one exact repeated record removed, leaving 838
- No ages flagged by the IQR rule; all ages retained
- Race changed into separate yes/no columns
- Example: GBM records have an older median age, but the groups overlap

**Visual:** [Age by class](../results/figures/age_by_class.png)

**Speaker notes:** I checked the data before cleaning it. Since there were no
missing values, I did not fill anything in. I removed one exact repeat to avoid
identical records being split between training and testing. Without patient IDs,
that is a judgment rather than proof of a repeated person. The box plot shows
an age difference in this sample, but age cannot perfectly separate the classes.

## Slide 6 - Four models and a fair test (65 seconds)

- Logistic Regression, Random Forest, AdaBoost, and XGBoost
- Small parameter grids and five-fold stratified GridSearchCV
- Thirty 80/20 splits, with the same records for every model in each split
- Tune on training data; report held-out test scores
- Scale Logistic Regression inside its pipeline

**Speaker notes:** Every model got the same split within a repetition. I tuned
settings using only the training set and chose them by GBM F1. The test set was
used afterward. I repeated the full process 30 times because one split can give
a misleading picture. Scaling stayed inside the Logistic Regression pipeline
so validation and test data did not set the scaling values.

## Slide 7 - Actual results (80 seconds)

| Model | Mean test accuracy | Mean test F1 |
|---|---|---|
| Logistic Regression | 0.8706 | 0.8566 |
| Random Forest | 0.8655 | 0.8514 |
| AdaBoost | 0.8633 | 0.8523 |
| XGBoost | 0.8641 | 0.8517 |

- Highest all-feature mean F1: **Logistic Regression, 0.8566**
- Lead over the next model: 0.0043; small differences are not proof of superiority
- Optional gene-only comparison: clinical features raised mean F1 in 1/4 models

**Visual:** [Mean scores](../results/figures/model_mean_scores.png)

**Speaker notes:** These scores are averages across all 30 test splits. The
chart's error bars show the standard deviation across those splits.
Logistic Regression had the highest mean F1 in the main comparison, but the lead was small.
The optional comparison also shows that adding clinical features did not improve
every model. The separate confusion-matrix figure shows seed 100 only, not a
combined result across all repetitions.

## Slide 8 - Conclusion and limits (35 seconds)

- All four models were tuned and tested under a shared process
- The highest mean F1 is a result for this setup, not a universal winner
- Small sample, overlapping test groups, and limited demographic coverage
- Needs external testing and human review before any practical medical use

**Speaker notes:** The main lesson is the importance of a fair comparison and
repeated evaluation. These models showed useful patterns in this dataset, but
we have not tested them on patients from another source or checked fairness
across groups. This remains a classroom study, not a clinical decision system.
