Reproducible Science
====================

A boilerplate for reproducible and transparent science with close resemblances to the philosophy of [Cookiecutter Data Science](https://github.com/drivendata/cookiecutter-data-science) and Mario Krapp's (cookiecutter)[https://github.com/mkrapp/cookiecutter-reproducible-science]: *A logical, reasonably standardized, but flexible project structure for doing and sharing data science work.*

This template is designed to document the creation of a dataset/presentations/papers. It has been refined over several research projects at the (UChicago Justice Project)[https://github.com/uchicago-justice-project]. 

An idealized data science workflow:

```mermaid
flowchart TD
    A("fa:fa-file data/raw/") -->|fa:fa-terminal clean.py| B("fa:fa-file data/interim/v1")
    B --> |fa:fa-terminal more_cleaning.py| C("fa:fa-file data/final/v2")
    C --> D[fa:fa-archive academic talk]
    C --> E[fa:fa-book academic paper]
```

Project Structure
-----------------

```
.
├── AUTHORS.md
├── LICENSE
├── README.md
├── data                    <- (not tracked by git. maybe tracked by DVC)
│   ├── raw                 <- The original, immutable data dumps from primary or third-party sources.
│   ├── interim             <- Intermediate data that has been transformed.
│   ├── final               <- The final, canonical data sets for modeling.
│   └── replication         <- Final data that was used in a paper, talk, etc.
|       └── my-paper        <- One folder per task/presentation
├── docs                    <- Documentation, e.g. data dictionaries, memos, project notes
├── notebooks               <- Interactive python or R notebooks
│   ├── exploratory         <- One-offs (one script per task)
│   └── replication         <- Report-generating scripts that were used in a paper, talk, etc. (one script per presentation)
├── pipeline                <- The actual data ETL process (a NUMBERED mix of scripts and notebooks)
├── reports                 <- For all non-data project outputs
|   ├── exploratory         <- One-offs
|   |   └── my-task         <- One folder per task/presentation
|   |       ├── figures     <- Visualizations
|   |       ├── tables      <- Descriptive tables
|   |       └── regressions <- Model outputs
│   └── replication         <- Outputs that were presented in a talk, paper, etc. (promote exploratory subfolders into here)
├── setup.py                <- Allows importing python files from src into notebooks
└── src                     <- Refactored helper code
    ├── data                <- Resusable data ETL steps
    ├── stats               <- Source code for modeling and statistics
    ├── viz                 <- Scripts for visualisation of your results, e.g., matplotlib, ggplot2 related.
    └── util                <- Any helper scripts go here
```

Setup
------------
Install `cookiecutter` command line: 

`pip install cookiecutter`    

For the error: "Unable to load extension: No module named 'jinja2_time'"

`pip install jinja2_time`

To start a new science project:

`cookiecutter gh:eric-mc2/cookiecutter-reproducible-science`

Create local python package from src to allow relative imports in notebooks (optional):

`cd <repo-name>; pip install -e`


Usage / Recommendations
------------

Don't painstakingly refactor your project to fit into this mold, but *do* use the
parts of this template that make sense in the context of your research goals.
This is a loosely-opinionated structure to help with some of the following goals:

* document the streamlined/idealized data generation process leading to the finalized dataset
* document the actual data generation process of an in-progress dataset
* document validation steps that motivated further data processing steps
* store data versions to triage issues and affected analyses

The opinionated workflow looks like this:

1. Pull your data into data/raw.
2. Apply transformations. 
    a. Transformed data goes in data/interim.
    b. All transformations increment the data version number, e.g. (census_v1.csv).
    c. Keep previous data versions! Storage is cheap!
    e. The highest-version files that are part of the "final product" go in data/final.
    f. Whenever you revise the "final" data, just move the file to interim, and add the new incremented version to final.
3. Document all transformations in pipeline/
    a. If the process was manual, still document it as a comment-only script.
    b. Number all pipeline files in the order they should run.
4. Promote all data, outputs, and scripts related to "published" work into replication.

A more realistic research data science workflow:

```mermaid
flowchart TD
    RAW("fa:fa-file data/raw")
    RAW --> EDA[/fa:fa-terminal notebooks/exploratory/eda.py/]
    EDA --> EXP[fa:fa-archive reports/exploratory/first-chart.png]
    CLEAN[/fa:fa-terminal pipeline/cleaning stages.py/]
    RAW -->CLEAN
    CLEAN --> INT("fa:fa-file data/interim/v++")
    INT --> CLEAN
    REG1[/fa:fa-terminal notebooks/exploratory/modeling/test/]
    INT --> REG1
    REG1 --> TALK[fa:fa-archive reports/exploratory/test-regression.tex]
    MORE(fa:fa-file data/raw/covariates)
    MORE --> MERGE[/fa:fa-terminal pipeline/merge.py/]
    INT --> MERGE
    MERGE --> FIN("fa:fa-file data/final")
    REG2[/fa:fa-terminal notebooks/replication/asr-paper/]
    FIN --> REG2
    REG2 --> PAPER[fa:fa-book academic paper]
```

License
-------
This project is licensed under the terms of the [BSD License](/LICENSE)
