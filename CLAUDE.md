# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A fork of [miguelfzafra/Latest-News-Classifier](https://github.com/miguelfzafra/Latest-News-Classifier)
(unmodified, per the upstream README) — a KSchool MSc data-science final
project: a supervised ML pipeline that classifies news articles by topic,
paired with a web scraper for current articles and a Dash web app that
serves live predictions. This is someone else's completed educational
project, not an in-progress `thediversecandidate` build — treat the
existing pipeline as reference material rather than a codebase under active
development, unless told otherwise.

## Structure

Everything lives under `0. Latest News Classifier/`, numbered by pipeline
stage (mixed R and Python/Jupyter, matching the original coursework):

1. `00. Raw dataset` — source BBC articles
2. `01. Dataset Creation` — R script/notebook building `News_dataset.csv`
3. `02. Exploratory Data Analysis` — Jupyter notebook
4. `03. Feature Engineering` — TF-IDF etc., pickled outputs in `Pickles/`
5. `04. Model Training` — one notebook per candidate model (Random Forest,
   SVM, KNN, MultinomialNB, Logistic Regression, GBM), then model selection
6. `05. News Scraping` — one notebook per source site (El País, The
   Guardian, Daily Mail, The Mirror)
7. `06. App Creation` — original Dash app (`dash-app-lnclass/`)
8. `07. Annex - Installation` — manual Ubuntu 18.04 + Anaconda + R setup
   instructions (not a script)
9. `08. Annex - Deployment` — Heroku deployment notes
10. `09. Report` — the write-up PDF
11. `10. App Creation v2` — a later revision of the Dash app
    (`dash-app-latnewclas/`), with its own `requirements.txt`,
    `environment.yml`, `nltk.txt`, `Procfile`, and pickled model
    (`Pickles/best_svc.pickle`, `tfidf.pickle`) — this is the app that was
    actually deployed to Heroku, not step 6's earlier version.

## Running the app

`10. App Creation v2/dash-app-latnewclas/` is the deployable unit:
`app.py` is the Dash entrypoint, `requirements.txt` / `environment.yml` list
dependencies, `Procfile` is Heroku's process definition. It loads the
pickled TF-IDF vectorizer + SVM classifier rather than retraining on
startup — if those pickles are regenerated, they need to come from step 3
(Feature Engineering) and step 4 (Model Training) using compatible library
versions.
