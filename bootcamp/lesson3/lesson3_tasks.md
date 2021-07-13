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
## Exercise 1: Azurite
### Steps

1. Find out how to stop Azurite from VSC code
2. Find out how to clean up Azurite from VSC code

---
## Exercise 2: Bindings

### Steps

1. Update bindings so that a function will be triggered by csv files only
2. Update bindings so that a function will be triggered by csv files, which names start with "processed-"

---
## Exercise 3: Azure Functions App and CLI

### Steps

1. Find out how to stop Azure Functions App by using Azure CLI
2. Find out how to restart Azure Function App by using Azure CLI
2. Find out how to remove Azure Function App by using Azure CLI

---
## 4. Home assignment

**Goal**

Get hands-on experience with near real-time serverless inference on Azure

Follow the steps in near real-time inference on Azure to:
1. Create a simple Blob triggered Azure Function (reads a file metadata, writes a string "Hello World from my own deployed function! to blob"), name it `RidgeBlobTrigger`, update bindings and Python script, deploy it as a function app `RidgeBlobTriggerApp` at App Service Plan `MLOPSplan`, add connection string.
2. Re-use local setup and continue to develop the function locally with Azurite to load ridge model and write predictions to the file(blob) with the same name.
3. Re-deploy `RidgeBlobTrigger` function to `RidgeBlobTriggerApp` with the updated bindings and function script (loads ridge model, returns prediction).