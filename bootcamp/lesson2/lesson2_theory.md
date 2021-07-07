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
6. Manually update config.json to correspond with Python Workspace class requirements:
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
EDA takes place locally, datasets registration - on Azure. Open [data preparation notebook](prepare_data.ipynb) and follow the steps.

### Model training
Model training takes place locally, experiment tracking - on Azure. Open [linear regression model training notebook](train_linreg_model.ipynb) and follow the steps.

### Model evaluation and registration
Model evaluation takes place locally, experiment tracking and registration - on Azure. After finalizing model training run
```
python evaluate_model.py <your model name>
```
Open [predictions exploration notebook](explore_predictions.ipynb) and follow the steps.

To register the model of choice run
```
az ml model register -n <your model name> --model-framework <your model framework> -p <path to your pkl>
```

---
## 2. Batch inference on Azure

### Prepare files for batch inference
For the sake of this usecase we prepare data for batch inferencing locally, batch files registration - on Azure. Open [generate batch data notebook](generate_batch_data.ipynb) and follow the steps.

### Scoring script
Batch inferencing service requires a scoring script to load the model and use it to predict new values. It must include two functions:
- init(): Called when the pipeline is initialized.
- run(mini_batch): Called for each batch of data to be processed.

Typically, you use the init function to load the model from the model registry, and use the run function to generate predictions from each batch of data and return the results.

We will create this script in the next step.

### Setup and schedule Batch Azure Machine Learning Pipeline
Azure Machine Learning provides a type of pipeline step specifically for performing parallel batch inferencing. Using the **ParallelRunStep class**, you can read batches of files from a File dataset and write the processing output to a **OutputFileDatasetConfig**.

Open [create batch pipeline notebook](create_batch_pipeline.ipynb) and follow the steps.

---
## 3. Reading materials (optional)
- [Manage costs for Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-plan-manage-cost)
- [Compute targets in Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-compute-target)