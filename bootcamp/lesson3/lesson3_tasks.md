# Bringing ML Models into Production Bootcamp
# Lesson 3: Near real-time Inference

Watch the recording of this lesson [here](https://youtu.be/O7hfLDMizyA).

## Goal

The goal of this lesson is to learn more about near real-time inference on Azure (serverless aproach)

---

## 0. Prerequisites
- resource group `mlops_bootcamp`, workspace `mlops` on Azure from lesson2
- registered `batch-data` dataset from lesson2
- trained, evaluated and registered ML models (`linear_regression` and `ridge`)
- `config.json` in the root folder

---
## Exercise 1: Azurite
### Steps

1. Stop Azurite in VSC
2. Clean up Azurite in VSC

---
## Exercise 2: Bindings

### Steps

1. Update bindings so that a function will be triggered by csv files only
2. Update bindings so that a function will be triggered by csv files, which names start with "processed-"

---
## Exercise 3: Azure Functions App and CLI

### Steps

1. Stop Azure Functions App by using Azure CLI
2. Restart Azure Function App by using Azure CLI
2. Remove Azure Function App by using Azure CLI

---
## 4. Home assignment

**Goal**

Get hands-on experience with near real-time serverless inference on Azure

Follow the steps in near real-time inference on Azure
1. Create a simple Blob triggered Azure Function
- to read a file metadata, write a string "Hello World from my own deployed function!" to blob in `predictions-output`
- name it `RidgeBlobTrigger` and update bindings and Python script accordingly
- deploy it as a function app `RidgeBlobTriggerApp` at App Service Plan `MLOPSplan`
- add connection string and test it by uploading a sample.dat file to `predictions-input` container.
2. Re-use local Azurite setup to continue developing the function locally. The function has to load ridge model and write predictions to the file (blob) with the same name in `predictions-output` container.
3. Re-deploy `RidgeBlobTrigger` function to `RidgeBlobTriggerApp` with the updated bindings and function script.