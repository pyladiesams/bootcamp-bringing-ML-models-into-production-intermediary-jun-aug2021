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
- `config.json` in the root folder

---
## 1. Near real-time inference on Azure

### Create and deploy a simple Blob triggered Azure Function
0. Create and activate conda environment
```
conda env create -f mlops_function.yml
conda activate mlops_function
```
1. Login to Azure
```
az login
```

2. Create a new folder `blob_function` inside of lesson3 directory
```
mkdir blob_function
```
3. Open Azure Functions VSC extension and choose Create New Project:
- browse to `blob_function` folder
- select Python
- select Manually enter Python interpreter or full path. To get the path to Python interpreter type `which python` in terminal with activated mlops_function environment, copy and paste the path in the window above
- select Azure Blob Storage trigger
- replace `BlobTrigger1` with `LRBlobTrigger`
- select Create new local app setting
- select your storage account `mlopsstorage<....>`
- replace `samples-workitems/{name}` with `predictions-input/{name}`
- wait until `blob_function` folder will be populated with LRBlobTrigger folder and files

4. Update function bindings and the script according to the video
- two most important components of our Azure Functions are `function.json` where we define the function bindings, and `__init__.py` where we define a Python script to be executed.

5. Create `predictions-input` and `predictions-output` containers in our `mlopsstorage` by using Azure Storage VSC Extension
- open Azure Storage VSC Extension
- navigate to Blob Containers
- select Create Blob Container
- add blob container `predictions-input`
- add blob container `predictions-output`
- verify that both containers are created

6. Open Azure Functions VSC extension, select `LRBlobTrigger` function and select Deploy to Function App
- select Create new Function App in Azure Advanced
- add `LRBlobTriggerApp`
- select Python 3.8
- select `mlops_bootcamp`
- select your location
- select Premium
- select Create new App Service Plan
- add `MLOPSplan`
- select EP1
- select your storage account `mlopsstorage<....>`
- select your application insights resource `mlopsinsights<....>`
- wait until function will be deployed on Azure

7. Copy connection string from your blob storage and add it to the app settings by using VSC extensions
- navigate to Azure Storage VSC extension, click on your mlopsstorage and select Copy Connection String
- navigate to Azure Functions VSC extension, click on `LRBlobTriggerApp` and click on `Application Settings`, select Add New Setting
- add StorageConnectionString as a new settings name
- add copied connection string as a value

8. Test our deployed function with VSC extensions
- in Azure Storage VSC extension navigate to `predictions-input`, click and select Upload Files..., choose sample.dat file, press Enter, check `predictions-output` container
- in Azure Functions VSC extension navigate to `LRBlobTriggerApp` -> Logs -> Application -> Functions -> Function -> LRBlobTrigger and open a log file

### Develop the Blob triggered Azure Function locally with Azurite
1. Local setup update

- TEST DATA: in Azure Storage VSC extension navigate to Blob Containers -> `azureml-blobstore-<....>` -> `batch-data` and select Download, browse to `lesson3` folder

- MODELS: create a new folder `models` in lesson3
```
mkdir models
```
- retrieve model ids
```
az ml model list \
-w mlops \
- g mlops_bootcamp
```
- download two registered models into `models` folder
```
az ml model download \
-i <your model id> \
-t models \
-w mlops \
-g mlops_bootcamp
```

- AZURITE: start Azurite in VSC (Command+Shift+P on Mac and Ctrl+Shift+P on Windows/Linux, select Azurite start), in Azure Storage VSC navigate to Attached Storage Accounts -> Local Emulator -> Blob Containers, select Create Blob Container, add blob container `predictions-input`, add blob container `predictions-output`, verify that both containers are created

- in local.settings.json add this connection string as a value for `AzureWebJobsStorage`
```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```
- in local.settings.json remove `mlopsstorage<....>` key-value pair and replace it with
```
"StorageConnectionString": "DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;"
```
- start the function locally and test it by uploading sample.dat file to `predictions-input` in Local Emulator
```
cd blob_function
func start
```
2. Near real-time serverless inferencing service requires a scoring script to load the model and use it to predict new values. Typically, you load the model from the model registry and use it to generate predictions. Follow the video for the azure function update part.

### Deploy the Blob triggered Azure Function
1. Open Azure Functions VSC extension, select `LRBlobTrigger` function and select Deploy to Function App
- select `LRBlobTriggerApp` and choose Deploy in pop up window
- wait until function will be deployed on Azure

2. Test our deployed function with VSC extensions
- in Azure Storage VSC extension navigate to `predictions-input`, click and select Upload Files..., choose one of the csv files, press Enter, check `predictions-output` container

3. Clean up the function script by removing commented-out lines and re-deploy function by repeating steps 1 and 2.
