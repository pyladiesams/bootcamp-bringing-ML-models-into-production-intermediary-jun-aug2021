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
- venv, conda, pinned libraries
- docs, type hinting, pre-commit
- print vs logging, error handling
- sys, argparse, configargparse, CLI
- versioning
- automation

**Tests**
- unit, integration, functional, regression tests
- data-specific tests (rows/cols, individual values, aggregate values) - great expectations to test the validity of the data
- model-specific tests (shapes and values of model output, important metrics: overall, per-class, slices, behavioral testing; loading artefacts, prediction, testing and benchmarking the tradeoffs)

**Pipelines**
- DataOps (get, join, validate, prepare, split, feature engineering)
- Model training
- Model evaluation (trade offs: performance, latency, size, compute, interpretability, bias checks, time to develop, time to retrain, maintenance overhead)
- Model deployment

**ML system monitoring**
- Model monitoring (system health, model performance (data drift, feature drift, concept drift; locate drift, measure drift, outliers; monitoring solution (alert, inspect, act))
