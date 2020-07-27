![Screenshot](BenettonIO.png)

# Goals
In the previous case, we learned how linear regression can be a powerful tool to understand the behavior of a variable of interest as being explained by other variables in our dataset. However, in many real instances, our data may not meet basic assumptions that one needs for a linear regression model to be suitable. In cases where linear regression is not *directly* applicable in these scenarios, we need to figure out how to go around this problem.

In this case, you will learn:

1. How to select and use appropriate variable transformations to correct our data such that it becomes applicable for linear regression
2. How to decide whether the addition of predictor variables actually benefit the model or create overfitting
3. How to further extend the applicability of linear models by taking into account non-linear interactions that can exist between the predictor variables

# Introduction
Business Context. You have been hired as a data scientist by a large real estate company in their Seattle office. Your job is to assist Seattle residents willing to sell their home with determining an optimal price to sell their property at in order to maximize their proceeds while still being able to find willing buyers. To do this, the firm would like you to build a pricing model for Seattle real estate, in order to maximize the probability of helping residents close sales (and thus maximizing commissions for the firm).

Business Problem. Your task is to build a model that uses past sales data in Seattle to recommend an optimal sell price for any particular property.

Analytical Context. The provided dataset was retrieved from Kaggle (https://www.kaggle.com/harlfoxem/housesalesprediction) and includes sales prices of houses in the state of Washington (King county, where Seattle is located) between May 2014 and May 2015. As we have learned, the primary tool to predict a response variable is the multiple regression model. However, sometimes the assumptions of a linear model are not met by our data. We will learn a set of strategies to mitigate some common issues that appear during regression analysis.

The case is structured as follows: you wil (1) conduct basic EDA of some of the variables to determine that standard linear regression is not sufficient; (2) learn about variable transformations and use these to improve the initial model; and finally (3) learn how to incorporate interaction effects (which are themselves a form of variable transformation involving two or more variables) into our model.

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── environment.yml    <- The conda environment file to reproduce the analysis environment. eg.
    │                         `conda env create -f environment.yml`
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── githubrequirements.txt <- Pip references to github repo's, referred to by both `environment.yml` and `requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.testrun.org


--------

## Getting started:

One should be up and running as follows:

    make create_environment
    source activate hackmakers_predictive_algorithm
    make requirements

If you've setup s3, one can sync to and from your bucket as follows:

    make sync_data_from_s3
    make sync_data_to_s3

Running the data preparation should then be as follows:

    make data

### Shortcut creating the environment using conda 
To get started in this project, you first need to setup an environment:

    conda env create -f environment.yml

### Installing Python module as egg
------------
If you want to reuse the code developed in other projects, you can install an egg directly from your checkout:

    pip install -e .
