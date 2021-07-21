# Bringing ML Models into Production Bootcamp
# Lesson 4: ML Best Practices

Watch the recording of this lesson [here](https://youtu.be/J2XgPmsTfGU).

## Goal

The goal of this lesson is to share ML Best Practices

---
## ML Best Practices

**Scope**
- define the main goal
- ML solution development:
    - visualize an ideal solution without any constraints
    - understand how the problem is solved
    - design with constraints in mind
- end to end MVP iterations

**Code structure**
- notebooks vs modular code
- venv, conda - pin the libraries, use docker
- docs, type hinting, pre-commit
- print vs logging, error handling
- sys, argparse, configargparse, click, typer
- automation

**Tests**
- unit, integration, functional, regression tests
- data-specific tests - check the validity of your data with [great expectations](https://greatexpectations.io/)
- model-specific tests (shapes and values of model output, metrics, loading artefacts, inference)

**Pipelines**
- DataOps (get data, join, validate, prepare, split, feature engineering)
- Model training
- Model evaluation (performance, latency, size, compute, interpretability, bias, time to develop, time to retrain, maintenance overhead)
- Model deployment (build, release pipelines)

**ML system monitoring**
- overall MLsystem health
- model performance (data drift, feature drift, concept drift)
- monitoring solution (alert, inspect, act)

---

Reading materials:
- [Calm Code](https://calmcode.io/)
- [ML Test Score](https://research.google/pubs/pub46555/)
- [Data and concept drift](https://towardsdatascience.com/machine-learning-in-production-why-you-should-care-about-data-and-concept-drift-d96d0bc907fb)