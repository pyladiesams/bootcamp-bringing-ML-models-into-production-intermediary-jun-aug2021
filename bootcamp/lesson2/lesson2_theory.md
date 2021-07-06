# Bringing ML Models into Production Bootcamp
# Lesson 2: Batch Inference

Watch the recording of this lesson [here](https://youtu.be/G1qxR1Hi3i8).

## Goal

The goal of this lesson is to learn more about:
- machine learning lifecycle building blocks in action
- Batch inference on Azure

---

## 0. Prerequisites
1. Login to Azure by usind Azure CLI

```
az login
```
2. Create Resource Group in your Azure subscription

List all locations to find the name of your location
```
az account list-locations -o table
```
```
az group create --name mlops_bootcamp --location <your location name here>
```
3. Install Azure ML cli v1.0
```
az extension add -n azure-cli-ml
```
4. Provision Azure Machine Learning including Azure Storage Account, Azure Application Insights, Azure Key Vault
```
az ml workspace create -w mlops -g mlops_bootcamp
```
5. Save Workspace config to your file. In our case we have only 1 workspace, that's why we pick the first element of the list.
```
az ml workspace list --query '[0]' > config.json
```
6. Manually update config.json to correspond to Python Workspace class requirements:
- open config.json
- replace "resourceGroup" with "resource_group"
- replace "subscriptionId" with "subscription_id"
- replace "workspaceName" with "workspace_name"
- save changes

7. Create conda environment from the conda file and configure VSC to use it
```
conda env create -f mlops_train.yml
conda activate mlops_train
python -s -m ipykernel install --user --name=mlops_train
```

---
## 1. Deployment setup

### Data preparations
EDA takes place locally, datasets registration - on Azure.

Open [data preparation notebook](data_preparation.ipynb) and follow the steps.

### Model training
Model training takes place locally, experiment tracking - on Azure.

Open [LR model training notebook](lr_model_training.ipynb) and follow the steps.

Open [Ridge model training notebook](ridge_model_training.ipynb) and follow the steps.

### Model evaluation and registration
Model evaluation takes place locally, experiment tracking and registration - on Azure.

After finalizing model training run
```
python evaluate_model.py linear_regression
python evaluate_model.py ridge
```
Open [Forecast output exploration notebook](forecast_output_explorations.ipynb) and follow the steps.

To register the model of choice run
```
az ml model register -n linear_regression --experiment-name Evaluation --model-framework ScikitLearn -p <path to your pkl>
```

---
## 2. Batch inference on Azure

### Scoring script
TODO

### conda.yml for inference
TODO

### Setup AML compute
TODO

### Setup Azure Machine Learning Pipeline
TODO
