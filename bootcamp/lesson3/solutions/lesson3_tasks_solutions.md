# Bringing ML Models into Production Bootcamp
# Lesson 3: Near real-time Inference

## Solutions to exercise 1: Azurite
### Steps

1. Stop Azurite in VSC

Command+Shift+P on Mac and Ctrl+Shift+P on Windows/Linux, select `Azurite: Close`. This command closes all Azurite services

2. Clean up Azurite in VSC

Command+Shift+P on Mac and Ctrl+Shift+P on Windows/Linux, select `Azurite: Clean`. This command resets all Azurite services persistency data.

---
## Solutions to exercise 2: Bindings
### Steps

1. Update bindings so that a function will be triggered by csv files only
```
{
  "scriptFile": "__init__.py",
  "bindings": [
    {
      "name": "inputBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "predictions-input/{name}.csv",
      "connection": "StorageConnectionString"
    },
    {
      "name": "predictions",
      "type": "blob",
      "direction": "out",
      "path": "predictions-output/{name}.csv",
      "connection": "StorageConnectionString"
    }
  ]
}
```
2. Update bindings so that a function will be triggered by csv files, which names start with "processed-"
```
{
  "scriptFile": "__init__.py",
  "bindings": [
    {
      "name": "inputBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "predictions-input/processed-{name}.csv",
      "connection": "StorageConnectionString"
    },
    {
      "name": "predictions",
      "type": "blob",
      "direction": "out",
      "path": "predictions-output/{name}.csv",
      "connection": "StorageConnectionString"
    }
  ]
}
```
---
## Solutions to exercise 3: Azure Functions App and CLI
### Steps

1. Stop Azure Functions App by using Azure CLI
```
az functionapp stop \
--name <function app name> \
-g mlops_bootcamp
```
2. Restart Azure Function App by using Azure CLI
```
az functionapp restart \
--name <function app name> \
-g mlops_bootcamp
```
3. Remove Azure Function App by using Azure CLI
```
az functionapp delete \
--name <function app name> \
-g mlops_bootcamp
```
