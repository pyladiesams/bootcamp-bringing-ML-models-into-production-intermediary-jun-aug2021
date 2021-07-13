# Bringing ML Models into Production Bootcamp
# Lesson 3: Near real-time Inference

Watch the recording of this lesson [here](https://youtu.be/O7hfLDMizyA).

## Goal

The goal of this lesson is to learn more about:
- near real-time inference on Azure (serverless aproach)

---

## 0. Prerequisites
- resource group `mlops_bootcamp`, workspace `mlops` on Azure from lesson2
- registered `batch-data` dataset from lesson2
- trained, evaluated and registered ML models (`linear_regression` and `ridge`)

---
## 1. Near real-time inference on Azure

### Create and deploy a simple Blob triggered Azure Function

1. Create a new folder `blob_function` inside of lesson3 directory
```
mkdir blob_function
```
2. Navigate to the folder
```
cd blob_function
```
3. Open Azure Functions VSC extension


### Develop the Blob triggered Azure Function locally with Azurite

Development setup
- create folder `test_data` and download sample of data from “batch-data” locally
- create folder `models` and download there both registered models
- setup and start Azurite VSC

Near real-time serverless inferencing service requires a scoring script to load the model and use it to predict new values.

Typically, you load the model from the model registry and use it to generate predictions.

### Deploy the Blob triggered Azure Function
tototo

---
## 2. Reading materials (optional)
//TODO Add additional materials
