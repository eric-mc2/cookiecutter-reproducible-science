{{cookiecutter.project_slug}}
==============================

{{cookiecutter.project_short_description}}

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
├── notebooks               <- Ipython or R notebooks
│   ├── data                <- Scripts and programs to process data
│   ├── exploratory         <- One-offs (one script per task)
│   └── replication         <- Report-generating scripts that were used in a paper, talk, etc. (one script per presentation)
├── reports                 <- For all non-data project outputs
|   ├── exploratory         <- One-offs
|   |   └── my-task         <- One folder per task/presentation
|   |       ├── figures     <- Visualizations
|   |       ├── tables      <- Descriptive tables
|   |       └── regressions <- Model outputs
│   └── replication         <- Outputs that were presented in a talk, paper, etc. (promote exploratory subfolders into here)
├── setup.py                <- Allows importing python files from src into notebooks
└── src                     <- Source code for this project
    ├── data                <- Scripts and programs to process data
    ├── stats               <- Source code for modeling and statistics
    ├── viz                 <- Scripts for visualisation of your results, e.g., matplotlib, ggplot2 related.
    └── util                <- Any helper scripts go here
```